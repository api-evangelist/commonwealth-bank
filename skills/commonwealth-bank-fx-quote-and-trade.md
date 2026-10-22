---
name: fx-quote-and-trade
description: Request, accept or cancel an FX quote and read valid trade dates via the partner-gated CommBank
  FX Pricing and Trading API.
api: openapi/commonwealth-bank-partner-api-openapi.yml
operations:
- partnerGetTradeDates
- partnerGetQuote
- partnerAcceptQuote
- partnerCancelQuote
auth: OAuth2 client_credentials issued at partner onboarding; x-request-id header
generated: '2026-10-20'
---

# fx-quote-and-trade

Request, accept or cancel an FX quote and read valid trade dates via the partner-gated CommBank FX Pricing and Trading API.

## Operations
- `partnerGetTradeDates` — GET /partner/api/markets/fx/trade-dates — partnerGetTradeDates
- `partnerGetQuote` — POST /partner/api/markets/fx/quote — partnerGetQuote
- `partnerAcceptQuote` — PUT /partner/api/markets/fx/quote — partnerAcceptQuote
- `partnerCancelQuote` — DELETE /partner/api/markets/fx/quote/{quote_id} — partnerCancelQuote

## Steps
1. Call partnerGetTradeDates for a currency pair.
2. Call partnerGetQuote (POST) to obtain a quote_id.
3. Call partnerAcceptQuote (PUT) to trade, or partnerCancelQuote (DELETE) to release it.
4. Accepting a quote executes a trade: require human confirmation.

## Rules
- Errors follow errors/commonwealth-bank-problem-types.yml; conventions in conventions/commonwealth-bank-conventions.yml.
- Auth: OAuth2 client_credentials issued at partner onboarding; x-request-id header.
