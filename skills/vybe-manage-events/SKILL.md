---
name: vybe-manage-events
description: Update, publish, unpublish, and cancel existing Vybe event pages, including ticket tiers, promotion settings, and host-side event details. Use when a user wants to edit a listing they already host, change tickets, or take an event live or offline.
license: MIT
metadata:
  author: Vybe
  homepage: https://tickets.vybe.social
---

# Manage Vybe events

Use this skill to change event pages the user already hosts on [Vybe](https://tickets.vybe.social). Call the hosted Vybe MCP server. Do not invent request bodies.

## Endpoints

- MCP: `https://tickets.vybe.social/api/mcp`
- OpenAPI (exact payloads): `https://tickets.vybe.social/openapi.json`

Fetch the live OpenAPI document before any update, publish, unpublish, or cancel call. Treat it as the source of truth for identifiers, writable fields, and side effects.

## When to use

- The user wants to edit an event they host
- Ticket tiers, prices, capacity, or sale windows need to change
- The user wants to publish, unpublish, cancel, or otherwise change listing status
- Promotion or host-side settings on an existing event need an update

## Workflow

1. Confirm the Vybe MCP tools are available. If they are missing, the user needs to connect the Vybe plugin or sign in at `https://tickets.vybe.social`.
2. Resolve the target event. Use an explicit event id or URL when the user provided one. Otherwise list the user's hosted events via MCP and confirm the match before writing.
3. Read the current event (and ticket objects) through MCP so updates are diffs against live state, not guesses.
4. Read `https://tickets.vybe.social/openapi.json` for the exact patch/update/status operations. Send only fields the user asked to change, using schema names and types from OpenAPI.
5. Apply the change. For destructive actions (cancel, unpublish, delete, refunds if exposed), confirm with the user first.
6. Re-read or use the mutation response to confirm the new state. Summarize what changed and what stayed the same.

## Rules

- Never embed or hardcode API schemas in notes, code, or follow-up files. Link to the live OpenAPI URL.
- Never invent event, ticket, or order ids. If lookup fails, say so and offer to list hosted events.
- Do not overwrite unspecified fields. Prefer partial updates when the API supports them.
- Status transitions must follow the OpenAPI operations (for example draft → published → canceled). Do not assume arbitrary status strings are valid.
- If MCP returns an auth or permission error, stop and ask the user to sign in. Host tools only work for events the signed-in account can manage.

## Handoff

- Creating a new event page → `vybe-create-events`
- Searching public or nearby events → `vybe-discover-events`
