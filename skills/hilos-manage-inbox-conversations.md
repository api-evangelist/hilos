---
name: Manage inbox conversations
description: List inbox conversations and update their state (assignment, status) programmatically.
api: openapi/hilos-openapi-original.yml
operations:
  - List Conversations
  - Update a Conversation
  - Partially update a Conversation
---

# Manage inbox conversations

Use this skill to read and update Hilos inbox conversations.

## Auth
`https://api.hilos.io/api/` with `Authorization: Token <YOUR_API_KEY>`.

## Steps
1. **List conversations.** Call `List Conversations` (`GET /api/inbox/conversation`), paging with
   `page` / `page_size`.
2. **Update one.** Use `Partially update a Conversation`
   (`PATCH /api/inbox/conversation/{id}/update`) to change only specific fields, or
   `Update a Conversation` (`PUT /api/inbox/conversation/{id}/update`) to replace the resource.

## Rules
- Use `PATCH` for targeted edits; `PUT` expects the full representation.
- Plain-JSON errors, codes 401/403/404/405/500 (`errors/hilos-problem-types.yml`);
  no idempotency-key header (`conventions/hilos-conventions.yml`).
