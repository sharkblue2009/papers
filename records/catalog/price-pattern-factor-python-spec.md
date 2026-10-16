# 股价走势模式因子 Python 实现清单

- **生成时间**：2026-04-24
- **用途**：把 price-pattern-factor-list-and-tasks.md 进一步压缩为可直接实现的 Python 口径、字段定义、伪代码与模块划分。
- **默认数据频率**：日频（后续可扩展到分钟频）

---

## 一、统一数据约定

### 1. 输入字段
默认原始数据表至少包含以下字段：

```python
['date', 'asset', 'open', 'high', 'low', 'close', 'volume', 'amount']
```

可选增强字段：

```python
['vwap', 'turnover', 'free_mkt_cap', 'industry', 'adj_factor']
```

### 2. 预处理约定

```python
# 复权价格
adj_open  = open  * adj_factor
adj_high  = high  * adj_factor
adj_low   = low   * adj_factor
adj_close = close * adj_factor

# 收益率
ret_1d = adj_close / adj_close.shift(1) - 1

# 振幅
intraday_range = (adj_high - adj_low) / adj_close.shift(1)
```

### 3. 基础辅助函数建议

```python
import numpy as np
import pandas as pd


def rolling_rank(x: pd.Series, window: int) -> pd.Series:
    return x.rolling(window).apply(lambda s: pd.Series(s).rank(pct=True).iloc[-1], raw=False)


def zscore_by_group(df: pd.DataFrame, col: str, group_col: str, date_col: str = 'date') -> pd.Series:
    return df.groupby([date_col, group_col])[col].transform(lambda s: (s - s.mean()) / (s.std(ddof=0) + 1e-12))
```

---

## 二、建议的代码模块划分

如果后面你要真正写 Python，推荐按这个结构组织：

```python
factors/
├── trend_basic.py        # 均线、突破、趋势强度
├── reversal.py           # 深跌反转、止跌修复、影线
├── pattern_discrete.py   # K线离散形态编码
├── pattern_structural.py # 波段结构、横盘压缩与突破
├── similarity.py         # 相似K线、DTW
├── dl_features.py        # CNN/embedding接口（先留占位）
├── filters.py            # 市场状态、行业强弱、量价过滤
└── utils.py              # 公共函数
```

---

## 三、逐因子实现清单

## A. 趋势基础类

### 1. 均线多头排列因子

**字段定义**：

```python
ma_5  = close.rolling(5).mean()
ma_10 = close.rolling(10).mean()
ma_20 = close.rolling(20).mean()
ma_60 = close.rolling(60).mean()
```

**离散版信号**：

```python
bull_ma_order = ((ma_5 > ma_10) & (ma_10 > ma_20) & (ma_20 > ma_60)).astype(int)
```

**连续版分数**：

```python
ma_order_score = (
    (ma_5 - ma_10) / (ma_10 + 1e-12) +
    (ma_10 - ma_20) / (ma_20 + 1e-12) +
    (ma_20 - ma_60) / (ma_60 + 1e-12)
)
```

**建议输出字段**：
- `bull_ma_order`
- `ma_order_score`

---

### 2. 相对位置/前高突破因子

**字段定义**：

```python
rolling_high_20 = high.rolling(20).max()
rolling_high_60 = high.rolling(60).max()
```

**实现口径**：

```python
dist_to_high_20 = close / (rolling_high_20 + 1e-12) - 1
breakout_20 = (close >= rolling_high_20.shift(1)).astype(int)
```

**建议输出字段**：
- `dist_to_high_20`
- `dist_to_high_60`
- `breakout_20`
- `breakout_60`

---

### 3. 趋势强度因子

**实现口径 1：区间收益**

```python
trend_ret_20 = close / close.shift(20) - 1
trend_ret_60 = close / close.shift(60) - 1
```

**实现口径 2：线性回归斜率**

```python
from numpy.linalg import lstsq

def rolling_slope(series, window=20):
    xs = np.arange(window)
    def _slope(y):
        A = np.vstack([xs, np.ones(len(xs))]).T
        m, _ = lstsq(A, y, rcond=None)[0]
        return m
    return series.rolling(window).apply(_slope, raw=True)
```

**建议输出字段**：
- `trend_ret_20`
- `trend_ret_60`
- `trend_slope_20`
- `trend_slope_60`

---

## B. 横盘/突破类

### 4. 横盘压缩因子

**逻辑**：识别价格波动收敛区间。

**实现方式**：

```python
range_ratio_20 = (high.rolling(20).max() - low.rolling(20).min()) / (close.rolling(20).mean() + 1e-12)
volatility_20 = close.pct_change().rolling(20).std()
```

值越低，说明越像横盘压缩。

**建议输出字段**：
- `range_ratio_20`
- `volatility_20`
- `sideway_score_20 = -zscore(range_ratio_20)`

---

### 5. 横盘突破 × 放量因子

**实现方式**：

```python
avg_vol_20 = volume.rolling(20).mean()
volume_ratio = volume / (avg_vol_20 + 1e-12)
breakout_strength = (close / (high.rolling(20).max().shift(1) + 1e-12) - 1) * volume_ratio
```

**建议输出字段**：
- `volume_ratio`
- `breakout_strength`
- `box_breakout_signal = ((breakout_20 == 1) & (volume_ratio > 1.5)).astype(int)`

---

## C. 反转类

### 6. 深跌反转因子

**实现口径**：

```python
cum_drop_20 = close / close.shift(20) - 1
long_lower_shadow = (np.minimum(open, close) - low) / ((high - low) + 1e-12)
reversal_after_drop = ((cum_drop_20 < -0.2) & (long_lower_shadow > 0.5)).astype(int)
```

**增强口径**：叠加缩量止跌

```python
vol_shrink = volume / (volume.rolling(5).mean() + 1e-12)
reversal_after_drop_v2 = ((cum_drop_20 < -0.2) & (long_lower_shadow > 0.5) & (vol_shrink < 0.8)).astype(int)
```

**建议输出字段**：
- `cum_drop_20`
- `long_lower_shadow`
- `reversal_after_drop`
- `reversal_after_drop_v2`

---

### 7. 上下影线因子

**实现方式**：

```python
k_range = high - low + 1e-12
upper_shadow = (high - np.maximum(open, close)) / k_range
lower_shadow = (np.minimum(open, close) - low) / k_range
body_ratio = np.abs(close - open) / k_range
```

**建议输出字段**：
- `upper_shadow`
- `lower_shadow`
- `body_ratio`
- `shadow_skew = lower_shadow - upper_shadow`

---

## D. 离散形态编码类

### 8. 单日K线离散编码

**思路**：将K线拆成几个维度离散化。

```python
body_sign = np.sign(close - open)   # -1, 0, 1
body_size_bucket = pd.qcut(body_ratio, q=3, labels=False, duplicates='drop')
upper_bucket = pd.qcut(upper_shadow, q=3, labels=False, duplicates='drop')
lower_bucket = pd.qcut(lower_shadow, q=3, labels=False, duplicates='drop')
```

组合成编码：

```python
pattern_code_1d = (
    body_sign.astype(str) + '_' +
    body_size_bucket.astype(str) + '_' +
    upper_bucket.astype(str) + '_' +
    lower_bucket.astype(str)
)
```

**建议输出字段**：
- `pattern_code_1d`

---

### 9. 多日K线组合编码

```python
pattern_code_2d = pattern_code_1d.shift(1).astype(str) + '__' + pattern_code_1d.astype(str)
pattern_code_3d = pattern_code_1d.shift(2).astype(str) + '__' + pattern_code_1d.shift(1).astype(str) + '__' + pattern_code_1d.astype(str)
```

然后统计每种编码未来收益均值：

```python
future_ret_5 = close.shift(-5) / close - 1
pattern_map = df.groupby('pattern_code_3d')['future_ret_5'].mean()
pattern_score_3d = df['pattern_code_3d'].map(pattern_map)
```

**注意**：
- 训练集和测试集必须分开
- 需要最小样本数过滤，如 `count >= 30`

**建议输出字段**：
- `pattern_code_2d`
- `pattern_code_3d`
- `pattern_score_2d`
- `pattern_score_3d`

---

## E. 波段结构类

### 10. 波段切分特征

**简化实现**：
先用局部极值近似波段。

```python
local_max = (high.shift(1) < high) & (high.shift(-1) < high)
local_min = (low.shift(1) > low) & (low.shift(-1) > low)
```

从局部极值构造：
- 上一波上涨幅度
- 上一波回撤幅度
- 上一波持续天数

**建议输出字段**：
- `last_swing_up_ret`
- `last_swing_down_ret`
- `last_swing_duration`

这部分先做近似版本即可，后续再精修。

---

## F. 相似度匹配类

### 11. 相似K线因子

**窗口标准化**：

```python
def normalize_window(arr):
    arr = np.asarray(arr, dtype=float)
    return (arr / arr[0]) - 1
```

**相似度计算**：

```python
def corr_similarity(x, y):
    if np.std(x) < 1e-12 or np.std(y) < 1e-12:
        return np.nan
    return np.corrcoef(x, y)[0, 1]
```

**核心输出**：
- 当前20日窗口与历史窗口的最大相似度
- top-k相似窗口未来收益均值

**建议输出字段**：
- `pattern_sim_max_20`
- `pattern_sim_top5_future_ret`

---

### 12. DTW 相似度因子

如果使用 `dtaidistance` 或 `tslearn`：

```python
from dtaidistance import dtw

def dtw_distance(x, y):
    return dtw.distance(x, y)
```

**输出口径**：
- 与历史高收益模板的最小 DTW 距离
- 或转换为相似度：`sim = 1 / (1 + dist)`

**建议输出字段**：
- `dtw_dist_to_winner_template`
- `dtw_sim_to_winner_template`

优先在 **行业指数** 层面先实现。

---

## G. 深度学习接口类

### 13. CNN 图像因子输入格式

推荐先把每个窗口转成矩阵，而不是立即画图片。

```python
window_features = np.stack([
    open_window,
    high_window,
    low_window,
    close_window,
    volume_window
], axis=0)   # shape = [5, T]
```

**标签建议**：

```python
label_rank = future_ret_5   # 排序标签优先
```

**输出建议**：
- `cnn_score`
- `cnn_embedding_1 ... cnn_embedding_k`

在你自己的研究里，先把这部分作为后续接口，不用第一阶段就上。

---

## H. 过滤器类

### 14. 市场状态过滤

```python
index_ret_20 = index_close / index_close.shift(20) - 1
index_vol_20 = index_close.pct_change().rolling(20).std()
market_regime = np.select(
    [index_ret_20 > 0.05, index_ret_20 < -0.05],
    ['up', 'down'],
    default='sideway'
)
```

**建议输出字段**：
- `market_regime`
- `index_ret_20`
- `index_vol_20`

---

### 15. 行业强弱过滤

```python
industry_ret_20 = industry_close / industry_close.shift(20) - 1
industry_rank_20 = industry_ret_20.groupby('date').rank(pct=True)
```

**建议输出字段**：
- `industry_ret_20`
- `industry_rank_20`

---

## 四、第一版最值得先实现的字段表

如果只做第一版，我建议先产出以下字段：

```python
[
    'bull_ma_order',
    'ma_order_score',
    'dist_to_high_20',
    'breakout_20',
    'trend_ret_20',
    'trend_slope_20',
    'range_ratio_20',
    'volume_ratio',
    'breakout_strength',
    'cum_drop_20',
    'upper_shadow',
    'lower_shadow',
    'shadow_skew',
    'reversal_after_drop',
    'pattern_code_1d',
    'pattern_code_3d',
    'pattern_score_3d',
    'market_regime',
    'industry_rank_20'
]
```

这套已经足够支持：
- 趋势
- 突破
- 反转
- K线离散模式
- 市场状态过滤

---

## 五、推荐研究顺序

### 第 1 周：手工规则特征库
实现：
- 均线、突破、横盘压缩、影线、深跌反转

### 第 2 周：离散形态打分
实现：
- 1日 / 2日 / 3日 pattern code
- pattern score 映射

### 第 3 周：相似度匹配
实现：
- 相关系数相似K线
- 行业层 DTW

### 第 4 周：状态过滤 + 组合测试
实现：
- 市场 regime
- 行业强弱分层
- 单因子/复合因子回测

---

## 六、一句话执行建议

第一版不要追求“最复杂的AI模型”，先把 **均线趋势、前高突破、横盘突破、深跌反转、K线离散打分、市场状态过滤** 这 6 个模块做扎实，它们已经足够构成一个有研究价值的股价走势模式因子原型。
