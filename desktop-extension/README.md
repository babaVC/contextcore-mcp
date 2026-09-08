# Pack the Desktop Extension (.mcpb)

OAuth bridge to `https://cloud.contextcore.md/mcp` via `@abluva/mcp-remote` (stdio → Streamable HTTP).

## Build (dev machine)

Requires Node.js 18+ and network access to npm.

```bash
cd desktop-extension
npx @anthropic-ai/mcpb validate manifest.json
npx @anthropic-ai/mcpb pack . ../dist/contextcore.mcpb
```

Optional: add a 512×512 `icon.png` beside `manifest.json` before packing (marketplace-style icon).

## Install (Claude Desktop)

1. Double-click `contextcore.mcpb`, **or**
2. Settings → Extensions → Advanced settings → Install Extension…

On first MCP use, the bridge opens browser OAuth (same flow as Custom Connectors).

## Primary Desktop path

**Custom Connectors** (Customize → Connectors → paste MCP URL) is the recommended path — account-synced, no local bridge process. Use this `.mcpb` when you prefer the Extensions UI or need a one-click offline installer artifact.

## Endpoint override

Production URL is baked into `manifest.json` args. For on-prem, rebuild with your instance `/mcp` URL or use Custom Connectors / Claude Code plugin variables instead.
