---
name: confirm-payee-name
description: Check an account name against BSB/account before paying, using CommBank NameCheck (partner-gated).
api: openapi/commonwealth-bank-accounts-api-openapi.yml
operations:
- post-accounts-name-check
auth: OAuth2 client_credentials; scope payments:namecheck:read; x-request-id header
generated: '2026-10-20'
---

# confirm-payee-name

Check an account name against BSB/account before paying, using CommBank NameCheck (partner-gated).

## Operations
- `post-accounts-name-check` — POST /payments/v1/accounts/namecheck — NameCheck

## Steps
1. POST the payee BSB, account number and name to post-accounts-name-check.
2. Act on the match result before initiating any payment.

## Rules
- Errors follow errors/commonwealth-bank-problem-types.yml; conventions in conventions/commonwealth-bank-conventions.yml.
- Auth: OAuth2 client_credentials; scope payments:namecheck:read; x-request-id header.
