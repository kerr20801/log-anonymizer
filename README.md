# 🪵 log-anonymizer

> 貼上 Log，一鍵遮蔽 IP · Token · 憑證 · 主機名。純瀏覽器執行，資料不離開你的電腦。
>
> Paste logs — auto-redact IPs, tokens, credentials, hostnames. Runs entirely in your browser, data never leaves your machine.

---

## 這是什麼？ / What is it?

分享 Log 給廠商或同事前，需要手動刪掉私有 IP、API Token、資料庫密碼、主機名……這既耗時又容易出錯。

Before sharing logs with vendors or teammates, you need to manually remove private IPs, API tokens, database passwords, hostnames — tedious and error-prone.

**log-anonymizer** 讓你貼上任何 Log，即時遮蔽敏感資料，下載遮蔽版 + 對照表（可還原），整個流程不超過30秒。

**log-anonymizer** lets you paste any log, see redacted output instantly, download the redacted version + a restore map — all in under 30 seconds.

---

## 功能 / Features

### 自動偵測 / Auto-detection

| 類型 / Type | 範例 / Example | 替換結果 / Replacement |
|---|---|---|
| 私有 IP (RFC 1918) / Private IP | `192.168.1.1`, `10.0.0.5` | `[[PRIVATE_IP_xxxxxx]]` |
| Email | `admin@example.com` | `[[EMAIL_xxxxxx]]` |
| MAC 位址 / MAC Address | `AA:BB:CC:DD:EE:FF` | `[[MAC_xxxxxx]]` |
| JWT | `eyJhbGci...` | `[[JWT_xxxxxx]]` |
| URL 憑證 / URL Credential | `redis://:password@host` | `[[URL_CRED_xxxxxx]]` |
| Token / API Key | `ghp_xxx`, `glpat-xxx`, `sk-xxx`, `AKIA...` | `[[TOKEN_xxxxxx]]` |
| Key=Value 憑證 / Key=Value Cred | `password=abc123`, `api_key: xyz` | `[[CRED_xxxxxx]]` |
| 自訂網域 / Custom Domain | `es01.internal.company.com` | `[[DOMAIN_xxxxxx]]` |
| 自訂字面值 / Custom Literal | 任意密碼、Token / any secret | `[[LITERAL_xxxxxx]]` |
| 使用者名稱 / Username | `/home/alice/app.log` | `[[USER_xxxxxx]]` |
| 啟發式 / Heuristic | `client_secret=...` | `[[SECRET_xxxxxx]]` |

### 格式自動偵測 / Log Format Detection

自動辨識 10 種常見格式：

Automatically identifies 10 common formats:

- nginx access / error log
- syslog / journalctl
- docker logs（ISO 8601 timestamp）
- kubernetes（glog 格式）
- apache access log
- python logging
- JSON log
- Windows event log

### 其他功能 / More

- **即時預覽** — 左側貼上，右側即時顯示，各類型以不同顏色標示 / Real-time preview with color-coded tag types
- **統計面板** — 各類型偵測數量一覽 / Per-type detection count in sidebar
- **規則開關** — 個別停用任何內建規則 / Toggle individual rules on/off
- **還原模式** — 下載 `.map.json`，之後可將遮蔽 Log 還原成原始內容 / Download `.map.json` to restore redacted logs later
- **穩定 ID** — 相同值永遠產生相同標籤（MD5），方便跨行比對 / Same value always gets same tag (MD5-based)
- **介面雙語** — 繁體中文 / English 切換 / Bilingual UI (ZH/EN toggle)
- **無框架、單一 HTML 檔案** / No framework, single HTML file

---

## 使用方式 / How to use

1. 開啟 `log-anonymizer.html`（直接雙擊，不需伺服器）
   Open `log-anonymizer.html` — double-click, no server needed
2. 貼上 Log 內容（左側輸入框）
   Paste your log content (left panel)
3. 右側即時顯示遮蔽結果，側欄顯示各類型統計
   See redacted output instantly on the right, with per-type counts in the sidebar
4. 下載遮蔽版 Log + `.map.json` 對照表
   Download the redacted log + `.map.json` restore map

### 還原 / Restore

1. 切換到「↩ 還原」分頁 / Switch to "↩ Restore" tab
2. 載入 `.map.json` / Load your `.map.json`
3. 貼上遮蔽後的 Log / Paste the redacted log
4. 右側即時顯示還原結果 / See original content restored on the right

---

## 自訂設定 / Custom Settings

| 功能 / Feature | 說明 / Description |
|---|---|
| 自訂網域 / Custom Domains | 加入內部網域，所有子網域自動覆蓋 / Add internal domains, all subdomains covered |
| 遮蔽字串 / Mask Strings | 貼上任意密碼或 Token，全文搜尋遮蔽 / Add any secret, masked everywhere |
| 使用者名稱 / Username | 遮蔽路徑中的使用者名 / Redact username from file paths |
| 規則開關 / Rule Toggles | 個別停用任何內建規則 / Disable individual built-in rules |

自訂網域與字串儲存在 `localStorage`，重開頁面後仍保留。

Custom domains and strings are saved to `localStorage` and persist across sessions.

---

## 隱私 / Privacy

所有處理在瀏覽器本機完成，Log 不會上傳到任何伺服器。

All processing happens locally in your browser. Logs are never uploaded anywhere.

- 無後端、無資料庫、無 Cookie、無追蹤 / No backend, no database, no cookies, no tracking
- 離線可用（無需載入外部函式庫）/ Works fully offline — no external libraries
- 原始碼完全公開，歡迎自行審查 / Source code fully open, audit freely

---

## License

MIT
