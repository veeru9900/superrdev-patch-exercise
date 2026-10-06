# Patch Notes

## Summary of changes
- Fixed task-search SQL precedence so the `archived = FALSE` and status filters apply to both title and description matches.
- Removed artificial controller delay that made short/blank searches unnecessarily slow.
- Added validation for `page` and `pageSize`, plus a clear 400 response for invalid statuses.
- Prevented stale frontend search responses from overwriting newer results with `AbortController`; errors are also cleared for each new request.
- Reset pagination to page 1 whenever the search text or status filter changes.
- Updated the Oracle reference SQL to mirror the corrected search predicate.

## What I chose not to change
I did not rewrite the repository around Spring `Pageable`, add new CRUD features, or redesign the UI. The current in-memory result/pagination approach is acceptable for this small exercise, and a larger refactor would exceed the requested focused patch.

## Biggest remaining risk
The backend still loads all matching tasks into memory before slicing the requested page. This will become a performance/scalability problem as the task table grows. A production version should use database-side pagination and a count query.

## Tools/AI used
I used ChatGPT to review the code, identify likely failure modes, and help draft focused fixes. I reviewed each change against the existing request/response flow and kept the patch limited to issues I could explain and defend.
