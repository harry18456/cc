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
| adhd-ste100-eli5 | [harry18456/cc-adhd-ste100-eli5](https://github.com/harry18456/cc-adhd-ste100-eli5) | An output style that makes answers cheap to read and cheap to act on — message shape from ADHD support practice, sentence mechanics from the ASD-STE100 controlled-English standard, word choice from ELI5; language-neutral | Cross-platform |
| docs | [harry18456/cc-docs](https://github.com/harry18456/cc-docs) | Evidence-tagged project knowledge: `doc-mine` interviews you, then mines the source into categorized `docs/` where every sentence cites `file:line` / official URL / actual run (gaps marked `[UNVERIFIED]`); `doc-distill` condenses it into one self-contained file | Cross-platform |
| qrcode | [harry18456/cc-qrcode](https://github.com/harry18456/cc-qrcode) | QR codes guaranteed to scan — logo in the middle, brand colors, dot / rounded modules, table cards; a deterministic engine picks EC level, version and logo size, then gates every design on per-block error budget, two decoders and robustness sweeps; runs with `uv` or plain Python 3.12–3.14, no system libraries | Cross-platform |
| jev-routing | [harry18456/cc-jev-routing](https://github.com/harry18456/cc-jev-routing) | Per-turn model routing: asks Jev (TypeSafe System One, ~400 ms, a fraction of a cent) which tier each prompt or subagent brief needs and runs it on haiku / sonnet / opus / fable, moving the effort with it; down-only by default, `policy none` moves only the effort and keeps the prompt cache untouched, confidence gate, fails open; `/jev` commands and a settings panel, per user / project / local; needs a TypeSafe API key | Cross-platform |
| inmu-king | [harry18456/cc-inmu-king](https://github.com/harry18456/cc-inmu-king) | A joke mod: every 淫夢 meme you type (or Claude does, at half points) lights rainbow letters of T A D O K O R O above the prompt, with the meme's meaning in English or 繁體中文; eight letters is a burst (a chant, a moving pixel picture, an 8-bit jingle) and one rank up a chart from #20 to #1, where Claude ends one reply with やりますねぇ！; a meme collection, your own clips, turn times as 114514 arithmetic; each session plays its own game, nothing is saved; sound on Windows and macOS | Cross-platform |

## Installation

Run in Claude Code:

```
/plugin marketplace add harry18456/cc
/plugin install hook-notify@harry18456
/plugin install cowork-insights@harry18456
/plugin install agy-image@harry18456
/plugin install codex-image@harry18456
/plugin install spec-orchestrate@harry18456
/plugin install adhd-ste100-eli5@harry18456
/plugin install docs@harry18456
/plugin install qrcode@harry18456
/plugin install jev-routing@harry18456
/plugin install inmu-king@harry18456
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
