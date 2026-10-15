# Flatten source summaries into records/ with summary/ and catalog/ subfolders

Status: accepted

All Markdown digests were moved out of `papers/` into `records/` so other agents can find them by filename without walking the source tree. Single-document summaries live in `records/summary/`, series and cross-document notes, reports, and indexes live in `records/catalog/`, and `records/` top level keeps only `总知识卡片.md`. Filename collisions get a `<dir>__` prefix instead of deduplication, because the colliding files differ in content. Relative links were dropped because the moved files had none. PDFs stay in `papers/`. This is hard to undo and was chosen over keeping summaries beside their sources, which made retrieval depend on the source tree.
