# Noon plugin for Claude

Noon is an AI recruiter. This plugin connects Claude to your Noon workspace so you can source candidates for a role, review who Noon found, edit the outreach it sends, and find out why a role's search is or isn't working.

It works in Claude Code and in Claude Cowork.

## What's inside

- **Noon MCP server** (`https://noon.fly.dev/mcp`): 16 tools for roles, the candidate feed, outreach sequences, and search diagnostics. You sign in with your Noon login the first time Claude uses it.
- **Skills**, which you can run as slash commands or let Claude pick up on its own:

| Command | What it does |
|---|---|
| `/noon:source <JD, job URL, or description>` | Settles the targeting with you, creates the role, and shows the first candidates |
| `/noon:review [role]` | Walks through a role's feed so you can accept or reject people |
| `/noon:outreach [role] [change]` | Shows and edits the role's LinkedIn and email sequence |
| `/noon:diagnose [role]` | Funnel, rejection reasons, and the one setting to loosen, with real numbers |

## Install

**Claude Code**

```
/plugin marketplace add noon-ai/claude-plugin
/plugin install noon@noon
```

**Claude (claude.ai) and Cowork:** go to Customize → Plugins → Add → Add marketplace, enter `https://github.com/noon-ai/claude-plugin`, then install **Noon**. Connect Noon from the plugin's Connectors tab.

## Requirements

- A Noon account at [www.noon.ai](https://www.noon.ai). Claude only sees the roles and candidates in your Noon workspace.
- Outreach goes out from the email and LinkedIn accounts connected in your Noon portal.

## What it connects to and what it stores

- The plugin connects to one service: Noon's MCP server at `https://noon.fly.dev/mcp`, which Noon runs. Every tool call goes there, with your Noon sign-in.
- The tools read and change data in your own Noon workspace: roles, candidate profiles, feed decisions, and outreach sequences. Accepting a candidate on a role with auto-contact on queues outreach to them from your connected accounts.
- The plugin itself runs no scripts and stores nothing on your machine. The skills are instructions for Claude.
- When you give `/noon:source` a job posting URL, Claude fetches that page with its own web tools to read the job description.

## Signing in

In Claude Code, run `/mcp`, pick `plugin:noon:noon`, and choose **Authenticate**. Your browser opens the Noon sign-in page; after you approve, Claude can use the tools.

## Support

support@noon.ai · [Privacy policy](https://www.noon.ai/privacy) · [Terms](https://www.noon.ai/terms)
