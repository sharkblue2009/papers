# DeepSeek V4 Pro金融投研能力评测

- 原文路径：papers/broker/202610/20260816-国金证券-大模型赋能投研系列之二十八：DeepSeek V4 Pro金融投研能力评测.pdf
- 系列：大模型赋能投研系列
- 日期：未知
- 主题：financial machine learning methodology、other / unclassified

## 核心结论
- DeepSeek V4 Pro正式版采用MoE架构，总参数1.6T、激活参数49B，支持100万Token上下文和384K最大输出；长上下文下单Token推理FLOPs约为V3.2的27%，KV Cache约为10%。
- 相比预览版，HLE工具、TerminalBench 2.1、DeepSWE、Toolathlon-Verified和AutomationBench Public分别提升24.5%、21.9%、389.8%、32.6%和148.4%。
- 估值任务中Kimi K3第一、V4 Pro第二；V4 Pro报告口径更新且结论审慎，但Excel关键公式系统性错位，修改假设后无法可靠重算。
- 回测和行业研究任务中V4 Pro均排名第一：回测扣除交易成本、区分信号日与执行日并剔除停牌；行业研究的投资框架可复算，Wiki来源页、实体页和综合页可追溯。

## 方法要点
报告结合官方公告、API文档、模型卡和Harness预览版，比较V4 Pro与Kimi K3、GLM-5.2在估值建模、多因子回测和行业研究三项任务中的交付。评测关注公式、交易约束、底稿复核、知识库沉淀和来源追溯，并以“100万未命中输入+20万输出”的长程Agent任务比较成本。

## 结果与局限
V4 Pro正式版七项共同Agent基准均值为65.0，接近Kimi K3的65.1；该长程任务成本约为闲时7.2元、高峰14.4元，闲时约为Kimi K3的17%。Harness采用插件化架构和追加式完整执行日志，说明模型能力需要与工具、提示词、重试及恢复机制协同评估。模型输出存在随机性、公式与事实错误风险，回测受成本和交易条件影响，数据与提示词变化也会改变结果。
