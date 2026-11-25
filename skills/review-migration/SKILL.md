---
name: review-migration
---

When adding table, review:
- Columns (any missing ones, any that should be removed)
- Types
- Constraints (e.g. not null)
- Defaults
- Indexes

When adding/altering columns, review:
- Types
- Constraints (e.g. not null)
- Defaults
- Indexes

When adding index, review:
- Whether an existing index covers it
- Order of columns
- Whether it should be partial
- If it's safe to create during deploy
