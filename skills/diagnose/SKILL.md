---
name: diagnose
description: Diagnose how a Noon role's search is going. Use when the user asks for a status update on a role, why the candidate pool is small or the feed is thin, why candidates are being rejected, or what to relax to widen the search.
argument-hint: "[role name or ID]"
---

# Diagnose a role's search

Role: $ARGUMENTS

If you don't have a role ID, call `list_roles` and match the user's description. All the tools below are read-only, so call them freely and in parallel where they don't depend on each other.

1. **Snapshot.** Call `get_role_state`: is sourcing running or paused, the sourcing cap, must-haves, active relaxations, and the search settings.

2. **Funnel.** Call `query_events` twice, once with `group_by="event"` (reviewed, accepted, rejected, added) and once with `group_by="rejection_reason"`. For category shares, divide by the sum of the rejection_reason buckets, not by the total rejected count: on large roles the categories only cover a sample.

3. **Find the constraint.**
   - If one rejection category is more than about 30% of the categorized total, or the role has reviewed many candidates and accepted almost none, call `rejection_analysis`. Its sole-blocker counts show how many otherwise-qualified people each must-have is costing.
   - If the pool itself is small, call `pool_diagnostics` to see whether the search filters or the evaluation are the bottleneck, and how many people each loosened filter would add.
   - If something changed recently ("it was fine last week"), call `search_trace`.
   - To compare people, use `find_candidates`, then `explain_candidate` for the evaluation behind a decision.

4. **Report in plain language, with the real numbers.** Lead with the answer ("The 3–5 year cap is rejecting 41% of reviewed candidates; 180 of them fail only that rule"), then give one concrete fix: widen the experience range, drop the fixed company list, loosen the seniority ceiling, or enlarge the location radius. Some of these settings never relax on their own; say so when one of them is the blocker.

Changing a role's settings is done in the Noon portal. Don't try to loosen a setting by sending feedback through `give_feed_feedback` or a rejection reason: that adds a new rule rather than relaxing the old one.
