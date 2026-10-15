# Advances in Financial Machine Learning

- **Source file**: `Advances_in_Financial_Machine_Learning_001.pdf`
- **Document type**: Book
- **Author**: Marcos López de Prado
- **Pages**: 393

## 核心主题
这本书是金融机器学习的系统方法论总纲，围绕金融数据结构、标签、样本权重、分数变换、交叉验证、特征重要性、贝叶斯/组合思想、回测偏差和高性能计算等问题，建立一套适合金融场景的 ML 工程框架。

## 本书结构
- Preamble
- Data Analysis
- Modelling
- Backtesting
- Useful Financial Features
- High-Performance Computing Recipes

## 主要内容
### 1. 金融数据结构
- 金融数据有 fundamental / market / analytics / alternative 等多种类型。
- Bars 不能只用固定时间 bar，还包括信息驱动采样、事件驱动采样等。
- 多产品序列、复权、合约切换、指数成分变化等都可能引入结构断点。

### 2. 标签构造
- 固定持有期标签容易失真。
- 书中重点强调 **triple-barrier method**、动态阈值、meta-labeling、side 与 size 的联合学习。

### 3. 样本权重
- 金融标签常重叠，不能把样本当独立同分布。
- 需要考虑 uniqueness、concurrency、time decay、return attribution。
- sequential bootstrap 可用于提高训练样本的有效独特性。

### 4. 分数变换与特征工程
- 分数差分（fractional differentiation）用于在保留记忆的同时尽量实现平稳性。
- 结构断点、熵特征、微观结构特征等可作为有用金融特征。

### 5. 建模与验证
- 金融数据上普通 K-fold 会失效，需要 purged K-fold、embargo、CPCV。
- 强调特征重要性、超参数调优和过拟合控制。
- 对于金融策略，log loss 往往比 accuracy 更合理，因为它反映概率质量与仓位大小。

### 6. 组合构建与风险
- 讨论 bet sizing、backtest statistics、strategy risk、HRP / NCO 等更稳健的资产配置框架。
- Markowitz 优化在高度相关资产上容易产生不稳定解，即 “Markowitz’s curse”。

### 7. 回测与过拟合
- 回测不是研究工具，而是验证工具。
- 强调 CPCV、synthetic data、deflated Sharpe ratio、backtest overfitting probability 等。
- 只有理论才能解释因果机制，回测不能替代理论。

## 关键结论
1. **金融机器学习是独立学科**，不能简单套用通用 ML。
2. **金融标签、样本权重和验证方法**是最核心的基础设施。
3. **普通随机切分和普通 accuracy 指标**会严重高估模型效果。
4. **分数差分、去噪协方差、聚类配置、HRP/NCO**是稳健组合的重要工具。
5. **回测必须服从理论与因果解释**，否则很容易落入 overfitting。

## 对量化研究的启发
- 这是构建量化研究平台时最值得反复查阅的一本参考书。
- 适合直接转化成研究流程：数据采样 → 标签 → 权重 → 特征 → 验证 → 组合 → 回测 → 过拟合控制。
- 对高频、事件驱动、指增、因子挖掘、组合优化都有强复用价值。

## 局限与注意事项
- 理论和工程内容很多，初读门槛较高。
- 需要结合代码实践才能真正消化。
- 部分方法对数据质量和样本量要求较高。

## 关键词
金融机器学习、三重障碍、元标签、样本权重、分数差分、purged CV、CPCV、特征重要性、HRP、NCO、回测过拟合

## 适合后续复用的知识点
- 金融场景必须先解决标签与样本权重，再考虑模型。
- 回测偏差控制比模型复杂度更重要。
- HRP/NCO 和去噪协方差是稳健配置的重要工具。
- log loss、deflated Sharpe、probability of backtest overfitting 是比普通 accuracy 更适合金融的评估视角。
