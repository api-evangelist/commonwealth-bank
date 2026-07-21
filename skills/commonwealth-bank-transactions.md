---
name: Retrieve CommBank account transactions
description: >-
  As an Accredited Data Recipient with consumer consent, page a CommBank
  account's transactions and fetch full transaction detail via the CDR
  Transactions API.
api: openapi/commonwealth-bank-cdr-transactions-openapi.json
operations: [getTransactions, getTransactionDetail]
auth: CDR ADR OAuth2 authorization_code + FAPI/mTLS (consumer consent)
---

# Retrieve CommBank account transactions

Authorised CDR surface. Base:
`https://secure.api.commbank.com.au/api/cds-au/v1/banking`. Requires an ADR
token with scope `bank:transactions:read` (obtain `accountId` first via the
accounts skill).

## Rules
- Send `x-v: 1` plus the FAPI headers and the consumer-consented token.
- Filter with `oldest-time` / `newest-time`, `min-amount` / `max-amount`,
  and `text`; paginate with `page` / `page-size`.
- Read-only; CDS `ResponseErrorList` error envelope.

## Steps
1. `getTransactions` — `GET /banking/accounts/{accountId}/transactions` with the
   desired time/amount filters. Collect `data.transactions[].transactionId`.
2. `getTransactionDetail` —
   `GET /banking/accounts/{accountId}/transactions/{transactionId}` for full
   detail (extended data, merchant, etc.).
3. Handle **406** (version), **404** (unknown account/transaction under this
   consent), **429** (rate limit) per `errors/commonwealth-bank-problem-types.yml`.
