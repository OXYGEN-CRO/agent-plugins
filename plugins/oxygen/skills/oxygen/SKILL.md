---
name: oxygen
description: OXYGEN — start here. Connect to the user's OXYGEN workspace, the agent-run GTM (go-to-market) workspace, and run their GTM work: tables, lead enrichment, outbound sequences, workflows, CRM records and the company knowledge graph. Use when the user wants to set up or connect OXYGEN, run a GTM motion in OXYGEN, or asks "what can I do with OXYGEN?".
---

# OXYGEN — start here

OXYGEN is revenue infrastructure for B2B startups: one hosted workspace that replaces most of the GTM stack a founder would otherwise wire together. It holds **tables** (typed datasets with run history and provenance), **enrichment** across 50+ data providers, outbound **sequences**, durable **workflows**, a **CRM** of records and a company **knowledge graph** (ICP, positioning, offers). Every run is observable, costed and approval-gated.

Describe these as the product's capabilities ("OXYGEN can enrich this list…"), and lead with a concrete first win, such as a table built from the user's own data, a few enriched leads or a draft sequence, rather than a catalog tour.

## Connect

This plugin adds OXYGEN's hosted MCP server, `oxygen`, at `https://oxygen-agent.com/mcp`. Its tools work after the user signs in through their browser and authorizes their own workspace. In Claude Code, `/mcp` lists the server and starts that sign-in.

1. Call `oxygen_whoami` and tell the user which workspace and role are active.
2. If it reports `organization_selection_required`, list the workspaces with `oxygen_orgs_list`, ask which one to use, select it with `oxygen_orgs_select`, and read `oxygen_whoami` again.
3. If sign-in is unavailable or fails, report the exact state and point the user to https://oxygen-agent.com to sign up or sign in. Credentials stay in the browser sign-in; ask for nothing in chat.

A tool that the server does not list runs by name through `oxygen_capabilities_read` (reads) or `oxygen_capabilities_call` (everything else).

The user needs an OXYGEN workspace. Signing up is free, and a new workspace starts with free credits.

## Work

1. Start from what the workspace already has: the company profile, existing tables, running campaigns and connected accounts. Load the `oxygen-onboarding` product skill with `oxygen_skills_get` and follow it; when the user has already picked a play, keep it and open that play's `oxygen-recipes` document instead.
2. Discover before acting: `oxygen_capabilities_search`, then `oxygen_capabilities_schema` for the exact inputs, cost and approval of the tool you need.
3. Keep results inspectable: return the OXYGEN links for every table, record, draft, run and preview you create or read, and read a write back before reporting success.

## Spend and external actions

OXYGEN runs a preview or dry run first. Anything that spends credits or writes outside OXYGEN (enrichment, live sends, CRM sync, purchases) executes only with explicit approval and a numeric credit ceiling. Show the preview, the exact scope and the ceiling, wait for the user's yes, and pass both to the tool. Approval for one run covers only that run.

## In a terminal (Claude Code)

The `oxygen` CLI exposes the same workspace with the full command surface and `--json` output. Offer it when the user wants terminal work, and ask before installing anything:

```sh
npm install -g @oxygen-agent/cli
oxygen login
oxygen whoami --json
```

`oxygen login` opens the same browser sign-in and installs OXYGEN's product skills for this agent. On the CLI, a paid or external command previews by default and runs live only with `--approved` and `--max-credits <n>`.
