# Per-host MCP configs

Replace `{workspace_id}` with your id (dashboard → **Channels → MCP**). Every host signs in
with OAuth on the first tool call. Production MCP doesn't accept API keys.

Braize's Keycloak doesn't offer DCR or CIMD yet. So each host must use the pre-registered
public client **`braize-mcp-cli`** (PKCE, scope `mcp:read`, loopback redirects only).

| Host | File | Where it goes | Sign-in notes |
|---|---|---|---|
| Claude Code | plugin (`../plugins/braize`) or `claude mcp add --transport http --client-id braize-mcp-cli --callback-port 8976 braize https://mcp.aize.dev/{workspace_id}` | plugin install or CLI | Claude Code tries CIMD, then DCR, then the static client id. Redirect `http://localhost:<port>/callback`. |
| Cursor | [`cursor.mcp.json`](cursor.mcp.json) | `~/.cursor/mcp.json` or `.cursor/mcp.json` | Static `auth.CLIENT_ID`. Redirect `http://localhost:8787/callback`. Deep link: `cursor://anysphere.cursor-deeplink/mcp/install?name=braize&config=<base64 of the braize entry>` |
| VS Code | [`vscode.mcp.json`](vscode.mcp.json) | `.vscode/mcp.json` | `oauth.clientId`. Redirect `http://127.0.0.1:33418/`. |
| Windsurf / Devin Desktop | [`windsurf.mcp_config.json`](windsurf.mcp_config.json) | `~/.config/devin/mcp_config.json` (legacy `~/.codeium/windsurf/mcp_config.json`) | **Blocked until DCR** unless the host lets you set a static client id (`braize-mcp-cli`). Its redirect URL isn't documented. |
| Codex | [`codex.config.toml`](codex.config.toml) | `~/.codex/config.toml`, then `codex mcp login braize` | **Blocked until DCR** unless Codex accepts a static client id (not verified). Loopback redirect. |
| Gemini CLI / Antigravity | [`../gemini-extension.json`](../gemini-extension.json) | `gemini extensions install ...` | `oauth.clientId`. Redirect `http://localhost:<random>/oauth/callback`. |
| Anything else | [`generic.mcp.json`](generic.mcp.json) | host-specific | Streamable HTTP, POST only (no GET/SSE stream). Needs a host that supports a static client id (`braize-mcp-cli`) until DCR exists. |
| MCP Registry | [`server.json`](server.json) | `mcp-publisher publish` (owner, DNS proof for `dev.aize`) | Metadata only. |

**Verified 2026-11-13 against production Keycloak (read-only authorize probes):**
`braize-mcp-cli` accepts loopback redirects on any port (`http://localhost:8976/callback`,
`http://localhost:8787/callback`, `http://127.0.0.1:33418/` reach the login form). Hosted
callbacks (`https://claude.ai/api/mcp/auth_callback`, `https://chatgpt.com/...`) are rejected
with "Invalid parameter: redirect_uri". Anonymous DCR returns `403`. A full sign-in per host
(with a real account) is still unverified.

The dashboard's own snippets (`services/dashboard/lib/mcpSetup.ts`) still use older flag names
(`claude mcp add ... --oauth-client-id --scope mcp:read --resource`). In `claude mcp add`,
`--scope` picks the config scope (local/user/project), not the OAuth scope. Tracked in ROADMAP.
