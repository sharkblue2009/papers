# 股价走势模式匹配文献阅读清单

- 生成时间：2026-04-23
- 主题：股价走势模式匹配 / 图形识别 / 时间序列相似性 / K线形态识别 / 深度学习图像化识别
- 说明：本清单聚焦“如何把价格走势模式匹配转化为可检验、可实现的量化研究问题”，优先保留对后续策略研究最有用的文献。

## 一、推荐阅读顺序

### 第一层：先建立经典框架
1. Andrew W. Lo, Harry Mamaysky, Jiang Wang, **Foundations of Technical Analysis: Computational Algorithms, Statistical Inference, and Empirical Implementation** (2000/2002)
2. Tak-chung Fu, Fu-Lai Chung, Robert W. P. Luk, Chak-man Ng, **Stock time series pattern matching: Template-based vs. rule-based approaches** (2006)
3. László Györfi, Frederic Udina, Harro Walk, **Nonparametric nearest neighbor based empirical portfolio selection strategies** (2008)

### 第二层：看工程改进与模式匹配细化
4. Yuqing Wan, Xueyuan Gong, Yain-Whar Si, **Effect of segmentation on financial time series pattern matching** (2015)
5. **Financial time series pattern matching with extended UCR Suite and Support Vector Machine** (2016)
6. Tai-Liang Chen, Fengyu Chen, **An intelligent pattern recognition model for supporting investment decisions in stock market** (2016)

### 第三层：看K线/蜡烛图与深度学习路线
7. Rodrigo Naranjo, Matilde Santos, **A fuzzy decision system for money investment in stock markets based on fuzzy candlesticks pattern recognition** (2019)
8. **Stock Chart Pattern Recognition with Deep Learning** (arXiv:1808.00418, 2018)
9. Duy Trong Nguyen, Tran Quy Ban, Anh Duy Tran, **Object Detection Approach for Stock Chart Patterns Recognition in Financial Markets** (2023)
10. Luca Cagliero, Jacopo Fior, Paolo Garza, **Shortlisting machine learning-based stock trading recommendations using candlestick pattern recognition** (2023)

### 第四层：看组合层与策略应用
11. Fayyaaz Loonat, Tim Gebbie, **Learning zero-cost portfolio selection with pattern matching** (2018)
12. Yang Wang, Dong Wang, **Market Symmetry and Its Application to Pattern-Matching-Based Portfolio Selection** (2019)
13. Ali Fereydooni, Sasan Barak, Seyed Mehrzad Asaad Sajadi, **A novel online portfolio selection approach based on pattern matching and ESG factors** (2023)

---

## 二、核心文献清单

## 1. 经典图形模式 / 技术分析算法化

### 1) Foundations of Technical Analysis: Computational Algorithms, Statistical Inference, and Empirical Implementation
- 作者：Andrew W. Lo, Harry Mamaysky, Jiang Wang
- 年份：2000/2002
- DOI：10.3386/w7613
- 主题：把传统技术分析中的图形模式（chart patterns）形式化、算法化，并做统计检验。
- 为什么值得读：
  - 是学术界把“图形识别”转成严肃经验研究的代表作。
  - 对后续所有 chart pattern recognition 文献几乎都是方法论起点。
- 建议关注：
  - 非参数平滑与图形提取方法
  - 模式定义如何去主观化
  - 模式出现后的条件收益分布

### 2) A computational implementation of stock charting: abrupt volume increase as signal for movement in New York Stock Exchange Composite Index
- 作者：William Leigh, Naval K. Modani, Ross Hightower
- 年份：2003
- DOI：10.1016/S0167-9236(03)00084-8
- 主题：把图表分析中的信号规则转成可计算实现，结合成交量突增等条件。
- 价值：适合看“图形+量能”的早期工程化思路。

### 3) Trading With a Stock Chart Heuristic
- 作者：William Leigh, Cheryl J. Frohlich, Steven Hornik
- 年份：2007
- DOI：10.1109/TSMCA.2007.909508
- 主题：将图形启发式规则转成可交易规则。
- 价值：适合作为“从图形识别到策略设计”的过渡文献。

### 4) An intelligent pattern recognition model for supporting investment decisions in stock market
- 作者：Tai-Liang Chen, Fengyu Chen
- 年份：2016
- DOI：10.1016/j.ins.2016.01.079
- 主题：用智能模式识别支持投资决策。
- 价值：偏应用导向，适合了解传统模式识别与决策支持系统如何结合。

---

## 2. 时间序列相似性 / 模板匹配 / 走势检索

### 5) Stock time series pattern matching: Template-based vs. rule-based approaches
- 作者：Tak-chung Fu, Fu-Lai Chung, Robert W. P. Luk, Chak-man Ng
- 年份：2006
- DOI：10.1016/j.engappai.2006.07.003
- 主题：比较模板匹配与规则匹配两类路线在股票时间序列模式识别中的表现。
- 为什么值得读：
  - 与“股价走势模式匹配”主题最直接相关。
  - 能帮助区分“相似路径检索”和“规则型形态定义”两种思想。
- 建议关注：
  - 模板库如何构建
  - 匹配距离如何定义
  - 不同匹配机制对预测效果的影响

### 6) Effect of segmentation on financial time series pattern matching
- 作者：Yuqing Wan, Xueyuan Gong, Yain-Whar Si
- 年份：2015
- DOI：10.1016/j.asoc.2015.10.012
- 主题：研究时间序列分段方式对模式匹配结果的影响。
- 价值：
  - 对实做非常重要。
  - 说明“窗口、分段、切点定义”常常比模型本身更影响结果。

### 7) Financial time series pattern matching with extended UCR Suite and Support Vector Machine
- 年份：2016
- DOI：10.1016/j.eswa.2016.02.017
- 主题：把高效时间序列检索（UCR Suite）和分类器结合到金融序列模式匹配中。
- 价值：适合参考更工程化、可扩展的实现路线。

### 8) Temporal pattern matching for the prediction of stock prices
- 作者：Richi Nayak, Paul te Braak
- 年份：2007
- 链接：http://crpit.com/abstracts/CRPITV84Nayak.html
- 主题：利用时间模式匹配做股价预测。
- 价值：适合补充“模式匹配→预测”的直接应用视角。

### 9) Measuring Financial Time Series Similarity with a View to Identifying Profitable Stock Market Opportunities
- 作者：Rian Dolphin, Barry Smyth, Yang Xu
- 年份：2021
- DOI：10.1007/978-3-030-86957-1_5
- 主题：用金融时间序列相似性去识别潜在盈利机会。
- 价值：更接近“检索相似状态→做交易筛选”的现代问题设定。

---

## 3. K线 / 蜡烛图模式识别

### 10) A fuzzy decision system for money investment in stock markets based on fuzzy candlesticks pattern recognition
- 作者：Rodrigo Naranjo, Matilde Santos
- 年份：2019
- DOI：10.1016/j.eswa.2019.05.012
- 主题：基于模糊K线模式识别构建投资决策系统。
- 为什么值得读：
  - 是 K线模式识别 方向里较有代表性的工作。
  - 比硬规则更柔性，适合处理K线形态边界模糊的问题。

### 11) Fuzzy modeling of stock trading with fuzzy candlesticks
- 作者：Rodrigo Naranjo, Javier Arroyo, Matilde Santos
- 年份：2017
- DOI：10.1016/j.eswa.2017.10.002
- 主题：进一步把模糊K线识别应用到交易建模中。

### 12) Fuzzy Candlesticks Forecasting Using Pattern Recognition for Stock Markets
- 作者：Rodrigo Naranjo, Matilde Santos
- 年份：2016
- DOI：10.1007/978-3-319-47364-2_31
- 主题：基于模式识别的模糊蜡烛图预测。
- 价值：适合补足该研究线的方法链条。

### 13) Candlestick Patterns Recognition using CNN-LSTM Model to Predict Financial Trading Position in Stock Market
- 作者：Aditya Rifky Ramadhan, Irma Palupi, Bambang Wahyudi
- 年份：2022
- DOI：10.47065/josyc.v3i4.2133
- 主题：将CNN-LSTM用于蜡烛图模式识别与交易仓位预测。
- 价值：连接传统K线模式与深度学习。

### 14) Shortlisting machine learning-based stock trading recommendations using candlestick pattern recognition
- 作者：Luca Cagliero, Jacopo Fior, Paolo Garza
- 年份：2023
- DOI：10.1016/j.eswa.2022.119493
- 主题：通过K线模式识别为机器学习交易推荐做筛选。
- 价值：更接近实际选股/推荐系统中的信号筛选模块。

---

## 4. 深度学习 / 图像化模式识别

### 15) Stock Chart Pattern Recognition with Deep Learning
- 年份：2018
- arXiv：1808.00418
- 链接：https://arxiv.org/abs/1808.00418
- 主题：用 CNN / LSTM 识别股票走势图中的常见图形模式。
- 价值：
  - 是“把价格走势看成图像/序列去识别”的直接代表。
  - 适合快速建立深度学习路线的 baseline 直觉。

### 16) Object Detection Approach for Stock Chart Patterns Recognition in Financial Markets
- 作者：Duy Trong Nguyen, Tran Quy Ban, Anh Duy Tran
- 年份：2023
- DOI：10.1145/3587828.3587851
- 主题：把图形模式识别建模为目标检测问题。
- 价值：
  - 方法现代。
  - 对头肩顶、三角形、箱体等局部结构识别更自然。

### 17) Using Deep Learning Neural Networks and Candlestick Chart Representation to Predict Stock Market
- 年份：2019
- arXiv：1903.12258
- 链接：https://arxiv.org/abs/1903.12258
- 主题：用K线图表示作为深度学习输入进行市场预测。
- 价值：适合研究“图像输入是否优于手工特征”。

### 18) Do VLMs Truly “Read” Candlesticks? A Multi-Scale Benchmark for Visual Stock Price Forecasting
- 年份：2026
- arXiv：2604.12659
- 链接：https://arxiv.org/abs/2604.12659
- 主题：检验视觉语言模型是否真正理解蜡烛图。
- 价值：
  - 很新。
  - 适合了解大模型/多模态模型在金融图形理解上的真实边界。

---

## 5. 模式匹配直接用于组合与交易

### 19) Nonparametric nearest neighbor based empirical portfolio selection strategies
- 作者：László Györfi, Frederic Udina, Harro Walk
- 年份：2008
- DOI：10.1524/stnd.2008.0917
- 主题：基于非参数最近邻的经验型组合选择策略。
- 为什么值得读：
  - 这条路线本质是“找到历史相似状态，再根据后续结果做当前决策”。
  - 比单纯的图形命名更贴近可落地量化策略。

### 20) Learning zero-cost portfolio selection with pattern matching
- 作者：Fayyaaz Loonat, Tim Gebbie
- 年份：2018
- DOI：10.1371/journal.pone.0202788
- 主题：模式匹配驱动的零成本组合选择。
- 价值：适合研究如何把 pattern matching 用到多空组合层。

### 21) Market Symmetry and Its Application to Pattern-Matching-Based Portfolio Selection
- 作者：Yang Wang, Dong Wang
- 年份：2019
- DOI：10.3905/jfds.2019.1.2.078
- 主题：市场对称性与模式匹配组合选择。
- 价值：更偏理论化地扩展 pattern-matching portfolio selection。

### 22) A novel online portfolio selection approach based on pattern matching and ESG factors
- 作者：Ali Fereydooni, Sasan Barak, Seyed Mehrzad Asaad Sajadi
- 年份：2023
- DOI：10.1016/j.omega.2023.102975
- 主题：把 pattern matching 与 ESG 因素结合到在线组合选择中。
- 价值：体现该路线向“多信息融合”扩展的趋势。

---

## 三、按研究问题归类

### 1. 如果你关心“图形形态是否真的有统计意义”
优先读：
- Lo, Mamaysky, Wang
- Leigh 系列
- Nguyen et al. (object detection)

### 2. 如果你关心“当前走势和历史哪些阶段最像”
优先读：
- Fu et al.
- Wan et al.
- Dolphin et al.
- Györfi et al.

### 3. 如果你关心“K线模式能否做成量化信号”
优先读：
- Naranjo 系列
- Ramadhan et al.
- Cagliero et al.

### 4. 如果你关心“深度学习是否能自动学出价格图形特征”
优先读：
- arXiv:1808.00418
- arXiv:1903.12258
- Nguyen et al. (2023)
- arXiv:2604.12659

### 5. 如果你关心“模式匹配如何直接落到组合/策略”
优先读：
- Györfi et al.
- Loonat & Gebbie
- Wang & Wang
- Fereydooni et al.

---

## 四、对后续量化研究最有用的稳定启发

1. **模式匹配本质上更像条件分布检索，而不是简单分类。**  
   真正有用的是：找到相似历史片段后，统计未来收益、波动和回撤分布，再做仓位决策。

2. **序列切片、归一化、对齐方式非常关键。**  
   固定窗/可变窗、收益率标准化、相似度度量（欧氏距离、相关系数、DTW、SAX）往往决定上限。

3. **传统图形名称通常不如“相似状态集合”稳健。**  
   头肩顶、双底这类离散标签主观性较强；top-k 相似路径检索更适合系统化策略。

4. **图像化深度学习路线可行，但要警惕学到绘图伪特征。**  
   如比例缩放、坐标轴、采样方式、图片渲染习惯都可能造成虚假可预测性。

5. **单纯价格形状通常不够，最好与量能、波动率、换手、市场风格状态结合。**

---

## 五、可直接展开的研究方向

### 方向 A：相似走势检索因子
- 输入：过去 N 日收益率路径 / OHLC 片段
- 方法：top-k 最近邻、DTW、相关距离、SAX
- 输出：
  - 相似历史样本未来 5/10/20 日平均收益
  - 正收益概率
  - 分位数回撤
- 备注：这条路线最适合做可解释型模式匹配因子。

### 方向 B：K线结构 embedding
- 将 OHLC 转为：实体长度、上下影线比例、缺口、连续K线组合特征
- 再做聚类 / motif discovery / 条件收益统计
- 适合构建离散事件型择时信号。

### 方向 C：图形检测 + 事件研究
- 用目标检测模型识别头肩顶、三角形、箱体、突破等事件
- 不直接交易图形标签
- 而是先做 event study：检验事件后收益、波动、回撤、成交量变化
- 适合避免“看起来像有效，但实际无法交易”的问题。

---

## 六、精简版：如果只先读 8 篇

1. Foundations of Technical Analysis
2. Stock time series pattern matching: Template-based vs. rule-based approaches
3. Nonparametric nearest neighbor based empirical portfolio selection strategies
4. Effect of segmentation on financial time series pattern matching
5. An intelligent pattern recognition model for supporting investment decisions in stock market
6. A fuzzy decision system for money investment in stock markets based on fuzzy candlesticks pattern recognition
7. Stock Chart Pattern Recognition with Deep Learning
8. Object Detection Approach for Stock Chart Patterns Recognition in Financial Markets

---

## 七、后续可衔接任务

如果后续继续深入，可以直接往下做两类工作：

1. **文献精读版**：逐篇提炼
   - 研究问题
   - 模式定义
   - 相似度度量
   - 数据频率
   - 评价指标
   - 交易可实现性

2. **策略实现版**：基于这些文献设计原型
   - 相似走势检索因子
   - K线结构聚类因子
   - 图形检测事件策略
   - pattern matching portfolio selection 原型
