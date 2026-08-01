---
name: Generate and download a SLOPE workbook report
description: Generate a workbook report, poll for completion, and download the output.
api: openapi/slope-software-openapi-original.json
operations: [GenerateWorkbookReport, GetWorkbookReportGenerationStatus, GetDownloadUrl]
generated: '2026-07-21'
method: generated
---

## Authentication
1. Exchange your API credentials at `POST /api/v1/Authorize` to receive a JWT `apiToken`.
2. Send `Authorization: Bearer <apiToken>` on every request.
3. Renew with `POST /api/v1/Authorize/Refresh` before expiry.

## Steps
1. `GenerateWorkbookReport` for the target workbook; capture the `generationId`.
2. Poll `GetWorkbookReportGenerationStatus` until generation completes.
3. `GetDownloadUrl` to obtain a pre-signed link and download the report.

## Conventions
- List endpoints paginate with `Offset` and `Limit`.
- Long-running work is asynchronous: start it, then poll the paired status endpoint until complete.
- Errors use the ProblemDetails envelope (`type`, `title`, `status`, `detail`); handle 400/401/403/404/409/429.
- On 429, back off and retry.

