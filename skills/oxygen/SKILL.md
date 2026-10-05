---
name: oxygen
description: Connect to an OXYGEN workspace through its hosted MCP server and carry out a founder's GTM work using tables, company research, enrichment, sequences, knowledge, and workflows. Use when the user asks to inspect or run a GTM motion in OXYGEN.
---

# Work in OXYGEN

OXYGEN is revenue infrastructure for B2B startups. This plugin connects the hosted OXYGEN MCP server. The customer needs an OXYGEN workspace; the MCP connection asks them to authorize access through their browser.

1. Connect the `oxygen` server and let the customer finish its authorization prompt. If authorization is unavailable or fails, report that state and give them the OXYGEN sign-in link: https://oxygen-agent.com. Never ask them to paste a password or token into chat.
2. Call `oxygen_whoami` to confirm the active workspace and role. If it reports `organization_selection_required`, use `oxygen_orgs_list`, ask the customer which workspace to use, then call `oxygen_orgs_select` for that exact choice and read `oxygen_whoami` again. Say which workspace you will use before changing anything.
3. Check the connected tool catalog. When `oxygen_skills_get` is available, load `oxygen-onboarding` and follow it. When the user already selected a play, preserve it and its workspace and open its `oxygen-recipes` document instead. Use available capability discovery to inspect current schemas, costs and approvals. The reviewed ChatGPT connector supports lead research only: inspect existing company/ICP context and use its exposed research tools, then give a handoff preserving the play and workspace for Claude or Codex to prepare it. Never claim unavailable skills, Sequences or follower capture can run through that connector.
4. Keep work inspectable in OXYGEN. Return links to the Tables, records, drafts, runs, and approval previews you create or inspect. Read back the result of a write before reporting success.
5. For an operation that spends credits or sends or changes data outside OXYGEN, show the preview, exact scope, and credit ceiling, then wait for the customer's approval before live execution. If a tool requires approval, provide the native approval step instead of retrying around it.

Start from what the workspace already has. Learn the company and the person, map the running campaigns and connected accounts, then offer two or three fitting plays from the Recipe catalog and prepare the one the customer picks for review: its first result, source evidence, current cost preview and workspace links. Preparation never enables a schedule, spends or sends.

The plugin adds no separate account, billing path, or background job. OXYGEN's workspace permissions and product approval controls govern every MCP call. For product terms and data handling, see https://oxygen-agent.com/terms and https://oxygen-agent.com/privacy.
