---
name: vybe-create-events
description: Create and publish Vybe event pages with tickets, schedule, location, and promotion settings. Use when a user wants to host an event, draft an event page, add ticket tiers, or publish a new listing on Vybe.
license: MIT
metadata:
  author: Vybe
  homepage: https://tickets.vybe.social
---

# Create Vybe events

Use this skill to create event pages on [Vybe](https://tickets.vybe.social). Call the hosted Vybe MCP server. Do not invent request bodies.

## Endpoints

- MCP: `https://tickets.vybe.social/api/mcp`
- OpenAPI (exact payloads): `https://tickets.vybe.social/openapi.json`

Fetch the live OpenAPI document before writing any create/publish call. Treat it as the source of truth for required fields, enums, formats, and nested objects.

## When to use

- The user wants to host or publish a new event
- The user is drafting an event page, ticket tiers, or a first listing
- Another skill found no existing event and the user asked to create one

## Workflow

1. Confirm the Vybe MCP tools are available. If they are missing, the user needs to connect the Vybe plugin or sign in at `https://tickets.vybe.social`.
2. Collect the event facts you do not already have. Ask only for missing required data. Typical inputs:
   - Title and public description
   - Start/end time and timezone
   - Location (in-person address/venue, virtual link, or hybrid)
   - Visibility (public vs unlisted/private, if the API supports it)
   - Ticket tiers (name, price, quantity, sale window)
   - Cover image or media, if the user has one
3. Read `https://tickets.vybe.social/openapi.json` and map the user's answers onto the create-event (and related ticket) operations. Use the schema names and types from OpenAPI — do not guess field names.
4. Create the event through MCP. Prefer a draft/unpublished create when the API offers one, then attach tickets and media, then publish.
5. Validate the response. Give the user the event id, public URL, and a short summary of what was published.
6. If create succeeds but publish or ticket setup fails, report the partial state and the next MCP call needed. Do not silently leave a half-finished listing.

## Rules

- Never embed or hardcode API schemas in notes, code, or follow-up files. Link to the live OpenAPI URL.
- Never fabricate event ids, ticket ids, or share URLs.
- Do not publish until the user has confirmed title, time, location, and pricing (including free).
- Prices, currencies, and datetimes must match the OpenAPI formats. Convert casual times (“Saturday 9pm”) into the API’s timezone-aware representation.
- If MCP returns an auth or permission error, stop and ask the user to sign in. Do not retry with invented tokens.

## Handoff

- Updating, canceling, or changing tickets on an existing event → `vybe-manage-events`
- Finding events to clone, link, or check for duplicates → `vybe-discover-events`
