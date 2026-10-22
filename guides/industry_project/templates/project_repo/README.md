# 〔專案簡稱〕

> 產學專案 repo（private）。交付時整個 repo 連同 commit 歷史，在 tag `delivery-v〔N〕` 交給產業方，所以這裡只放產業方可以看的東西；產業方給的原檔（音檔、逐字稿、原始需求文件、來信）不放進來。規則見 Lab-Hub [產學分支](https://github.com/SigSpeechAI-NTNU/Lab-Hub/blob/main/guides/industry_project/industry_track.md)。這段提示在 README 填好後刪掉。

## 專案

〔一句話：任務、輸入、輸出〕

需求規格表：`spec/requirement_spec.md` v〔N〕（〔YYYY-MM-DD〕確認）

## 安裝

```
uv sync
```

- Python 〔版本〕（見 `.python-version`）、CUDA 〔版本〕、PyTorch 〔版本〕
- 測試資料：〔機器與路徑〕；〔檔案數〕個檔、約〔時數〕小時；檔案清單 md5：〔　〕
- 切分清單：`eval/splits/dev.txt`、`eval/splits/accept.txt`（只有檔案 ID）

## 怎麼跑驗收

```
uv run 〔驗收指令〕 〔驗收集路徑〕
```

預期結果（`delivery-v〔N〕`）：〔每個指標的數字，對應研究測試報告第 5 節〕

## 目前驗收狀態（更新：〔YYMMDD〕）

| 驗收指標 | 門檻 | 目前最好 | 差距 | 狀態 | 測在 |
|---|---|---|---|---|---|
| 〔　〕 | 〔　〕 | 〔　〕 | 〔　〕 | 〔達標／未達／未測〕 | 〔開發集／驗收集〕 |

## 誰負責哪一塊

| 部分 | 負責 |
|---|---|
| 〔驗收腳本／某個方法／研究測試報告〕 | 〔姓名〕 |

## 結構

| 資料夾 | 放什麼 |
|---|---|
| `spec/` | 需求規格表；改版時舊版另存，不覆蓋 |
| `src/` | 模型、訓練、推論的程式 |
| `configs/` | 驗收過的每個系統一個 config |
| `eval/` | 驗收腳本；`splits/` 是開發集與驗收集的檔案 ID 清單 |
| `results/` | `acceptance.csv`（驗收集每跑一次記一行）、報告用到的 `results.csv` 列 |
| `meetings/` | kickoff 與月報投影片（qmd 與 html）、會後紀錄、`theme.scss` |
| `report/` | 研究測試報告（qmd、html、docx） |

## 授權

用到的預訓練模型、資料集、套件各自的授權，見最新一版研究測試報告的附錄 C。
