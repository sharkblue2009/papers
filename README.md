# papers 入口页

这个目录用于管理金融研报、书籍摘要和长期知识沉淀。

## 直接可用文件

- `records/catalog/books__INDEX.summary.md`：books 目录总索引
- `records/总知识卡片.md`：稳定结论卡片
- `docs/adr/`：目录布局与阅读约定的决策记录
- `memories.json`：机器可读共享记忆

## 目录约定

- `books/`：金融书籍与方法论资料
- `broker/`：券商研报与系列文档

## 已沉淀的重点主题

### 金融机器学习
- 先标签，再样本权重，再验证，再模型，再组合，再回测
- 重点基础设施：triple-barrier、meta-labeling、purged K-fold、embargo、CPCV、feature importance、fractional differentiation、HRP/NCO
- 回测只是验证工具，不是研究工具

### 研报系列
- 海通选股因子系列：已形成跨年度稳定结论
- 开源市场微观结构系列：微观结构变量与短周期 alpha 的关系已系统化
- 兴业海外“西学东渐”系列：已有多篇摘要，可继续增量维护

## 给后续模型的建议

1. 先读 `records/总知识卡片.md`
2. 再读 `records/catalog/books__INDEX.summary.md` 或对应系列索引
3. 需要单篇细节时查 `records/summary/` 下对应摘要
4. 新文档优先判断是否重复，重复则跳过
