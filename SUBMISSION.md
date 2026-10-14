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
| **Full plugin (recommended)** | `npx plugins add babaVC/contextcore-mcp --target cursor` or Customize → search **ContextCore** |
| **OAuth MCP (browser button)** | `https://cursor.com/install-mcp?name=contextcore&config=…` — Account / landing |
| **OAuth MCP (native deeplink)** | `cursor://anysphere.cursor-deeplink/mcp/install?…` — fallback |
| **Discovery** | [cursor.directory/plugins/contextcore](https://cursor.directory/plugins/contextcore) |

`plugin/install?repo=` returns **Unrecognized deep link** in current Cursor builds. After official marketplace listing, switch to `plugin/add?id=<catalog-id>`.

If review stalls: **marketplace-publishing@cursor.com**

---

## Claude Code plugin directory

**Status: DEAD SUBMISSION — never entered review.** Diagnosed 2026-10-14.

### What happened

Submitted 2026-09-08 through the **Claude Console** plugin-submissions form. That form
is **no longer supported** — Anthropic moved plugin intake to a developer portal at
[claude.ai/directory/manage](https://claude.ai/directory/manage), and submissions left in
the old Console queue do not migrate themselves. Ours sat there; it never reached the
review pipeline that feeds the catalog.

Evidence:

- `anthropics/claude-plugins-community` catalog was last synced **2026-10-14** and lists
  **2,283 plugins** — the queue is moving, so this was not a slow review
- no `contextcore` entry, and no babaVC-owned entry of any name, in that catalog
- repo is **public**, in sync with `origin/main` (`dfbe60d`), MIT licensed — nothing on our side blocked it
- `claude plugin validate .` → **passed**
- the old URL in these notes (`platform.claude.com/plugin-submissions`) now **404s**
- the canonical intake, `clau.de/plugin-directory-submission`, redirects to
  [claude.com/docs/directory/publish](https://claude.com/docs/directory/publish), which has a
  section titled *"Move an earlier submission to the developer portal"* describing exactly this case

Name `contextcore` is still **free** in the catalog. Nearest neighbours are unrelated
third-party plugins (`context-os` by sravan27, `contextmatic`, `contextstellar`) — no
blocking collision, though a look-alike reviewer hold is possible.

### Owning account — decided 2026-10-14

Submit from **david@babavc.com**. The first organization to submit a given repository
folder holds that listing permanently, and the portal refuses a second organization's
submission of the same one — so this is a one-way door. Matches `plugin.json`
(`author.name` ContextCore, `hello@babavc.com`); no manifest change needed.

Do **not** submit from the older personal account. Its developer portal
(`claude.ai/directory/manage`) shows *"Nothing submitted yet"*, confirmed 2026-10-14 —
expected, because the dead 2026-09-08 entry lives in the **Claude Console**, a separate
system. That also means there is no portal draft to delete before emailing.

Because david@babavc.com is a different org from the September submitter, the
*"Already submitted by another organization"* refusal is **likely**, not hypothetical.
Treat the refusal as the diagnostic rather than hunting for the Console page first.

Before submitting, confirm on david@babavc.com:

- **Plan** is Pro, Max, Team, or Enterprise — Free accounts cannot submit
- **Role**, if it is a Team/Enterprise workspace — an Owner submits, or a member granted
  the Directory permission via a custom role under Organization settings → Roles

### Recovery path

1. Sign in to the **Claude Console** and open its Plugin submissions page
   - **Withdraw button present** → Withdraw, then resubmit at `claude.ai/directory/manage`
   - **no Withdraw button** → email **directory@anthropic.com** to have it moved to the
     portal instead of starting fresh
2. Do *not* submit in the portal first. Until the Console entry is withdrawn or moved, the
   portal can refuse **Submit for review** for the same repo + folder with
   *"Already submitted by another organization."* If a portal draft already exists for this
   repo, delete the draft before emailing
3. Submit from the **org that should own the listing long term** — the first org to submit a
   given repo folder holds it permanently, and the portal refuses a second org for the same one
4. Submit the gateway **separately as an MCP connector** (new since our last pass): a remote
   MCP server always gets its own connector listing, even when a bundle references it. Gains
   a health/usage dashboard per tool, its own listing + auth config, and **pairing** with the
   bundle when both come from the same org. Point both at `https://cloud.contextcore.md/mcp`
   so users with both see one set of tools
5. Run the portal's **Validate** on the Source step before submitting — it checks the
   directory rules that `claude plugin validate` does not (README, license, name taken)

### Portal validation + migration request — 2026-10-14

Ran **Validate** in the developer portal against `main @ 22b4df4`. Result: **7 checks,
0 blocking**, 1 warning, 3 policy holds. A policy hold is not a rejection — it routes the
version to a human reviewer.

| Check | Result |
|---|---|
| Repository fetched · 24 files, 70.7 kB · `plugin.json` valid · 1 skill, 1 command, 1 MCP server (`contextcore`) | Pass |
| Directory lints · Name and publisher checks | Passed with warnings |
| **Name may be confused with an existing listing** | **Policy hold** |
| **Uses a credential from the user's machine** (2 findings) | **Policy hold** |
| No privacy policy URL | Warning → **fixed**, `privacyPolicyUrl` set (`597fbf6`) |
| Images and fonts passed without a code check (`assets/logo-marketplace.png`) | Informational, no action |

**The name hold is the September submission, not a coincidence.** Verbatim:

> `"contextcore"` matches the display name "ContextCore" of plugin
> `"babavc/contextcore-mcp"`, which is **not yours**. Held for review.

That repository *is* ours. The directory already holds a claim on it, registered to the
org that submitted through the Console on 2026-09-08, and from the submitting account it
reads as a stranger's listing. No repo change can clear this — only withdrawal or
migration can.

**Emailed `directory@anthropic.com` on 2026-10-14** asking them to move or withdraw the
Console submission, with the listing to belong to the **david@babavc.com** org. Awaiting
reply. Do not click **Submit for review** from any other account while this is open: the
first org to submit holds the listing permanently, so submitting from the wrong one to
dodge the collision would settle ownership on the wrong account irreversibly.

**Free diagnostic, still unrun:** from the *old* account, open a submission and press
**Validate**, then stop. If the name hold disappears, that account's org owns the claim
and can withdraw it directly. If it persists, the claim sits elsewhere and the email is
the only path. Validate is read-only; Submit is the one-way door.

### Open: "Uses a credential from the user's machine" (2 findings)

Not yet resolved — the portal's two file paths have not been read off the expanded row.
The rule: *don't read a credential already set in the user's environment and send it to a
server, even in a README example; ask through a `userConfig` entry with `sensitive: true`.*

Near-certain culprit is `bin/cli.js:42` — `process.env.CONTEXTCORE_TOKEN`, forwarded to
the gateway. The other is probably one of the `"env": { "CONTEXTCORE_TOKEN": "YOUR_TOKEN" }`
examples in `README.md` or `EDITORS.md`.

Three ways out, in rough order of correctness:

1. **Split the npm proxy out of the plugin folder.** The Claude Code bundle never loads
   `bin/cli.js` — `.claude-plugin/plugin.json` declares only the skill, the command, and
   the OAuth-only `.mcp.json`. The stdio proxy is cargo from this repo doing double duty as
   the `contextcore-mcp` npm package. Cleanest, but moves what the npm package builds from
2. **Declare `userConfig` with `sensitive: true`** in `plugin.json` — the validator's own
   suggested remedy, though it declares a token the bundle's MCP server never uses
3. **Accept the hold.** All three holds reach the same reviewer anyway, and a user's own PAT
   for our own gateway is a defensible pattern

### Repo cleanup — done 2026-10-14

Checked against the current [pre-submission checklist](https://claude.com/docs/plugins/pre-submission-checklist).
Plugin folder is the repo root (`source: "./"`), so **every tracked file counts**.

| Finding | Severity | Resolution |
|---|---|---|
| `desktop-extension/manifest.json` ran `npx -y @abluva/mcp-remote` — unpinned launcher, a third-party fork of `mcp-remote` fetched at runtime | **Blocked** + security-scan risk | **Deleted** `desktop-extension/`. MCPB is deprecated anyway |
| `package.json` beside `package-lock.json` at plugin root → *"Dependencies install from a lockfile"* | Reviewer hold | **Removed lockfile from git** + gitignored. The dep install fires only when a `package.json` and a lockfile sit together, and npm excludes `package-lock.json` from published tarballs — so npm consumers are unaffected |
| `npx -y contextcore-mcp` unpinned in README/EDITORS stdio examples | **Blocks** (unpinned npx) if the scanner reads doc code blocks | **Pinned** to `contextcore-mcp@0.1.0` |
| `metadata.repository` in `marketplace.json` — unknown field | Warning | **Removed**; repo URL already in `plugin.json` |

`claude plugin validate .` → **passed, no warnings**. All manifest component paths resolve;
both MCP configs are `type: http` on absolute `https://` URLs with no embedded credential.

**Correction to an earlier note in this file:** `mcp.json` is *not* a stray duplicate of
`.mcp.json`. It is the **Cursor** plugin's MCP config, pinned by
`.cursor-plugin/plugin.json`. Both files are required; keep their URLs in sync.

Clean: README 836 words (≥40 ✓), `LICENSE` + `license` field ✓, 17 tracked files (≤512 ✓),
largest file 30 KB (≤256 KiB ✓), `node_modules/` gitignored ✓, skill and command front
matter parse with text `description` ✓.

### Install path (post-listing)

Once approved, users install from the **community** catalog:

```bash
claude plugin marketplace add anthropics/claude-plugins-community
claude plugin install contextcore@claude-community
```

Until listed, the self-hosted marketplace still works:

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

### Checklist

- [x] `.claude-plugin/plugin.json` + `.claude-plugin/marketplace.json`
- [x] `.mcp.json` — OAuth URL, no embedded token
- [x] Skills + commands synced from `mcpPlaybook.js`
- [x] `claude plugin validate .` passes clean, no warnings (marketplace `source` must be `./` not `.`)
- [x] ~~Submit form — Console 2026-09-08~~ — **dead queue, form no longer supported**
- [ ] Withdraw / migrate the Console submission (step 1 above)
- [x] Remove `desktop-extension/`; pin npx; drop lockfile (2026-10-14) — `mcp.json` **kept**, it is the Cursor config
- [ ] Resubmit plugin bundle at `claude.ai/directory/manage` **as david@babavc.com**, Validate before submitting
- [ ] Submit `cloud.contextcore.md/mcp` as an MCP connector **from the same account**, pair with the bundle
- [ ] Approved → appears in `anthropics/claude-plugins-community` catalog
- [ ] Smoke: community install → OAuth → `/contextcore:contextcore-init` or first prompt

### Submitter requirements

Paid plan (Pro / Max / Team / Enterprise). On Team/Enterprise an **Owner** submits;
Enterprise Owners can grant a **Directory** permission via a custom role.

---

## Claude Desktop Extension (.mcpb) — DEPRECATED

**Do not pursue.** As of the 2026-10-14 docs check, desktop-extension listings in the
directory are **deprecated**, and the directory **no longer accepts local MCP servers
packaged as desktop extensions (MCPB)**. To distribute a local MCP server through the
directory, include it in a plugin bundle instead.

Our gateway is remote anyway, so nothing is lost — the bundle's `.mcp.json` plus the
separate MCP connector submission cover every surface. `desktop-extension/` should be
deleted from the repo: it also carries the unpinned `npx @abluva/mcp-remote` launcher that
would block or flag validation (see the table above).

---

## After any listing goes live

- [ ] Update `context-os` docs + `McpConnectPanel` with marketplace search links
- [ ] Remove "awaiting review" notes from README when Cursor listing is confirmed
