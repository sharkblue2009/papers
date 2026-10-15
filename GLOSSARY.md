# Glossary

Domain vocabulary for the financial-engineering knowledge base in this repo.

## Terms

**Source document**: an original file under `papers/` (a PDF research report, book, or Markdown file). Source documents are never modified.

**Summary**: a Markdown digest of one source document, named `<source>.summary.md`. Summaries are the primary input for other agents.

**Record**: a Markdown file under `records/` that holds a summary or a consolidated note. Records are the consumer-facing knowledge layer.

**Index**: a Markdown file that lists records and their topics. `records/books__INDEX.summary.md` is the books index.

**Knowledge card**: a short file of stable conclusions for a directory, stored in `knowledge/` at the repo root, such as `knowledge/总知识卡片.md`.

**Source series**: the broker or publisher series a document belongs to (for example 海通选股因子系列, 开源微观系列, 兴业海外). Recorded as metadata, not as the classification axis.

**Topic**: a classification label. Each record may carry several topics. The first-pass topics are:
- market, industry, and stock state (regime and state identification)
- factor and stock selection
- financial machine learning methodology
- deep learning and pattern recognition
- microstructure and high frequency
- risk, portfolio, and asset allocation
- industry rotation and prosperity
- other / unclassified

**Flat layout**: single-document summaries sit in `records/summary/` with no subdirectories. Series-level and cross-document reports, notes, and indexes sit in `records/catalog/`. Knowledge cards live in `knowledge/`, outside `records/`. Retrieval is by filename.

**Name collision prefix**: when two source files share a basename, the record filename gets the source directory name plus `__` as a prefix (for example `B202205__<name>.md`).
