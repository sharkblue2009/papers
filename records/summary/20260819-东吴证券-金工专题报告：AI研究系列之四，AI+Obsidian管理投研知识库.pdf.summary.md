# AI研究系列之四：AI+Obsidian管理投研知识库

- **source filename**: `20260819-东吴证券-金工专题报告：AI研究系列之四，AI+Obsidian管理投研知识库.pdf`
- **date**: 2026-08-19
- **institution / author**: 东吴证券研究所；于明明、孙石、吴彦锦
- **extraction confidence**: high

## Core question
报告讨论如何把研报、调研纪要、卖方观点和个人判断从一次性对话或分散文件，沉淀为可长期检索、关联、复核和复用的投研知识库。核心方案是以 Obsidian 作为本地 Markdown 载体，以大语言模型协助提炼、建链、更新和发现分歧。

## Methods / data
- 以 Obsidian 的文件夹、标签、属性、双向链接和搜索组织原始资料与 Wiki 页面。
- 使用 Web Clipper、Claudian、Pandoc、Dataview、Karpathy llm wiki、QuickAdd 等插件。
- 案例覆盖海外产品报告撰写、卖方观点跟踪、券商金股数据库和基金经理调研纪要。
- 通过机构、日期、主题、观点方向、股票、行业、推荐状态等字段建立结构化卡片和动态看板。

## Key findings
- LLM Wiki 强调预先结构化和持续维护，与每次查询才临时检索的传统 RAG 工作流不同。
- Claudian 支持“阅读—修改—检查—重构”式报告协作；Dataview 可汇总共识、分歧和观点变化。
- 金股和基金经理案例显示，结构化字段可支持跨机构、跨时间回溯，但报告未提供收益或 Sharpe 等策略绩效数字。

## Quant takeaways
- 可将研报抽取为带来源、时间和主题字段的事件/观点因子，再测试观点变化对收益、行业轮动或风格暴露的预测力。
- 需要保留原文链接和版本记录，防止 AI 幻觉、遗漏及插件兼容与数据安全问题；知识库结论仍须回到原始资料核验。
