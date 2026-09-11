# Vybe Agent Skills

Official [Agent Skills](https://agentskills.io/) for creating, managing, and discovering events on [Vybe](https://tickets.vybe.social).

This public repository is the installable Vybe skills package. It also ships as an [Agent Plugin](https://agent-plugins.org/) so Cursor and other compatible clients can load the skills together with the Vybe MCP server.

## Install

Install every Vybe skill:

```bash
npx skills add vybe-company/vybe-mcp
```

Or install one focused skill:

```bash
npx skills add vybe-company/vybe-mcp --skill vybe-create-events
npx skills add vybe-company/vybe-mcp --skill vybe-manage-events
npx skills add vybe-company/vybe-mcp --skill vybe-discover-events
```

The Skills CLI supports Cursor, Claude Code, Codex, and other Agent Skills clients. Add `--agent <agent-name>` to target one client or `-g` to install globally.

Preview what a source would install without writing files:

```bash
npx skills add vybe-company/vybe-mcp --list
```

## Included skills

| Skill | Use it for |
| --- | --- |
| [`vybe-create-events`](skills/vybe-create-events/SKILL.md) | Event drafts, sections, artwork, ticket strategy, and human handoff |
| [`vybe-manage-events`](skills/vybe-manage-events/SKILL.md) | Safe edits, invitations, scanners, participants, balances, and pixels |
| [`vybe-discover-events`](skills/vybe-discover-events/SKILL.md) | Public search, nearby browsing, event reads, and recommendations |

Creating and managing events requires Vybe MCP. Discovery uses the public REST API and does not require authentication.

## MCP

Vybe MCP endpoint:

```text
https://tickets.vybe.social/api/mcp
```

This package declares that remote server in [`mcp.json`](mcp.json). Cursor and other Agent Plugin clients can connect it automatically. Authentication, when required, stays client-managed.

## OpenAPI

Use the live schema for exact request and response fields. Do not copy those schemas into the skills.

```text
https://tickets.vybe.social/openapi.json
```

## Cursor and Agent Plugins

Cursor loads this repository as both an Agent Plugin and a Cursor Plugin:

| File | Role |
| --- | --- |
| [`plugin.json`](plugin.json) | Agent Plugins 1.0.0 manifest |
| [`.cursor-plugin/plugin.json`](.cursor-plugin/plugin.json) | Cursor plugin metadata |
| [`mcp.json`](mcp.json) | Vybe MCP server (`streamable-http`) |
| [`skills/`](skills/) | The three installable Agent Skills |

Install the plugin from Customize, add the public GitHub repository to a team marketplace, or use the Skills CLI commands above.

## License

[MIT](LICENSE)
