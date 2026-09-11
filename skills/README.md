# Vybe Agent Skills

Portable [Agent Skills](https://agentskills.io/) for creating, managing, and
discovering events on Vybe.

## Install

Install all Vybe skills from this public repository:

```bash
npx skills add vybe-company/vybe-mcp
```

Or install one focused skill:

```bash
npx skills add vybe-company/vybe-mcp --skill vybe-create-events
npx skills add vybe-company/vybe-mcp --skill vybe-manage-events
npx skills add vybe-company/vybe-mcp --skill vybe-discover-events
```

The Skills CLI supports Cursor, Claude Code, Codex, and other Agent Skills
clients. Add `--agent <agent-name>` to target one client or `-g` to install
globally.

## Included skills

| Skill | Use it for |
|---|---|
| `vybe-create-events` | Event drafts, sections, artwork, ticket strategy, and human handoff |
| `vybe-manage-events` | Safe edits, invitations, scanners, participants, balances, and pixels |
| `vybe-discover-events` | Public search, nearby browsing, event reads, and recommendations |

Creating and managing events requires Vybe MCP at
`https://tickets.vybe.social/api/mcp`. Discovery uses the public REST API and
does not require authentication.

Use `https://tickets.vybe.social/openapi.json` for the live request and
response schemas. Do not copy those schemas into the skills.
