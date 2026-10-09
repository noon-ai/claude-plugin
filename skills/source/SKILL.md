---
name: source
description: Start sourcing candidates with Noon for a job. Use when the user wants to recruit, source, or find candidates for a role, pastes a job description, or shares a job posting URL.
argument-hint: "[job description, job posting URL, or a short description of the role]"
---

# Source candidates for a role with Noon

The user wants Noon to start sourcing for a job: $ARGUMENTS

1. **Get the job details.** If you were given a job posting URL, fetch it and pull out the title, location, full JD text, and the stated requirements. If you were given a JD, use it as is.

2. **Settle the targeting before creating anything.** A role created from just a name sources very broadly. Fill in what the JD implies, then show the user one short block to confirm:
   - Titles to search for, and seniority
   - Location(s), and whether remote is OK
   - Years-of-experience range
   - Must-haves: the 3–5 things every candidate has to have
   - Nice-to-haves
   - Target companies, described in words ("Series B–D fintech", "YC B2B SaaS"), or "source broadly"

   Ask only about what is genuinely missing. Do not use `only_source_from_companies` unless the user says candidates must come from a fixed list; a short exclusive list starves the role.

3. **Create the role.** Call `create_role` with the name, the full `jd`, and everything from step 2. Give the user the portal link it returns.

4. **Wait for the first candidates.** Call `get_candidate_feed` for the new role about once a minute until candidates appear (usually a few minutes). Then show the first batch as a table: name, current title and company, location, years of experience, and Noon's one-line reason. If the feed is still empty after about 10 minutes, tell the user sourcing is running and they can review candidates in the portal.

5. **Offer next steps:** accept or reject specific people (see the `review` skill), set up outreach (the `outreach` skill), or check the search's health once the first batch is reviewed (the `diagnose` skill).
