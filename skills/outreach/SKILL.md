---
name: outreach
description: Write or edit the outreach sequence Noon sends for a role (LinkedIn connection invite, InMail, emails, follow-ups). Use when the user wants to see, write, rewrite, shorten, or reorder a role's outreach messages.
argument-hint: "[role name or ID] [what to change]"
---

# Write or edit a role's outreach sequence

Request: $ARGUMENTS

1. **Find the role** with `list_roles` if you don't have its ID.

2. **Read the current sequence** with `get_outbound_sequence`. Show it to the user as numbered steps: type, wait time, subject, and message.

3. **Draft the change.** `update_outbound_sequence` replaces every step, so always send the complete sequence, including the steps you didn't touch, and keep each step's `signature` value as it was.
   - Placeholders filled per candidate: `{first_name}`, `{last_name}`, `{company}`, and `{ai_intro}`, an AI-written personal opening line. Put `{ai_intro}` in the first InMail and the first email.
   - A typical sequence: connection invite, then an InMail 2 days later, then 2–3 email follow-ups.
   - A connection invite note is at most 300 characters. An InMail after a connection invite needs `wait_days` of at least 1.
   - Leave out `connection_accepted` to keep the role's existing "invite accepted" messages; set it to `null` only if the user wants them turned off.

4. **Confirm, then save.** Show the full new sequence and wait for the user's OK before calling `update_outbound_sequence`, since these messages go to real candidates from the user's own email and LinkedIn accounts. After saving, show the sequence the tool returns.
