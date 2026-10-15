# Working conventions for agents reading papers/

Status: accepted

Agents must read `records/` before `papers/`, and must skip any source that already has a summary in `records/summary/` or `records/catalog/`. Summaries are written in Chinese and named `<source>.summary.md`; the directory-level entry points are `records/catalog/books__INDEX.summary.md`, `records/catalog/broker__INDEX.summary.md`, and `records/总知识卡片.md`. Stable research findings (triple-barrier, purged K-fold/CPCV, HRP, and the year-by-year 海通 and 开源 conclusions) live in the catalog notes and the knowledge card, not in this ADR. This replaces the earlier rule that summaries sit beside their source files, which is no longer in effect.
