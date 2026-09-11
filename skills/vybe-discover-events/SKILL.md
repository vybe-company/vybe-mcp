---
name: vybe-discover-events
description: Search and browse Vybe event pages by time, location, and other live filters. Use when a user wants to find events, see what is soonest or nearby, open an event page, or look up a listing before creating or editing one.
license: MIT
metadata:
  author: Vybe
  homepage: https://tickets.vybe.social
---

# Discover Vybe events

Use this skill to find event pages on [Vybe](https://tickets.vybe.social). Call the hosted Vybe MCP server. Do not invent filters or response shapes.

## Endpoints

- MCP: `https://tickets.vybe.social/api/mcp`
- OpenAPI (exact payloads): `https://tickets.vybe.social/openapi.json`

Fetch the live OpenAPI document before searching or fetching events. Treat it as the source of truth for query parameters, sort orders, and response fields.

## When to use

- The user wants to browse or search events
- The user asks for soonest, nearby, or otherwise filtered listings
- You need to look up an event by id, slug, or URL before linking or editing it
- You are checking for an existing listing before creating a new one

## Workflow

1. Confirm the Vybe MCP tools are available. If they are missing, the user needs to connect the Vybe plugin or sign in at `https://tickets.vybe.social`. Some discovery tools may still work anonymously — use whatever the MCP server exposes.
2. Turn the user's request into search inputs the API actually supports. Common intents on Vybe:
   - Soonest upcoming events
   - Nearby / location-based events
   - A specific event opened from a URL or name
3. Read `https://tickets.vybe.social/openapi.json` and use the documented list/search/get operations. Do not invent query keys such as unofficial `q`, `lat`, or `sort` names.
4. Call MCP. If the user asked for nearby results, you need a location (coordinates or place). Ask for it when it is missing instead of assuming a city.
5. Present a concise list: title, time, place, and a link or id for each result. Then offer to open details for one event.
6. For a single event, fetch the detail operation from OpenAPI rather than reconstructing the page from search-card fields alone.

## Rules

- Never embed or hardcode API schemas in notes, code, or follow-up files. Link to the live OpenAPI URL.
- Never fabricate events, attendance counts, or ticket availability.
- If search returns nothing, say so and suggest relaxing filters. Do not pad results.
- Discovery is read-only. Creating a listing → `vybe-create-events`. Editing a hosted listing → `vybe-manage-events`.

## Handoff

- Hosting a new event → `vybe-create-events`
- Changing an event the user already hosts → `vybe-manage-events`
