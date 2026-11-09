---
name: find-people
description: Find people or companies that match criteria with Data Legion search. Use when the user wants a prospect or target list, for example "engineers at fintech companies in Austin" or "software companies with more than 200 employees".
---

To build a list with search:

1. Turn the request into a SQL WHERE clause over the `people` table (`person_search`) or the `companies` table (`company_search`). Start the query with `SELECT * FROM people WHERE ...` or `SELECT * FROM companies WHERE ...`.
2. Useful people columns: `job_title`, `company_name`, `city`, `state`, `country`, `linkedin_url`, and the cross-table columns `title`, `organization_name`, `skills`, `headline` and `summary`. Useful company columns: `industry` (lowercase LinkedIn industry values, for example `'software development'`) and `legion_employee_count`.
3. Match text loosely with `ILIKE '%term%'`, and combine conditions with `AND` / `OR`.
   Instead of SQL, `query` can be a query object on the response's field names, for example `{"bool": {"filter": [{"term": {"state": "texas"}}, {"match": {"job_title": "engineer"}}]}}` (`bool`, `term`, `terms`, `match`, `match_phrase`, `range`, `exists`, `prefix`, `wildcard`, `nested`).
4. Don't put LIMIT or OFFSET in the SQL. Use the `limit` and `offset` parameters: start with `limit: 10` to check the results look right, then page with `offset`. To go past 10,000 results or export a whole list, pass each page's `next_cursor` back as `cursor` instead of `offset`; the last page has none.
5. Trim results with `include_fields` so a page of results stays readable.
6. Show results as a table and say how to get the next page. If a promising person is missing contact details, offer to run `person_enrich` on them.
