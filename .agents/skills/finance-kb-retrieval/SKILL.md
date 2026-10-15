---
name: finance-kb-retrieval
description: Read and retrieve summaries from the 金融工程文献知识库 (records/). Use before opening any source in papers/, when answering questions about quantitative finance research reports or books, or when looking for a summary, series index, or stable conclusion.
---

# Finance KB Retrieval

The knowledge base in `records/` holds Chinese summaries of the research reports and books in `papers/`. Read the records first. Open a source PDF only when a record lacks the detail you need.

## Rules

1. **Check records before papers.** If a summary exists, use it. Do not re-read the source PDF to rebuild a summary that already exists.
2. **Retrieve by filename.** Layout is flat. There are no subdirectories to walk and no relative links to follow.
3. **Start from the top.** Read the knowledge card, then the index for the series or book you need, then the single-document summary.
4. **Do not modify `papers/`.** Source documents are read-only. Write new records only under `records/`.

## Where things are

| Need | Location |
|------|----------|
| Stable conclusions across the library | `knowledge/总知识卡片.md` (knowledge cards live in `knowledge/`) |
| Books index | `records/catalog/books__INDEX.summary.md` |
| Broker series indexes | `records/catalog/broker__INDEX.summary.md`, `records/catalog/海通选股因子系列__INDEX.summary.md`, `records/catalog/开源微观系列__INDEX.summary.md` |
| Series synthesis notes | `records/catalog/*总纲笔记*.md` (the `_快速版` files are the short versions) |
| Cross-document reports | `records/catalog/alpha选股因子汇总报告.md`, `records/catalog/alpha选股因子逐因子报告.md`, `records/catalog/机器学习选股模型详细汇总报告.md` |
| Price-pattern reading lists | `records/catalog/股价走势模式*.md` |
| State-definition literature | `records/catalog/状态定义与状态识别文献汇总.summary.md` |
| One document's digest | `records/summary/<source-file-name>.summary.md` (about 4,500 files) |
| Topic and term definitions | `GLOSSARY.md` (root) |
| Architecture decisions | `docs/adr/` |

## Finding a summary

Summary names mirror the source PDF name:

```
papers/.../20120615-海通证券_中期策略报告-量化选股之事件驱动策略.pdf
→ records/summary/20120615-海通证券_中期策略报告-量化选股之事件驱动策略.pdf.summary.md
```

Name collisions were resolved with a `<dir>__` prefix, for example `B202205__<name>.md`. If a name is not found, search by keyword:

```powershell
Get-ChildItem records -Recurse -Filter '*.md' | Where-Object Name -like '*<keyword>*' | Select-Object -ExpandProperty FullName
```

Search inside summaries for a concept:

```powershell
Select-String -Path records\summary\*.md, records\catalog\*.md -Pattern '<term>' -List | Select-Object -ExpandProperty Path
```

## Answering from records

- Cite the record file you used, not the PDF, unless you read the PDF.
- If the records conflict, prefer the series 总纲笔记 over a single-document summary, and state the conflict.
- If no record covers the question, say so and then read the source PDF in `papers/`. Offer to write a new summary into `records/summary/`.
- Respond to the user in Chinese. Summaries are in Chinese; keep technical terms such as triple-barrier, purged K-fold, CPCV, and HRP as written.

## Document sync workflow

Run this when the user asks to sync new papers. It is triggered manually.

1. **Find new sources.** List PDFs under `papers/` whose modified date is in the target period. A PDF is new if no `records/summary/<pdf-name>.summary.md` exists. Match by filename, and check for `<dir>__` prefixed names on collisions.
2. **Extract text.** Use Node `pdf-parse` (or an equivalent) into a temp folder outside the repo. Skip files with no extractable text and report them.
3. **Write summaries.** One file per PDF in `records/summary/`, named `<pdf-name>.summary.md`. Use the template: title, `- 原文路径：`, `- 系列：`, `- 日期：`, `- 主题：` (labels from `GLOSSARY.md`), then `## 核心结论`, `## 方法要点`, `## 结果与局限`. Write in Chinese.
4. **Update indexes.** Add the new entries to the matching series index in `records/catalog/` only. Do not edit `knowledge/` during a sync.
5. **Report.** Give the count written, the skipped files, and the remaining backlog of PDFs without summaries.

## Known gaps

- `records/` has no master `INDEX.md` yet. Use the series indexes in `records/catalog/` instead.
- Older summaries may lack the metadata header. Filter by filename and content.
