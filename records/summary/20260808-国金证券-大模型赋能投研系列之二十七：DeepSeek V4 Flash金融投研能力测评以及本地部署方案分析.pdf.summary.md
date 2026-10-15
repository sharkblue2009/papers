# DeepSeek V4 Flash金融投研能力测评以及本地部署方案分析

- 原文路径：papers/broker/202610/20260808-国金证券-大模型赋能投研系列之二十七：DeepSeek V4 Flash金融投研能力测评以及本地部署方案分析.pdf
- 系列：大模型赋能投研系列
- 日期：2026-08-08
- 主题：financial machine learning methodology、deep learning and pattern recognition、other / unclassified

## 核心结论
- DeepSeek V4 Flash为284B总参数、13B激活参数的MoE模型，支持100万Token上下文、最大384k输出；官方混合精度权重文件约167GB，输入/输出价格为每百万Token 1元/2元。
- 本地部署可用官方vLLM或SGLang多卡方案，也可用GGUF量化配合llama.cpp；社区案例以2张RTX PRO 6000、总显存192GB和256K上下文实现约98.33 token/s。
- 报告以估值建模、多因子回测和行业研究三类任务比较DeepSeek V4 Flash、Kimi K3与GLM-5.2。综合表现Kimi K3最佳，DeepSeek的工程实现、数据口径和底稿可复算性最好。
- 估值任务中DeepSeek交付10个工作表、三表和估值模块联动，DCF终值约占企业价值83%，但收入实际由年度增速驱动，销量与ASP没有接入模型；敏感性表还有一处公式缺失导致结果为0。
- 多因子回测中，DeepSeek是三者中唯一明确使用历史成分股和行业分类、扣除交易成本并剔除不可交易个股的模型；行业研究中唯一保留原始资料层且无断链。

## 方法要点
测评使用相同结构化提示词，要求模型完成工具调用、数据获取、Excel建模、回测、资料溯源和报告输出。部署评估考虑权重文件、KV Cache、上下文长度和并发；GGUF参考包体积约90.9—162GB，128GB内存主要适合低位量化版本，Q4/Q8通常需要256GB及以上。

## 结果与局限
公开基准中Kimi K3的Terminal-Bench 2.1、DeepSWE和Toolathlon-Verified分别为88.3、67.5和73.2，DeepSeek分别为82.7、54.4和70.3。测评次数有限，结果受提示词和样本影响；模型仍可能产生公式、数据、推理和来源管理错误，本地部署也受硬件、缓存和并发约束。
