# Mitra Planner for Claude

Plan multi-day weddings with Claude. Two layers:

- **Planning guidance (no account needed).** The `wedding-planning-guide` skill activates when someone is planning, budgeting or organising a wedding.
- **Your real wedding data (Mitra Planner account).** The bundled MCP server connects Claude to guests, RSVPs, budget, vendors and quotes, payments, tasks, events and timelines in your Mitra Planner workspace, using your account's own permissions.

## Contents

| Path | Purpose |
| --- | --- |
| `.claude-plugin/plugin.json` | Plugin manifest |
| `.mcp.json` | Remote MCP server `https://www.mitraplanner.com/api/mcp` (OAuth) |
| `skills/wedding-planning-guide` | General planning advice; works without a connection |
| `skills/mitra-workspace` | Rules for reading and changing Mitra Planner data safely |
| `skills/wedding-checkin` | Read-only status summary and next actions |

## Install

From this repository's marketplace:

```
/plugin marketplace add mitra-planner/claude-plugin
/plugin install mitraplanner@mitraplanner
```

Then run `/mcp`, pick `mitraplanner` and sign in with your Mitra Planner account. In Claude chat or Cowork, connect `mitraplanner` from the Connectors tab instead.

## What this plugin runs, sends and fetches

- **Runs:** nothing. It contains three text skills and one MCP server declaration. There are no hooks, scripts, executables, agents or commands, and no packages are installed.
- **Sends and fetches:** once you connect it, Claude sends tool requests (for example "list guests" or "add a task") to `https://www.mitraplanner.com/api/mcp` over HTTPS and receives your wedding data back. You sign in with OAuth in the browser; the plugin stores no credentials and asks for no API keys. Without connecting, nothing is sent anywhere.
- **Permissions:** it can only read and change what your Mitra Planner account is allowed to. It does not change Claude's permission settings.
- **Personal data:** wedding data (guest names, RSVPs, budgets, schedules) passes through your Claude session and Mitra Planner's servers. Anything you add or change through Claude is saved in your Mitra Planner account like any other change and kept until you delete it or close your account. The plugin itself stores nothing. Mitra Planner's [privacy policy](https://www.mitraplanner.com/privacy) applies.

Local development:

```
claude --plugin-dir ./plugins/mitraplanner-claude
claude plugin validate ./plugins/mitraplanner-claude
```

## Notes

- The MCP endpoint, OAuth flow, usage limits and per-tool annotations are the same ones used by the ChatGPT plugin in `plugins/mitraplanner/`. Server behaviour lives in `src/lib/mcp/`.
- Write and destructive tools are annotated; the skills additionally require confirmation before deleting data or sending invitations.
- Keep `version` in `.claude-plugin/plugin.json` in sync with releases. Claude Code only updates installed copies when the version changes.

## Distribution

- **Official directory:** submit the plugin through Anthropic's plugin directory submission form (linked from the Claude Code plugin docs) to be listed in the in-product marketplace.
- **Public mirror:** the `Claude Plugin Publish` workflow (`.github/workflows/claude-plugin-publish.yml`) copies only `.claude-plugin/marketplace.json` and this folder into `mitra-planner/claude-plugin` on every push to `main` that touches them. That repo is what users add as a marketplace. Edit the plugin here, never in the mirror; the mirror's root `README.md` and `LICENSE` are managed there.
- **Publishing a change:** bump `version` in `.claude-plugin/plugin.json` and merge to `main`. Installed copies only update when the version changes.
- **Allowlist:** `scripts/stage-claude-plugin.mjs` fails the workflow if this folder contains a file that is not on its allowlist (manifest, `.mcp.json`, README, icon, `skills/*/SKILL.md`). Add new file types there deliberately.
- **Anthropic directory:** submit in the developer portal (https://claude.ai/directory/manage) with repository `mitra-planner/claude-plugin`, plugin path `plugins/mitraplanner-claude`, branch `main`. New versions are then picked up from pushes to that branch, so the mirror workflow is also the release mechanism. Raise `version` on every release.
