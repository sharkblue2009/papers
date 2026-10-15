# 标题
在2022年的论文“Are Transformers Effective for Time Series Forecasting?”中，作者提出了一种简单

## 文档类型
“逐鹿”Alpha专题报告（十七）：基于TiDE及其改进的

## 核心主题
各类基于transformer的模型也层出不穷，如Informer，Temporal Fusion Transformer, PatchTST等，均取

## 方法与数据
“逐鹿”Alpha专题报告（十七）：基于TiDE及其改进的；随着transformer结构近年来在自然语言处理（NLP）和计算机视觉领域大放异彩，在时间序列预测的问题上，

## 关键结论
- 的TiDE模型中加入GRU encoder结构，我们提出了TiDGE模型，能够提高模型表现
- 本文我们尝试将TiDE模型应用于选股，结果表明，原始的TiDE模型并不适合股票收益率的预测，通过在原始
- 发布日期：2023年10月24日
- 自从GOOGLE在2017年的经典论文Attention is All You Need中

## 量化启发
量化上，该文提示可优先围绕选股、GRU、Transformer、LSTM这类信号做滚动检验、分层组合或复合加权；实盘需继续验证样本外稳定性、交易成本与约束条件。

## 局限与注意点
结论基于历史样本回测，可能受样本外失效、交易成本、数据口径变化和市场结构切换影响。

## 关键词
选股、GRU、Transformer、LSTM、收益、Alpha、因子