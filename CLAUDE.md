# CLAUDE.md — ~/Lab-Hub repo 規範（2026-10-02 建立）

> 每次對話起手都會讀本檔。本 repo 對應 GitHub `SigSpeechAI-NTNU/Lab-Hub`，**學生看得到**。
> 給人讀的入口在 `README.md`；Project 指令備份在 `project-instructions/`。本檔保持短。

## 一、目的與讀者

教指導的碩博生怎麼做研究：入門題目、用 Deep Research 建地圖、讀論文、做論文閱讀投影片、記錄實驗、報告進度。讀者是研究生；教授決定教什麼，AI 寫成學生能照著做的版本。

## 二、與其他 Hub 的關係

| Hub | 本 Project 對它 | 從它取什麼 |
|---|---|---|
| Research-Hub | 只讀 `docs/` | 研究方法的做法（改寫成學生版）。其他資料夾含未發表內容，使用者點名某檔時才讀 |
| Paper-Hub | 只讀 `writer/` | 論文閱讀與寫作的規範（改寫成學生版）。`papers/`（審查中的稿件）與 `reviewing/`（替期刊審的稿，保密）不讀 |
| Coach-Hub、Course-Hub 與其他未列出的 Hub | **不讀** | —（含個資、教師端內容，或與教材無關；Course-Hub 自 2026-10-03 起不讀） |

一份檔案只有一個 Project 會改它：本 repo 的檔案只有 Lab-Hub 改；其他 Hub 的檔案本 Project 不碰。取材一律改寫，不整段搬。
開對話時只勾選需要的資料夾（可直接勾子資料夾，例如 `~/Paper-Hub/writer`）。本 repo 是公開的，**跨 Hub 的待辦不寫進本 repo**，在對話中告訴使用者。（2026-10-03）

## 三、結構

```
~/Lab-Hub/
  README.md                       學生入口：有哪些教材、先讀哪份
  CLAUDE.md                       本檔
  project-instructions/           Project 指令備份與版本表
  guides/
    deep_research/                兩輪 Deep Research 指令模板（round1_map.md、round2_dive.md）
    ideation/                     出題：idea card 與 idea log（idea_card.md）
    experiment_design/            實驗設計：先畫 Table 1（design_table1.md）
    experiment_log/               復現 baseline、錯誤分析、實驗紀錄（reproduce_and_log.md）
    progress_report/              進度報告：group meeting 怎麼報（group_meeting.md）
    paper_reading/                論文報告：把一篇論文變成投影片與講稿（paper_to_slides.md）
    <主題>/                       之後的教材各自一個資料夾
  conventions/                    實驗室慣例：ask_professor.md（要問教授的事總表）、review_reconciliation.md（審稿對帳）
  student-template/               學生 repo 範本（巢狀獨立 repo，.gitignore 排除）
```

## 四、公開 repo 的界線

不放：學生個資、未發表的實驗結果、授權語料的內容或路徑、其他 Hub 的內部規範、金鑰。

## 五、研究路徑與教材待辦（2026-10-03 定稿；每做完一站勾掉）

學生從拿到題目到投出論文的路徑。站次已和使用者討論定案，教材逐站補。

| 站 | 學生在做什麼 | 產出 | 教材 | 狀態 |
|---|---|---|---|---|
| 0 入門 | 跑 Round 1、核對、親讀 5 篇 | `_r1_checked.md`、10 分鐘報告 | `guides/deep_research/round1_map.md` | ✅ |
| 1 選路線 | 帶 §9 問教授 → Round 2 → one-pager | `_r2_*.md`、教授改過的 one-pager | `guides/deep_research/round2_dive.md` | ✅ v4.1，5 點已補（2026-10-08） |
| 1b 出題 | 寫 idea card，教授挑；之後每次進度報告帶一張新的或改過的 | idea card、idea log | `guides/ideation/idea_card.md` | ✅ v1，使用者已審（2026-10-08） |
| 2 實驗設計 | 畫 Table 1、消融表、method figure、定 baseline 與資料、pilot | 三張表圖＋一頁決策紀錄，group meeting 審，檔尾留審核紀錄 | `guides/experiment_design/design_table1.md` | ✅ v1.1，使用者已審（2026-10-08） |
| 3 復現＋錯誤分析 | 復現 baseline 到對上數字；看它在哪類輸入上失敗 → 回 1b 改 card | `reproduce.md`、`error_analysis.csv` | `guides/experiment_log/reproduce_and_log.md`（與 4 合寫） | ✅ v1.1，使用者已審（2026-10-08） |
| 4 執行與紀錄 | 填 Table 1；實驗日誌、config、版本管理 | repo、`results.csv`、`notes/log.md` | 同上 | ✅ 同上 |
| 5 進度報告 | group meeting：先報進度與自己的 card，教授後講 | Quarto 投影片＋GitHub Issue | `guides/progress_report/group_meeting.md` | ✅ v1.2，使用者已審（2026-10-08） |
| 6 寫作 | 把 Table 1 變成初稿 | 初稿 | 從 Paper-Hub 取材改寫學生版；commit 前使用者親審 | ⏸ 保留，使用者約 2026-12 再談 |
| 貫穿 | 讀論文、做論文報告投影片 | 論文卡＋Quarto 投影片 | `guides/paper_reading/paper_to_slides.md` | ✅ v2.1，使用者已審（2026-10-08） |

橫向文件：AI 使用規範不做；要問教授的事總表 ✅ `conventions/ask_professor.md`（各站教材改「要問教授」時同步）；檔案與命名慣例不另寫，在範本 repo 的 README（2026-10-08）。命名：週報 `progress_YYMMDD`、Issue `YYMMDD 進度`；論文報告 `〔會議〕_〔年份〕_〔第一作者的姓〕` 全小寫。

2026-10-08：0–5 站與論文報告全部定稿並經使用者審過；剩第 6 站（約 12 月）。下一階段是**實際用**：第一個學生走完一輪後，把卡住的地方回填各教材。

### 已定的設計決策（寫教材時遵守）
- 1b：學生先講、教授後講；教授給的 idea 由學生寫成 card（含「我為什麼沒看到」一格）；idea log 連退掉的一起留並註明原因；考核寫 card 的動作不考核好壞；AI 可發散但 card 上的痛點要附學生自己的證據；退回代碼七種 BIG／DONE／DATA／DULL／VAGUE／GPU／LATER
- 2：預設長論文（4 頁照長論文修剪）；產出含 method figure；顯著性列為考量但一句話交代不走火入魔；工具鏈與資料集寫具體名稱、授權不設關卡；研究倫理只寫原則（方案 A）；示例 contextual biasing STT、baseline 以方法類型標示。Table 1 先畫再寫程式；baseline 四層（必備／最強公開／消融／簡單）3–5 個；貢獻點只動一格；資料三層（標準公開／公開自組／自建），主實驗至少一個標準公開資料集，自建不得是唯一評測集；截稿日不到 4 個月不開新蒐集
- 3＋4：學生 repo 在 `SigSpeechAI-NTNU` 底下、private、命名 `〔名字〕_〔題目簡稱〕`；不強制追蹤工具，必備 config 進 git＋`results.csv`＋日誌；復現判準相對 ±5%／±10%，各指標暫同一套；卡住 3 個工作天先找 partner 再問教授、復現 3 週找教授；錯誤分析 100 個樣本親耳聽、學生先擬 5–8 類；GPU 是學校機器，共用規矩教材不寫
- Repo：一切跟著題目走（讀法 1，2026-10-08）——一題一 repo，論文筆記、idea log、週報都在裡面，不開個人 notes repo；題目結束封存，idea log 與 papers 複製到新 repo；repo 可改名。程式與筆記同一 repo（方案 A），toolkit fork 或釋出時再拆
- 實驗室慣例：partner 制——相關議題 2–3 人一組，各有主責題目，彼此知道對方的題目；分組由使用者定，學生都已知道，不另寫文件。GPU 共用規矩不訂（2026-10-08）
- 2 的但書：seed 數與顯著性依目標會議、資料量、算力和教授討論後定（語音會議通常不要求 multi-seed）
- 5：group meeting 每週一次、partner 一定出席；進度報告每人每週都報（每人 30 分鐘），論文報告在 partner 組內輪流（一篇 20 分鐘）；順序：先全部人的進度，再論文；學生先報 card、教授後講。學生自己的紀錄用 Markdown（第 4 站）；對教授用固定格式投影片，由學生請 AI 以 Quarto（qmd → html）製作、附演講稿；進度投影片固定 8 頁：問題定義示意圖、idea／架構示意圖（每週沿用）、對帳、Table 1 現況、關鍵結果、卡住、card、下週與要問（2026-10-08 定稿）；30 分鐘含討論，報告 10 分鐘以內。書面不用提前交。教授回饋用 GitHub Issue 留痕（不用 Notion／Teams 做紀錄）：學生當場記，教授也可自己留言或開 Issue；partner 不另外報告
- 語言：進度投影片可中文；論文報告投影片本體一律英文、講稿中文（2026-10-08）
- 論文報告：固定 13 頁（一句話／背景／痛點／架構／訓練／推論／走線／物理意義／設定與公平性／主結果／消融與賣點圖／我的判斷／啟發）、方法 8 分鐘、走線必講；架構圖可截圖但必加標註，沒有就自己畫或請 AI 畫；流程為 PDF 餵 AI 生草稿 → 學生帶著草稿讀論文逐頁核對 → 和 AI 對話修正；走線、我的判斷、啟發三頁 AI 不生、學生自己寫；講稿格式【講述】＋【提示】、YAML 1280×800 與講稿數學 MathML 腳本（機制取自 Course-Hub，改寫）
- 6：選 B（改寫學生版放 Lab-Hub），Paper-Hub 不公開

### 學生 repo 範本（2026-10-08）
住在 `~/Lab-Hub/student-template/`，但是**巢狀的獨立 repo**（自己的 `.git`，push 到 `SigSpeechAI-NTNU/student-template`，private、設為 template），Lab-Hub 的 `.gitignore` 排除它。改它的檔案後，git 指令要 `cd ~/Lab-Hub/student-template` 分開做。內容是學生研究 repo 的骨架（README、.gitignore、design 模板、results.csv 表頭、日誌／復現／idea log／論文核對模板、進度 8 頁與論文 13 頁的 qmd、Issue 模板）。使用者會把它搬成獨立 repo `SigSpeechAI-NTNU/student-template` 並設為 template；搬走後本資料夾刪除，README 的工具表改連到那個 repo。範本內容與教材的模板要同步：改教材模板時一起改範本。

### 2026-10-08 邏輯修正（已做）
- 七份教材各加一節「審稿人會怎麼看這一站的產出」（README 的宣稱因此成立）；之後新教材也要有這一節
- README 整份重寫（含時程表、四件先講清楚、工具表）；六份教材各加一張 Mermaid 流程圖（round1 操作流程、card 的一生＋品味循環、card 到開跑、復現判準與卡住、一週的循環、論文報告五步）；Mermaid 節點標籤不含括號引號斜線
- 第 5 站：每週報告從第 2 站起；第 0、1 站只報兩次（Round 1 的 10 分鐘骨架、Round 2 的 one-pager），不做每週變體（使用者 2026-10-08 定）；論文報告教材兩處殘留引用修掉
- README 加「一個會議週期」示例時程表（約 24 週）
- Round 1 §8 商機保留（使用者：幫學生想得廣、對痛點有概念）
- **repo 從第 0 站就建**（原本第 3＋4 站才建，Deep Research 報告與設計文件無處放）：round1 操作方法加第 0 步；round1／round2／第 2 站／1b 的檔案位置全改為 repo 內的 `research/`、`design/`、`notes/`
- 第 3＋4 站 §1.1 結構對齊範本；README 定為五段（目的／安裝／怎麼跑／目前結果／結構），「目前結果」每週更新，是教授看 repo 的第一眼
- 週小結五格和第 5 站投影片對齊（原本四格對不上）；第 5 站 §4.2 不再自己放一份不完整的 YAML，指向範本

### 2026-10-08 整體審閱後的補強（已做）
- 第 2 站：決策紀錄加「論文骨架」（英文題目、150 字摘要、三條 contribution）
- 第 3＋4 站：10 句話過擬合；評測腳本 partner 盲測
- 論文報告：淺讀 log（每週 2 篇 5 行）；審稿預測練習（OpenReview，每三次論文報告輪一次）
- 第 5 站：第 4 頁「距上次新數字 N 週」＋月度停損（> 4 週固定討論）；第 8 頁加淺讀
- 範本同步：design_template、reading_log.md、進度 qmd、Issue 模板、README
- 1b §6 改為六段 AI 指令（limitation／future work 挖掘、錯誤分析發散、跨領域移植、挑戰前提、card 壓力測試、novelty 查詢式）

### 品味的循環（2026-10-08 定）
讀（淺讀 log）→ 猜（card 預測、審稿預測）→ 對答案（教授的判斷、OpenReview、真實審稿）→ 記漏的那一類（reading_log「我容易漏的」）→ 對照規則（`conventions/taste.md`，見下）。已做：1b §5 預測步驟與 idea log 預測紀錄；`conventions/review_reconciliation.md` 審稿對帳。

### 待累積：教授的品味清單 `conventions/taste.md`
使用者決定不一次寫，改為**在往後對話中逐條說出**。規則：使用者在對話裡講到「我不做 X 因為⋯」「我偏好 Y」這類挑題目的判斷時，Claude 主動提議「這條要不要記進 taste.md」，同意後才寫（第一條進來時建檔）。格式：一條一行，附日期與一個示例或真實案例（真實案例不放學生個資與未發表結果）。學生寫 card 時在「我沒把握的地方」引用條號。

### 備忘：第 −1 站 bootcamp（使用者計畫 2027 暑假前規劃，現在不做）
進 lab 前 4–6 週，四項可檢核的產出：(1) 從頭跑通一個標準 recipe 並對上數字（第 3 站預演）；(2) 自己實作最小的 CTC 或 Conformer block 在小資料訓到收斂，不用現成模組；(3) 讀 5 篇論文各填核對紀錄；(4) 一頁英文摘要重寫。另附「新生第一個月」週課表。可能一併處理：Round 1 §8 商機對學生無用，考慮砍或改選填。
其他建議未採行、留待使用者決定：雙週 15 分鐘一對一；第一篇投 Interspeech、第二篇才投 ML 主會的投稿順序。

### 交叉引用檢查（2026-10-08 做過一次）
七份教材＋總表＋範本的節號引用全部對過，一致。`design_table1.md` §3.2 引用的「Round 2 §8 接受論文解剖」與 `idea_card.md` §7 的「Round 2 §7 補充點」在 v4.1 之後都已存在。之後改任一教材的節號，grep `§` 與 `第 N 站` 重做一次。

### Round 2 的 5 點（2026-10-08 補完，v4.1）
prior work 欄、pilot 與放棄判準、接受論文解剖、arXiv 手動搜尋與 Scholar alert、短／長論文條件——都已在 `round2_dive.md`。

### 其他
- [x] `README.md`：路徑圖、教材清單、先讀哪份、工具表（2026-10-07）
