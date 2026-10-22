---
name: list-accounts
description: As an Accredited Data Recipient acting on consumer consent, enumerate a customer's CommBank
  accounts and fetch account detail via the CDR Accounts API.
api: openapi/commonwealth-bank-accounts-api-api-openapi.yml
operations:
- listAccounts
- getAccountDetail
auth: CDR Accredited Data Recipient OAuth2 authorization_code + FAPI/mTLS (consumer consent); x-v header
generated: '2026-10-20'
---

# list-accounts

As an Accredited Data Recipient acting on consumer consent, enumerate a customer's CommBank accounts and fetch account detail via the CDR Accounts API.

## Operations
- `listAccounts` — GET /accounts — Get Accounts
- `getAccountDetail` — GET /accounts/{accountId} — Get Account Detail

## Steps
1. Obtain a consented access token through the CDR ADR OAuth2/FAPI flow over mTLS.
2. Call listAccounts (paged; follow links.next).
3. Call getAccountDetail for each accountId needed.

## Rules
- Errors follow errors/commonwealth-bank-problem-types.yml; conventions in conventions/commonwealth-bank-conventions.yml.
- Auth: CDR Accredited Data Recipient OAuth2 authorization_code + FAPI/mTLS (consumer consent); x-v header.
