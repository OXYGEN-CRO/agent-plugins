# OXYGEN for Claude

OXYGEN is the agentic GTM platform for B2B GTM teams. This plugin lets Claude work in your OXYGEN workspace: build and enrich GTM tables, research companies and people, draft outbound sequences and workflows, and keep your CRM records and company knowledge graph current. Every run stays visible in OXYGEN with its cost, its results and a link to inspect it.

## What the plugin contains

- **One remote MCP server**, `oxygen`, at `https://oxygen-agent.com/mcp`. Claude connects to it over HTTPS. You sign in through your browser (OAuth) and authorize your own workspace; the plugin stores no credentials.
- **One skill**, `oxygen`, that tells Claude how to connect, find the right OXYGEN tool, and ask for approval before anything that costs credits or acts outside OXYGEN.

The plugin has no hooks, scripts, commands, agents or local servers, and it changes none of Claude's permission settings. Claude asks before each OXYGEN tool call according to your own permission settings.

## What it sends and fetches

- When Claude calls an OXYGEN tool, the tool's inputs (for example a table name, rows you import, a search prompt or a draft message) go to OXYGEN's servers at `oxygen-agent.com`, and the results come back to Claude. OXYGEN stores workspace data in your workspace.
- Some OXYGEN tools query third-party data providers on your behalf, such as company and contact enrichment. They run only when Claude calls that tool, and a paid lookup previews its cost and runs only after you approve it with a credit ceiling.
- Sends to other platforms (email, LinkedIn, CRM sync) happen only through OXYGEN tools that you approve, using the accounts you connected in OXYGEN.
- In Claude Code, the skill can offer to install the OXYGEN command-line tool from npm (`npm install -g @oxygen-agent/cli`) and run `oxygen login`, which opens the same browser sign-in and saves a login token on your machine. Claude asks before running either command.

How OXYGEN handles data: [connector privacy policy](https://oxygen-agent.com/connector-privacy).

## Requirements and cost

You need an OXYGEN account; signing up at [oxygen-agent.com](https://oxygen-agent.com) is free, and a new workspace starts with free credits. The plugin is proprietary and adds no separate plugin fee. OXYGEN usage is billed in credits under your plan ([pricing](https://oxygen-agent.com/pricing)); the plugin adds no separate billing.

## Install in Claude Code

```
/plugin marketplace add OXYGEN-CRO/agent-plugins
/plugin install oxygen@oxygen
```

Then run `/mcp`, sign in to OXYGEN, and ask Claude: "Connect to OXYGEN, tell me which workspace is active, and show me my tables."

## Support

- Documentation: https://oxygen-agent.com/docs/surfaces/claude-code
- Support: https://oxygen-agent.com/docs/surfaces/support or support@oxygen-agent.com
- Terms: https://oxygen-agent.com/terms

Copyright (c) 2026 OXYGEN GTM Inc. All rights reserved. The [OXYGEN Proprietary License](LICENSE) permits unmodified use with an authorized OXYGEN account; redistribution, resale and reuse in other products require OXYGEN’s written permission.
