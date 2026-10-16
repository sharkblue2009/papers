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
| Stable conclusions across the library | `knowledge/master-knowledge-card.md` (knowledge cards live in `knowledge/`) |
| Books index | `records/catalog/books__INDEX.summary.md` |
| Broker series indexes | `records/catalog/broker__INDEX.summary.md`, `records/catalog/海通选股因子系列__INDEX.summary.md`, `records/catalog/开源微观系列__INDEX.summary.md` |
| Series synthesis notes | `records/catalog/*master-notes*.md` |
| Cross-document reports | `records/catalog/alpha-factor-summary-report.md`, `records/catalog/alpha-factor-per-factor-report.md`, `records/catalog/ml-stock-selection-detailed-report.md` |
| Price-pattern reading lists | `records/catalog/price-pattern-*.md` |
| State-definition literature | `records/catalog/regime-identification-literature-summary.summary.md` |
| ML and LLM report index (447 reports) | `records/catalog/ml-models__INDEX.summary.md` (columns: 模型族, 具体模型, 数据与样本, 核心结论, 局限) |
| ML and LLM knowledge card | `knowledge/ml-research-knowledge-card.md` (model-family distribution and cross-report risks) |
| Sector rotation report index (327 reports) | `records/catalog/sector-rotation__INDEX.summary.md` (columns: 原文文件名, 研报系列, 日期, 方法类别, 具体方法, 数据与样本, 核心结论, 局限) |
| Sector rotation knowledge card | `knowledge/sector-selection-knowledge-card.md` (method distribution, common conclusions, risks) |
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
- If the records conflict, prefer the series `broker__master-notes.md` over a single-document summary, and state the conflict.
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
