---
name: Run a SLOPE projection from a template
description: Pick a model, instantiate a projection from a template, run it, and poll for results.
api: openapi/slope-software-openapi-original.json
operations: [ListModels, GetProjectionTemplatesByModelId, CreateProjectionFromTemplate, RunProjectionById, GetProjectionById]
generated: '2026-07-21'
method: generated
---

## Authentication
1. Exchange your API credentials at `POST /api/v1/Authorize` to receive a JWT `apiToken`.
2. Send `Authorization: Bearer <apiToken>` on every request.
3. Renew with `POST /api/v1/Authorize/Refresh` before expiry.

## Steps
1. `ListModels` (Offset/Limit) to find the target `ModelId`.
2. `GetProjectionTemplatesByModelId` to choose a projection template.
3. `CreateProjectionFromTemplate` with the template + inputs to create a projection; capture `projectionId`.
4. `RunProjectionById` to kick off the run.
5. Poll `GetProjectionById` until the run status is complete, then read results.

## Conventions
- List endpoints paginate with `Offset` and `Limit`.
- Long-running work is asynchronous: start it, then poll the paired status endpoint until complete.
- Errors use the ProblemDetails envelope (`type`, `title`, `status`, `detail`); handle 400/401/403/404/409/429.
- On 429, back off and retry.

