# Perplexity: custom remote connector

Perplexity (Pro, Max, Enterprise) lets each user, or an org admin, add a remote MCP
connector. There is no public directory submission today, so this path is self-serve.

1. Perplexity → **Customize → Connectors** (Enterprise: **Organization settings →
   Connectors → Custom connector**. Members also need "Allow members to add custom
   connectors").
2. **Add custom → Add MCP connector → Remote.**
3. Name: `Braize | Agent unlimited memory`. URL: `https://mcp.aize.dev/{workspace_id}`.
4. Advanced → transport **Streamable HTTP**, auth **OAuth**.

**Status: blocked for OAuth** until Perplexity's callback URL is registered in Keycloak
(Perplexity shows it in the connector dialog; it isn't published). Perplexity's API-key
mode can't be used either: production MCP doesn't accept workspace API keys (owner
decision pending, see ROADMAP). Both are tracked in the publishing plan.

Suggested Space/system instructions once connected: use
[`../docs/example-agent-prompt.md`](../docs/example-agent-prompt.md).
