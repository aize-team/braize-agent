# Connect an agent to Braize: OAuth or API key

Braize has two ways in. Pick by what your agent host supports.

| | MCP + OAuth (recommended) | REST + API key |
|---|---|---|
| Endpoint | `https://mcp.aize.dev/mcp` (or `/{workspace_id}`) | `https://apibr.aize.dev/v1` |
| Who you read as | The signed-in person. Their source permissions apply (ACL pre-filter). | The workspace-public principal: **public-scope content only**. |
| Works in | Claude Code, Codex, Cursor, VS Code, Windsurf, Gemini CLI and other MCP hosts that sign in on `localhost` | Any host that can send an HTTP header: ChatGPT GPT Actions, scripts, CI, custom agents |
| Memory | `append_memory` / `search_memory`, private to the signed-in person | `/v1/memory`, shared by every key holder in the workspace |

Production MCP does **not** accept API keys. A `bzk_...` key sent to `mcp.aize.dev` gets `401`.

## 1. Find your workspace id

Dashboard → **Channels → MCP** shows your exact MCP URL with the workspace id filled in.

## 2a. OAuth (MCP)

Point your host at the MCP URL. The first tool call returns `401` with a
`WWW-Authenticate` header that names the protected-resource metadata. Your host opens a
browser so you can sign in. Values the host needs if it asks:

- client id: `braize-mcp-cli` (pre-registered public PKCE client, `localhost` / `127.0.0.1` redirects only)
- scope: `mcp:read`
- resource: `https://mcp.aize.dev`

Per-host config files are in [`../mcp/`](../mcp/). Hosted web apps (claude.ai, chatgpt.com,
Perplexity) can't finish this sign-in until their callback URLs are registered. See the
publishing plan.

## 2b. API key (REST)

1. Dashboard → **Settings → API keys** (workspace owners and admins only).
2. Create a key with scope **query**. That scope can read, retrieve, ask and write agent
   memory. Never give an agent an **admin** key.
3. Give it a name that says where it runs (e.g. `cursor-laptop-ali`), so you can revoke just
   that key later.
4. Store it as an environment variable or in the host's secret store. Never paste it into a
   prompt, a repo or a config file you commit:

   ```bash
   export BRAIZE_API_KEY="<paste from the dashboard>"
   ```

5. Test it:

   ```bash
   curl -sS https://apibr.aize.dev/v1/sources -H "Authorization: Bearer $BRAIZE_API_KEY"
   ```

   `200` with `{"data": ...}` means you're connected. `401` means the key is wrong or revoked.

### What an API key can and can't see

A `query` key reads as the **workspace-public principal**. `meta.scope` in every
`/v1/retrieve` response is `"public"`. Documents restricted to specific people are never
returned. This is deliberate (default-deny). To read with a person's own permissions, use
MCP with OAuth.

### Revoke and rotate

Dashboard → **Settings → API keys** → **Revoke** on the row. Only that key stops working.
Rotate by creating a new key, switching the agent over, then revoking the old one.

### Limits

Calls count against your plan's monthly query quota and indexed-page limit (see
[pricing](https://br.aize.dev/pricing)). When a quota runs out the API returns `429`
`quota-exceeded`.
