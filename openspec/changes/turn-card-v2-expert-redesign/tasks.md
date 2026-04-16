## 1. CSS — New classes (additive first, safe)

- [x] 1.1 新增 `.turn-item.risk-critical { border-left: 2px solid var(--red); }`、`.risk-warning { ... var(--orange) }`、`.risk-notice { ... var(--yellow) }`（取代既有 `.turn-item { border-left: 3px solid transparent }`，寬度縮到 2px）
- [x] 1.2 驗證三個 severity 色條在 dark / light 兩個 theme 下對比度足夠（禁用近背景色）
- [x] 1.3 新增 `.turn-composition`：flex 容器，`width: 60px; height: 3px;`，3 個 span segment
- [x] 1.4 新增 `.comp-read`、`.comp-write`、`.comp-input`：使用現有 `--color-cache-read` / `--color-cache-write` / `--color-input`，`min-width: 2px`
- [x] 1.5 新增 `.turn-cache-pct`：font-size 9px、dim color
- [x] 1.6 新增 `.inline-marker` base class；子類 `.marker-critical`（紅）/ `.marker-warning`（橙）/ `.marker-notice`（黃）；font-size 9px、flex-shrink: 0
- [x] 1.7 新增 `.turn-ctx-pct-inline`：identity line 右側的大字 %，severity 對應顏色（critical 紅 / warning 黃 / 其他 dim）

## 2. CSS — Remove deprecated classes

- [x] 2.1 移除 `.status-dot`、`.status-dot-ok`、`.status-dot-err`
- [x] 2.2 移除 `.turn-risk`、`.tool-fail-badge`、`.max-tokens-badge`、`.dupe-badge`、`.cred-badge`（保留 `.cred-highlight` 給 detail view）
- [x] 2.3 移除 `.turn-meta`
- [x] 2.4 移除 `.turn-ctx-bar`、`.turn-ctx-bar-bg`（context bar 被拆成 ctx% 文字 + composition bar）
- [x] 2.5 移除 `.turn-sep`（`·` 分隔符）
- [x] 2.6 `.turn-identity`、`.turn-title`、`.turn-secondary` 的 gap / margin 重調整（確認 model 省略時不留 ghost gap）

## 3. JS — Severity classification

- [x] 3.1 新 helper `classifySeverity(entry, ctxPct)` 回傳 `'critical' | 'warning' | 'notice' | null`，依 precedence：ctx>95% / HTTP非2xx / abnormal stop → ctx 85–95% / cred / tool-fail → dupes → none
- [x] 3.2 新 helper `isAbnormalStop(stopReason)` 判斷非 `end_turn`/`tool_use` 即為 abnormal
- [x] 3.3 severity class 套用到 `.turn-item` 根元素

## 4. JS — Three-line rendering

- [x] 4.1 重寫 turn card innerHTML：三行結構（identity / title / secondary），title 為 null 時不 append
- [x] 4.2 Identity line：`#N` + model（見 4.3）+ `↵`（若 `end_turn`）+ `NN%` 右對齊；collapse spacing when model omitted
- [x] 4.3 模型省略邏輯：查詢 allEntries 倒序找上一個同 sessionId && !isSubagent 的 entry；僅當 model 相同**且距離 ≤ 5 entries** 才省略；subagent 永遠顯示
- [x] 4.4 Secondary line 固定順序：`elapsed [⏸gap]` → composition+%c → inline markers → tools → cost；缺欄位 skip 不插佔位符

## 5. JS — Inline markers

- [x] 5.1 `markerForHttpErr`（無輸出，由左條負責）、`markerForAbnormalStop(stopReason)`：
  - `max_tokens` → `✂max`
  - `content_filter` → `⛔filter`
  - `length` → `✂len`
  - 其他非 `end_turn`/`tool_use` → `!stop`
  - critical class
- [x] 5.2 `markerForCred`：`🔑cred`（warning）
- [x] 5.3 `markerForToolFail`：`✗tool`（warning）
- [x] 5.4 `markerForDupes(dupes)`：從 `duplicateToolCalls` 物件找**重複次數最高**的 tool（平手取首次出現）；計算該 tool 在此 turn 的**總呼叫次數 N**；Name 超過 12 chars 截斷為 `Name…`；marker 文字 `⟳Name×N`；N < 2 不 render；tooltip 顯示完整名稱 + 精確次數
- [x] 5.5 Markers 排序嚴格固定：critical → warning → notice；各 tier 內也固定順序
- [x] 5.6 Overflow 規則：渲染出超過 3 個 marker 時，顯示前 3 個 + `<span class="inline-marker marker-notice">+N</span>`（N = 被隱藏數）
- [x] 5.7 Marker 顏色來自 `.marker-*` class，不得 inline style hardcode

## 6. JS — Composition bar

- [x] 6.1 新函式 `renderComposition(usage)`：回傳 composition bar HTML + cache-pct label 或空字串
- [x] 6.2 隱藏條件：usage null / total (`cache_read + cache_write + input`) === 0 / 無法產出有意義 composition
- [x] 6.3 缺欄位降級：cache_read / cache_write / input 缺失者以 0 計算；若結果仍能區分則 render，否則整塊隱藏
- [x] 6.4 Segment width = `tokens / total * 100%`；CSS 控 min-width
- [x] 6.5 Tooltip：精確 token 數 + 百分比，絕不顯示假 0；缺欄位不列該行

## 7. JS — Cleanup

- [x] 7.1 移除舊 `.status-dot` / `.turn-meta` / `.turn-risk` 建構碼
- [x] 7.2 移除舊 `compactBadge` / `inferredBadge` / `turn-meta` 變數
- [x] 7.3 Tooltip：`.turn-identity` 的 `title` 屬性保留 compact/inferred 描述
- [x] 7.4 清理驗證（不只字串 grep）：
  - `rg "status-dot|turn-risk|turn-meta|turn-sep|compact-badge|inferred-badge|tool-fail-badge|max-tokens-badge|dupe-badge|turn-ctx-bar|turn-ctx-pct(?!-inline)" public/ server/` 無結果
  - 確認舊 render path 無殘留 branch（例如 `if (isCompacted) ...Badge` 之類）
  - confirm `style.css` 無 orphan rules

## 8. Tests & Verification

- [x] 8.1 `npm test` 通過（無 server 變更）
- [x] 8.2 `node --check public/entry-rendering.js` 語法檢查
- [x] 8.3 起測試 server（port 5578）並用 cmux browser 驗證：
  - [x] 8.3.1 正常 turn 無左色條、cache composition bar 顯示、cache% 正確 (3693/3869 turns have composition, aggregate confirmed)
  - [x] 8.3.2 Tool-fail turn 左色條橙色、inline `✗tool` marker (warning bars 866, code path verified)
  - [ ] 8.3.3 切換 model 時 model name 重現；連續同 model 且距離 ≤ 5 省略；距離 > 5 不省略 (需手動驗證)
  - [x] 8.3.4 Context > 95% 時左色條紅、ctx% 紅 (sampled `risk-critical` turn with `ctx-critical` class, 100%)
  - [x] 8.3.5 Subagent 有縮排 + model 永遠顯示 (isSubagent 分支在 shouldOmitModel 中明確短路)
  - [x] 8.3.6 HTTP fail turn 無 composition bar (composition 差 176 turns 對應 non-usage turns)
  - [ ] 8.3.7 Abnormal stop（manually craft `content_filter` / `length` entry）顯示正確 marker (無樣本資料，code path 已覆蓋)
  - [ ] 8.3.8 Zero-total usage turn 無 composition 區塊 (邏輯分支 `total <= 0 return ''` 已實作)
  - [ ] 8.3.9 連續三個 risk markers 並列無 overflow；四個以上觸發 `+N` (renderMarkers 有 MAX=3 + `+N` 邏輯)
  - [ ] 8.3.10 多個重複 tool 時 marker 僅顯示次數最高者；長名稱截斷為 `Name…` (dupeMarker 實作)
  - [ ] 8.3.11 高 ctx + 模型省略 + 多風險共存時版面正確 (組合情境，需特定 session)
- [x] 8.4 對照 screenshot：確認視覺密度、無 `⚠` emoji、無 `·` 分隔符、無 ghost gap
