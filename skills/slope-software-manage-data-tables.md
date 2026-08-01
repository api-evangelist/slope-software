---
name: Import and update SLOPE data tables
description: Upload a file via pre-signed URL and load/update a SLOPE data table.
api: openapi/slope-software-openapi-original.json
operations: [GetUploadUrl, SaveUpload, ImportDataTable, GetDataTableData, UpdateDataTableData]
generated: '2026-07-21'
method: generated
---

## Authentication
1. Exchange your API credentials at `POST /api/v1/Authorize` to receive a JWT `apiToken`.
2. Send `Authorization: Bearer <apiToken>` on every request.
3. Renew with `POST /api/v1/Authorize/Refresh` before expiry.

## Steps
1. `GetUploadUrl` to obtain a pre-signed upload URL.
2. Upload the file to that URL, then confirm with `SaveUpload`.
3. `ImportDataTable` to create a data table from the uploaded file.
4. `GetDataTableData` to verify the loaded rows.
5. `UpdateDataTableData` to patch values as needed.

## Conventions
- List endpoints paginate with `Offset` and `Limit`.
- Long-running work is asynchronous: start it, then poll the paired status endpoint until complete.
- Errors use the ProblemDetails envelope (`type`, `title`, `status`, `detail`); handle 400/401/403/404/409/429.
- On 429, back off and retry.

