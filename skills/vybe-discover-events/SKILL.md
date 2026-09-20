---
name: vybe-discover-events
description: Search, compare, and recommend public Vybe events using the public discovery API. Use when a user asks what is happening, wants events by date or location, needs nearby recommendations, searches by theme or name, or wants details about a Vybe event link or token.
license: MIT
compatibility: Requires network access to the public Vybe API at https://tickets.vybe.social/api/v1.
metadata:
  author: vybe
  category: events
---

# Discover events on Vybe

Find relevant public events without requiring authentication.

## Choose the request

Use:

- `GET https://tickets.vybe.social/api/v1/discovery` to search and browse;
- `GET https://tickets.vybe.social/api/v1/events/{token}` to inspect a specific public event.

Discovery parameters:

- `query` — typo-tolerant name and primary-description search;
- `location` — locality text filter;
- `sort=top|soonest|nearby`;
- `latitude`, `longitude`, and optional `radiusKm` for nearby search;
- `limit` from 1 to 50;
- opaque `pageToken` for the next page.

`nearby` requires both latitude and longitude. Ask before using a user's precise location; prefer a city or user-provided coordinates when that is sufficient.

## Search workflow

1. Ask only for missing constraints that materially change the result: location, date preference, event type, party size, accessibility, budget, or distance.
2. Start with the narrowest useful discovery request.
3. Follow `nextPageToken` only when more results are needed, keeping all filters unchanged.
4. Fetch a specific event by token before answering detailed questions about tickets, timing, venue, or policies.
5. Compare only fields present in the response. Never infer age limits, availability, refund policy, accessibility, lineup, exact location, or ticket inclusions. Public event `required_fields` may include `date_of_birth` and `gender`; those values are not part of public discovery or public profiles. Organizer identities use `username`, not `handle`.

## Recommendations

Present a short ranked list with:

- event name;
- date/time and time zone;
- public or approximate location;
- visible ticket offer or price when returned;
- one concrete reason it matches;
- canonical event URL.

Distinguish fact from recommendation. If no result is a strong match, say so and suggest one useful filter change rather than broadening silently.

Location may intentionally be privacy-safe. Do not claim an approximate location is the exact entrance; participant-only details are revealed to eligible ticket holders.

Use `https://tickets.vybe.social/openapi.json` for the complete response schema and current query constraints.
