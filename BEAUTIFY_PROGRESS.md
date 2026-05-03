# 📋 POCUS 教案美化專案進度表

> **目的**：記錄「**讀書會共筆風格教案改寫專案**」的進度與規範，
> 方便未來任何時間點接手都能無縫銜接。
>
> **專案啟動**：2026-05-03
> **最後更新**：2026-05-03（Module 07-09 完成 — **🎉 9/9 全部完成**）

---

## 🎯 專案目標

把 POCUS 教案集 9 個模組共 36 堂教案，
從「平鋪 markdown」升級為「**讀書會共筆風 + 套色 callout + 結構化表格**」的美化版本。

每堂課的最終版本應包含：
1. 📌 **本課速覽**（minimal callout，1 段話講完核心）
2. 🎯 **課程目標**（callout-note）
3. 📋 **案例介紹**（panel-tabset + callout-tip 案例 + vital sign 解讀欄）
4. ⚖️ **鑑別診斷 / 解剖 / 病理 / 治療**（依教案性質）
5. 🪤 **常見陷阱 / 易錯點**（callout-caution）
6. 💬 **討論議題**
7. ✅ **自我評估**（4 題 + collapsed 答案解析）
8. 🎓 **回家三句話**（callout-important，呼應讀書會共筆 take-home）
9. 📚 **參考閱讀**（每篇 Vancouver 格式 + 完整作者 + PMID 可選）

---

## ✅ 已完成模組（9 / 9 — 🎉 100%）

| 模組 | 主題 | 教案 | 編修醫師 | Commit | 狀態 |
|:----:|------|:----:|----------|:------:|:----:|
| **01** | 急性胸痛 | 1-4 | 曾新育 | `f5efdcf` | ✅ 完成 |
| **02** | 急性肺水腫 | 5-8 | **洪國軒** ⚠️ | `1e50501` | ✅ 完成 + 改名 |
| **03** | 急性肢端疼痛 | 9-12 | **蕭喻中** ⚠️ | `284b396` | ✅ 完成 + 改名 |
| **04** | 休克 | 13-16 | 陳麒心 | `120f624` | ✅ 完成 |
| **05** | 心跳停止 | 17-20 | 陳麒心 | `2f37199` | ✅ 完成 |
| **06** | PE & DVT | 21-24 | 謝慕揚、林彥良 | `4fcc996` | ✅ 完成 |
| **07** | 急性腹痛 | 25-28 | 李宜家 | `a51d923` | ✅ 完成 |
| **08** | 呼吸喘 | 29-32 | 范程羿 | `89d93e7` | ✅ 完成 |
| **09** | 肺炎與 ARF | 33-36 | 多位醫師 | _本次 commit_ | ✅ 完成 |

⚠️ = 此模組進行了**作者改名**（原作者退出計畫）

---

## 🎊 待完成模組

**全部完成！** 無待辦模組。

未來工作：
- 手繪插圖第二階段 18 張中尚有 2 張未完成（見 PROGRESS.md / memory）
- Marp slides 與 lesson qmd 同步更新
- 偶爾回頭微調套色、修正 typo

---

## 🛠 美化工作流程（SOP）

接手任何新模組時，依下列步驟操作：

### 1️⃣ 環境確認

```powershell
# 檢查當前模組原作者
Grep -pattern "^author:" -path pocus-guide/chapters/0X-name/

# 檢查現有檔案數量（應為 1 個 index + 4 個 lessons）
Glob "pocus-guide/chapters/0X-name/*.qmd"
```

### 2️⃣ 處理作者更換（若需要）

若原作者已退出（見 memory contributor list），需在 **6 個位置**同步更新：

1. `chapters/0X-name/index.qmd` 編修醫師
2. `chapters/0X-name/0Y-*.qmd` × 4 的 `author: "..."` YAML
3. `index.qmd` 根目錄編輯團隊
4. `chapters/00-overview.qmd` 編修醫師表（4 列）
5. `slides/module-0X-name.md` 第一張投影片
6. `PROGRESS.md` 進度表（4 列）

### 3️⃣ 讀取現有 5 個檔案

```
chapters/0X-name/index.qmd
chapters/0X-name/0Y-symptoms.qmd
chapters/0X-name/0Z-anatomy.qmd
chapters/0X-name/0W-diagnosis.qmd
chapters/0X-name/0V-treatment.qmd
```

### 4️⃣ 改寫 5 個檔案

依 [本檔最上方的「9 大結構」](#專案目標) 重寫，保留：
- 原檔案的章節骨架（學習目標、案例、討論題、自我評估等）
- 原案例的核心臨床事實（vital signs、診斷、處置）

新增：
- emoji 標題前綴（🎯 📋 🚨 💊 🔍 ✅ 🎓 📚 等）
- 套色 callout（note / warning / tip / caution / important）
- vital sign **解讀欄**（如 `🚨 低血氧`）
- 至少 1 個「**🪤 常見陷阱**」callout-caution
- 結尾「**🎓 回家三句話**」callout-important

### 5️⃣ Commit 規範

```bash
git add 9_or_so_files
git commit -m "Rewrite module 0X <topic> lessons[; transfer authorship to <new>醫師]

[bullet list of major rewrites per file]

[if name change:]
Authorship change: <old>醫師 has withdrawn from the project; replaced
with <new>醫師 across N files (...).

Co-Authored-By: Claude Opus 4.7 (1M context) <noreply@anthropic.com>"
git push
```

### 6️⃣ 更新本檔

完成一個模組後，更新本檔：
- 把該模組從「⏳ 待完成」移到「✅ 已完成」
- 填入 commit hash
- 更新「最後更新」日期

---

## 🎨 套色配置（quick reference）

定義在 `assets/css/custom.scss`：

| 顏色 | Hex | 用途 | callout class |
|:----:|:----:|------|---------------|
| 🔵 Blue | `#006699` | 學習目標、討論議題、概念 | `.callout-note` |
| 🔴 Red | `#cc3333` | 致命診斷、緊急處置、警示 | `.callout-warning` |
| 🟢 Green | `#2e8b57` | 案例、答案解析 | `.callout-tip` |
| 🟠 Orange | `#e67e22` | 鑑別陷阱、易錯點 | `.callout-caution` |
| 🟡 Gold | `#d4a017` | 重點回顧、回家三句話、本章總結 | `.callout-important` |
| 🟣 Purple | `#6f42c1` | h4 標題、quiz 框 | （SCSS 直接定義） |
| 🔷 Teal | `#17a2b8` | 影像、切面 | `$info` |

---

## 👥 編修醫師（Active List as of 2026-05-03）

| Module | 主題 | Active 醫師 | 已退出（不可署名） |
|:------:|------|------------|--------------------|
| 01 | 急性胸痛 | 曾新育 | — |
| 02 | 急性肺水腫 | **洪國軒** | ~~黃冠智~~ |
| 03 | 急性肢端疼痛 | **蕭喻中** | ~~林姝含~~（已離職） |
| 04 | 休克 | **陳麒心** | — |
| 05 | 心跳停止 | **陳麒心** | — |
| 06 | PE & DVT | 謝慕揚、林彥良 | — |
| 07 | 急性腹痛 | 李宜家 | — |
| 08 | 呼吸喘 | 范程羿 | — |
| 09 | 肺炎與 ARF | 多位醫師 | — |

⚠️ **重要原則**：已退出醫師不可繼續署名（侵權嫌疑）。
新章節署名前，必須詢問用戶確認 active 醫師清單。

---

## 🔮 下一步建議（給未來的我）

1. **每週 1 個模組** — 維持步調、避免過度疲勞
2. **接手前先確認 active 醫師** — 不要直接複製舊作者名
3. **手繪圖整合** — 第二階段 12 張插圖（lesson 層 supplementary）
   仍未全部整合到 lesson qmd，可在改寫時順便加入
4. **檢視 SCSS** — 偶爾回頭看 custom.scss 是否需要新增 utility class
5. **PROGRESS.md 不是這份文件** — 不要混淆：
   - `PROGRESS.md` = 整本書的章節進度（已存在）
   - `BEAUTIFY_PROGRESS.md`（本檔）= 美化專案的進度與 SOP

---

## 📞 接手時的快速 checklist

- [ ] 讀本檔 → 知道目前進度與 SOP
- [ ] 讀 `~/.claude/projects/.../memory/MEMORY.md` → 確認最新醫師名單
- [ ] 讀 `assets/css/custom.scss` → 確認套色仍有效
- [ ] 確認 `quarto preview` 在本地能跑
- [ ] 選擇下一個模組（從「⏳ 待完成」表挑）
- [ ] 跑一次 `git pull origin main` → 確保是最新版
- [ ] 開工！
