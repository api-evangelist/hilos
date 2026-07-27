---
name: Sync a contact and run a flow
description: Upsert a contact by phone, then trigger a no-code Hilos flow for them and track execution.
api: openapi/hilos-openapi-original.yml
operations:
  - Create or Update Contact
  - Create a Flow Execution
  - Get Flow Execution
  - List Flow Execution Contact
---

# Sync a contact and run a flow

Use this skill to onboard/update a contact and start an automated WhatsApp flow for them.

## Auth
`https://api.hilos.io/api/` with `Authorization: Token <YOUR_API_KEY>`.

## Steps
1. **Upsert the contact.** Call `Create or Update Contact` (`POST /api/contact`). Hilos matches on
   `phone`: if a contact with that phone exists it is partially updated, otherwise created — so this
   is safe to call repeatedly. Use `overwrite_meta` / `overwrite_tags` if you need to replace rather
   than merge `meta`/`tags`.
2. **Run the flow.** Call `Create a Flow Execution` (`POST /api/flow/{id}/run`) with the flow `id`
   and the contact(s) to enroll.
3. **Track it.** Poll `Get Flow Execution` (`GET /api/flow-execution/{id}`) for overall status, and
   `List Flow Execution Contact` (`GET /api/flow-execution-contact`) to see per-contact progress.

## Rules
- Pagination is `page` / `page_size` (`conventions/hilos-conventions.yml`).
- Plain-JSON errors, codes 401/403/404/405/500 (`errors/hilos-problem-types.yml`).
