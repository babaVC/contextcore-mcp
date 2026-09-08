# Which editor?

This repo serves **four install paths**. Pick the row that matches yours.

| Editor | Install | Initialize | Playbook |
|--------|---------|------------|----------|
| **Cursor** | **Plugin** — MCP + skill + `/contextcore-init` | Type `/contextcore-init` | Bundled `skills/contextcore/SKILL.md` |
| **Claude Code** | **Plugin** — MCP + skill + init (same repo) | `/contextcore:contextcore-init` or paste first prompt | Bundled skill + `read_skill` slug `contextcore` |
| **Claude Desktop (chat)** | **Custom Connector** — paste MCP URL | Paste first prompt | Over MCP: `read_skill` slug `contextcore` |
| **Claude Desktop Extensions** | **`.mcpb`** — OAuth bridge (optional) | Paste first prompt | Over MCP: `read_skill` slug `contextcore` |
| **Other MCP clients** | Remote URL or stdio npm (see README) | Paste first prompt | Over MCP: `read_skill` slug `contextcore` |
| **Terminal / CI** | [`contextcore-cli`](https://www.npmjs.com/package/contextcore-cli) | `contextcore` commands | N/A |

**MCP endpoint (all remote paths):** `https://cloud.contextcore.md/mcp`

## Cursor — full plugin

**[Cursor Directory](https://cursor.directory/plugins/contextcore)** — Add to Cursor on the MCP and Commands tabs (skill + `/contextcore-init`).

**OAuth MCP one-click:** use **Add to Cursor** on [cloud.contextcore.md/account](https://cloud.contextcore.md/account) (MCP deeplink — not the deprecated `plugin/install?repo=` URL).

Local test: copy this repo to `~/.cursor/plugins/local/contextcore` and reload Cursor.

## Claude Code — plugin (recommended)

```bash
claude plugin marketplace add babaVC/contextcore-mcp
claude plugin install contextcore@contextcore-mcp
```

Bundled: remote MCP (OAuth), `skills/contextcore/SKILL.md`, init command. Invoke **`/contextcore:contextcore-init`** or paste **`Set up ContextCore and initialize it.`**

**MCP-only fallback** (no plugin bundle):

```bash
claude mcp add --transport http contextcore https://cloud.contextcore.md/mcp
```

Submit listing: [Claude plugin directory](https://clau.de/plugin-directory-submission) — see [SUBMISSION.md](./SUBMISSION.md).

## Claude Desktop (chat) — Custom Connector

1. **Customize → Connectors → Add custom connector**
2. URL: `https://cloud.contextcore.md/mcp`
3. Enable connector in a chat → browser OAuth on first use
4. Paste: `Set up ContextCore and initialize it.`

Syncs across Claude Desktop and claude.ai when signed in.

## Claude Desktop — Extension (.mcpb)

Optional one-click install for Settings → Extensions. OAuth bridge via `@abluva/mcp-remote` — see [desktop-extension/README.md](./desktop-extension/README.md).

Build: `npx @anthropic-ai/mcpb pack desktop-extension dist/contextcore.mcpb`

Primary Desktop path remains **Custom Connectors** (no local bridge process).

## Other editors

**Remote HTTP (OAuth when supported):**

```json
{
  "mcpServers": {
    "contextcore": {
      "url": "https://cloud.contextcore.md/mcp"
    }
  }
}
```

**Stdio-only clients** — `npx contextcore-mcp` with a PAT from ContextCore **Account → Integrations → Advanced**.

## Same gateway for everyone

All paths hit **`https://cloud.contextcore.md/mcp`** (or your on-prem URL). Federation, review gates, and OAuth are server-side.

## MCP config files in this repo

| File | Used by |
|------|---------|
| `mcp.json` | Cursor plugin (pinned in `.cursor-plugin/plugin.json`) |
| `.mcp.json` | Claude Code plugin (pinned in `.claude-plugin/plugin.json`) |

Do not diverge URLs between the two without updating both.
