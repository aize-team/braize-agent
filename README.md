# Braize | Agent unlimited memory: agent plugins

Everything other AI agents need to use Braize: permission-aware, always-synced company
knowledge with cited passages. This package **wraps** the live Braize surfaces. It never
duplicates them:

- MCP server `https://mcp.aize.dev/mcp` (OAuth 2.1; routes to your workspace, or lists your workspaces' URLs if you belong to several). `https://mcp.aize.dev/{workspace_id}` targets one workspace directly. Tools come from
  the server's `tools/list`.
- REST API `https://apibr.aize.dev/v1` (bearer API key). Contract:
  [br.aize.dev/docs](https://br.aize.dev/docs).

| Path | For |
|---|---|
| [`.claude-plugin/marketplace.json`](.claude-plugin/marketplace.json) | Makes this folder a Claude Code plugin marketplace |
| [`plugins/braize/`](plugins/braize/) | Claude Code plugin: remote MCP config + the `braize-memory` Agent Skill |
| [`plugins/braize/skills/braize-memory/SKILL.md`](plugins/braize/skills/braize-memory/SKILL.md) | Portable Agent Skill (Claude, Codex, Cursor, Letta and others): when to use `/v1/retrieve` vs `/v1/query`, citing, freshness, abstaining |
| [`gemini-extension.json`](gemini-extension.json) + [`GEMINI.md`](GEMINI.md) | Gemini CLI / Antigravity extension (at the root, where the gallery crawler looks) |
| [`chatgpt/`](chatgpt/) | GPT Action schema (**generated**) + instructions; ChatGPT plugin notes |
| [`perplexity/`](perplexity/) | Perplexity custom connector guide |
| [`mcp/`](mcp/) | Cursor, VS Code, Windsurf, Codex, generic configs + MCP Registry `server.json` |
| [`docs/api-key-setup.md`](docs/api-key-setup.md) | OAuth vs API key, minting and revoking keys, what a key can see |
| [`docs/example-agent-prompt.md`](docs/example-agent-prompt.md) | Host-neutral system prompt |
| [`store-listing/listing.md`](store-listing/listing.md) | Title, short and long copy, assets |

This folder is published as the public repo [`aize-team/braize-agent`](https://github.com/aize-team/braize-agent) (MIT).

## Install

Claude Code:

```bash
claude plugin marketplace add aize-team/braize-agent
```

```bash
claude plugin install braize@braize
```

Gemini CLI:

```bash
gemini extensions install https://github.com/aize-team/braize-agent
```

## Where it lives

Built and tested in the private Braize repository next to the contracts it wraps (a contract test fails if the skill's tool table or the GPT Action drift), and mirrored here on each release.

## Rules

- Never hand-edit `chatgpt/gpt-action.openapi.yaml`. Regenerate it:
  `uv run python scripts/build_gpt_action_spec.py`.
- Never list connectors here. Agents call `list_sources`, because MCP and REST are
  registry-driven.
- Never commit a key. Configs carry `{workspace_id}` placeholders only.
- New agent capability = new MCP tool in `contracts/mcp_tools.json` first (additive-only),
  then the skill table.
- Copy stays honest. Anything not built is "coming soon".
