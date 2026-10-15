# 金融机器学习总知识卡片

- **目录范围**：`/mnt/d/myspace/papers/books/`
- **关联索引**：[[INDEX.summary.md]]
- **用途**：把本目录两本书的稳定结论压缩成可复用的研究卡片，供后续做因子、策略和研报转译时直接调用。

## 一句话结论

金融机器学习在资管里的核心价值，不是预测价格，而是把金融问题转成可验证、可交易、可复用的研究流程：**先标签与样本权重，再验证与过拟合控制，最后才是特征、模型和组合**。

## 核心稳定结论

### 1. 先定义金融问题，再选模型
- ML 在资管中更适合用来辅助构建金融理论
- 研究顺序应是：问题定义 → 标签 → 样本权重 → 特征 → 验证 → 组合 → 回测
- 不能把通用机器学习流程直接搬到金融场景

### 2. 标签是金融 ML 的第一基础设施
- 固定持有期标签容易失真
- 更稳健的做法包括：
  - triple-barrier method
  - meta-labeling
  - 动态阈值
  - side / size 联合学习
- 标签设计决定了后续模型能否学到真正可交易的信号

### 3. 样本不是独立同分布
- 金融标签常重叠，不能按普通 IID 数据处理
- 需要考虑：
  - uniqueness
  - concurrency
  - time decay
  - return attribution
- sequential bootstrap 有助于提高有效样本独特性

### 4. 普通验证方式在金融里不可靠
- 普通随机 K-fold 容易泄漏信息
- 更适合的验证方式：
  - purged K-fold
  - embargo
  - CPCV（combinatorial purged cross-validation）
- 回测是验证工具，不是研究工具
- 样本外稳定性比样本内拟合更重要

### 5. 特征重要性比盲目堆模型更重要
- 研究重点不是“模型多复杂”，而是“哪些特征真的在贡献信息”
- 需要关注：
  - 特征重要性
  - 替代效应
  - 特征冗余
  - 结构断点
- 分数差分、去噪协方差、微观结构特征都属于高复用模块

### 6. 组合构建要避免不稳定优化
- 直接用 Markowitz 往往不稳健
- 更稳健的方向是：
  - 去噪 / detoning
  - 聚类
  - 层次化配置
  - HRP / NCO
- 高相关资产环境下，结构化配置通常优于直接矩阵求逆

### 7. 回测必须服从理论与因果解释
- 回测不能替代理论
- 没有经济解释的高回测结果通常不稳健
- 过拟合控制应作为研究的一部分，而不是最后补丁
- 适合金融的评估视角包括：
  - log loss
  - deflated Sharpe ratio
  - probability of backtest overfitting

## 两本书各自的定位

### 《Machine Learning for Asset Managers》
- 更偏资管实践入口
- 强调去噪、聚类、标签、特征重要性
- 适合作为“金融 ML 怎么用”的第一本书

### 《Advances in Financial Machine Learning》
- 更偏方法论总纲
- 覆盖数据、标签、采样、验证、组合、回测偏差
- 适合作为“金融 ML 应该怎么做”的基础设施手册

## 可直接复用到后续研究的模板

### 研究起手式
1. 先定义经济问题或交易问题
2. 选择合适标签，而不是先选模型
3. 处理样本重叠与权重
4. 做 purged / CPCV 验证
5. 检查特征重要性与替代效应
6. 再谈组合构建与仓位管理
7. 最后评估交易成本与落地约束

### 适合优先复用的模块
- triple-barrier 标签
- meta-labeling
- sample weighting
- purged CV / CPCV
- fractional differentiation
- feature importance
- clustering / detoning
- HRP / NCO
- deflated Sharpe / PBO

## 与本目录现有文献的关系

- `Machine_Learning_For_Asset_Managers.summary.md`：偏实践入口
- `Advances_in_Financial_Machine_Learning_001.summary.md`：偏方法论总纲
- `INDEX.summary.md`：目录级总索引

## 最后归纳

如果后续要把研报观点转成策略，这一套知识可以简化成三句话：

1. **先把标签做对。**
2. **再把验证做严。**
3. **最后才轮到模型和组合。**
