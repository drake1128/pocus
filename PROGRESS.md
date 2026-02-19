# POCUS 教案集 專案進度追蹤

**最後更新**: 2026-02-19
**網站網址**: https://drake1128.github.io/pocus/index.html
**GitHub Repo**: https://github.com/drake1128/pocus

---

## 🔧 Quarto 設定進度

### 已完成的 Quarto 設定
- [x] 專案類型：`book`
- [x] 輸出目錄：`_book`
- [x] HTML 格式：cosmo 主題
- [x] 章節結構：4 大部分 + 附錄
- [x] GitHub Actions 自動部署

### 目前 `_quarto.yml` 設定（精簡版）
```yaml
project:
  type: book
  output-dir: _book

book:
  title: "POCUS 超音波案例討論教案集"
  chapters:
    - index.qmd
    - chapters/00-overview.qmd
    - part: "第一部分：心血管急症"
      chapters: [...]
    # ... 其他章節

format:
  html:
    theme: cosmo
```

### 待恢復的 Quarto 功能
- [ ] 自訂 SCSS 樣式（`assets/css/custom.scss`）
- [ ] 中文語言設定（`lang: zh-TW`）
- [ ] 側邊欄設定（搜尋、折疊層級）
- [ ] 頁面導覽與分享功能
- [ ] 頁尾版權資訊
- [ ] PDF 格式輸出（需要 TinyTeX + CJK 字型）
- [ ] 交叉引用設定（圖、表前綴）

### GitHub Actions 部署設定
**檔案**: `.github/workflows/publish.yml`

```yaml
name: Quarto Publish
on:
  push:
    branches: [main]

permissions:
  contents: read
  pages: write
  id-token: write

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: quarto-dev/quarto-actions/setup@v2
      - run: quarto render --to html
      - uses: actions/upload-pages-artifact@v3
        with:
          path: _book

  deploy:
    needs: build
    runs-on: ubuntu-latest
    steps:
      - uses: actions/deploy-pages@v4
```

### 部署問題排除記錄

| 問題 | 原因 | 解決方案 |
|------|------|----------|
| gh-pages 分支未建立 | 使用舊版部署方式 | 改用 GitHub Actions Pages 部署 |
| Render 步驟失敗 | `downloads: [pdf]` 但未生成 PDF | 移除 PDF 下載設定 |
| Render 步驟失敗 | 自訂 SCSS 路徑問題 | 暫時改用預設 cosmo 主題 |
| Render 步驟失敗 | PDF 格式設定驗證錯誤 | 移除 PDF 格式區塊 |
| Render 步驟失敗 | R/webexercises 相依性 | 移除 R 安裝步驟（使用純 Markdown） |
| 網站顯示 README | 瀏覽器快取 | 使用 `/index.html` 完整路徑 |

### 恢復完整功能的步驟

當需要恢復完整功能時，按以下順序逐步加入：

1. **加入中文設定**
   ```yaml
   lang: zh-TW
   ```

2. **加入側邊欄設定**
   ```yaml
   book:
     sidebar:
       style: docked
       search: true
   ```

3. **加入自訂樣式**（確認 SCSS 語法正確）
   ```yaml
   format:
     html:
       theme: [cosmo, assets/css/custom.scss]
   ```

4. **加入 PDF 輸出**（需要在 workflow 加入 TinyTeX）
   ```yaml
   format:
     pdf:
       documentclass: book
       pdf-engine: xelatex
       CJKmainfont: "Noto Sans CJK TC"
   ```

---

## ✅ 已完成項目

### 基礎建設
- [x] 建立 Quarto Book 專案結構
- [x] 設定 GitHub Actions 自動部署
- [x] 網站成功上線 GitHub Pages
- [x] 9 個章節、36 堂課程架構完成
- [x] 導覽列與搜尋功能正常運作
- [x] 行動裝置響應式設計

### 內容完成度
- [x] 首頁 (`index.qmd`) - 完整
- [x] 課程總覽 (`chapters/00-overview.qmd`) - 完整
- [x] 教案 1：症狀辨識 (`01-symptoms.qmd`) - 完整範例，含案例與測驗

---

## 📝 待辦事項

### 高優先級 - 章節內容

#### 第一部分：心血管急症
| 教案 | 檔案 | 狀態 | 負責醫師 |
|------|------|------|----------|
| 1 | `01-chest-pain/01-symptoms.qmd` | ✅ 完成 | 曾新育 |
| 2 | `01-chest-pain/02-anatomy.qmd` | ⬜ 待填寫 | 曾新育 |
| 3 | `01-chest-pain/03-diagnosis.qmd` | ⬜ 待填寫 | 曾新育 |
| 4 | `01-chest-pain/04-treatment.qmd` | ⬜ 待填寫 | 曾新育 |
| 5 | `02-pulmonary-edema/05-symptoms.qmd` | ⬜ 待填寫 | 黃冠智 |
| 6 | `02-pulmonary-edema/06-anatomy.qmd` | ⬜ 待填寫 | 黃冠智 |
| 7 | `02-pulmonary-edema/07-diagnosis.qmd` | ⬜ 待填寫 | 黃冠智 |
| 8 | `02-pulmonary-edema/08-treatment.qmd` | ⬜ 待填寫 | 黃冠智 |

#### 第二部分：肢端血管與血栓疾病
| 教案 | 檔案 | 狀態 | 負責醫師 |
|------|------|------|----------|
| 9 | `03-limb-pain/09-symptoms.qmd` | ⬜ 待填寫 | 林姝含 |
| 10 | `03-limb-pain/10-anatomy.qmd` | ⬜ 待填寫 | 林姝含 |
| 11 | `03-limb-pain/11-diagnosis.qmd` | ⬜ 待填寫 | 林姝含 |
| 12 | `03-limb-pain/12-treatment.qmd` | ⬜ 待填寫 | 林姝含 |
| 21 | `06-pe-dvt/21-symptoms.qmd` | ⬜ 待填寫 | 謝慕揚、林彥良 |
| 22 | `06-pe-dvt/22-anatomy.qmd` | ⬜ 待填寫 | 謝慕揚、林彥良 |
| 23 | `06-pe-dvt/23-diagnosis.qmd` | ⬜ 待填寫 | 謝慕揚、林彥良 |
| 24 | `06-pe-dvt/24-treatment.qmd` | ⬜ 待填寫 | 謝慕揚、林彥良 |

#### 第三部分：休克與心跳停止
| 教案 | 檔案 | 狀態 | 負責醫師 |
|------|------|------|----------|
| 13 | `04-shock/13-recognition.qmd` | ⬜ 待填寫 | 陳麒心 |
| 14 | `04-shock/14-classification.qmd` | ⬜ 待填寫 | 陳麒心 |
| 15 | `04-shock/15-rush-protocol.qmd` | ⬜ 待填寫 | 陳麒心 |
| 16 | `04-shock/16-megacode.qmd` | ⬜ 待填寫 | 陳麒心 |
| 17 | `05-cardiac-arrest/17-acls.qmd` | ⬜ 待填寫 | 陳麒心 |
| 18 | `05-cardiac-arrest/18-differential.qmd` | ⬜ 待填寫 | 陳麒心 |
| 19 | `05-cardiac-arrest/19-e-als.qmd` | ⬜ 待填寫 | 陳麒心 |
| 20 | `05-cardiac-arrest/20-megacode.qmd` | ⬜ 待填寫 | 陳麒心 |

#### 第四部分：腹部與呼吸急症
| 教案 | 檔案 | 狀態 | 負責醫師 |
|------|------|------|----------|
| 25 | `07-abdominal-pain/25-gi.qmd` | ⬜ 待填寫 | 李宜家 |
| 26 | `07-abdominal-pain/26-renal-vascular.qmd` | ⬜ 待填寫 | 李宜家 |
| 27 | `07-abdominal-pain/27-female.qmd` | ⬜ 待填寫 | 李宜家 |
| 28 | `07-abdominal-pain/28-comprehensive.qmd` | ⬜ 待填寫 | 李宜家 |
| 29 | `08-dyspnea/29-symptoms.qmd` | ⬜ 待填寫 | 范程羿 |
| 30 | `08-dyspnea/30-anatomy.qmd` | ⬜ 待填寫 | 范程羿 |
| 31 | `08-dyspnea/31-diagnosis.qmd` | ⬜ 待填寫 | 范程羿 |
| 32 | `08-dyspnea/32-treatment.qmd` | ⬜ 待填寫 | 范程羿 |
| 33 | `09-pneumonia-arf/33-basics.qmd` | ⬜ 待填寫 | 多位醫師 |
| 34 | `09-pneumonia-arf/34-pathology.qmd` | ⬜ 待填寫 | 多位醫師 |
| 35 | `09-pneumonia-arf/35-basic-application.qmd` | ⬜ 待填寫 | 多位醫師 |
| 36 | `09-pneumonia-arf/36-advanced.qmd` | ⬜ 待填寫 | 多位醫師 |

#### 附錄
| 檔案 | 狀態 |
|------|------|
| `appendices/a-machine-operation.qmd` | ⬜ 待填寫 |
| `appendices/b-abbreviations.qmd` | ⬜ 待填寫 |
| `appendices/c-references.qmd` | ⬜ 待填寫 |

---

### 中優先級 - 圖片與多媒體

#### 圖片需求
- [ ] 建立 `images/` 資料夾結構
  - [ ] `images/common/` - 共用圖片（心臟解剖、探頭等）
  - [ ] `images/lesson01/` ~ `images/lesson36/` - 各課程專用圖片
- [ ] 從現有 PDF 教案提取圖片（使用 `scripts/extract_pdf_images.py`）
- [ ] 超音波影像截圖
- [ ] 解剖示意圖
- [ ] 流程圖（可使用 Mermaid 語法）

#### 影片資源
- [ ] 收集/製作超音波示範影片
- [ ] 上傳至 YouTube
- [ ] 在課程中嵌入影片連結

---

### 低優先級 - 功能增強

#### 樣式改進
- [ ] 恢復自訂 SCSS 樣式（`assets/css/custom.scss`）
- [ ] 調整 POCUS 品牌色系
- [ ] 優化表格樣式
- [ ] 改進行動版閱讀體驗

#### PDF 輸出
- [ ] 設定 PDF 格式（需要 TinyTeX + CJK 字型）
- [ ] 測試中文 PDF 輸出
- [ ] 加入 QR Code 連結影片

#### 互動功能
- [ ] 評估是否需要 webexercises R 套件
- [ ] 加入更多自我評估題目
- [ ] 考慮加入進度追蹤功能

---

## 📁 專案結構

```
pocus-guide/
├── _quarto.yml              # 主要設定檔
├── index.qmd                # 首頁
├── PROGRESS.md              # 本進度追蹤檔案
├── README.md                # 專案說明
│
├── chapters/                # 課程內容
│   ├── 00-overview.qmd
│   ├── 01-chest-pain/
│   ├── 02-pulmonary-edema/
│   ├── 03-limb-pain/
│   ├── 04-shock/
│   ├── 05-cardiac-arrest/
│   ├── 06-pe-dvt/
│   ├── 07-abdominal-pain/
│   ├── 08-dyspnea/
│   └── 09-pneumonia-arf/
│
├── appendices/              # 附錄
├── images/                  # 圖片資源（待建立）
├── assets/css/              # 樣式檔案
├── latex/                   # PDF 輸出設定
└── .github/workflows/       # 自動部署設定
```

---

## 🔧 開發指令

```bash
# 本地預覽
quarto preview

# 建置網站
quarto render --to html

# 推送更新（自動部署）
git add .
git commit -m "更新內容"
git push
```

---

## 📋 內容撰寫範本

每個教案建議包含：

```markdown
---
title: "教案 X：標題"
author: "醫師姓名"
---

## 課程目標
::: {.callout-note}
## 學習目標
1. 目標一
2. 目標二
:::

## 案例介紹
::: {.panel-tabset}
### 案例一
案例內容...

### 案例二
案例內容...
:::

## 重點提示
::: {.callout-warning}
## 重點
重要內容...
:::

## 超音波示範
（影片或圖片）

## 自我評估
::: {.content-visible when-format="html"}
**問題**：選項
- [ ] 錯誤選項
- [x] 正確答案
- [ ] 錯誤選項
:::

## 參考資料
1. 參考文獻...
```

---

## 📅 里程碑

| 階段 | 目標 | 狀態 |
|------|------|------|
| Phase 1 | 網站架構與部署 | ✅ 完成 |
| Phase 2 | 第一章完整內容 | 🔄 進行中 |
| Phase 3 | 所有章節基本內容 | ⬜ 待開始 |
| Phase 4 | 圖片與影片整合 | ⬜ 待開始 |
| Phase 5 | PDF 輸出與最終校對 | ⬜ 待開始 |

---

## 📝 更新日誌

### 2026-02-19
- ✅ 初始專案建立
- ✅ GitHub Actions 部署成功
- ✅ 網站上線：https://drake1128.github.io/pocus/
- ✅ 36 堂課程架構完成
- ✅ 教案 1 完整範例

---

*此檔案用於追蹤 POCUS 教案集專案進度，請定期更新。*
