# Lab-Hub

SigSpeechAI-NTNU 實驗室的研究方法教材，給碩博班研究生。它教的是**從拿到一個題目到投出一篇會議論文**這條路上每一步怎麼做：怎麼用 AI 建文獻地圖並核對、怎麼寫出自己的 idea、怎麼設計實驗、怎麼復現與記錄、怎麼在 group meeting 報進度與報論文。

教材是用來照著做的，不是用來讀過就算。每份都有步驟、要自己填的欄位（用 `〔〕` 標示）、產出長什麼樣、怎麼核對，以及「要先問教授的事」。

## 研究路徑

```mermaid
flowchart LR
  S0[0 入門 建地圖] --> S1[1 選路線 深挖]
  S1 --> S1b[1b 出題 idea card]
  S1b --> S2[2 實驗設計 先畫 Table 1]
  S2 --> S3[3 復現 baseline 錯誤分析]
  S3 -->|錯誤分析回頭改 card| S1b
  S3 --> S4[4 實驗執行與紀錄]
  S4 --> S6[6 寫作 投稿]
  S5[5 每週 group meeting 進度報告] -.-> S1b
  S5 -.-> S4
  P[論文報告 輪流] -.-> S1b
```

- 實線是主線，每站一份教材。
- 第 5 站「進度報告」每週都做，報的是第 2–4 站的進度加一張 card；論文報告在 partner 組內輪流，讀到的論文會回到 1b 變成新的 card。
- 第 3 站做完錯誤分析要回 1b 改 card——出題不是一次性的，最能投的 idea 通常來自復現時看到的失敗。
- 第 6 站的教材還沒寫。

## 教材清單（照路徑順序）

| 站 | 教材 | 什麼時候用 | 做完會有什麼 |
|---|---|---|---|
| 0 | [Deep Research 第一輪：建地圖](guides/deep_research/round1_map.md) | 教授給了一個題目或一段應用情境，你完全不熟，要在一個月內看懂全貌 | 核對過的地圖報告 `_r1_checked.md`、10 分鐘口頭報告骨架 |
| 1 | [Deep Research 第二輪：深挖路線](guides/deep_research/round2_dive.md) | 和教授討論、選定一條技術路線後，以投一篇會議論文為目標 | `_r2_*.md`、教授改過的研究提案 one-pager |
| 1b | [出題：idea card 與 idea log](guides/ideation/idea_card.md) | Round 2 之後第一次寫；之後每次進度報告帶一張新的或改過的 | idea card、累積的 idea log（退掉的也留） |
| 2 | [實驗設計：先畫 Table 1](guides/experiment_design/design_table1.md) | 教授挑定你的 card 之後、寫任何程式之前 | Table 1 空表、消融表、方法圖、一頁決策紀錄（教授審過才開始寫程式） |
| 3＋4 | [復現 baseline、錯誤分析、實驗紀錄](guides/experiment_log/reproduce_and_log.md) | Table 1 審過之後，一直到投稿 | GitHub repo、`results.csv`、實驗日誌、復現紀錄、錯誤分析 |
| 5 | [進度報告：group meeting 怎麼報](guides/progress_report/group_meeting.md) | 每週 | Quarto 投影片（含講稿）、GitHub Issue 上的教授回饋 |
| 貫穿 | [論文報告：把一篇論文變成投影片與講稿](guides/paper_reading/paper_to_slides.md) | 輪到你報論文時 | 13 頁 Quarto 投影片（含講稿）、一頁核對紀錄 |
| 6 | 從結果表到論文初稿 | — | （還沒寫） |
| 總表 | [要問教授的事](conventions/ask_professor.md) | 任何時候不確定「這該不該自己決定」 | 各站問題按時間排的一頁索引 |
| 慣例 | [審稿對帳](conventions/review_reconciliation.md) | 審稿意見回來的 48 小時內 | 一張「每條意見對回當初決策」的表；我容易漏的那一類 |

## 先讀哪份

- **剛進實驗室、教授剛給題目**：第 0 站。讀完跑完再看第 1 站，中間要和教授談一次。
- **已經有題目、要開始做實驗**：1b → 2 → 3＋4，照順序，不要跳。第 2 站的 Table 1 沒經教授審過不要寫程式。
- **這週要報進度**：第 5 站。它假設你已經在做第 2–4 站的事。
- **這週輪到報論文**：貫穿那份。

## 三件先講清楚的事

- **AI 產出的報告是地圖，不是文獻。** 你在報告、投影片、論文裡引用的每一篇，都必須是你自己開過、讀過的。每份教材都有「怎麼核對」一節，那一節不是選讀。
- **AI 產出要標明。** 和教授討論時，說清楚哪些是 AI 的產出、哪些是你核對過的、哪些是你自己的判斷。教授要的是你的判斷。
- **題目、資料、GPU、目標會議由教授決定。** 教材裡會告訴你哪些問題要帶去問；不要自己猜。

## 你會用到的工具

| 工具 | 用在哪 | 哪份教材教 |
|---|---|---|
| AI 的 Deep Research 功能 | 第 0、1 站建地圖與深挖 | 第 0、1 站 |
| GitHub（lab 的 org `SigSpeechAI-NTNU`） | 你的程式碼、實驗紀錄、每週報告的 Issue；從範本 [`student-template`](https://github.com/SigSpeechAI-NTNU/student-template) 建 repo | 第 3＋4、5 站 |
| Quarto | 進度與論文的投影片（qmd → html，含講稿） | 第 5 站、論文報告 |
| Markdown | 日誌、idea log、決策紀錄、核對紀錄——所有給自己看的紀錄 | 各站 |

## 這個 repo 怎麼維護

教材由教授與 AI 共同編寫，教授定稿。改動都記在各檔尾的「修改紀錄」。發現教材寫不清楚、或照著做卡住，直接跟教授說，那是教材要改的訊號。

repo 規範與待辦在 [`CLAUDE.md`](CLAUDE.md)。
