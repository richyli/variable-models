# 變數與理論模型工具

以 [Variable.base](../Variable.base) 的篩選條件（tags 含 `variable`）為基礎，把 `-work/Notes/` 裡的變數 note、理論 note 與它們之間的邊整理成一個離線互動頁。

- 開啟：直接用瀏覽器開 `index.html`（不必伺服器；資料已嵌在頁面裡）
- 重建：`python tools/variable_model_tool.py`（加 `--report` 會印出沒對到 note 的名稱、沒掛理論的變數）
- 設定：`variable_aliases.yml`（同義變數、類似變數、理論標籤對應、補充的標準模型）

## 頁面怎麼用

1. 上方搜尋框打字（英文名、別名都找得到）或從左側清單點一個變數。
2. 右側「理論模型」列出這個變數出現的每個模型，各一張概念圖；黃色節點＝目前變數，橘色＝類似變數。
3. 圖上任何節點都可以點，點了就跳到那個變數；瀏覽器上一頁可以回來。
4. 「使用類似變數的模型」列出沒有這個變數、但有它類似變數的模型。
5. `↗` 連結用 `obsidian://` 開對應 note（vault 名稱在 yml 的 `vault:`）。
6. 每張模型卡依圖的寬度自動佔 1–4 欄；「⤢ 整列」可強制放大；頂列「☰ 清單」收合左側清單；按 `/` 跳到搜尋框；點標題回到全部模型。

版面審查紀錄在 `UX_REVIEW.md`。

## note 要怎麼寫才會被抓到

| 想表達 | 寫法（任一） |
|---|---|
| 這是變數 | frontmatter `tags: [variable]` 或內文 `#variable` |
| 這個變數屬於哪個理論 | `#T_TAM` 這類標籤，或連結 `[[T TPB  Planned Behaviroal]]`；標籤與理論 note 的對應在 yml 的 `theory_tags` |
| A 影響 B | `A --> [[B]]`、`[[A]] -> [[B]]`、`[[A]] ++ [[B]]`（正向）、`[[A]] -- [[B]]`（負向，兩邊都要是連結） |
| C 調節 A→B | `[[C]] ++ [[A]] to [[B]]`，或關係 note 裡寫 `Moderated by [[C]]` |
| 名稱不同但同一個變數 | frontmatter `aliases:`、連結顯示名 `[[Behavior\|Use]]`，或 yml 的 `same` |
| 意思相近但不合併 | 內文 `Similar to [[X]]`，或 yml 的 `similar` |

邊會掛在它上面最近一個理論標籤／理論連結的脈絡下；遇到標題行（`#`、`##`）脈絡就重設。理論 note（檔名 `T ` 開頭或 tags 含 `Theory`）本身也會被掃描。

## 兩種來源的邊

- 實線：note 裡寫的邊（滑鼠停在線上會顯示出處 note）
- 虛線：`seed_models` 補的教科書標準結構，只是為了讓只貼了圖的理論也有概念圖；不代表 note 裡寫過

要關掉補充結構，把 yml 裡對應理論的 `seed_models` 條目刪掉即可。
