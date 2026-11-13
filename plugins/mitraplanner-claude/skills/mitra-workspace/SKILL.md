---
name: mitra-workspace
description: Work with a connected Mitra Planner wedding workspace through the mitraplanner MCP tools. Use when the user asks about their wedding's guests, RSVPs, budget, vendors and quotes, payments, tasks, events or timeline in Mitra Planner, or asks to add or change any of it.
---

# Mitra Planner workspace

Use the `mitraplanner` MCP tools to read and update the user's real wedding data. All access is limited to what their account is allowed to see and change.

## If the tools are not available

The MCP server needs the user to sign in. Tell them to connect `mitraplanner` and complete the browser sign-in with their Mitra Planner account (in Claude Code run `/mcp` and choose `mitraplanner`; in Claude chat or Cowork use the Connectors tab). An account with active access is required. If sign-in or a tool call reports an access or usage limit, relay that message plainly. Do not retry in a loop and do not push purchases.

## Always resolve the wedding first

1. Call `list_weddings`.
2. If several match the user's description, ask which one. Never pick silently.
3. If none match, say so and offer the names you found. Do not invent a wedding, ID, or detail.
4. Use `get_wedding` for core details (dates, city, currency, budget target). If a field is empty, say it's empty.

## Reading

| Question | Tools |
| --- | --- |
| Guests and RSVPs | `get_rsvp_stats`, `list_guests`, `list_guest_groups` |
| Budget | `get_budget_overview`, `list_allocations` |
| Vendors, quotes, payments | `list_quotes`, `list_payments`, `list_service_needs` |
| Tasks | `list_tasks` |
| Schedule | `list_days`, `list_events`, `list_timeline_slots` |

Report only what the tools return. Quote currencies as stored; never add amounts in different currencies into one figure. State totals and differences explicitly (for example allocated vs. target).

## Writing

- Ask for any missing required detail (a guest's name, a task title) before calling a write tool. Do not fill it in.
- Say what you are about to change when it isn't obvious, then call the tool, then report success only after the tool succeeds.
- **Confirm first** before anything destructive (`delete_guest`, `delete_all_guests`, deleting events, categories, payments or templates) and before anything that sends messages or invitations. For a preview request, use read tools to describe what would be affected, ask for confirmation, and stop if the user declines.
- Make the smallest change that satisfies the request. Don't modify unrelated records.

## Style

Lead with the answer, then the supporting numbers. For long lists, summarise and offer to show the rest. Flag anything that needs attention (overdue tasks, unallocated budget, RSVPs still pending close to a deadline) without being asked to do more than what was requested.
