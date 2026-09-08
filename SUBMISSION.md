# Marketplace submissions

Repo: `https://github.com/babaVC/contextcore-mcp`

Plugin name: **contextcore** (manifest `name`; display name **ContextCore**)

---

## Cursor marketplace

**Status:** Submitted **2026-09-03** — awaiting review.

| Target | URL | Status |
|--------|-----|--------|
| **Official marketplace** | https://cursor.com/marketplace/publish | Submitted 2026-09-03 |
| **Cursor Directory** | https://cursor.directory/plugins/new | Submitted 2026-09-03 |

### Pre-submit checklist (Cursor)

- [x] `.cursor-plugin/plugin.json` — `mcpServers` pinned to `./mcp.json`
- [x] Skill + command synced from `context-os` via `npm run sync:cursor-plugin`
- [x] Marketplace logo — `assets/logo-marketplace.svg`
- [ ] Local test: `~/.cursor/plugins/local/contextcore` → `/contextcore-init`

### Deeplinks

| Format | URL |
|--------|-----|
| Plugin (repo) | `cursor://anysphere.cursor-deeplink/plugin/install?repo=babaVC%2Fcontextcore-mcp` |
| MCP only | `cursor://anysphere.cursor-deeplink/mcp/install?name=contextcore&config=…` |

If review stalls: **marketplace-publishing@cursor.com**

---

## Claude Code plugin directory

**Status:** Validation passed 2026-09-08 — submit at [Console form](https://platform.claude.com/plugins/submit) or [claude.ai form](https://claude.ai/admin-settings/directory/submissions/plugins/new) (Team/Enterprise).

### Install path (post-listing)

```bash
claude plugin marketplace add babaVC/contextcore-mcp
claude plugin install contextcore@contextcore-mcp
```

Marketplace manifest: `.claude-plugin/marketplace.json`  
Plugin manifest: `.claude-plugin/plugin.json`  
MCP config: `.mcp.json` (remote OAuth URL only)

### Suggested listing copy

**Name:** ContextCore

**One-liner:** Product context for AI agents — MCP gateway, Initialize skill, browser OAuth.

**Description:** ContextCore gives Claude Code secure access to your project's context (components, rules, skills, risks, open questions) via a hosted MCP gateway. Browser OAuth — no token to paste. Includes the Initialize playbook skill and `contextcore-init` for first-run setup. Same gateway as Cursor and Claude Desktop Connectors.

**Repository:** https://github.com/babaVC/contextcore-mcp

**Homepage:** https://contextcore.md/docs/mcp

**Trust:** https://contextcore.md/trust

### OAuth / privacy note (for reviewers)

- MCP endpoint: `https://cloud.contextcore.md/mcp`
- Auth: OAuth 2.1 via Supabase (RFC 9728 PRM discovery)
- Scopes: user selects projects + optional write (propose) on consent screen
- No PAT required for primary path
- Federation enforced server-side — token never sees more than the user can read in-app

### Pre-submit checklist (Claude)

- [x] `.claude-plugin/plugin.json` + `.claude-plugin/marketplace.json`
- [x] `.mcp.json` — OAuth URL, no embedded token
- [x] Skills + commands synced from `mcpPlaybook.js`
- [x] `claude plugin validate .` passes (marketplace `source` must be `./` not `.`)
- [ ] Submit form — **GitHub repo URL only:** `https://github.com/babaVC/contextcore-mcp`
- [ ] Smoke: plugin install → OAuth → `/contextcore:contextcore-init` or first prompt

### Official marketplace (follow-up)

For Anthropic-held OAuth credentials or Connectors Directory listing, contact **mcp-review@anthropic.com** after community listing is live.

---

## Claude Desktop Extension (.mcpb)

**Status:** Source in `desktop-extension/` — pack with `@anthropic-ai/mcpb`, attach to GitHub Releases.

Not submitted to Anthropic Extensions directory in this pass — build artifact + README documented.

Pack command:

```bash
cd desktop-extension
npx @anthropic-ai/mcpb validate manifest.json
npx @anthropic-ai/mcpb pack . ../dist/contextcore.mcpb
```

---

## After any listing goes live

- [ ] Update `context-os` docs + `McpConnectPanel` with marketplace search links
- [ ] Remove "awaiting review" notes from README when Cursor listing is confirmed
