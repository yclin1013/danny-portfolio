# Danny Lin Portfolio

林鈺奇（Danny Lin）的個人作品集網站——內容企劃・專案管理・社群行銷。

## 線上連結

🔗 [yclin1013.github.io/danny-portfolio](https://yclin1013.github.io/danny-portfolio)

## 技術棧

純 HTML/CSS/JS，無框架、無建置流程，單一檔案 `index.html`（HTML／CSS／JS all-in-one）。

## 專案結構

```
danny-portfolio/
├── index.html          # 網站主體（唯一的程式碼檔案）
├── DESIGN.md            # 設計規格文件（色彩、字體、各區塊規格、待補清單、維護紀錄）
├── CLAUDE.md             # Claude Code 自動載入的專案規則（修改前必讀）
├── README.md             # 本檔案
├── images/               # 案例封面（SVG）、燈箱照片、個人照片、工具截圖
└── YCLin_履歷表.pdf      # 履歷 PDF，供網站下載按鈕連結
```

## 相關文件

- [`DESIGN.md`](./DESIGN.md) — 設計系統規範（色彩、字體、各區塊規格、維護紀錄）
- [`CLAUDE.md`](./CLAUDE.md) — Claude Code 自動載入的專案規則

## 維護/部署方式

- **修改前務必先讀 `DESIGN.md`**——裡面記錄了完整的設計系統（配色規則、各區塊規格、❌ 禁止事項）與維護紀錄。所有異動都應符合其中規格，並在修改後於「七、維護紀錄」新增一筆紀錄。
- 新增圖片統一放 `images/`，命名規則為「案例名稱_描述」，副檔名一律小寫。
- 案例封面固定使用 SVG 插畫（`cover_case0N_*.svg`），不用實際照片（比例不一會破版）。
- 不需要建置指令。任何對 `index.html` 或 `images/` 的異動，`git push` 到 `main` 後 GitHub Pages 會自動重新部署。
