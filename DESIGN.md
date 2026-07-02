# Danny Lin Portfolio — 設計規格文件

> 每次請 Claude Code 執行大任務時，在指令開頭加上：
> 「請先讀取 DESIGN.md，依照其中的設計規格執行，並保留所有已確認的設計決策。」

---

## 一、色彩系統（CSS 變數）

```css
:root {
  --color-primary: #cc785c;        /* coral 主色，用於按鈕、標籤、強調 */
  --color-primary-dark: #a85a40;   /* 深 coral，用於 hover 或次要按鈕 */
  --color-canvas: #faf9f5;         /* 米白，主要背景 */
  --color-soft: #f5f0e8;           /* 淺奶油，次要背景 */
  --color-card: #efe9de;           /* 卡片背景（淺色區塊） */
  --color-placeholder: #e8e0d2;    /* 佔位圖背景 */
  --color-dark: #1a1a18;           /* 深墨色，深色區塊背景 */
  --color-dark-elevated: #252320;  /* 深色卡片背景 */
  --color-ink: #141413;            /* 主要文字 */
  --color-body: #3d3d3a;           /* 內文文字 */
  --color-muted: #6c6a64;          /* 次要文字、說明文字 */
}
```

---

## 二、字體

| 用途 | 字體 |
|---|---|
| 全站中文（標題 + 內文） | LXGW WenKai TC |
| 英文／數字 | LXGW WenKai TC |
| 導覽列 | LXGW WenKai TC |

**Google Fonts 引入：**
```html
<link href="https://fonts.googleapis.com/css2?family=LXGW+WenKai+TC&display=swap" rel="stylesheet">
```

**Icon 庫：**
```html
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/@tabler/icons-webfont@latest/tabler-icons.min.css">
```

---

## 三、色彩節奏（各區塊背景依序）

| 區塊 | 背景色 | 特殊效果 |
|---|---|---|
| Hero | `--color-canvas` | — |
| 關於我 | `--color-soft` | — |
| 核心能力 | `--color-canvas` | — |
| 工作職能 | `--color-dark` | 噪點紋理 |
| 自我進修 | `--color-canvas` | — |
| 成果分享 | `--color-soft` | — |
| 工具開發 | `--color-canvas` | — |
| 工作經歷 | `--color-dark` | 噪點紋理 |
| 聯絡我 | `--color-primary` | 文字全白 |

**噪點紋理（深色區塊）：**
```css
.dark-section { position: relative; }
.dark-section::before {
  content: '';
  position: absolute;
  inset: 0;
  background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 200 200' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='noise'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.85' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23noise)' opacity='0.08'/%3E%3C/svg%3E");
  background-size: 200px 200px;
  opacity: 0.4;
  pointer-events: none;
  z-index: 0;
}
.dark-section > * { position: relative; z-index: 1; }
```

---

## 四、RWD 斷點

| 裝置 | 寬度 | 欄數 |
|---|---|---|
| 手機 | 375px | 單欄 |
| 平板 | 768px | 兩欄 |
| 桌機 | 1280px | 三欄 |

**手機版規則：**
- 所有 hover 效果改為點擊觸發
- 翻轉卡片改為點擊翻轉
- 工作職能卡片點擊展開/收合
- Hero 關鍵字雲改為靜態散布（不需動畫）
- 關於我區塊順序：照片 → 文字 → 標籤

---

## 五、各區塊設計規格

### Hero
- 左側：姓名 + 職稱打字機效果 + CTA 按鈕
- 右側（桌機）：職涯關鍵字雲，浮動動畫
- 右側（手機）：靜態關鍵字散布，固定高度約 200px

### 關於我
- 桌機：左右兩欄等寬（grid-template-columns: 1fr 1fr），垂直對齊頂部
- 右側欄：照片水平置中（display: flex; justify-content: center）
- 右側：正方形照片佔位圖（約 320x320px），點擊燈箱顯示多張照片
- 手機：單欄，順序：照片 → 文字 → 標籤
- 標籤（文字下方）：讀書會、戶外運動、貓奴、追劇、AI 工具開發、數位行銷
- 標籤樣式：細框圓角，文字深灰，背景 `--color-soft`

### 核心能力
- 呈現方式：翻轉卡片（3張）
- 卡片尺寸：撐滿欄寬，aspect-ratio: 1（正方形）
- 正面：icon（36px）+ 職位名稱（18px），垂直水平置中，white-space: nowrap
- 背面樣式（樣式 C）：
  - 背景：`--color-dark`
  - padding：16px 20px
  - 職位名稱：15px，#faf9f5，置中
  - 標籤：直向排列，寬度統一 130px，置中
  - 標籤樣式：border: 1px solid `--color-primary`，color: `--color-primary`
  - border-radius: 20px，padding: 4px 0，font-size: 12px，gap: 6px

| 卡片 | Icon | 背面標籤 |
|---|---|---|
| 內容企劃 | ti-file-text | 文案撰寫、SEO、季度規劃、EDM、新聞稿 |
| 專案管理 | ti-clipboard-list | 跨部門協作、預算控制、時程規劃、廠商接洽 |
| 社群行銷 | ti-brand-instagram | FB & IG 經營、KOC 合作、廣告投放、數據分析 |

### 工作職能
- 呈現方式：3欄網格，hover 展開標籤（手機版點擊展開）
- 背景：`--color-dark` + 噪點紋理
- 卡片背景：`--color-dark-elevated`
- 標籤：線條框，hover 填滿 coral

| 職能 | Icon | 標籤 |
|---|---|---|
| 內容企劃 | ti-file-text | 服務建議書、預算配置、市場分析、文案撰寫 |
| 社群經營 | ti-message-circle | 日常貼文、特殊節日、知識宣導、廣告投放 |
| KOC 合作 | ti-speakerphone | 推廣大使、開箱文、體驗文、影片 |
| 專案執行 | ti-target | 產品體驗、標章推廣、制度宣導、展場設計 |
| 美編設計 | ti-palette | 貼文圖片、公版設計、快訊節慶 |
| AI 工具開發 | ti-robot | Claude 開發、產品設計、問題解決 |

### 自我進修
- 呈現方式：分類手風琴，預設全部收合
- 標籤：線條框，hover 填滿 coral

| 分類 | Icon | 項目 |
|---|---|---|
| 行銷與社群 | ti-speakerphone | SEO 操作實務及應用趨勢、SEO 工具與連結策略、新聞稿實務班、LAP 廣告投手訓練營、會員管理與大數據行銷 |
| 數據與工具 | ti-chart-bar | GTM 操作實務班、Google Analytics、Google Skillshop |
| AI 應用 | ti-robot | Claude / AI 工具應用 |

### 成果分享（原「案例分享」）
- eyebrow：Case Studies；主標題：成果分享
- 卡片上方：16:9 封面圖，點擊燈箱顯示實際照片
- 封面圖規格：背景 `--color-placeholder`，置中白色圓形徽章（72px），徽章內繪 `--color-primary`（coral）色線稿 icon（單一主題用 1 個 icon，複合主題用 2 個並排小 icon）；右下角疊加圖片張數標籤（例如 `1 / 3`），尚無實際照片者標示「圖片待補」且不可點擊
- 卡片內文：標題（h3）→ 副標（灰色小字 `.gallery-role`，位於標題與內文之間，格式同「專案項目」區塊的 `.project-role`）→ 內文說明 → 標籤
- 無分類 Tab 篩選

| 專案 | 標籤 | 副標 | 封面圖主題 | 燈箱圖片 |
|---|---|---|---|---|
| MIT 微笑標章社群行銷 | 社群行銷、內容企劃 | — | 社群互動（笑臉 + 對話框） | MIT_社群貼文_社團體驗.png、MIT_社群貼文_廠商推廣.png、MIT_社群貼文_KOC合作.png |
| 實體活動企劃執行 | PM、社群行銷 | — | 活動企劃（地標 + 行事曆） | 實體活動企劃執行_大甲媽祖遶境.png、實體活動企劃執行_超級悠遊卡記者會.png、實體活動企劃執行_落成典禮.png、實體活動企劃執行_輪動台灣.png |
| T 客邦實體課程開發 | PM、內容企劃 | — | 課程開發（書本） | T客邦課程_社群推廣.png、T客邦課程_課程推廣.png |
| 跨部門大型活動協作 | PM | 活動內容企劃、現場執行 | 跨部門協作（連結節點） | 跨部門大型活動協作_科技金獎.png、跨部門大型活動協作_通訊大賽.png、跨部門大型活動協作_黑客松.png |
| 美編設計 | 美編設計 | 視覺設計 · 版面規劃 | 美編設計（調色盤 + 畫筆） | 待補（先以佔位圖顯示，實際截圖待補） |

### 工具開發
- 卡片上方：正方形佔位圖（1:1），點擊燈箱顯示截圖
- 卡片內文整體置中
- 條列說明：coral 色實心圓點（6px）+ 文字靠左對齊圓點，整組置中

| 工具 | 狀態 | 連結 | 燈箱圖片 |
|---|---|---|---|
| 🐾 寵物日記 | 已完成 | https://pet-care-diary-beryl.vercel.app/ | 寵物日記_1首頁.PNG、寵物日記_2指數.PNG、寵物日記_3飲食.PNG、寵物日記_4健康.PNG |
| 🗺️ 寵物地圖 | Coming Soon | — | — |
| 🌐 個人網頁 | Coming Soon | — | — |

### 工作經歷
- 呈現方式：時間軸，左側 coral 色線條，右側卡片
- 背景：`--color-dark` + 噪點紋理
- 卡片背景：`--color-dark-elevated`
- 時間軸下方數字亮點（計數器動畫）：100+ 堂工作坊、產量增加 10 倍、3 個產業跨域經驗

| 時間 | 公司 | 職稱 |
|---|---|---|
| 2022/04 – 2025/07 | 台灣星榜文化傳播有限公司（決策公關） | 專案企劃 |
| 2016/06 – 2020/08 | T 客邦（城邦集團） | 社群策展行銷 |
| 2014/03 – 2016/03 | 晨暉生物科技股份有限公司 | 製程副工程師 |

### 聯絡我
- 背景：全版 coral，文字全白
- 標題：打字機效果，輪流顯示三句話
- 按鈕：Email（深 coral）、LinkedIn（白色線框）
- Email：dannylin1013@gmail.com

---

## 六、待補項目

- [ ] 個人照片（關於我區塊右側）
- [ ] LinkedIn 網址
- [ ] 工具 Icon 圖片（工具開發區塊）
- [ ] 寵物日記 QR Code
- [ ] 長照點數計算工具（未來新增）
- [ ] 美編設計成果分享卡片（燈箱圖片待補，目前為佔位圖）

---

## 七、維護紀錄

| 日期 | 異動內容 |
|---|---|
| 2026/06/26 | 初版建立 |
| 2026/07/02 | 字體改為 LXGW WenKai TC 全站 |
| 2026/07/02 | 關於我照片改為右側等寬欄位水平置中 |
| 2026/07/02 | 新增待補項目：美編設計案例分享 |
| 2026/07/02 | 「案例分享」更名為「成果分享」；「作品 · 專案集」更名為「專案項目」；新增第五張卡片「美編設計」（燈箱圖片待補）；「跨部門大型活動協作」卡片新增副標；五張卡片封面圖改為線稿 icon 圓形徽章樣式 |

```
每次手動調整後，在這裡新增一筆紀錄，格式：
| YYYY/MM/DD | 調整了什麼 |
```
