---
name: collect-payto-payments
description: Initiate a payment under an active PayTo agreement and poll its status via the partner-gated
  CommBank PayTo Payments API.
api: openapi/commonwealth-bank-payments-api-openapi.yml
operations:
- post-agreements-id-payments
- get-payments-id
auth: OAuth2 client_credentials issued at partner onboarding; scopes payments:payments:*
generated: '2026-10-20'
---

# collect-payto-payments

Initiate a payment under an active PayTo agreement and poll its status (partner-gated CommBank PayTo API).

## Operations
- `post-agreements-id-payments` — POST /agreements/{id}/payments — Create Payment
- `get-payments-id` — GET /payments/{id} — Get Payment

## Steps
1. Confirm the agreement is active (get-agreements-id in the manage-payto-agreements skill).
2. Initiate a payment with post-agreements-id-payments, sending x-idempotency-id and x-request-id.
3. Poll get-payments-id until the payment reaches a final status.

## Rules
- Errors follow errors/commonwealth-bank-problem-types.yml; conventions in conventions/commonwealth-bank-conventions.yml.
- This moves money: never retry without the same idempotency id the spec defines.
- Auth: OAuth2 client_credentials issued at partner onboarding; scopes payments:payments:*.
