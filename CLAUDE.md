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
    <主題>/                       之後的教材各自一個資料夾
  conventions/                    實驗室慣例（建立時再開）
```

## 四、公開 repo 的界線

不放：學生個資、未發表的實驗結果、授權語料的內容或路徑、其他 Hub 的內部規範、金鑰。

## 五、未完成事項（清空後刪這節）

- [ ] 論文閱讀投影片的教材（`guides/paper_reading_slides/`）：做法待與使用者討論；可從 Paper-Hub 與 Course-Hub 取材
- [ ] `README.md` 的「先讀哪份」順序：等教材超過兩份再排
- [ ] Research-Hub 那邊：`CLAUDE.md` Hub 分工表加 Lab-Hub 一列、`research_profile.md` 第四節「招收學生」那行的措辭——由使用者在 Research-Hub 決定
