---
name: fetch-product-reference-data
description: Retrieve CommBank's public CDR banking product catalogue (rates, fees, features, eligibility)
  with no auth and no consent, then drill into one product.
api: openapi/commonwealth-bank-products-api-api-openapi.yml
operations:
- listProducts
- getProductDetail
auth: none (public CDR PRD); x-v header required
generated: '2026-10-20'
---

# fetch-product-reference-data

Retrieve CommBank's public CDR banking product catalogue (rates, fees, features, eligibility) with no auth and no consent, then drill into one product.

## Operations
- `listProducts` — GET /products — Get Products
- `getProductDetail` — GET /products/{productId} — Get Product Detail

## Steps
1. Call listProducts, filtering/paging with the CDR page and page-size query params; follow links.next until absent.
2. Pick a productId and call getProductDetail for full rates, fees and eligibility.
3. Send x-v (and optionally x-min-v); a 406 means the requested version is unsupported.

## Rules
- Errors follow errors/commonwealth-bank-problem-types.yml; conventions in conventions/commonwealth-bank-conventions.yml.
- Auth: none (public CDR PRD); x-v header required.
