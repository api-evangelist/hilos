---
name: Send a WhatsApp template message
description: Look up an approved WhatsApp template and send it to a recipient with variables.
api: openapi/hilos-openapi-original.yml
operations:
  - List WhatsApp Templates
  - Get WhatsApp Template
  - Send a WhatsApp Template Message
---

# Send a WhatsApp template message with Hilos

Use this skill to send a single templated WhatsApp message through Hilos.

## Auth
Every request goes to `https://api.hilos.io/api/` with header
`Authorization: Token <YOUR_API_KEY>` (create keys at https://app.hilos.io/dev/api-keys).

## Steps
1. **Find the template.** Call `List WhatsApp Templates` (`GET /api/channels/whatsapp/template`).
   You can narrow the list with `?search=<name>` and page with `page` / `page_size`.
2. **(Optional) Inspect it.** Call `Get WhatsApp Template` (`GET /api/channels/whatsapp/template/{id}`)
   to read the template body and the variables it expects. Only `status: APPROVED` templates can be sent.
3. **Send.** Call `Send a WhatsApp Template Message`
   (`POST /api/channels/whatsapp/template/{id}/send`) with the recipient phone number and the
   variable values the template requires.

## Rules
- Errors are plain JSON with status codes 401 (bad token), 403, 404, 405, 500 — see
  `errors/hilos-problem-types.yml`.
- There is no idempotency-key header (`conventions/hilos-conventions.yml`); do not blindly retry a
  send on a timeout without checking delivery, to avoid duplicate messages.
