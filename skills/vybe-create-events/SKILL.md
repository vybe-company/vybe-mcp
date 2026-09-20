---
name: vybe-create-events
description: Create polished, conversion-focused Vybe event drafts through Vybe MCP. Use when a user asks to create, host, plan, draft, or set up an event, tickets, event artwork, lineup, venue details, FAQs, waitlists, group chats, or promoter programs on Vybe.
license: MIT
compatibility: Requires network access and a Vybe MCP connection at https://tickets.vybe.social/api/mcp.
metadata:
  author: vybe
  category: events
---

# Create events on Vybe

Create complete Vybe drafts from verified user input. Act as an event-page editor, not a form filler.

## Before creating

Ask a concise batch of questions for material facts that are missing or ambiguous. Never invent:

- event concept or name;
- start/end date, time, or time zone;
- venue, exact guest entrance, entry instructions, or location privacy;
- ticket price, currency, capacity, sale windows, visibility, or unlock order;
- artist identities, links, attractions, VIP benefits, policies, artwork, or tracking IDs.

Do not require every optional detail before beginning. Separate facts required to create a valid draft from improvements that can be added later.

## Build the draft

1. If media is needed, call `media.create_upload` with a typed `target` (`profile_gallery`, `event_cover`, `event_section`, `event_theme`, or `event_lineup`), upload the exact declared JPEG or MP4 bytes to the signed URL, then call `media.confirm` with the same `target`. Use returned `mediaId` values in sections.
2. Call `events.create` once with one ordered `sections` array and optional `ticketTypes`.
3. Give the user the returned event URL and human claim/publish URL. The agent creates a draft; a human becomes main host and publishes it.

Required singleton sections:

- `event_name` — short and memorable;
- `theme`;
- `required_fields` — may include `first_name`, `last_name`, `instagram_handle`, `profile_picture`, `phone`, `date_of_birth`, and `gender`;
- `visibility` — `public` or `unlisted`;
- `date_time` — accurate `startsAt`, `endsAt`, and IANA `timeZone`.

Recommended when relevant and known:

- `cover_image` with a strong poster;
- the first `text` section as a concise primary description explaining what, where, and why to attend;
- `location` with venue name, exact entrance, optional entry instructions, approximate public location, and `public` or `participants_only` privacy.

## Page quality

Keep the first screen clear and persuasive. Use only sections that support the event:

- `lineup` for artists, imagery, Instagram, Spotify, and Apple Music links;
- `images` followed by focused `text` for venue, past-event proof, attractions, or VIP areas;
- `faq` for verified pre-purchase questions such as entry rules, age limits, accessibility, transport, refunds, timing, and what to bring;
- `group_chat`, `waitlist`, and `promoter_program` when they have an actual role.

Avoid filler, duplicated claims, irrelevant sections, and unsupported hype.

## Tickets

For each ticket pool, confirm name, description, price, ISO currency, capacity, sale window, and visibility.

- Use `visibility: hidden` for invite-only pools.
- During creation, use `clientId` and `triggerPoolClientId` to unlock a later pool when an earlier one sells out.
- Do not infer prices, capacities, or refund terms.

## After creation

- Offer to create labelled door-staff access with `events.create_scanner_code`; the scanner is at `https://tickets.vybe.social/scanner`.
- Explain that at least 65% of sold tickets must be scanned in person before payouts unlock unless the event has a waiver.
- Do not claim to publish, request payouts, or transfer ownership. These actions are human-only.

Profiles use `username`, not `handle`.

Use `https://tickets.vybe.social/openapi.json` when exact payload fields are needed.
