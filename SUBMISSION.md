# Marketplace submissions

Repo: `https://github.com/babaVC/contextcore-mcp`

Plugin name: **contextcore** (manifest `name`; display name **ContextCore**)

---

## Cursor marketplace

**Cursor Directory:** **Published** — https://cursor.directory/plugins/contextcore

**Official marketplace** (`cursor.com/marketplace/publish`): Submitted **2026-09-03** — separate queue, no public status page.

| Target | URL | Status |
|--------|-----|--------|
| **Cursor Directory** | https://cursor.directory/plugins/contextcore | **Live** (2026-09-03 submit) |
| **Official marketplace** | https://cursor.com/marketplace/publish | Submitted 2026-09-03 — awaiting email |

### Install paths (Cursor)

The old `cursor://…/plugin/install?repo=` deeplink returns **Unrecognized deep link** in current Cursor builds. Use:

| Path | URL / action |
|------|----------------|
| **OAuth MCP (one-click)** | `cursor://anysphere.cursor-deeplink/mcp/install?name=contextcore&config=…` with `{ type: "http", url: "https://cloud.contextcore.md/mcp" }` — generated in-app on Account / Agents |
| **Full plugin** | [cursor.directory/plugins/contextcore](https://cursor.directory/plugins/contextcore) — Add to Cursor on MCP + Commands tabs |

If review stalls: **marketplace-publishing@cursor.com**

---

## Claude Code plugin directory

**Status:** Submitted **2026-09-08** via [Console](https://platform.claude.com/plugin-submissions) — **pending review**.

### Install path (post-listing)

Once approved, users install from the **community** catalog:

```bash
claude plugin marketplace add anthropics/claude-plugins-community
claude plugin install contextcore@claude-community
```

Until listed (~24h after approval), self-hosted marketplace still works:

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
- [x] Submit form — Console **2026-09-08** (`https://github.com/babaVC/contextcore-mcp`)
- [ ] Approved → appears in `anthropics/claude-plugins-community` catalog
- [ ] Smoke: community install → OAuth → `/contextcore:contextcore-init` or first prompt

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
