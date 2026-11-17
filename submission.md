**標題：** 宜蘭大學 B1243023 資工系四年級 楊立安 提示工程（Prompt Engineering）

# 1. LLM Wiki 主題與簡短介紹
主題：**提示工程**。Wiki 以 5 篇 arXiv 論文為來源（Brown 2020、Wei 2022、Kojima 2022、Yao 2022、Schulhoff 2024），整理出 5 個概念頁：提示工程、少樣本提示、思維鏈、零樣本思維鏈、ReAct。建立方式為先確定主題與讀者，再逐篇查證、寫入，最後才生成簡報；每條內容都標註來源。

# 2. LLM Wiki 連結或成果
- 連結：【GitHub 連結待填】（資料夾 `prompt-wiki/`）
- 成果結構：`index.md`、`log.md`、`sources/` 5 篇、`concepts/` 5 頁

| 來源 | 連結 |
|---|---|
| Brown et al. 2020, Language Models are Few-Shot Learners | https://arxiv.org/abs/2005.14165 |
| Wei et al. 2022, Chain-of-Thought Prompting | https://arxiv.org/abs/2201.11903 |
| Kojima et al. 2022, LLMs are Zero-Shot Reasoners | https://arxiv.org/abs/2205.11916 |
| Yao et al. 2022, ReAct | https://arxiv.org/abs/2210.03629 |
| Schulhoff et al. 2024, The Prompt Report | https://arxiv.org/abs/2406.06608 |

# 3. 教學 HTML 簡報連結
https://claude.ai/artifact/3uEdgk7QzDwncV5g2kE7bQ
（如老師要求 GitHub Pages，請改貼 Pages 網址）

# 4. loop / graph 流程說明
```
[A 討論主題與讀者] → [B 搜尋來源] → [C 驗證來源] → [D 寫入 Wiki]
                          ↑ 失敗         │通過            │
                          └──────────────┘                ↓
      [H 輸出 HTML] ← [G 對照 Wiki 檢查] ← [F 生成簡報] ← [E 查詢 Wiki 整理重點]
                          │不通過
                          └──────────→ 回到 E 或 F
```
- 重複執行：B→C→D 每篇來源跑一次（5 次）；G 不通過時重跑 F。
- 檢查／重生成：C 確認論文頁面真的檢索到；G 確認簡報每個引用、連結、數字都能對應到 Wiki。
- 設計原因：避免模型寫出沒有依據的內容，驗證放在進入 Wiki 前，對照放在輸出前。

# 5. 一次實際執行的結果與檢查紀錄
執行結果：5 篇來源全部 ingest；簡報 5 個段落皆有引用。檢查紀錄（腳本實際執行輸出）：

```
[檢查1] ingest 來源數 = 5（要求 ≥5）→ 通過
[檢查2] 5 篇 source 頁皆有 arXiv 連結與查證紀錄 → 通過
[檢查3] 5 個 concept 頁共 11 條 claim，缺來源 0 條 → 通過
[檢查4] HTML 引用編號 1–5 皆有對應來源 → 通過
[檢查5] HTML 的 5 個連結皆出現在 Wiki → 通過
[檢查6] HTML 中的「58 種技術」在 Wiki → 是
```
過程中發現的問題：搜尋結果混入二手整理站，其數字未在論文頁面找到，已排除；建檔時資料夾名稱未展開導致檔案沒寫入，重跑後修正。

# 6. 反思
- **最常出錯的節點：** B/C（搜尋與驗證）。二手網站的數字看起來可信，但不一定出自論文本身。
- **如何調整檢查流程：** 把來源驗證從「生成簡報之後」前移到「寫入 Wiki 之前」（新增 C 關卡），並在 `index.md` 規定二手站只當線索。原因是錯誤一旦進入 Wiki，後面每一步都會放大它。
- **是否修改 graph：** 有，新增 C 關卡與 G→F 的回圈。
