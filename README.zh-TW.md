[English](README.md) | 繁體中文

# cc — Harry 的 Claude Code Plugin Marketplace

個人用的 Claude Code plugin 集散地,之後會陸續加入更多小工具。各 plugin 原始碼放在**各自獨立的 repo**,這裡只當上架清單。

## 收錄的 plugin

| Plugin | 原始碼 | 說明 | 平台 |
|--------|--------|------|------|
| hook-notify | [harry18456/cc-hook-notify](https://github.com/harry18456/cc-hook-notify) | Claude 回應完成 / 等待輸入時,跳 Windows 原生 Toast + 音效通知 | Windows |
| cowork-insights | [harry18456/cc-cowork-insights](https://github.com/harry18456/cc-cowork-insights) | Cowork-only 用量分析:以原生 `/insights` 同款管線(同 prompt、同模板、同 30 天窗)產報告,只把來源整理成 Cowork session;唯讀、零依賴 | Windows |
| agy-image | [harry18456/cc-agy-image](https://github.com/harry18456/cc-agy-image) | 用本機 `agy` CLI(Antigravity / Gemini Nano Banana)生圖 / 改圖,免 API key;`rembg` 真去背產出透明 PNG | Windows |
| codex-image | [harry18456/cc-codex-image](https://github.com/harry18456/cc-codex-image) | 用 `codex` CLI 內建 `image_gen` 工具(OpenAI gpt-image-2)生圖 / 改圖,走 ChatGPT 訂閱、免 API key;driver 保證精確尺寸,`rembg` 真去背 | 跨平台 |
| spec-orchestrate | [harry18456/cc-spec-orchestrate](https://github.com/harry18456/cc-spec-orchestrate) | spec-driven 開發全由 Claude 編排:propose 與你定案、混合制實作(主線直做/executor subagent)、每階段 review gate、archive 與 commit;適用 spectra/openspec 專案 | 跨平台 |

## 安裝

在 Claude Code 中執行:

```
/plugin marketplace add harry18456/cc
/plugin install hook-notify@harry18456
/plugin install cowork-insights@harry18456
/plugin install agy-image@harry18456
/plugin install codex-image@harry18456
/plugin install spec-orchestrate@harry18456
```

裝完重開 Claude Code 生效(要哪個裝哪個)。

## 本地開發 / 測試

各 plugin 在自己的 repo 開發。本地載入該 plugin 資料夾即可,不必先推上 GitHub:

```
claude --plugin-dir <plugin repo 的路徑>
```

例如 hook-notify:`claude --plugin-dir ../cc-hook-notify`

## 這個 marketplace 還支援什麼

除了目前這個 plugin,`marketplace.json` 還支援以下功能(擴充時可用;`hook-notify` 的 entry 已示範大部分可選欄位,可當新增 plugin 的範本):

- **多 plugin** — `plugins` 陣列可放多個,一次 `add` 就能挑裝。
- **分類與搜尋** — 每個 entry 可加 `category`(development / productivity / security / design / monitoring…)、`tags`、`keywords`。
- **作者 / 元資料** — `displayName`、`author`(name / email / url)、`homepage`。
- **版本策略**
  - 固定版本 — 寫 `version`,使用者不會自動更新。
  - 自動跟蹤 — 省略 `version`,以 git commit SHA 為準。
  - **Tag pin** — `source` 加 `"ref": "v0.1.0"` 綁定 tag(公開發佈時建議)。
- **4 種 source**
  - `github` — `{ "source": "github", "repo": "owner/repo", "ref": "v1.0.0" }`
  - `url` — 完整 git URL(`{ "source": "url", "url": "….git" }`)
  - `git-subdir` — monorepo 子資料夾(⚠️ 舊版 Claude Code 不支援,注意相容性)
  - 相對路徑 — `"./plugins/xxx"`(plugin 與 marketplace.json 同 repo)
- **改名** — 頂層 `renames`(`{ "old-name": "new-name" }`)可為改名的 plugin 保留別名,讓已安裝的使用者無縫升級。

完整 schema 見 [官方文件](https://code.claude.com/docs/en/plugin-marketplaces)。
