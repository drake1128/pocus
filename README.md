# POCUS 超音波案例討論教案集

Point-of-Care Ultrasound Case Discussion Curriculum

## 簡介

本專案使用 [Quarto](https://quarto.org) 建置 POCUS 教學網站與 PDF 教科書。

## 專案結構

```
pocus-guide/
├── _quarto.yml          # 主要設定檔
├── index.qmd            # 首頁
├── chapters/            # 9 個章節，36 堂課程
├── appendices/          # 附錄
├── images/              # 圖片資源
├── assets/              # CSS 樣式
└── .github/workflows/   # GitHub Actions 自動部署
```

## 本地開發

### 安裝需求

1. 安裝 [Quarto](https://quarto.org/docs/get-started/)
2. 安裝 [R](https://cran.r-project.org/) (用於互動測驗)
3. 安裝 R 套件：
   ```r
   install.packages(c("webexercises", "knitr", "rmarkdown"))
   ```
4. 安裝 TinyTeX (用於 PDF 輸出)：
   ```bash
   quarto install tinytex
   ```

### 預覽網站

```bash
quarto preview
```

### 建置所有輸出

```bash
quarto render
```

### 僅建置特定格式

```bash
quarto render --to html   # 僅網站
quarto render --to pdf    # 僅 PDF
```

## 部署到 GitHub Pages

### 首次設定

1. 在 GitHub 建立新的 repository
2. 將本專案推送至 repository
3. 在 Settings > Pages 設定：
   - Source: Deploy from a branch
   - Branch: gh-pages

### 自動部署

推送到 `main` 分支後，GitHub Actions 會自動建置並部署。

### 手動發布

```bash
quarto publish gh-pages
```

## 內容編輯

### 新增課程內容

1. 編輯對應的 `.qmd` 檔案
2. 使用 Markdown 語法撰寫內容
3. 使用 Quarto callout 語法：
   ```markdown
   ::: {.callout-note}
   ## 學習目標
   內容...
   :::
   ```

### 新增圖片

1. 將圖片放入 `images/` 資料夾
2. 在 `.qmd` 中引用：
   ```markdown
   ![說明文字](images/filename.png)
   ```

### 新增測驗題目

```markdown
::: {.content-visible when-format="html"}
**問題**：選項

- [ ] 錯誤選項
- [x] 正確選項
- [ ] 錯誤選項
:::
```

## 授權

本教材由 POCUS 教學團隊編製。

## 聯絡資訊

如有問題或建議，請透過 GitHub Issues 聯繫。
