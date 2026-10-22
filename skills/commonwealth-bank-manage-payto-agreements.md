---
name: manage-payto-agreements
description: Validate, create, read, amend and change the status of PayTo agreements via the partner-gated
  CommBank PayTo Agreements API.
api: openapi/commonwealth-bank-agreements-api-openapi.yml
operations:
- agreements-validate
- CreateAgreement
- get-agreements-id
- patch-agreement-id
- change-agreement-status
auth: OAuth2 client_credentials issued at partner onboarding; scopes payments:agreements:*
generated: '2026-10-20'
---

# manage-payto-agreements

Validate, create, read, amend and change the status of PayTo agreements (partner-gated CommBank PayTo API).

## Operations
- `agreements-validate` — POST /agreements/validate — Validate Agreement
- `CreateAgreement` — POST /agreements — Create Agreement
- `get-agreements-id` — GET /agreements/{id} — Get Agreement
- `patch-agreement-id` — PATCH /agreements/{id} — Modify Agreement
- `change-agreement-status` — PATCH /agreements/{id}/status — Change Agreement Status

## Steps
1. Optionally check service health first with `HealthCheck` (GET /agreements/health, in openapi/commonwealth-bank-utilities-api-openapi.yml).
2. Call agreements-validate, then CreateAgreement.
3. Read with get-agreements-id; amend with patch-agreement-id (send x-idempotency-id and x-request-id); suspend/resume/cancel with change-agreement-status.
4. To collect funds under an active agreement, continue with the collect-payto-payments skill.

## Rules
- Errors follow errors/commonwealth-bank-problem-types.yml; conventions in conventions/commonwealth-bank-conventions.yml.
- Writes change mandate state: never retry a write without the same idempotency id the spec defines.
- Auth: OAuth2 client_credentials issued at partner onboarding; scopes payments:agreements:*.
