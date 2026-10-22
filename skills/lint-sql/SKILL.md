---
name: lint-sql
---

When writing SQL queries:

- Only use schemas for components in the monorepo.
- Write queries without database names and schema names.
- Write queries using lowercase for keywords.
- Use “join” instead of “inner join” if there are no other joins (e.g. outer, cross).
- When using no joins, avoid using aliases.
- When joining, use first letter of each word in table name as alias (e.g. `po` for payment order).
- When making changes to queries, add comments for what you changed. Exclude changes for rules mentioned here.
- Write queries for Snowflake, but prefer syntax that can be used for both Snowflake and Postgres:
    - `current_timestamp - interval '1 year'` instead of `dateadd('year', -1, current_timestamp)`
    - `current_timestamp` instead of `now`
