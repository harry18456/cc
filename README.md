English | [繁體中文](README.zh-TW.md)

# cc — Harry's Claude Code Plugin Marketplace

A personal collection of Claude Code plugins, with more small tools to come. Each plugin lives in **its own repo** — this repo is just the marketplace listing.

## Plugins

| Plugin | Source | Description | Platform |
|--------|--------|-------------|----------|
| hook-notify | [harry18456/cc-hook-notify](https://github.com/harry18456/cc-hook-notify) | Native Windows toast + sound notification when Claude finishes responding or waits for input | Windows |
| cowork-insights | [harry18456/cc-cowork-insights](https://github.com/harry18456/cc-cowork-insights) | Cowork-only usage analytics: reports via the same pipeline as the built-in `/insights` (same prompts, same template, same 30-day window), with sources curated to Cowork sessions; read-only, zero-dependency | Windows |
| agy-image | [harry18456/cc-agy-image](https://github.com/harry18456/cc-agy-image) | Generate / edit images with the local `agy` CLI (Antigravity / Gemini Nano Banana), no API key; true background removal via `rembg` producing transparent PNGs | Windows |
| codex-image | [harry18456/cc-codex-image](https://github.com/harry18456/cc-codex-image) | Generate / edit images with the `codex` CLI's built-in `image_gen` tool (OpenAI gpt-image-2) on a ChatGPT subscription, no API key; exact sizes guaranteed by the driver, true background removal via `rembg` | Cross-platform |
| spec-orchestrate | [harry18456/cc-spec-orchestrate](https://github.com/harry18456/cc-spec-orchestrate) | Autonomous spec-driven development orchestrated entirely by Claude — propose→apply→review→archive→commit with no approval waits, hybrid main-thread/subagent execution, per-stage review gates, runtime verification; for spectra/openspec repos | Cross-platform |

## Installation

Run in Claude Code:

```
/plugin marketplace add harry18456/cc
/plugin install hook-notify@harry18456
/plugin install cowork-insights@harry18456
/plugin install agy-image@harry18456
/plugin install codex-image@harry18456
/plugin install spec-orchestrate@harry18456
```

Restart Claude Code to take effect (install only the ones you want).

## Local development / testing

Each plugin is developed in its own repo. Load the plugin folder locally — no need to push to GitHub first:

```
claude --plugin-dir <path to the plugin repo>
```

For example, hook-notify: `claude --plugin-dir ../cc-hook-notify`

## What else this marketplace supports

Beyond the current plugins, `marketplace.json` supports the following (useful when extending; the `hook-notify` entry already demonstrates most optional fields and can serve as a template for new plugins):

- **Multiple plugins** — the `plugins` array can hold many entries; a single `add` lets users pick what to install.
- **Categories & search** — each entry can have `category` (development / productivity / security / design / monitoring…), `tags`, and `keywords`.
- **Author / metadata** — `displayName`, `author` (name / email / url), `homepage`.
- **Versioning strategies**
  - Pinned version — set `version`; users won't auto-update.
  - Auto-tracking — omit `version`; the git commit SHA is authoritative.
  - **Tag pin** — add `"ref": "v0.1.0"` to `source` to pin a tag (recommended for public releases).
- **4 source types**
  - `github` — `{ "source": "github", "repo": "owner/repo", "ref": "v1.0.0" }`
  - `url` — full git URL (`{ "source": "url", "url": "….git" }`)
  - `git-subdir` — a monorepo subfolder (⚠️ not supported by older Claude Code versions; mind compatibility)
  - Relative path — `"./plugins/xxx"` (plugin lives in the same repo as marketplace.json)
- **Renames** — top-level `renames` (`{ "old-name": "new-name" }`) keeps an alias for renamed plugins so existing installs upgrade seamlessly.

Full schema: [official docs](https://code.claude.com/docs/en/plugin-marketplaces).
