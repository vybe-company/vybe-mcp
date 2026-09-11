# Vybe Agent Skills

Agent Skills for creating, discovering, and managing event pages on [Vybe](https://tickets.vybe.social).

Install the package from the repository root:

```bash
npx skills add vybe-company/vybe-mcp
```

Or install one skill at a time:

```bash
npx skills add vybe-company/vybe-mcp --skill vybe-create-events
npx skills add vybe-company/vybe-mcp --skill vybe-manage-events
npx skills add vybe-company/vybe-mcp --skill vybe-discover-events
```

## Skills

| Skill | Use when |
| --- | --- |
| [`vybe-create-events`](./vybe-create-events/SKILL.md) | Hosting or publishing a new event page |
| [`vybe-manage-events`](./vybe-manage-events/SKILL.md) | Editing, publishing, or canceling an event you already host |
| [`vybe-discover-events`](./vybe-discover-events/SKILL.md) | Searching soonest, nearby, or named event listings |

## Live API

Skills call the hosted Vybe MCP server and read exact payloads from the live OpenAPI document. Do not copy schemas into a skill.

- MCP: `https://tickets.vybe.social/api/mcp`
- OpenAPI: `https://tickets.vybe.social/openapi.json`
