---
name: retrieve-transactions
description: Page a consented CommBank account's transactions and fetch full detail for a transaction
  via the CDR Transactions API.
api: openapi/commonwealth-bank-transaction-api-api-openapi.yml
operations:
- getTransactions
- getTransactionDetail
auth: CDR Accredited Data Recipient OAuth2 authorization_code + FAPI/mTLS (consumer consent); x-v header
generated: '2026-10-20'
---

# retrieve-transactions

Page a consented CommBank account's transactions and fetch full detail for a transaction via the CDR Transactions API.

## Operations
- `getTransactions` — GET /accounts/{accountId}/transactions — Get Transactions
- `getTransactionDetail` — GET /accounts/{accountId}/transactions/{transactionId} — Get Transaction detail

## Steps
1. Call getTransactions for an accountId, bounding with oldest-time/newest-time and paging via links.next.
2. Call getTransactionDetail for extended data on a transactionId.

## Rules
- Errors follow errors/commonwealth-bank-problem-types.yml; conventions in conventions/commonwealth-bank-conventions.yml.
- Auth: CDR Accredited Data Recipient OAuth2 authorization_code + FAPI/mTLS (consumer consent); x-v header.
