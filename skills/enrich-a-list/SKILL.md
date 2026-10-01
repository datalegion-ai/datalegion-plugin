---
name: enrich-a-list
description: Enrich a list of people or companies with Data Legion. Use when the user shares contacts, emails, LinkedIn URLs, domains or a spreadsheet and wants titles, employers, contact details or firmographics filled in.
---

To enrich a list:

1. Work out whether each row is a person or a company. People need at least one of email, phone, LinkedIn or other social URL, or a name plus context (company, location, school, job title). Companies need a domain, name, LinkedIn URL or ticker.
2. If inputs look messy (mixed-case emails, phone formatting, URLs with tracking parameters), run `utility_clean` or `utility_validate` first. Both are free and raise match rates.
3. Call `person_enrich` or `company_enrich` once per row. Pass only the fields the user needs with `include_fields` (for example `full_name,job_title,company_name,work_email`) so results stay short.
4. Use `min_confidence: "high"` when the user needs precision over coverage, and `required_fields` when a row is only useful with a given field (for example `work_email` or `phones.type:mobile`).
5. Each successful match uses a credit. Before enriching more than about 25 rows, tell the user the row count and ask them to confirm.
6. Return a table with one row per input, the fields requested, and a column for rows that didn't match. Don't paste raw JSON.
