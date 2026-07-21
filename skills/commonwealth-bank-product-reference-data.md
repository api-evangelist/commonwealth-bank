---
name: Fetch CommBank product reference data
description: >-
  Retrieve Commonwealth Bank's public banking product catalogue (rates, fees,
  features, eligibility) via the CDR Product Reference Data API — no auth, no
  consent. Use to compare CBA products or seed a product-detail lookup.
api: openapi/commonwealth-bank-cdr-products-openapi.json
operations: [listProducts, getProductDetail]
auth: none (public CDR PRD surface)
---

# Fetch CommBank product reference data

The CDR Product Reference Data (PRD) surface is **public and unauthenticated**.
Base: `https://api.commbank.com.au/public/cds-au/v1/banking`.

## Rules
- Send a supported version header `x-v: 3` on every request. Missing/unsupported
  version returns **HTTP 406**.
- Page results with `page` and `page-size` (max 1000); read `meta.totalPages`
  and follow `links.next`.
- Errors come back as a CDS `ResponseErrorList` (`errors[].code` URN,
  `title`, `detail`) — never `application/problem+json`. See
  `errors/commonwealth-bank-problem-types.yml`.

## Steps
1. `listProducts` — `GET /banking/products` (optionally filter by
   `product-category`, `open-status`). Collect `data.products[].productId`.
2. For each product of interest, `getProductDetail` —
   `GET /banking/products/{productId}` for rates/fees/features/eligibility.
3. Handle **429** with backoff; handle **406** by correcting `x-v`.
