---
name: sql-lint
---

When writing SQL queries:

- Write queries for Snowflake.
- Only use schemas for components in the monorepo.
- Write queries without database names and schema names.
- Write queries using lowercase for keywords.
- Avoid using aliases if a query or subquery has no joins.
- Use “join” instead of “inner join” if there are no other joins (e.g. outer, cross).
- When making changes to queries, add comments for what you changed. Exclude changes for rules mentioned here.
- Do date math like `current_timestamp - interval ‘1 year’` instead of `dateadd(’year’, -1, current_timestamp)` (the former can be used for both Snowflake and Postgres if needed).
