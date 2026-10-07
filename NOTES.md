# Patch Notes

## Summary

- Grouped title and description search conditions so archive and status filters apply to every match.
- Moved result paging into the database query and reject invalid status, page, or excessively large page-size requests.
- Removed artificial request latency; cancel obsolete browser requests and recover loading/error state correctly.
- Reset pagination when search filters change. Kept the Oracle reference and H2 query aligned.

## What I left unchanged

I did not redesign the UI, change the API response shape, or add write operations. The dataset is small, but database paging avoids loading every matching task for each page request.

## Biggest remaining risk

The list endpoint has no authentication or authorization, which is acceptable for this local exercise but must be addressed before production. Search terms also treat `%` and `_` as `LIKE` wildcards. `npm ci` reported eight dependency advisories, including five high severity; I did not upgrade dependencies in this focused patch.

## Tools

I used GitHub Copilot to inspect the code and implement the patch, then checked it with Maven, npm, and direct API requests. I reviewed the resulting changes and will write the required explanations by hand and add photos under `handwritten/` before submitting.