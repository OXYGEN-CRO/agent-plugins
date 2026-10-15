# OXYGEN agent plugins

First-party agent plugins for **OXYGEN**, the agentic GTM platform for B2B GTM teams. This repository holds the OXYGEN plugin for Claude (Claude Code, Cowork and Anthropic's Claude plugin directory) and a portable [Agent Plugins](https://agent-plugins.org/) package for Cursor and Grok Bot.

Both connect the hosted OXYGEN MCP server at `https://oxygen-agent.com/mcp`. Connecting asks the user to authorize access to their OXYGEN workspace in the browser; the plugins contain no credentials. The plugins are proprietary, with no separate plugin fee. The [OXYGEN Proprietary License](LICENSE) permits unmodified use with an authorized OXYGEN account; redistribution, resale and reuse in other products require OXYGEN’s written permission. OXYGEN's service has its own [pricing](https://oxygen-agent.com/pricing), [terms](https://oxygen-agent.com/terms), and [privacy policy](https://oxygen-agent.com/privacy).

## Claude

```
/plugin marketplace add OXYGEN-CRO/agent-plugins
/plugin install oxygen@oxygen
```

Then run `/mcp`, sign in to OXYGEN, and ask Claude to connect to OXYGEN. The plugin's own [README](plugins/oxygen/README.md) lists everything it contains, sends and fetches.

To set it up for everyone working in a repository, run this once from that repository and commit the `.claude/settings.json` it writes:

```
claude plugin marketplace add OXYGEN-CRO/agent-plugins --scope project
claude plugin install oxygen@oxygen --scope project
```

## Cursor and Grok Bot

The portable plugin is at this repository's root: `plugin.json`, `mcp.json`, and `skills/oxygen/SKILL.md`, under the [OXYGEN Proprietary License](LICENSE). This package is not eligible for the Cursor Marketplace under its current [licensing policy](https://cursor.com/help/security-and-privacy/marketplace-security). Cursor users can connect the hosted server at `https://oxygen-agent.com/mcp` directly and complete browser authorization; see the [generic MCP setup guide](https://oxygen-agent.com/docs/surfaces/generic-mcp).

Before marketplace approval, Grok Bot accounts that offer **Settings → Plugins → custom MCP server** can add `https://oxygen-agent.com/mcp` directly and complete its browser authorization. This connects the hosted tools; it does not install the packaged skill. If the authorization does not complete, use the [generic MCP setup guide](https://oxygen-agent.com/docs/surfaces/generic-mcp) and report the exact error. This custom route has not yet been verified in a Grok Bot account.

Try a read-only first task: “Connect to my OXYGEN workspace, tell me which workspace is active, and show me the Tables I can inspect.” For live enrichment or outreach, review OXYGEN's preview, scope, and credit ceiling before approving execution.

## What's inside

```
├── plugin.json                    # portable Agent Plugins manifest (Cursor, Grok Bot)
├── mcp.json                       # portable hosted MCP connection
├── skills/oxygen/SKILL.md         # MCP-first GTM skill for Cursor and Grok Bot
├── LICENSE
├── .claude-plugin/
│   └── marketplace.json           # Claude marketplace `oxygen` → plugin `oxygen`
└── plugins/oxygen/                # the Claude plugin
    ├── .claude-plugin/plugin.json # manifest, version and directory listing fields
    ├── .mcp.json                  # hosted OXYGEN MCP server (OAuth)
    ├── skills/oxygen/SKILL.md     # start-here skill
    ├── assets/icon.png
    ├── README.md
    └── LICENSE
```

The repository ships only Markdown, JSON and one icon: no hooks, scripts, runtime build step or dependencies.

## Releasing the Claude plugin (maintainers)

The source lives in the OXYGEN monorepo under `agent-plugin/`; `.github/workflows/publish-agent-plugin.yml` mirrors it here after each production deploy, committing only when the published files changed.

The Claude plugin has its own version. Claude Code keeps users on the version they installed until it changes, and Anthropic's directory reviews each new version, so every change under `plugins/oxygen/` raises `version` in its `plugin.json`:

```
npm run agent-plugin:check   # directory readiness + version discipline (no build needed)
npm run agent-plugin:write   # after raising the version, record it in release.lock.json
```

`scripts/build-agent-plugin.mjs` owns both checks. It runs in local verification and the merge queue for any change under `agent-plugin/`, and again before every publish. The Anthropic directory submission runbook is `docs/connector/claude-plugin-submission.md` in the monorepo.
