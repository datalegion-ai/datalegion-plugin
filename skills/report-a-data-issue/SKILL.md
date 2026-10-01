---
name: report-a-data-issue
description: Report a wrong or outdated Data Legion record. Use when the user says a person or company result is incorrect, stale, belongs to someone else, merges two people, or is a duplicate.
---

To report a data issue:

1. You need the record's `legion_id` from an earlier `person_enrich`, `person_search`, `company_enrich` or `company_search` result.
2. Pick `issue_type`: `incorrect` (a value is wrong), `outdated` (a value is stale), `misattributed` (a value belongs to someone else), `frankenstein` (the record merges more than one real person), `not_a_real_person`, or `duplicate`.
3. Pick `issue_level`: `record` for the whole record, `group` for a field group such as `experience`, or `field` for one field such as `job_title`. Set `field` for group and field level.
4. Include `correct_value`, a `comment`, or both, and the `observed_value` when the user quoted it.
5. Call `report_person` or `report_company`. Reports are free. Tell the user the report id and that Data Legion reviews each report.
