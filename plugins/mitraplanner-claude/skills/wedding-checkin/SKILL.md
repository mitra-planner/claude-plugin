---
name: wedding-checkin
description: Produce a status check-in for a connected Mitra Planner wedding covering RSVPs, budget, overdue and upcoming tasks, and the next events. Use when the user asks "where do we stand", for a weekly update, a progress summary, or what to do next on their wedding.
---

# Wedding check-in

Follow the `mitra-workspace` rules (resolve the wedding first, never invent data, no writes unless asked). This is a read-only summary.

## Steps

1. `list_weddings` → pick the wedding (ask if ambiguous). `get_wedding` for dates, currency and budget target.
2. Fetch in parallel: `get_rsvp_stats`, `get_budget_overview`, `list_allocations`, `list_tasks`, `list_events`.
3. Work out, from the returned data only:
   - Days until the first event.
   - RSVP counts: confirmed, declined, pending; share still pending.
   - Budget: target, total allocated, unallocated difference, any category over its allocation.
   - Tasks: overdue, due in the next 14 days, count completed vs. remaining.
   - The next three events.

## Output

Use this shape and keep it short:

**Wedding** — name, first event date, days to go

**Guests** — confirmed / declined / pending

**Budget** — target, allocated, unallocated (flag categories over allocation)

**Tasks** — overdue (list), due soon (list), progress

**Coming up** — next events

**Suggested next 3 actions** — concrete, ordered by urgency, each tied to a number above

End by asking whether the user wants any of the actions carried out. Do not make changes without that.
