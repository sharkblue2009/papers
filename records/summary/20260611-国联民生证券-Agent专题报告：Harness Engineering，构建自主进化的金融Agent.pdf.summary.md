# Harness Engineering：构建自主进化的金融Agent

- 原文路径：papers/broker/202610/20260611-国联民生证券-Agent专题报告：Harness Engineering，构建自主进化的金融Agent.pdf
- 系列：无
- 日期：2026-06-11
- 主题：financial machine learning methodology、deep learning and pattern recognition

## 核心结论
- 报告采用“Agent = Model + Harness”的框架，认为真实任务中的可用性和稳定性主要取决于模型之外的工具、记忆、流程、护栏和反馈设计。
- Harness 的核心模块包括 Agent Loop、Agent 记忆、Agent 优化和 Agent 熵管理；工具治理、安全护栏、上下文治理及容错恢复也是金融系统需要补充的设施。
- Agent Loop 采用 ReAct 式“思考—行动—观察”循环；记忆采用索引先行、按需加载的渐进式文档披露，以控制上下文和 Token 开销。
- 报告以 Wyckoff 技术分析搭建 Predictor、Critic、Reflector、Evolver 四个子 Agent，通过结构化 JSON 完成“预测—批判—反思—进化”闭环；实测示例显示，Agent 在银行股上学到短期均值回复，在科技股上学到趋势跟随。

## 方法要点
系统使用程序化 Wyckoff 快照作为客观输入，将情境记忆写成带 YAML 头的 Markdown 笔记，由 MEMORY.md 负责索引，最多注入 5 条相关记忆。GEPA 反思式提示词进化让 Reflector 阅读执行轨迹、定位失败原因，再由 Evolver 修改预测器，并通过验证集回测和新旧策略融合确认更新。

## 结果与局限
Meta-Harness 的 Proposer—Evaluator—共享文件记忆结构支持持续优化；Hermes-Agent 的经验积累则需要与 Skill 归档、合并和清理配对，否则会出现重复技能、提示词膨胀和状态漂移。报告中的股票判断仅用于测试，学习依赖历史样本，市场结构变化可能使 Agent 失效；系统还面临模型随机性、工具调用错误和记忆熵增风险。
