# CLAUDE.md — ~/Lab-Hub repo 規範（2026-10-02 建立）

> 每次對話起手都會讀本檔。本 repo 對應 GitHub `SigSpeech-NTNU/Lab-Hub`，**學生看得到**。
> 給人讀的入口在 `README.md`；Project 指令備份在 `project-instructions/`。本檔保持短。

## 一、目的與讀者

教指導的碩博生怎麼做研究：入門題目、用 Deep Research 建地圖、讀論文、做論文閱讀投影片、記錄實驗、報告進度。讀者是研究生；教授決定教什麼，AI 寫成學生能照著做的版本。

## 二、與其他 Hub 的關係

| Hub | 本 Project 對它 | 從它取什麼 |
|---|---|---|
| Research-Hub | 只讀 | 研究方法的做法（改寫成學生版） |
| Paper-Hub | 只讀 | 論文閱讀與寫作的規範（改寫成學生版） |
| Course-Hub | 只讀 | 投影片製作的做法 |
| Coach-Hub | 只讀，通常不需要 | — |

一份檔案只有一個 Project 會改它：本 repo 的檔案只有 Lab-Hub 改；其他 Hub 的檔案本 Project 不碰。取材一律改寫，不整段搬。

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
    <主題>/                       之後的教材各自一個資料夾
  conventions/                    實驗室慣例（建立時再開）
```

## 四、公開 repo 的界線

不放：學生個資、未發表的實驗結果、授權語料的內容或路徑、其他 Hub 的內部規範、金鑰。

## 五、研究路徑與教材待辦（2026-10-03 定稿；每做完一站勾掉）

學生從拿到題目到投出論文的路徑。站次已和使用者討論定案，教材逐站補。

| 站 | 學生在做什麼 | 產出 | 教材 | 狀態 |
|---|---|---|---|---|
| 0 入門 | 跑 Round 1、核對、親讀 5 篇 | `_r1_checked.md`、10 分鐘報告 | `guides/deep_research/round1_map.md` | ✅ |
| 1 選路線 | 帶 §9 問教授 → Round 2 → one-pager | `_r2_*.md`、教授改過的 one-pager | `guides/deep_research/round2_dive.md` | ✅ 待補 5 點（見下） |
| 1b 出題 | 寫 idea card，教授挑；之後每次進度報告帶一張新的或改過的 | idea card、idea log | `guides/ideation/idea_card.md` | ✅ v1，待使用者審 |
| 2 實驗設計 | 畫 Table 1、消融表、method figure、定 baseline 與資料、pilot | 三張表圖＋一頁決策紀錄，group meeting 審，檔尾留審核紀錄 | `guides/experiment_design/design_table1.md` | ✅ v1，待使用者審 |
| 3 復現＋錯誤分析 | 復現 baseline 到對上數字；看它在哪類輸入上失敗 → 回 1b 改 card | 復現紀錄、錯誤分析 | 與 4 合寫 | ⬜ |
| 4 執行與紀錄 | 填 Table 1；實驗日誌、config、版本管理 | 持續更新的結果表＋日誌 | `guides/experiment_log/`（暫名） | ⬜ |
| 5 進度報告 | group meeting：先報進度與自己的 card，教授後講 | 固定格式的報告（含 card 欄位） | `guides/progress_report/`（暫名） | ⬜ |
| 6 寫作 | 把 Table 1 變成初稿 | 初稿 | 從 Paper-Hub 取材改寫學生版；最後做；commit 前使用者親審 | ⬜ |
| 貫穿 | 讀論文、做閱讀投影片 | 投影片 | `guides/paper_reading_slides/`；可從 Paper-Hub、Course-Hub 取材 | ⬜ |

橫向文件（各站都用到，最後收尾）：要問教授的事總表、AI 使用規範（每站可做什麼、怎麼核對、怎麼標明）、檔案與命名慣例 → `conventions/`。

討論順序：2 → 1b → 3+4 → 5 → 貫穿 → 6 與橫向。

### 已定的設計決策（寫教材時遵守）
- 1b：學生先講、教授後講；教授給的 idea 由學生寫成 card（含「我為什麼沒看到」一格）；idea log 連退掉的一起留並註明原因；考核寫 card 的動作不考核好壞；AI 可發散但 card 上的痛點要附學生自己的證據；退回代碼七種 BIG／DONE／DATA／DULL／VAGUE／GPU／LATER
- 2：預設長論文（4 頁照長論文修剪）；產出含 method figure；顯著性列為考量但一句話交代不走火入魔；工具鏈與資料集寫具體名稱、授權不設關卡；研究倫理只寫原則（方案 A）；示例 contextual biasing STT、baseline 以方法類型標示。Table 1 先畫再寫程式；baseline 四層（必備／最強公開／消融／簡單）3–5 個；貢獻點只動一格；資料三層（標準公開／公開自組／自建），主實驗至少一個標準公開資料集，自建不得是唯一評測集；截稿日不到 4 個月不開新蒐集
- 6：選 B（改寫學生版放 Lab-Hub），Paper-Hub 不公開

### Round 2 待補 5 點
- [ ] §7 每題加「最接近的 2–3 篇 prior work 與差異」
- [ ] §7 每題加「2 週 pilot 與放棄判準」；one-pager 時程加 pilot 里程碑
- [ ] §8 改為解剖目標會議近兩年 3 篇同路線接受論文（貢獻類型、baseline 數、資料集數、消融數、主表樣貌）
- [ ] 操作方法加一步：手動 arXiv 搜尋＋Google Scholar alert 補工具盲區
- [ ] 「我的條件」加「目標會議屬於短論文／長論文」，§7 排序納入

### 其他
- [ ] `README.md`：教材超過兩份後加路徑圖與「先讀哪份」順序
