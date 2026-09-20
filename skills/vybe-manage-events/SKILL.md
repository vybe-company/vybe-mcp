---
name: vybe-manage-events
description: Safely manage existing Vybe events through Vybe MCP. Use when a user asks to edit event pages, change tickets, invite guests, manage co-host access, scanner codes, participants, balances, payouts readiness, or Meta and TikTok pixels on Vybe.
license: MIT
compatibility: Requires network access and a Vybe MCP connection at https://tickets.vybe.social/api/mcp.
metadata:
  author: vybe
  category: events
---

# Manage events on Vybe

Make narrow, verified changes while preserving everything the user did not ask to change.

## Read before writing

1. Resolve the intended event with `events.list` when necessary.
2. Call `events.get` before every edit.
3. Confirm ambiguous requests, especially dates, location privacy, ticket economics, destructive changes, and tracking credentials.
4. Call `events.update` with only the required `sectionDiffs` and `ticketTypeDiffs`.
5. Read the event again when the result must be verified or used by a later operation.

Never rebuild the full event from memory.

## Section changes

Use `CREATE`, `UPDATE`, and `DELETE` diffs.

- Use stable section IDs returned by `events.get`.
- Structural sections have `event.*` IDs. Update them in place; never recreate them.
- Never delete required `event_name`, `theme`, `required_fields`, `visibility`, or `date_time` sections.
- Delete `cover_image` only when the user explicitly wants the optional poster removed.
- Preserve section order unless reordering is part of the request.
- Upload new media with `media.create_upload` and `media.confirm` before referencing its `mediaId`. Both calls require a typed `target`: `profile_gallery`, `event_cover`, `event_section`, `event_theme`, or `event_lineup`. `media.get` and `media.delete` use the same `target`.

## Ticket changes and invitations

- Confirm price, ISO currency, capacity, sale windows, visibility, and trigger behavior before changing a pool.
- Use ticket-type IDs returned by `events.get`.
- Do not delete or materially restrict a ticket pool without explaining the guest impact.
- Use `events.invite_participants` to issue selected public or hidden-pool tickets to verified email addresses. Treat addresses and ticket details as confidential.

## Door operations

- `events.list_scanner_codes` lists current codes.
- `events.create_scanner_code` creates labelled access for a staff member or entrance.
- `events.rename_scanner_code` changes or clears its label.
- `events.delete_scanner_code` revokes future access; already-confirmed scans remain confirmed.
- Share the code and `https://tickets.vybe.social/scanner` only with intended door staff.

After ticket changes, remind the host that at least 65% of sold tickets must be scanned before payouts unlock unless waived.

## Participants, balance, and measurement

- `events.list_participants` returns ticket-holder profiles by username, emails, join times, and tickets. `date_of_birth` and `gender` appear only when that event's `required_fields` selected them. Minimize exposure and never disclose this personal data unnecessarily.
- `events.get_balance` returns sales, fees, refunds, available funds, and scan readiness. Reading is allowed; payout requests remain human-only.
- `events.get_pixels` returns Meta/TikTok IDs and whether server tokens exist, never stored secrets.
- `events.update_pixel` sets or removes a pixel. Ask before changing tracking. Omit `accessToken` to preserve the existing secret; an empty `pixelId` removes the integration.

## Ownership and lifecycle

- For a human-owned event, use `events.create_agent_invite` and send the approval URL to the current owner.
- Publishing, payout requests, ownership transfer, cancellation, and other owner-only lifecycle actions must return or use the human-action URL. Do not imply the agent completed them.

Profiles use `username`, not `handle`.

Use `https://tickets.vybe.social/openapi.json` when exact payload fields are needed.
