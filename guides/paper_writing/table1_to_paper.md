# 寫作：從填滿的 Table 1 到投稿（v1，2026-10-22）

> 位置：第 6 站。前置是 Table 1 的主實驗與消融已經填滿（分析可以還在跑），手上有第 2 站決策紀錄的「論文骨架」、`results/results.csv`、第 3 站的錯誤分析。
> 這一站的目的：把手上的證據寫成**審稿人讀一遍就懂、每一句都撐得住**的論文。審稿人最不原諒兩件事：寫得比證據強（包括任何一個編出來的數字或引用），和要讀兩遍才懂的段落。這份教材每一節都在防這兩件事。
> 流程：**三張表（教授審）→ 你寫段落大綱 → AI 照大綱起草英文 → 你逐句核對 → AI 冷讀＋partner 盲讀 → 截稿前 10 天交教授**。之後由教授接手最後一輪修改與投稿。
> 產出：你 repo 裡的 `paper/`：一節一檔的 LaTeX、`refs.bib`、三張表（投稿規定、主張與篇幅、數字出處）、AI 使用紀錄、兩份審查與處理表。結構和教授自己寫論文用的資料夾一樣，教授接手時整個資料夾直接用。範本 repo 已附好骨架。
> 預設目標是長論文（正文 8 頁以上，例如 ACL 主會、ICML／NeurIPS／ICLR），和第 2 站一樣；要投 4 頁的 Interspeech／ICASSP，照 §4.3 修剪。
> 鐵律：**分析裡的「為什麼」、Limitations 的內容，AI 不生，你自己寫。** 其餘段落 AI 照你的大綱起草，你逐句對回證據。
> **參與產學計畫的人**：產業方資料的結果能不能寫進論文、投稿前要給產業方看多久，動筆前問教授。見[產學分支](../industry_project/industry_track.md) §3.3、§8。

---

## 0. 這一站怎麼接前後

```mermaid
flowchart LR
  T[Table 1 填滿 論文骨架] --> V[投稿規定表]
  T --> C[主張證據表 篇幅預算]
  V --> C
  C --> R{教授審}
  R -->|撐不住| X[補實驗 或砍主張]
  X --> C
  R -->|通過| O[你寫段落大綱]
  O --> D[AI 起草 你逐句核對]
  D -->|下一節 由內往外| O
  D --> S[AI 冷讀 partner 盲讀]
  S --> K[檢查清單]
  K --> P[截稿前 10 天交教授]
  P --> Q[教授接手 投稿]
  Q --> RR[審稿回來 審稿對帳]
```

這一站不做新的研究決策，只用前面各站已經有的東西：

| 從哪站 | 拿什麼 | 變成論文的哪裡 |
|---|---|---|
| 第 2 站決策紀錄 | 一句話主張、論文骨架（題目、摘要、三條 contribution）、長論文預留的分析維度與失敗情境 | 主張–證據表的起點（§2.2）；摘要、引言的第一版 |
| 第 2 站 | method figure | Figure 1 的草稿 |
| 第 3 站 | 錯誤分析 | 引言裡「觀察到的失敗」；分析節 |
| 第 4 站 | `results.csv`、填滿的 Table 1 與消融表 | 實驗與結果節；每個數字的出處（§1.1） |
| 論文報告、`notes/papers/` | 你讀過、有核對紀錄的論文 | related work 與所有引用（§1.2） |
| Round 2 | prior work 欄、接受論文解剖 | related work 的分組；同一個會議的論文怎麼寫 |

時程從截稿日倒推（**示例**，以教授定的為準）：

| 截稿前 | 做什麼 | 交什麼 |
|---|---|---|
| 6 週 | 三張表（§2） | `venue.md`、`plan.md` 給教授審 |
| 6–3 週 | 由內往外寫（§4），每節：大綱 → AI 起草 → 核對 → 編譯 | 每週進度報告第 4 頁照報 Table 1，另加一行：寫完哪幾節、紅字剩幾個 |
| 3–2 週 | AI 冷讀、partner 盲讀、處理意見（§8） | 處理表 |
| 10 天 | 檢查清單（§8.4），交教授 | PDF、`plan.md`、處理表 |
| 10 天到截稿 | 教授接手；你回答問題、補教授要的分析、填 checklist | — |

4 頁的論文大約短一半（3–4 週）。

---

## 1. 兩條不能破的規則

### 1.1 每個數字都有出處

論文裡的每個數字——表格的每一格、正文裡的每個數字、摘要裡的改善幅度——都要對得回 `results/results.csv` 的某一列，或你引用的那篇論文的某張表。對法寫在 `paper/results/index.md`，一個數字一行（示例）：

```markdown
| 論文裡的位置 | 數字 | 出處 | 怎麼算 |
|---|---|---|---|
| tab:main，Ours 列，test-other B-WER | 9.2 | results.csv：20270108_ours_s1／librispeech／test-other／b_wer | 單次 |
| abstract：relative reduction | 14.8% | tab:main 的 Ours 與 deep biasing 兩列 | (10.8 − 9.2) ÷ 10.8 |
| tab:main，〔最強開源方法〕列 | 〔數字〕 | 〔cite key〕 Table 〔N〕 第 〔N〕 列 | 引用，條件寫在表註 |
```

- **還沒有的數字寫紅字佔位** `\NEEDNUM{test-other B-WER, mean of 3 seeds}`（§1.3），不要先放一個看起來合理的值——你會忘記它是假的
- **算出來的數字用程式算**：相對改善、平均、差距，不心算。建議表格直接用 script 從 `results.csv` 產生（例如 `scripts/make_tables.py` 輸出到 `paper/tables/`），手打的數字最容易錯
- 改了實驗、重跑了 run，`index.md` 的那一行一起改；指到舊 run 的行就是錯的行

### 1.2 每篇引用你都讀過，BibTeX 從出版方來

- 每個 `\cite` 都是你開過的論文，而且**被引用的那句話，那篇論文真的有說**。讀過的論文應該在 `notes/papers/` 有核對紀錄，或在 `reading_log.md` 有一行
- BibTeX 的來源，由可靠到要小心：ACL Anthology 頁面、DBLP、出版方頁面（IEEE Xplore 的 Cite This、ISCA Archive、PMLR、OpenReview）、arXiv 的 Export BibTeX。Google Scholar 匯出的常缺頁碼、會議名稱不一致、把 arXiv 版當正式版，用了要對過
- **不跟 AI 要 BibTeX。** AI 給的作者、年份、會議看起來都對，常常有一格是編的
- 有正式出版版本就引正式版，不引 arXiv 版
- **引原始論文，不引 toolkit、不引 survey。** 用 HuBERT 就引 HuBERT 的論文，不是引 s3prl；用 Conformer 引 Conformer 的論文，不是 ESPnet。toolkit 另外引，只為了 toolkit 本身。用到的每個語料、每個 pretrained checkpoint 都引它自己的論文或官方頁面；Whisper 這類模型要寫版本與大小
- 缺的寫 `\NEEDCITE{a paper reporting X on Y}`，最後一次查完

為什麼這麼嚴：一個假引用會讓審稿人懷疑你每一個數字。ACL 系列的投稿須知把「編造的、或不支持論點的引用」列為 desk reject（不送審直接退稿）的原因之一（以當屆的作者須知為準）。

### 1.3 紅字佔位

範本 repo 的 `paper/placeholders.tex`：

```latex
\usepackage{xcolor}
\newcommand{\NEEDNUM}[1]{\textcolor{red}{\textbf{[NUM: #1]}}}
\newcommand{\NEEDCITE}[1]{\textcolor{red}{\textbf{[CITE: #1]}}}
```

在 `main.tex` 的 preamble 最後（`\begin{document}` 前一行）加 `\input{placeholders}`。紅色粗體是故意的：PDF 一翻就看到，不可能混進投稿。

寫不出數字或引用的時候，**寫紅字，不要寫一句模糊的話繞過去**（例如用 "considerably improves" 代替一個你還沒有的數字）。模糊的句子搜不到，會跟著投出去。投稿前在 repo 根目錄跑這一行，必須沒有輸出：

```
grep -rnE 'NEEDNUM|NEEDCITE' paper/sections paper/tables
```

---

## 2. 動筆前三張表

這三張表是第 2 站「先畫 Table 1 再寫程式」的寫作版：先決定論文要講什麼、講到多強、每節多長，再寫句子。教授審過 `plan.md` 才寫正文。

### 2.1 投稿規定表 `paper/venue.md`

頁數、必要章節、匿名規定、checklist、AI 使用聲明**每一屆都可能改**。去年的論文、AI 的記憶、學長姐的經驗都不算數。來源的優先順序：

1. **這一屆的 paper kit**：style 檔、範例 `.tex`、作者須知。下載後解壓進 `paper/`。排版（字級、邊界、review 與 final 選項）以它為準
2. **這一屆的 call for papers 與作者須知頁**：頁數、必要章節與順序、匿名、checklist、AI 聲明、補充材料、日期以它為準
3. **去年的規定**：只能當參考，表裡標「未確認」

兩者衝突時，範本管排版、call 管其他，衝突告訴教授。**自己查，不讓 AI 查**；入口在 Lab-Hub README 的會議表。

`paper/venue.md`（範本 repo 已附）每一行都要有出處和查證日：

| 項目 | 這一屆的規定 | 出處（網址或檔名） | 查證日 |
|---|---|---|---|
| 截稿日與時區 | | | |
| 正文頁數；參考文獻、附錄、Limitations 算不算 | | | |
| 範本與選項（review／final、字級下限） | | | |
| 必要章節與順序 | | | |
| 匿名規定 | | | |
| checklist：名稱、放哪、沒填的後果 | | | |
| AI 使用聲明：要不要、放哪、怎麼寫 | | | |
| 補充材料與程式碼 | | | |
| 一稿多投、preprint | | | |

長論文會議常見的（**以當屆為準，這裡只是告訴你要找什麼**）：ACL 系列有必填的 Responsible NLP Checklist，Limitations 一節不算頁數但沒有就退稿；NeurIPS 的 paper checklist 附在 PDF 後面，答案會被審；ICLR 鼓勵附 reproducibility 與 ethics statement。

### 2.2 主張–證據表 `paper/plan.md`

先把第 2 站的一句話主張用**實際結果**重寫一次。結果和預期不同時，改主張，不改結果。

然後每條 contribution 一列：

| # | 主張（英文，論文裡會出現的那句） | 證據（哪張表、哪一列） | 證據現在有嗎 | 用詞等級（§3） | 要更強需要什麼 |
|---|---|---|---|---|---|
| C1 | | | | | |

- 「證據現在有嗎」寫「沒有」的主張，三條路：補實驗、降用詞、砍掉。走哪條問教授
- 砍掉的寫進「這篇不講的主張」。寫下來是為了提醒自己：引言和結論也不准偷偷講
- 一句話主張和每條主張是你的判斷，所以你自己填；AI 可以幫你挑用詞的毛病（§6.6），不能替你決定論文主張什麼
- 同一個檔下面有「術語表」：每個東西在論文裡只用一個名字（§5.2），第一次出現就定

### 2.3 篇幅預算

先放圖表，剩下的才是文字。在 `plan.md` 寫每節分幾欄（兩欄排版，1 頁＝2 欄）。

長論文示例（正文 8 頁＝16 欄；以投稿規定表為準）：

| 節 | 欄 | 裡面的圖表 |
|---|---|---|
| Introduction | 2 | Figure 1（方法圖或問題示意） |
| Related work | 1.5 | |
| Method | 3.5 | |
| Experimental setup | 2 | 資料集表 |
| Results | 3 | Table 1、消融表 |
| Analysis | 3 | 分析圖、失敗案例 |
| Conclusion | 0.5 | |
| 留給圖表浮動 | 0.5 | |

4 頁示例（8 欄）：Introduction（含 related work）1.5、Method 2、Experimental setup 1、Results 2、Analysis 1、Conclusion 0.5。

頁數用編譯出來的 PDF 量，不用估：每寫完一節編譯一次（§7.1）。

`plan.md` 檔尾的「審核紀錄」沒有教授的一行之前，不寫正文。

---

## 3. 用詞等級：動詞要和證據一樣強

審稿人看到 "substantially" 會回頭看表格；表上差 0.3，你就在他心裡扣分了。用詞是一級一級的台階，每一級有它要的證據；證據到哪一級，你就寫哪一級。

### 3.1 台階

| 用詞 | 要有的證據 | 證據不夠時 |
|---|---|---|
| differs from、changes | 任何量到的差異 | — |
| improves over、outperforms | 同一個指標、同一個 split、可比的設定與調參預算 | differs from |
| substantially、markedly | 差距是 seed 之間差異（spread）的好幾倍，spread 寫在論文裡，而且這個大小在這個指標上有意義 | improves over |
| significantly | **只能**配一個寫出名字的統計檢定（例如 paired bootstrap）。它不是「很多」的意思 | 直接寫差距 |
| consistently | 至少三個條件（資料集、語言、設定），方向一致，全部在論文裡 | on A and B |
| robust to X | 有一個實驗在改變 X | — |
| generalizes | 至少兩個語料、語言或條件；同一個語料的另一個 split 不算 | on X |
| state-of-the-art | 你親自核對過、同 split 同條件的已發表數字 | 不寫，或教授同意後寫 the best result we are aware of |
| first to | 不寫。教授要你寫的話，先做過 prior-art 搜尋 | — |
| zero-shot、unseen speaker | 寫清楚 pretrained checkpoint 用了哪些資料，說明測試條件不在裡面。用大型公開 checkpoint 的論文最常死在這裡 | 寫實際的條件 |
| real-time、streaming | RTF < 1，加上硬體、batch、精度；streaming 要寫演算法延遲（lookahead 加 chunk，單位 ms） | 寫 RTF 本身 |
| more natural、higher quality | 主觀聽測（§3.2）；只有 UTMOS 這類自動分數，只能寫 higher UTMOS | higher 〔指標〕 |
| low-resource | 每個語言幾小時有標註、幾小時沒標註 | 寫小時數 |
| understands、reasons（LLM） | benchmark 分數不證明「理解」 | 寫看得到的：answers X% correctly on … |

證據不到你想要的那一級時，照證據寫，然後在 `plan.md` 的「要更強需要什麼」記下差什麼——要不要補，問教授。

### 3.2 語音論文最常被抓的四件事

- **錯誤率的改善要寫絕對還是相對。** 「WER 降 8%」有兩種讀法，審稿人會選對你不利的那種。寫成 "from 12.4% to 11.4% WER (1.0 absolute, 8.1% relative)"。相對改善＝(舊 − 新) ÷ 舊＝1.0 ÷ 12.4＝8.1%。CER、EER、DER 一樣
- **從論文抄來的 baseline 數字要標明**（例如加 † 並在表註寫條件）。條件和你的不同時，贏它只能寫 differs from。條件怎麼對，見第 2 站 §3.3
- **主觀聽測（MOS、CMOS、偏好測試）** 要寫聽者數、每題幾個人聽、題數、是不是母語者、群眾外包還是實驗室、信賴區間。不同論文的 MOS 不能互比。信賴區間重疊就是「沒有量到差異」，不是 "comparable"，也不是 "slightly better"
- **seed 數。** 語音會議常見單次比較（第 2 站 §3.3 的但書），但差距比這個指標平常的 seed 波動還小時，不要寫 improves。投 ML 主會時，每個數字都要有 3 個以上 seed 的 spread，不然要寫為什麼。seed 數由教授定

### 3.3 主張鏈：摘要 ≤ 引言 ≤ 結果

摘要、引言的 contribution 清單、結論，講的是同一組主張，而且強度由內往外只能持平或變弱：**結果節是天花板，引言不能超過它，摘要不能超過引言。**

「摘要承諾的比結果多」是最常見的審稿意見之一，幾乎都是這樣來的：結果節改過，摘要沒跟著改。每次改結果節，就用 §6.6 的指令把三處並排檢查一次。

---

## 4. 寫作順序與各節任務

### 4.1 由內往外寫

順序：**方法 → 實驗設定與結果 → 分析 → related work → 引言 → Limitations → 摘要 → 結論。**

主張的強度從結果往外推（§3.3）。先寫引言或摘要，結果一出來就要重寫；更糟的是，你會不自覺地挑結果去配合已經寫好的引言。第 2 站的論文骨架是草稿，不是定稿：寫到引言和摘要時拿出來，對照結果改。

### 4.2 每一節要做到什麼

| 節 | 要做到 | 審稿人在這節找 | 最常見的錯 |
|---|---|---|---|
| Method | 別人讀完能重做：每個符號第一次出現就定義，維度、取樣率、frame rate 都寫出來 | 你動的是哪一格、和 baseline 差在哪 | 符號先用後定義；把實驗設定寫進方法 |
| Experimental setup | 先講設定、再講結果：語料與 split 的名稱、小時數、取樣率、模型參數量、訓練步數、optimizer 與學習率、seed 數、解碼設定、指標的實作（哪個 scorer、哪種文字正規化） | 比較公不公平 | 少了 seed 數；少了 baseline 的條件 |
| Results | 主張需要的結果；每張表一句「看哪裡」 | Table 1 | 逐格念表格；沒寫絕對或相對 |
| Analysis | 方法在哪裡有效、在哪裡失效、為什麼。好論文和「剛好被接受的論文」差在這一節 | 改善集中在哪；失敗案例 | 只放贏的；講了機制卻沒有實驗支持 |
| Related work | 依「每條路線做了什麼選擇、那個選擇的代價」分組，不是一篇一句的書目 | 你知不知道最接近的那篇、你和它差在哪 | 列清單；漏了最接近的那篇 |
| Introduction | 問題是一個觀察到的具體失敗，不是「文獻有缺口」；contribution 每條對到一節、一張表 | 第一段就知道要解決什麼 | 從 "With the rapid development of…" 開始 |
| Limitations | 真的限制結論範圍的方法上的限制：只測了哪些語言、哪種錄音條件、單 seed、哪個假設沒驗證 | 誠不誠實 | 寫成 future work；寫成客套的謙虛 |
| Abstract | 一句問題、一句方法、帶數字的結果、一句意義；不引用；現在式 | 主張和數字 | 比引言講得更強 |
| Conclusion | 不加新主張，短 | — | 把摘要重寫一次 |

Related work 若 `refs.bib` 還很薄，先不要寫成文字：在大綱裡列出分組、每組要引哪幾篇，把缺的論文讀完、BibTeX 補齊再寫。用一堆 `\NEEDCITE` 撐起來的段落不算草稿。

### 4.3 投哪種會議，寫法哪裡不同

| 會議 | 審稿人是誰 | 寫法 |
|---|---|---|
| ICML、NeurIPS、ICLR | 不做語音的 ML 研究者 | 主張要能**不提語音 benchmark** 就講清楚：方法的性質、訓練方式、評測方法、一個現象。實驗依「問題」組織，不依資料集；每張圖表有 spread；寫算力（GPU 型號、數量、時數）。語音論文在這裡最常被拒的理由是 "interesting but domain-specific"，這要在 §2.2 就處理，潤飾救不了 |
| ACL 系列 | 計算語言學者 | 問題用他們認得的方式講：一個語言現象、一個語言、一個評測的缺口。失敗分析放正文，不放附錄 |
| Interspeech（4 頁） | 很多來自鄰近領域（語音學、聽覺、對話） | 開頭講語音現象或失敗（在訊號的哪裡、什麼條件下），不是講模型。只在你那個小角落通用的術語要解釋 |
| ICASSP（4 頁） | 訊號處理工程師 | 寫出機制；敘事太多會扣分 |

**從長論文修剪成 4 頁**，照這個順序，夠了就停：

1. 刪贅字、疊在一起的限定語、重複其他節已經講過的話
2. 合併句子；名詞化改回動詞（"perform an evaluation of" → "evaluate"）
3. 刪掉和別張圖表重複資訊的欄或子圖
4. related work 併進引言；分析只留最強的一張；代價（Params、RTF）併進 Table 1 的欄
5. 最後才砍內容，砍什麼問教授

不准砍的：重做實驗所需的設定、讓主張準確的限定語、告訴讀者看哪裡的那一句。塞不下就是塞不下，不准擠版（§7.3）。

---

## 5. 段落與句子：審稿人只讀一遍

想像你的讀者：這週要審六篇，先跳到表格，再回頭讀文字找表格的意思，在螢幕上、只讀一遍。讀兩遍才懂的段落，會被當成比較弱的結果——審稿人不會把「難讀」和「沒說服力」分開打分。

### 5.1 段落

- **一段一個主張。** 兩個就拆成兩段；沒有主張的段落是過場，併進下一段變成一個子句
- **第一句就是重點**，不是鋪陳（示例）：
  - 弱："Several factors affect rare-word recall. The bias list size, the number of distractors and the word frequency all matter. We found that the number of distractors dominates."
  - 好："The number of distractors in the bias list dominates rare-word recall; list size and word frequency have smaller effects."
- **舊資訊在前、新資訊在後。** 每一句從讀者已經知道的東西開始，把新東西放句尾；下一句再從這個新東西開始。這樣句子自己就接得起來，不用一直加 however、moreover（示例）："We bias the decoder with a list of rare words. The list is built from the user's contacts." 第二句從上一句句尾的 list 開始
- **連接詞只用在關係看不出來的時候。** 兩句明顯是因果，therefore 是雜訊；是對比而讀者可能沒注意，才寫 however。不要連續三段都用連接詞開頭
- **任何東西用之前先定義**：符號、縮寫、資料集簡稱、消融的代號
- **每次提到表或圖，告訴讀者看哪裡。** "Results are shown in Table 3." 浪費了這次引用；寫 "Table 3 shows that the gain is concentrated on utterances with more than five bias words."（示例）。只說兩件事怎麼相關、沒有新數字的句子也有用，不要為了省字砍掉

### 5.2 句子與術語

- 主詞靠近動詞：句首疊了三個介系詞片語才出現主詞，讀者會回頭重讀
- 一句一個限定語："may potentially somewhat improve" 讀起來像你不敢負責
- 主詞是我們或系統時用主動（"We train the encoder on…"）；主詞不重要時用被動很正常（"Audio was resampled to 16 kHz"），實驗設定節本來就多被動
- 句子長短要有變化；一長串限定之後接一句短的，重點才落得下來
- **一個東西只用一個名字。** 前面叫 bias list，後面就不能叫 context list、keyword set——技術寫作裡換一個字，讀者會以為是另一個東西。寫進 `plan.md` 的術語表；重複讀起來太重，就改句子結構，不要換名字
- 縮寫第一次出現時展開，摘要裡另外展開一次。ASR、WER、TTS、MOS 在語音會議不用展開；投 ML 或 NLP 會議要展開。你自己取的名字一律展開
- 單位：數字和單位之間空一格，照 SI：16 kHz、10 ms、3 dB、960 h、7B parameters

### 5.3 不要用的字

這些字在推銷你的工作，不是在描述它。審稿人讀過大量 AI 寫的文字，看到就認得出來，好感在讀內容之前就扣掉了。

- 開頭："In this paper, we propose a novel…"、"With the rapid development of…"、"Recent years have witnessed…"、"X has attracted increasing attention"、"To the best of our knowledge, we are the first…"
- 字：novel（自誇時）、leverage（當動詞）、delve、showcase、underscore、pivotal、crucial、comprehensive、extensive（"extensive experiments"）、holistic、nuanced、intricate、realm、landscape、paradigm shift、seamless、unlock、harness、shed light on、pave the way、groundbreaking、cutting-edge、remarkable、impressive、notably、importantly、furthermore、moreover、additionally、it is worth noting
- 句型："Not only X but also Y"、"X is not Y; it is Z"、只有兩項有內容的三項列舉、"we believe that"、反問句。em-dash（—）一節最多一個

判斷原則：這個字會不會出現在這篇論文的新聞稿裡？會的話，不要放進論文。也不要矯枉過正：統計句裡的 significant、"novel-word detection" 的 novel、"loss landscape" 的 landscape 都沒問題；換成彆扭的繞口說法比原來的字更糟，改寫整句才對。

### 5.4 中文母語者最常犯的錯

| 錯 | 例 | 改 |
|---|---|---|
| 句首 This／It 指的是什麼不清楚 | "This improves recall."（前一整句？兩句前的哪個名詞？） | 把東西寫出來："This bias list improves recall." |
| 本篇特定的東西少了 the | "We freeze encoder." | "the encoder"。判斷看「在這篇裡是不是特定那一個」，不是看可不可數 |
| the former／the latter 指三個以上的東西，或跨句指 | | 直接寫名字 |
| 不可數名詞加 s | informations、evidences、feedbacks、researches | information、evidence、feedback、research |
| 中文的主題句型 | "As for the decoder, it uses…" | "The decoder uses…" |
| 成對的連接詞 | "Because X, so Y"、"Although X, but Y" | 只留一個 |
| 時態 | 實驗節用現在式寫已經做完的事 | 做過的實驗用過去式；結果顯示什麼、這篇論文做什麼（"Section 4 reports…"）、別人的論文做什麼，用現在式 |
| 我們是主詞卻寫成被動 | "It is proposed that…" | "We propose…" |
| however 用逗號連接兩句 | "X improves, however Y degrades." | 用分號或句號 |
| 搭配詞 | "do an experiment"、"shown from Figure 2" | conduct an experiment、shown in Figure 2 |
| 冗詞 | in order to、can be able to、the reason is because | to、can、because |

這張表是起點，你自己的錯記在 `notes/writing_errors.md`：同一類錯被 AI 或教授抓到第二次，記一行；每次潤飾前先自己查這幾類，也把它貼進 §6.5 的指令。換題目時和 idea log 一樣複製到新 repo。

---

## 6. AI 怎麼用

### 6.1 分工

| 你 | AI |
|---|---|
| 三張表（§2） | 照大綱起草英文（§6.3） |
| 每一節的段落大綱（§6.2） | 段落結構檢查（§6.4） |
| 分析裡的「為什麼」、Limitations 的內容 | 英文潤飾（§6.5） |
| 逐句核對 AI 的草稿；決定 AI 補進來的東西留不留 | 主張檢查（§6.6）、冷讀自審（§8.1） |

AI 不可以：給數字、給引用、給 BibTeX；把你沒講過、證據裡也沒有的理由寫進正文。

**AI 最危險的不是英文寫錯，是它替你補了一個你沒驗證過的理由。** 例如你的大綱只寫「list 越長，改善越大」，AI 的草稿多了一句 "This is because the encoder disambiguates acoustically similar entries."——讀起來很合理，但你有沒有實驗證明是這個原因？沒有，它就是一句編出來的主張，和編一個數字一樣危險。所以每一段指令都要求 AI 把這種句子另外標成 [NEW]，由你決定：有證據就留下並指到那個證據；沒有就刪掉，或在分析節寫成假設（"We hypothesize that…"）並說明哪個實驗可以驗證。

教授會另外給你一套給 Claude 用的論文寫作工作區（不放在這個公開 repo）；拿到的照它的說明用，規則和這份教材一致。沒拿到不用找，這份就夠。

產學計畫的東西照產學分支 §3.2：數字和我們自己寫的文件可以進 AI，產業方的原檔不行。

### 6.2 段落大綱：寫在節檔裡

大綱用 LaTeX 註解（`%` 開頭的行不會印出來）寫在節檔裡，一段一行：那段的重點（就是之後的第一句）和要用的證據。中英文都可以（示例）：

```latex
% paper/sections/analysis.tex
\section{Analysis}
\label{sec:analysis}
% P1 重點：改善隨 bias list 變長而變大 | 證據：fig:listsize（10／100／1000 詞的 B-WER）
% P2 重點：參考答案裡沒有 bias 詞的句子，WER 沒有變差 | 證據：tab:nobias
% P3 為什麼（我自己寫）：〔你認為的原因，和支持它的實驗〕
% P4 失敗案例：list 裡有同音詞時比 baseline 差 | 證據：error_analysis.csv 的 homophone 類
```

- 大綱是這一節的骨幹。AI 起草後，每段的第一句要和大綱那一行講同一件事；講的不一樣，是 AI 改了你的論點，改回來
- 大綱留在檔案裡，partner 和教授審的時候可以對照
- 寫不出某一段的重點，表示你還不知道那段要講什麼；先想清楚，不要交給 AI 去猜
- 放 arXiv 之前要清掉註解：arXiv 會公開 LaTeX 原始檔。Google 的 `arxiv_latex_cleaner` 可以做（請自行查證用法）

### 6.3 指令一：照大綱起草

一次一節。附上這一節的 `.tex`（含大綱）、`paper/plan.md`、這一節會用到的數字（`paper/results/index.md` 的相關行），整段複製：

```
我在寫一篇投〔會議 年份〕的論文，我是第一作者。請把附件這一節的段落大綱寫成英文。
大綱是 .tex 裡 % P1、% P2… 開頭的註解，一行一段。主張和證據由我決定，你只負責把它寫清楚。

附件：
1. 這一節的 .tex（含大綱）
2. plan.md（主張證據表、用詞等級、術語表、篇幅預算）
3. 這一節用到的數字與出處

規則，每一條都要遵守：
- 每段的第一句就是大綱那一行的重點；一段只講一個主張
- 數字只能用我給的。缺的寫 \NEEDNUM{缺什麼}，不准寫看起來合理的數字
- 引用只能用我給的 \cite key。缺的寫 \NEEDCITE{需要什麼樣的論文}，不准自己寫作者、年份或 BibTeX
- 用詞強度照 plan.md 的「用詞等級」，不准往上加（substantially、significantly、consistently、robust、generalizes、state-of-the-art 都有門檻）
- 錯誤率的改善一律寫絕對值和相對值
- 大綱沒寫、證據裡也沒有的理由、機制、動機、後果，不准寫進正文；你覺得需要的，列在最後的 [NEW] 區，說明要我確認什麼
- 大綱標「我自己寫」的段落，只保留大綱那一行，正文留空
- 術語照術語表，一個東西只用一個名字
- 不用這些字：novel, leverage, delve, crucial, comprehensive, extensive, notably, importantly, furthermore, moreover, additionally, remarkable, seamless, pave the way
- 所有 LaTeX 指令（\cite、\ref、\label、數學式）原樣保留；大綱註解保留在每段上方

輸出：
1. 這一節完整的 .tex
2. 用到的每個數字和它的出處，一行一個
3. 剩下的 \NEEDNUM、\NEEDCITE，各是什麼
4. [NEW] 區
5. 估計長度（幾欄），和 plan.md 的預算比
6. 你最沒把握的三個地方
```

拿到草稿後，逐段做三件事：第一句對大綱、每個數字對 `index.md`、[NEW] 一條一條決定。然後編譯，看頁數。

### 6.4 指令二：段落檢查（內容不變，讀起來順）

```
下面是我論文的一節。請逐段檢查，不要寫新的內容：
1. 用一句話說你認為這段的重點；說不出來就直接說「看不出重點」並引用這段
2. 重點在不在第一句
3. 每一句和上一句的關係看不看得出來；this、it、these 指的是什麼，指不清楚的列出來
4. 有沒有東西先用後定義（符號、縮寫、資料集簡稱、消融代號）
5. 每次提到表或圖，有沒有一句告訴讀者看哪裡
修改建議從最小的改起：寫清楚指的是什麼 → 調整句子順序 → 拆段 → 併段 → 加一句連接。
任何會加進新的理由、機制、動機的句子，放在最後的 [NEW] 區，不要混進修改。
我的句子有兩種讀法時，引用原句、寫出兩種讀法、問我，不要自己選一種寫順。
```

### 6.5 指令三：英文潤飾（只改英文）

```
只改英文。不改內容、不改句子順序、不改主張的強度。LaTeX 指令原樣保留。
輸出一張表：原句｜改後｜理由（2–4 個字），依錯誤類別分組；指涉與冠詞（this、it、the）放最前面。
不要把專有名詞換成比較常見但比較模糊的字；不確定我的意思時，標出來問我，不要改。
結構性的問題（重點不在第一句、一段講兩件事）不要在這裡改，最後列一行就好。
拼字一律用〔American／British，問教授〕。
我常犯的錯誤類別，先查這幾類：
〔貼上 notes/writing_errors.md〕
```

### 6.6 指令四：主張檢查

每改一次結果節、摘要、引言或結論，就跑一次：

```
附件是我論文的 PDF 和 plan.md。只列問題，不要寫新的段落。
1. 把摘要、引言的 contribution 清單、結論裡的主張並排成一張表
2. 每條主張對到結果節的哪張表、哪一列；對不到的標出來
3. 強度：結果節是天花板，引言不能超過它，摘要不能超過引言；超過的引用原句
4. 用詞：每個 improves、substantially、significantly、consistently、robust、generalizes、state-of-the-art、zero-shot、real-time，對照 plan.md 的用詞等級；超過的列出原句和降級的寫法
5. 每個錯誤率的改善，有沒有寫清楚絕對或相對；用表格裡的數字重算，寫出算式
```

AI 寫出的算式，你用程式再算一次。

### 6.7 AI 使用紀錄 `paper/ai_use.md`

一次一行：日期、工具與版本、做了什麼（起草哪一節、潤飾、檢查、冷讀）、你改了多少。多數會議要求聲明 AI 的使用，形式每屆不同（checklist 的一題、致謝裡的一句、單獨一段聲明）；ACL 系列在 checklist 裡有一題，用了沒聲明是退稿的原因（以當屆為準）。聲明照這份紀錄寫、由教授確認，不要事後憑印象寫。

---

## 7. LaTeX 與檔案

### 7.1 `paper/` 的結構與編譯

```
paper/
  main.tex            從範本的範例 .tex 改名：只留 preamble、\input 的順序、參考文獻指令
  placeholders.tex    紅字佔位（§1.3）
  sections/           一節一檔：abstract、intro、related、method、experiments、analysis、limitations、conclusion、appendix
  tables/             一表一檔，從節檔 \input
  figures/            線圖、統計圖用 PDF；頻譜圖、熱圖用 PNG 300–600 dpi
  refs.bib
  results/index.md    每個數字的出處（§1.1）
  venue.md            投稿規定表（§2.1）
  plan.md             主張–證據表、篇幅預算、術語表（§2.2、§2.3）
  ai_use.md           AI 使用紀錄（§6.7）
  reviews/            AI 冷讀、partner 盲讀與處理表（§8）；真的審稿回來放 1/R1.md、1/R2.md…
  build/              編譯產物，不進 git
```

- **一節一檔是硬規定**，不管論文多短。每次改的範圍小、diff 看得懂，教授接手時也是這個格式。會議要求的額外章節（ethics、聲明）也各自一檔
- 把這一屆的 paper kit 解壓進 `paper/`，範例 `.tex` 改名 `main.tex`，再拆成一節一檔。範本的 style 檔一個字都不改
- 在 `paper/` 裡編譯：

  ```
  latexmk -pdf -interaction=nonstopmode -outdir=build main.tex
  ```

  `main.tex` 要寫出來，不然 latexmk 會把資料夾裡每個 `.tex` 都編一次。編完看 `build/main.log` 有沒有 undefined reference 與 undefined citation 的警告
- 用哪個平台編輯與協作（本機、Overleaf 或其他）問教授。不論在哪裡改，**repo 是正本**；在別處改的要搬回 repo commit

### 7.2 表格與圖

- 表格用 `booktabs`（`\toprule`、`\midrule`、`\bottomrule`），不畫直線；數字小數點對齊，同一欄位數一致；只把最好的那個加粗，caption 說粗體代表什麼
- caption 自己讀得懂；表格的 caption 在上、圖的在下（照範本）
- 表格太寬：改寫表格（拆欄、欄名縮寫加表註）加 `\small`，不用 `\resizebox`，它會讓每張表的字級都不一樣
- 圖印出來的字不小於 8 pt（範本有規定照範本）；灰階印也分得出線條；用色盲友善的配色；圖例不看 caption 也讀得懂。畫圖程式進 repo
- 引用與參照的指令照範本和檔案現有的習慣（`\citep` 或 `\cite`、`\ref` 或 `\cref`），一篇只用一種。`Table~\ref{tab:main}` 用 `~` 避免斷行；`\cref` 會自己產生 Table，前面不要再寫
- label 用前綴：`sec:`、`tab:`、`fig:`、`eq:`。改 label 要找出所有指到它的 `\ref`

### 7.3 不准用的擠版手法

超頁時**不准**：負的 `\vspace`、改行距（`\linespread`、`\baselinestretch`）、改邊界或 `geometry`、縮小參考文獻的字、把 `\tabcolsep`、`\arraystretch` 調到範本的值以下、對文字用 `\resizebox`、字級低於規定。這些會被抓到，會被 desk reject。唯一可以調的是圖表周圍的間距，而且要告訴教授。

塞不下就是塞不下：回 §4.3 的修剪順序，或問教授砍什麼。

### 7.4 匿名

長論文會議幾乎都是雙盲審查（審稿人不知道作者是誰）：

- 不寫名字、單位、致謝；引用自己的論文用第三人稱（"Lee et al. [3] showed…"，不是 "our previous work [3]"）
- 程式碼與 demo 用匿名連結（例如 Anonymous GitHub，請自行查證），不放 lab 的 GitHub
- 補充材料的檔名、demo 頁不能透露系統名稱或單位
- PDF 的作者資訊要是空的：`pdfinfo build/main.pdf` 看 Author 欄
- 能不能先放 arXiv、什麼時候放，每個會議規定不同，問教授

---

## 8. 三道審

### 8.1 AI 冷讀：一個沒看過草稿的審稿人

- **開一個新對話**，送出第一則訊息之前把記憶（Memory）關掉。不要在起草的那個對話裡審：它記得你想表達什麼，會替你找理由
- 只上傳編譯好的 PDF，不給 repo、不給 `plan.md`——審稿人也只看得到 PDF
- 分兩步：先要摘要和問題，你回 PDF 對過，再要它打分。先打分的話，它會為了配合分數去找理由

第一步，整段複製：

```
你是〔會議〕的資深審稿人，研究〔子領域〕，這週要審六篇，這是其中一篇。
只根據附件的 PDF 判斷，不要上網搜尋作者或這篇論文。

這一則只做以下幾件事，不要打分：
1. 用三到五句話摘要這篇的主張、方法、主要結果；數字附 PDF 的表號或節號
2. 列出三到六個最可能讓這篇被拒的問題，依嚴重程度排序。每個問題寫：
   - 一句話說問題
   - 支持你判斷的原文，逐字引用，附頁碼或表號
   - 改寫就能修、用現有實驗再分析能修，還是需要新實驗
3. 每個 improves、substantially、significantly、consistently、robust、generalizes 之類的用詞，證據夠不夠
4. 摘要和引言講的，結果節有沒有撐住
說「論文沒寫」之前，先在全文（含附錄）搜尋過，寫出你搜了哪些詞。
不要客套，不要稱讚開場，不要總結段。每個問題都要只適用於這篇論文；換一篇論文也說得通的批評（例如「實驗可以更完整」）不要寫。
```

你對過之後，第二步：

```
請照〔會議〕的審稿表單打分。表單欄位如下：
〔從這一屆的 reviewer guidelines 貼上；ARR 的表單有 Soundness、Excitement、Overall Assessment、Confidence 等〕
每個分數附一句理由，理由對到第一步的問題編號。
```

- 存成 `paper/reviews/self-1/review.md`。修完、時間還夠，再開一個新對話冷讀一次（`self-2`）
- **核對**：它引用的每一句原文，回 PDF 找得到嗎？找不到的那一條刪掉——AI 審稿人也會編
- AI 的分數是預測，不是紀錄

### 8.2 partner 盲讀

- partner 只拿 PDF，不問你、讀完。他沒看過你的大綱，是最接近真的審稿人的人
- 他交一頁：三行摘要、三個最大的問題（附頁碼）、看不懂的地方。約 60–90 分鐘
- 存成 `paper/reviews/partner-1/review.md`。輪到 partner 寫論文時，你還他一次
- **「看不懂的地方」最有價值**：和你同領域的 partner 都看不懂，鄰近領域的審稿人一定看不懂

### 8.3 處理意見

把 AI 冷讀和 partner 的意見併成一張表，存 `paper/reviews/triage-1.md`：

| # | 來源 | 意見（一句話） | 修／不修（為什麼）／問教授 | 怎麼修 | 改了哪裡 |
|---|---|---|---|---|---|
| 1 | self-1／partner-1 | | | 改寫／再分析／新實驗 | |

- **怎麼修分三種**：改寫（主張講太強、讀不懂）、用現有的 run 再分析（seed 之間的差異、顯著性檢定、按條件拆開的錯誤分析）、新實驗。再分析通常比新實驗便宜得多，而且修得掉很多「可不可信」的問題，先想這一種
- **改寫只能修「講太強」，修不了實驗本身的缺陷。** baseline 不公平、資料洩漏，改句子沒用，要問教授
- 不修的寫理由。兩個人都誤讀的地方是寫作的問題，要改

### 8.4 交教授前的檢查清單

- [ ] `grep -rnE 'NEEDNUM|NEEDCITE' paper/sections paper/tables` 沒有輸出
- [ ] 論文裡每個數字在 `results/index.md` 都有一行；隨機抽 5 行回 `results.csv` 對
- [ ] 每個 `\cite` 你都讀過；BibTeX 都從出版方來；有正式版的不是 arXiv 版
- [ ] 摘要、引言、結論並排過（§6.6），沒有超過結果
- [ ] 每個錯誤率的改善都寫了絕對或相對
- [ ] 投稿規定表逐行對過：頁數（看編譯出來的 PDF）、必要章節與順序、checklist、AI 聲明
- [ ] 匿名（§7.4）
- [ ] 沒用 §7.3 的擠版手法
- [ ] `build/main.log` 沒有 undefined reference、undefined citation
- [ ] `reviews/triage-1.md` 每一條都有結論
- [ ] `ai_use.md` 是最新的

**截稿前 10 天交教授**（日期由教授定），附 PDF、`plan.md`、`reviews/triage-1.md`。之後教授接手最後一輪修改與投稿；你負責回答問題、補教授要的分析、填 checklist。

---

## 9. 投出去之後

- 投稿由教授送出。投出去的版本在你的 repo 打一個 tag（例如 `submitted-icml2027`），之後的修改才分得清楚
- arXiv：放不放、什麼時候放由教授定；放之前清掉 LaTeX 註解（§6.2）
- 審稿回來：一位審稿人一個檔，放 `paper/reviews/1/R1.md`、`R2.md`⋯；48 小時內做[審稿對帳](../../conventions/review_reconciliation.md)。rebuttal 由教授主導，你準備每條意見對回哪一節、哪一張表，要補實驗的話補不補得完。只承諾做得到的
- 被拒、改投別的會議：回 §2.1 重做投稿規定表——換會議就是換規定
- 被接受：camera-ready（去匿名、加致謝與經費、用掉多給的那一頁、紅字 0）的分工由教授告訴你

---

## 10. 示例

> **以下全部是示例**，延續第 2 站 §7 的 contextual biasing STT。數字、方法名稱都是虛構的，只示範格式。

**主張–證據表的一列**（示例）

你想寫：

> "Our method substantially reduces biased-word errors and generalizes across domains."

證據：LibriSpeech test-other，單一 seed；B-WER 從 attention-based deep biasing 的 10.8% 降到 9.2%；U-WER 從 6.1% 到 6.2%；只有一個語料。

| # | 主張 | 證據 | 現在有嗎 | 用詞等級 | 要更強需要什麼 |
|---|---|---|---|---|---|
| C1 | On LibriSpeech test-other, the pronunciation-aware encoder reduces B-WER from 10.8% to 9.2% (1.6 absolute, 14.8% relative) over attention-based deep biasing, while U-WER moves from 6.1% to 6.2%. | tab:main，deep biasing 與 Ours 兩列 | 有（單 seed） | improves over | substantially：3 seeds，差距是 spread 的好幾倍；generalizes：第二個錄音條件不同的語料 |

"generalizes across domains" 進「這篇不講的主張」，除非教授決定補第二個語料。

**大綱 → AI 草稿 → 核對**（示例）

大綱：

```latex
% P1 重點：改善隨 bias list 變長而變大 | 證據：fig:listsize
```

AI 草稿：

> "The advantage of the pronunciation-aware encoder grows with bias list size (Figure~\ref{fig:listsize}): the B-WER gap is 0.1 absolute at 10 entries, 0.9 at 100 and 2.3 at 1,000. This is because the encoder disambiguates acoustically similar entries, which matters more as the list grows."

核對：

- 第一句和大綱一致 ✓
- 0.1、0.9、2.3 在 `index.md` 都有一行 ✓
- 第二句是 AI 補的機制，你沒有實驗證明 ✗。照指令它應該標成 [NEW]，它沒標，是你核對時抓到的。你的選擇：把錯誤分析的同音詞類別按 list 長度拆開，有支持就留下並指到那張表；沒有就刪掉，或在分析節寫成 "We hypothesize that…" 並說明要什麼實驗驗證。「為什麼」本來就是你自己寫的那一段（§6.1）

**一段改寫前後**（示例）

改寫前（重點在最後一句）：

> "We evaluate three bias list sizes. With 10 entries, both systems perform similarly. With 100 entries, the gap is 0.9 absolute. With 1,000 entries, the gap reaches 2.3 absolute. Thus, the advantage of our encoder grows with list size."

改寫後就是上面草稿的第一句：重點先講，數字當證據跟在後面；"both systems perform similarly" 這種模糊的話換成數字（0.1）。

---

## 11. 怎麼核對

這一站的核對都要你親手做：

1. **數字**：`index.md` 每一行回 `results.csv` 對；算出來的數字用程式重算
2. **引用**：每個 `\cite` 打開原文，找到你引用它說的那件事；BibTeX 的作者、年份、會議對出版方頁面
3. **主張**：§6.6 的並排表，每條對到一張表的一列
4. **AI 起草的每一段**：第一句對大綱；每個數字在 `index.md`；[NEW] 每一條都決定過，沒標 [NEW] 的也要自己找（§10 的例子）
5. **AI 冷讀的每一條**：它引用的原文在 PDF 裡找得到

AI 可以幫你列表、並排、挑用詞的毛病；AI 不能替你開論文對引用，不能替你對數字。

---

## 11b. 審稿人會怎麼看這一站的產出

這一站的產出就是審稿人讀的東西本身。審稿表單上扣分的地方，這份教材各有一節在防（表單欄位每個會議、每一屆不同，以當屆的 reviewer guidelines 為準）：

| 審稿人寫 | 落在表單哪一欄 | 哪一節防 |
|---|---|---|
| 摘要講的比結果多 | soundness | §3.3、§6.6 |
| 寫 "substantially"，表上差 0.3 | soundness | §3.1 |
| 8% 是絕對還是相對？ | soundness、clarity | §3.2 |
| baseline 數字是抄的，條件不同 | soundness | §3.2、第 2 站 §3.3 |
| 這段讀了兩遍還是不懂 | clarity；ARR 沒有單獨的表達分數，寫不清楚會扣在 Soundness 與 Excitement | §5、§6.4、§8.2 |
| 引用錯、引 toolkit 不引方法、引用的論文沒說這件事 | quality of references | §1.2 |
| 為什麼有效、什麼時候無效？ | excitement、contribution | §4.2 的分析、第 2 站 §2.3 |
| 重做不出來 | reproducibility | §4.2 的實驗設定 |
| Limitations 敷衍 | ARR 表單有單獨一欄 | §4.2 |
| interesting but domain-specific | contribution（ML 主會） | §4.3 |
| 不送審直接退：超頁、擠版、匿名、checklist、沒聲明 AI | — | §2.1、§7.3、§7.4、§8.4 |

---

## 12. 要問教授的事

帶著 `venue.md` 和 `plan.md` 去問，不要空手問。

| 問題 | 什麼時候問 |
|---|---|
| 目標會議、哪一屆、長論文還是短論文？ | 動筆前（第 1 站定過的確認一次） |
| 作者名單與順序？ | 動筆前 |
| `plan.md` 的主張–證據表與篇幅預算審過了嗎？ | 動筆前；審核紀錄沒有教授的一行不寫正文 |
| 交全文是哪一天？（預設截稿前 10 天） | 動筆前 |
| 用哪個平台編輯與協作？拼字用美式還是英式？ | 動筆前 |
| 主張撐不住：補實驗、降用詞，還是砍？ | `plan.md` 有「證據現在有嗎＝沒有」的時候 |
| seed 數與顯著性（投 ML 主會時尤其要問） | 寫實驗設定前；第 2 站問過的照舊 |
| 程式碼、資料、demo 要不要公開？ | 寫實驗設定前（影響匿名與 checklist） |
| 超頁砍哪裡？ | 修剪到「砍內容」那一步時 |
| AI 冷讀或 partner 的意見裡，要新實驗或拿不定修不修的那幾條 | 處理意見時（§8.3） |
| arXiv 放不放、什麼時候放？ | 投稿前 |
| AI 使用聲明怎麼寫？ | 交全文時，附 `ai_use.md` |
| 產學：產業方資料的結果能不能寫、怎麼寫；投稿前要給產業方看多久 | 動筆前；見產學分支 §3.3、§8 |

---

## 修改紀錄

### v1（2026-10-22）
- 初版。取材自教授的論文寫作協定，改寫成學生版：數字與引用的規則、紅字佔位、用詞等級、主張鏈、由內往外的寫作順序、各節任務、段落與句子、不要用的字、中文母語者的錯誤、LaTeX 與擠版禁令、投稿規定表、AI 冷讀
- 使用者定：學生寫段落大綱（用 LaTeX 註解寫在節檔），AI 起草、學生逐句核對；分析的「為什麼」與 Limitations 學生自己寫；教材自成一體；學生寫到內部審過，截稿前 10 天交教授，之後教授接手；預設長論文，4 頁照 §4.3 修剪
- 範本 repo 加 `paper/` 骨架（`README.md`、`placeholders.tex`、`venue.md`、`plan.md`、`results/index.md`、`ai_use.md`、`sections/`、`tables/`、`figures/`、`reviews/`）與 `notes/writing_errors.md`
