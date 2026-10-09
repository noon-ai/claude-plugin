---
name: review
description: Review the candidates Noon sourced for a role and accept or reject them. Use when the user asks who Noon found, wants to go through the feed, or wants to accept or reject candidates.
argument-hint: "[role name or ID]"
---

# Review a role's candidate feed

Role: $ARGUMENTS

1. **Find the role.** If you don't have a role ID, call `list_roles` and match the user's description. If more than one role fits, ask which.

2. **Show the feed.** Call `get_candidate_feed` (up to 25 at a time). Present a table: number, name, current title and company, location, years of experience, and Noon's reason for the match. Keep the candidate IDs so the user can refer to people by number or name.

3. **Act on the user's decisions.**
   - `accept_candidate` adds the person to the role's project and syncs them to the ATS. If the role has auto-contact on, it also queues outreach to them, so say that before accepting.
   - `reject_candidate` removes one person. Pass the user's reason in their own words whenever they give one. Noon turns it into a screening rule and drops other feed candidates with the same problem.
   - When the user's complaint is about the feed as a whole ("too many consultants", "everyone is too senior"), use `give_feed_feedback` once instead of rejecting people one by one.

4. **Feedback adds rules; it doesn't edit settings.** Each rejection reason or piece of feed feedback becomes a new screening rule. Feedback that contradicts an earlier rejection reason can reverse that rejection and bring those people back. It cannot change the role's settings: the titles, locations, experience range, must-haves set when the role was created, or a fixed company list. When the user wants to loosen one of those, don't send it as feedback, because "be less strict about X" would just become another rule. Point them to the role's settings in the Noon portal instead.

5. After a decision, say what changed (for example, how many feed candidates a new rule dropped) and offer the next batch.
