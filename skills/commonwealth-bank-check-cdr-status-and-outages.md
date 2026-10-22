---
name: check-cdr-status-and-outages
description: Check the operational status and scheduled outages of CommBank's CDR APIs before calling
  them.
api: openapi/commonwealth-bank-discovery-api-api-openapi.yml
operations:
- getStatus
- getOutages
auth: none (public discovery endpoints); x-v header
generated: '2026-10-20'
---

# check-cdr-status-and-outages

Check the operational status and scheduled outages of CommBank's CDR APIs before calling them.

## Operations
- `getStatus` — GET /status — Get Status
- `getOutages` — GET /outages — Get Outages

## Steps
1. Call getStatus; if not OK, back off.
2. Call getOutages to plan around scheduled maintenance.

## Rules
- Errors follow errors/commonwealth-bank-problem-types.yml; conventions in conventions/commonwealth-bank-conventions.yml.
- Auth: none (public discovery endpoints); x-v header.
