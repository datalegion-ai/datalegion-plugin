---
name: find-people
description: Find people or companies that match criteria with Data Legion Discover or search. Use when the user wants a prospect or target list, for example "engineers at fintech companies in Austin" or "software companies with more than 200 employees".
---

To build a list:

1. If the request is in plain words, try `person_discover` or `company_discover` first with the request exactly as the user wrote it, a `limit` (start with 10: it returns one record unless asked for more) and `include_fields`: Data Legion writes the search and returns it as `generated_query`. Then show the results as in steps 6 and 7. If it refuses a part it cannot filter on (a school, funding, contact details), tell the user and offer the search for the rest that the error names. If it answers 403 saying the team has no contract for the endpoint, or that this key is limited to other endpoints, it can't use Discover: write the search yourself as below. For the next page, pass the previous page's `next_cursor` back as `cursor` with the same query and no `offset`: it reruns the same search.
2. Turn the request into a SQL WHERE clause over the `people` table (`person_search`) or the `companies` table (`company_search`). Start the query with `SELECT * FROM people WHERE ...` or `SELECT * FROM companies WHERE ...`.
   Instead of SQL, `query` can be a query object on the response's field names, for example `{"bool": {"filter": [{"term": {"state": "texas"}}, {"match": {"job_title": "engineer"}}]}}` (`bool`, `term`, `terms`, `match`, `match_phrase`, `range`, `exists`, `prefix`, `wildcard`, `nested`).
3. Useful people columns: `job_title`, `company_name`, `city`, `state`, `country`, `linkedin_url`, and the cross-table columns `title`, `organization_name`, `skills`, `headline` and `summary` (SQL only: in a query object use the response paths, such as `experience.title.cleaned`). Useful company columns: `industry` (lowercase LinkedIn industry values, for example `'software development'`), `size` (a range such as `'51-200'`) and `legion_employee_count` (headcount, on plans with premium company fields; on others filter by `size`).
4. Match text loosely with `ILIKE '%term%'`, and combine conditions with `AND` / `OR`.
5. Don't put LIMIT or OFFSET in the SQL. Use the `limit` and `offset` parameters: start with `limit: 10` to check the results look right, then page with `offset`. To go past 10,000 results or export a whole list, pass each page's `next_cursor` back as `cursor` instead of `offset`; on the last page it is null.
6. Trim results with `include_fields` so a page of results stays readable.
7. Show results as a table and say how to get the next page. If a promising person is missing contact details, offer to run `person_enrich` on them.
