# vybe-mcp

Agent Skills and Cursor plugin for creating, discovering, and managing event pages on [Vybe](https://tickets.vybe.social).

## Install skills

Install every skill in this repository:

```bash
npx skills add vybe-company/vybe-mcp
```

Install one skill at a time:

```bash
npx skills add vybe-company/vybe-mcp --skill vybe-create-events
npx skills add vybe-company/vybe-mcp --skill vybe-manage-events
npx skills add vybe-company/vybe-mcp --skill vybe-discover-events
```

Preview what the package provides without installing:

```bash
npx skills add vybe-company/vybe-mcp --list
```

## Skills

| Skill | Use when |
| --- | --- |
| `vybe-create-events` | Hosting or publishing a new event page |
| `vybe-manage-events` | Editing, publishing, or canceling an event you already host |
| `vybe-discover-events` | Searching soonest, nearby, or named event listings |

See [`skills/README.md`](./skills/README.md) for the skill catalog.

## Vybe MCP

Point agents at the hosted Vybe MCP server:

```
https://tickets.vybe.social/api/mcp
```

This repository ships that URL in [`mcp.json`](./mcp.json) so the Cursor plugin can connect automatically. Sign in at [tickets.vybe.social](https://tickets.vybe.social) when a tool requires an authenticated host session.

## OpenAPI

Use the live OpenAPI document for exact request and response payloads. Do not copy schemas into skills or local notes.

```
https://tickets.vybe.social/openapi.json
```

## Cursor plugin

This repo is also a Cursor plugin (`.cursor-plugin/plugin.json` + `mcp.json`). After it is listed on the Cursor Marketplace, install **Vybe** from **Cursor Settings → Plugins**. Locally, clone this repository and add it as a plugin from source.

## License

[MIT](./LICENSE)
