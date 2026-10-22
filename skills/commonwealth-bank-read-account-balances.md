---
name: read-account-balances
description: Read balances for one, all, or a chosen set of consented CommBank accounts via the CDR Balances
  API.
api: openapi/commonwealth-bank-balances-api-api-openapi.yml
operations:
- getBalances
- listBalancesBulk
- listBalancesSpecificAccounts
auth: CDR Accredited Data Recipient OAuth2 authorization_code + FAPI/mTLS (consumer consent); x-v header
generated: '2026-10-20'
---

# read-account-balances

Read balances for one, all, or a chosen set of consented CommBank accounts via the CDR Balances API.

## Operations
- `getBalances` — GET /accounts/{accountId}/balance — Get Balances
- `listBalancesBulk` — GET /accounts/balances — Get Bulk Balances
- `listBalancesSpecificAccounts` — POST /accounts/balances — Get Balances For Specific Accounts

## Steps
1. For one account call getBalances.
2. For every consented account call listBalancesBulk (paged).
3. For a chosen set POST accountIds to listBalancesSpecificAccounts — a read, not a write, so it is safe to retry.

## Rules
- Errors follow errors/commonwealth-bank-problem-types.yml; conventions in conventions/commonwealth-bank-conventions.yml.
- Auth: CDR Accredited Data Recipient OAuth2 authorization_code + FAPI/mTLS (consumer consent); x-v header.
