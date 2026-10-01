---
name: research-a-company
description: Research a company with Data Legion. Use when the user asks about a company's size, industry, growth, hiring or makeup, or wants an account brief before outreach.
---

To research a company:

1. Call `company_enrich` with the best identifier available: domain first, then LinkedIn URL or ticker, then name. When only a name is known, add `industry` (a lowercase LinkedIn industry value) to narrow the match, and confirm with the user if more than one company could be meant.
2. Summarize what the result shows: industry, headquarters, employee count and its trend, hiring and attrition, and how the workforce breaks down by function and seniority.
3. If the user wants people at the company, follow up with `person_search` (for example `SELECT * FROM people WHERE company_name ILIKE '%acme%' AND job_title ILIKE '%director%'`).
4. Write the brief in short sections with figures, and say which figures come from Data Legion.
