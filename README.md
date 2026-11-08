# 個人財務決策工具

房貸 PMT、投資 FV、退休 PV 的動態試算網站。純靜態、無建置步驟、無外部套件；所有運算都在瀏覽器內完成，不會上傳資料。

## 專案結構
```
├─ index.html          網站本體（HTML + CSS + JavaScript）
├─ _headers            安全與快取標頭
├─ wrangler.jsonc      Cloudflare 設定
├─ docs/               選用：GitHub Actions 自動部署範本
├─ .gitignore
└─ README.md
```

## 一、上傳到 GitHub
1. GitHub → New repository，名稱例如 `finance-planner`，建立空 repo（不要勾選 README）。
2. 在本資料夾執行：
```
git init
git add .
git commit -m "Initial commit"
git branch -M main
git remote add origin https://github.com/<你的帳號>/finance-planner.git
git push -u origin main
```
（或在 repo 頁面按 uploading an existing file，把所有檔案拖進去。）

## 二、在 Cloudflare 部署（連結 GitHub，自動更新）
1. Workers & Pages → Create → Pages → Connect to Git，選擇 `finance-planner`。
2. 設定：Production branch `main`；Framework preset `None`；Build command 留空；Build output directory 留空（或填 `/`）。
3. Save and Deploy，完成後網址為 `https://finance-planner.pages.dev`。之後每次 push 到 `main` 都會自動部署。

## 其他部署方式
- 拖放上傳：Pages → Upload assets，直接拖入本 zip 或解壓後的資料夾。
- 指令：`npx wrangler pages deploy . --project-name finance-planner`
- 本機預覽：直接用瀏覽器開啟 `index.html`，或 `npx wrangler pages dev .`

## 功能
- 16 個參數：滑桿與數字輸入同步，即時重算
- 輸出：每月房貸 PMT、負擔率、期末資產 FV、退休金需求 PV、達標缺口與所需月投資，附警示
- 7 張動態圖：PMT / FV / PV 敏感度（紅點為目前設定）、還款結構、資產負債走勢、FV 對 PV、龍捲風圖
- 動畫：自動掃描利率、年限、報酬率、每月投資；情境：保守 / 基準 / 樂觀

本工具僅供試算與教學，不構成理財建議。
