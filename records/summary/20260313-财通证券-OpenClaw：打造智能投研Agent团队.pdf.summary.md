# 研报摘要

- **源文件**：`20260313-财通证券-OpenClaw：打造智能投研Agent团队.pdf`
- **日期/机构/类型**：2026-03-13，财通证券，金融工程专题报告

## 核心问题
OpenClaw 这类开源 Agent 框架为什么会快速走红？它如何被配置成适用于投研工作的“智能团队”？

## 方法/数据
- 主要是**产品/框架拆解**，不是金融回测报告。
- 逐项介绍 OpenClaw 的核心配置文件：`AGENTS`、`SOUL`、`IDENTITY`、`USER`、`TOOLS`、`HEARTBEAT`、`BOOTSTRAP`。
- 介绍六类专业 Agent：`HR`、`ClawGuide`、`ClawScout`、`ClawWatch`、`ClawQuant`、`ClawResearch`。
- 对比虚拟机 + Ubuntu 与云平台两种部署方案，并说明模型配置、通讯集成、Skills 体系等。

## 关键发现
- OpenClaw 的价值在于：**开源、模块化、可协作、可私有化部署**。
- `HR Agent` 可管理其他 Agent；`ClawScout` 负责复盘与信息追踪；`ClawWatch` 做盯盘与风险预警；`ClawQuant` 做因子研究、回测代码和绩效报告；`ClawResearch` 辅助公司研究。
- 虚拟机 + Ubuntu 的方案更适合需要环境隔离和图形操作的投研团队，长期成本也更低。

## 量化要点
- 核心配置文件共 **7 个**。
- 专业 Agent 共 **6 类**。
- 部署方案对比 **2 种**：虚拟机/云平台。
- 报告强调 OpenClaw 在 2026 年 1 月 25 日重大更新后关注度快速上升，但未给出金融回测绩效。

## 局限性
- 这不是策略有效性验证报告，更多是工具链与工作流说明。
- Agent 输出存在随机性、理解偏差和信息安全风险，必须人工复核。

## 关键词
OpenClaw、AI Agent、投研工作流、私有化部署、Skills、ClawQuant、ClawResearch