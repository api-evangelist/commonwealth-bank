---
name: List CommBank accounts and balances
description: >-
  As an Accredited Data Recipient acting on consumer consent, enumerate a
  customer's CommBank accounts and read their balances via the CDR Accounts and
  Balances APIs over the authenticated ADR channel.
api: openapi/commonwealth-bank-cdr-accounts-openapi.json
operations: [listAccounts, getAccountDetail, listBalancesBulk, getBalances, listBalancesSpecificAccounts]
auth: CDR ADR OAuth2 authorization_code + FAPI/mTLS (consumer consent)
---

# List CommBank accounts and balances

Authorised CDR surface. Base:
`https://secure.api.commbank.com.au/api/cds-au/v1/banking`. Requires an ADR
access token issued under explicit consumer consent (scopes
`bank:accounts.basic:read`, `bank:accounts.detail:read`). See
`authentication/commonwealth-bank-authentication.yml` and
`scopes/commonwealth-bank-scopes.yml`.

## Rules
- Send `x-v: 1` (per-endpoint version), the FAPI headers
  (`x-fapi-interaction-id`, `x-fapi-auth-date`), and the bearer/mTLS-bound token.
- Read-only: no idempotency key needed.
- Paginate with `page` / `page-size`; follow `links.next`.

## Steps
1. `listAccounts` — `GET /banking/accounts` (filter by `product-category`,
   `open-status`, `is-owned`). Collect `data.accounts[].accountId`.
2. `getAccountDetail` — `GET /banking/accounts/{accountId}` for full account
   detail where needed.
3. Balances — either `listBalancesBulk` (`GET /banking/accounts/balances`) for
   all accounts, `listBalancesSpecificAccounts`
   (`POST /banking/accounts/balances` with an accountIds body), or `getBalances`
   (`GET /banking/accounts/{accountId}/balance`) for one.
4. On **406** fix `x-v`; on **429** back off; surface `errors[].detail`.
