# Mitra Planner for Claude Code

A [Claude Code](https://code.claude.com) plugin for planning multi-day weddings.

- **Planning guidance, no account needed.** Claude gives practical advice on budgets, guest lists, timelines and multi-day events when you're planning a wedding.
- **Your real wedding data.** Connect your [Mitra Planner](https://www.mitraplanner.com) account to review guests and RSVPs, budget, vendors and quotes, payments, tasks, events and timelines, and to make changes within your account's permissions. An account with active access is required.

## Install

```
/plugin marketplace add mitra-planner/claude-plugin
/plugin install mitraplanner@mitraplanner
```

Then run `/mcp`, choose `mitraplanner`, and sign in with your Mitra Planner account.

Try: "Show my weddings", "Where do we stand on RSVPs and budget?", or "I'm planning a wedding for 120 guests, where do I start?"

## What's included

| Skill | Purpose |
| --- | --- |
| `wedding-planning-guide` | General planning advice; works without a connection |
| `mitra-workspace` | Reads and updates your Mitra Planner data, confirming before deletions or sending invitations |
| `wedding-checkin` | Read-only status summary with suggested next actions |

The plugin connects to `https://www.mitraplanner.com/api/mcp` over OAuth.

## Support and privacy

- Support: https://www.mitraplanner.com/app-support
- Privacy policy: https://www.mitraplanner.com/privacy
- Terms: https://www.mitraplanner.com/terms

## About this repository

This repository is published automatically from Mitra Planner's source repository and is overwritten on each release, so pull requests here can't be merged. Please report issues through the support link above.

Licensed under the [MIT License](LICENSE).
