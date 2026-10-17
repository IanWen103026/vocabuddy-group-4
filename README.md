# VocaBuddy — Vocabulary-Go

VocaBuddy 是一個使用 Python、Gradio 製作的英文單字學習工具，可在 Google Colab 上執行。使用者可以管理分類單字、匯入與匯出 CSV，並透過單字測驗、AI 例句和句子挖空練習加強英文能力。

本專案不需要另外建立後端伺服器；主要功能與介面都在 [VocaBuddy.ipynb](VocaBuddy.ipynb) 中實作。

## 小組名稱

pmπ隊｜第 4 組（vocabuddy-group-4）

## 組員

| 姓名   | GitHub 帳號                                           | 角色             |
| ------ | ----------------------------------------------------- | ---------------- |
| 温世揚 | [@IanWen103026](https://github.com/IanWen103026)       | Repository Owner |
| 翁浩洋 | [@lucasw0908](https://github.com/lucasw0908)           | Developer A      |
| 周裕閎 | [@Watermelon-1234](https://github.com/Watermelon-1234) | Developer B      |
| 鄭向晴 | [@LilyKensa](https://github.com/LilyKensa)             | Developer C      |
| 李承修 | [@LucasLee1221](https://github.com/LucasLee1221)       | Reviewer         |

## 組員分工

1. **温世揚 @IanWen103026（Repository Owner）**：建立 GitHub Repository、邀請 Collaborators、建立 `VocaBuddy.ipynb` 初版
2. **翁浩洋 @lucasw0908（Developer A）**：新增英文單字與中文解釋，建立單字資料
3. **周裕閎 @Watermelon-1234（Developer B）**：新增隨機單字與分類測驗功能
4. **鄭向晴 @LilyKensa（Developer C）**：新增學習紀錄、正確率統計與錯題複習功能
5. **李承修 @LucasLee1221（Reviewer）**：新增弱項單字功能、整理程式與 README，檢查 GitHub commit 紀錄

## 主要功能

- **單字庫管理**：依分類查看英文、中文、例句及答題紀錄。
- **新增與刪除單字**：手動新增英文單字、中文解釋和分類，也可以刪除單字。
- **學習統計**：統計單字總數、答對次數、答錯次數、整體正確率及分類分佈。
- **CSV 匯入**：支援選取 CSV 檔案或直接貼上 CSV 文字，並可指定匯入分類。
- **CSV 匯出**：將目前完整單字庫匯出成含有 `English`、`Chinese`、`Category` 欄位的 CSV 檔案。
- **AI 例句**：使用 Groq API 為單字產生簡短英文例句及繁體中文翻譯；已經有例句的單字會略過。
- **句子挖空測驗**：將例句中的目標單字挖空，根據中文翻譯和句子線索作答。
- **分類測驗**：可選擇全部單字或指定分類，並設定 1 至 20 題。
- **答題回饋**：提交答案後顯示答對或答錯、正確答案、完整原句及本次正確率。
- **離線備援題目**：Groq API 未設定或生成失敗時，使用內建英文範例句完成測驗。
- **獨立挖空工具**：輸入任意英文句子和目標單字，即可查看挖空結果、最佳匹配字詞和相似度。

## 內建單字

程式啟動時會建立 8 個內建單字，分成「水果」和「核心單字」兩個分類：

| 分類     | 英文單字        | 中文解釋       |
| -------- | --------------- | -------------- |
| 水果     | `apple`       | 蘋果           |
| 水果     | `banana`      | 香蕉           |
| 水果     | `orange`      | 橘子           |
| 核心單字 | `abandon`     | 放棄；遺棄     |
| 核心單字 | `accomplish`  | 完成；實現     |
| 核心單字 | `demonstrate` | 證明；展示     |
| 核心單字 | `innovation`  | 創新；變革     |
| 核心單字 | `brilliant`   | 傑出的；燦爛的 |

新增或匯入的單字會直接加入目前的 `VocabularyManager` 單字庫，並保留答對、答錯及已生成例句等資料。

## Google Colab 開啟連結

[在 Google Colab 開啟 VocaBuddy.ipynb](https://colab.research.google.com/github/IanWen103026/vocabuddy-group-4/blob/main/VocaBuddy.ipynb)

## 程式執行方式

1. 點擊上方連結開啟 `VocaBuddy.ipynb`。
2. 在 Colab 依序執行所有儲存格，或選擇「執行階段」→「全部執行」。
3. 第一個安裝儲存格會安裝 `httpx` 和 `opencc-python-reimplemented`；Gradio 介面儲存格會安裝 `gradio` 和 `pandas`。
4. 執行完成後，在最後一個儲存格啟動 Gradio 介面。
5. 若要使用 AI 例句，於登入頁輸入 Groq API Key，按「驗證並進入」。
6. 進入主畫面後，可從「單字庫」、「匯入 / 匯出」、「AI 例句」、「開始測驗」和「挖空工具」分頁使用功能。

> API Key 僅應輸入在自己的 Colab 工作階段中，請勿將金鑰寫入 Notebook 或提交至 GitHub。

## Groq AI 例句

AI 例句功能會呼叫 Groq 的 OpenAI 相容 Chat Completions API：

- API 端點：`https://api.groq.com/openai/v1/chat/completions`
- 預設模型：`qwen/qwen3.8-27b`
- 請求逾時：20 秒
- 每個單字最多嘗試生成 3 次
- 回應格式為「英文例句｜繁體中文翻譯」
- 程式會使用 OpenCC 將翻譯轉換為繁體中文，並檢查目標單字在英文句子中的相似度是否至少為 `0.45`

也可以在執行前透過環境變數提供金鑰：

```python
import os
os.environ["GROQ_API_KEY"] = "gsk_..."
```

如果金鑰無效、請求受到限制、連線失敗或模型沒有產生有效格式，程式會顯示錯誤，測驗則改用離線備援句：

```text
This is an example sentence featuring the word apple.
```

## 句子挖空演算法

`BlankifyEngine` 會先在句子中尋找與目標單字或片語最相似的文字，再將符合的位置挖空：

- 使用 `SequenceMatcher` 計算文字相似度。
- 支援單字及多字片語的連續比對。
- 找不到高相似度結果時，會進行包含關係的備援搜尋。
- 短字、介系詞會顯示為 `___`。
- 一般較長單字會保留首尾字母，例如 `demonstrated` 會顯示為 `d____d` 的形式。
- 挖空時會保留原句標點符號。

## 單字管理

手動新增單字時，會自動移除前後空白並將英文轉為小寫；未填寫分類時使用「預設」分類。若同分類中已有相同英文單字，會更新該單字的中文解釋。

```python
vocab_manager.add_word("apple", "蘋果", "水果")
vocab_manager.add_word("practice", "練習", "自訂")
```

刪除時可以指定分類；若沒有指定分類，會從所有分類刪除相同英文單字。

## CSV 匯入與匯出

匯入可使用檔案路徑或 CSV 文字，預設欄位順序為英文、中文，也能辨識常見表頭：

```csv
English,Chinese
apple,蘋果
practice,練習
```

程式可辨識逗號或第一行含有 Tab 的資料，也支援 UTF-8、UTF-8 BOM、Big5、CP950 和 GBK 編碼的檔案。匯入時可指定分類，空白資料列會被略過。

匯出結果預設為 `vocabulary_export.csv`，內容包含：

```csv
English,Chinese,Category
apple,蘋果,水果
```

## 測驗流程與紀錄

1. 在「開始測驗」選擇分類及題數。
2. 系統隨機抽取題目；每題會優先使用已快取的例句。
3. 閱讀中文翻譯與挖空句子，輸入英文單字後提交答案。
4. 答對或答錯後，系統顯示結果和完整原句，再按「下一題」繼續。
5. 測驗結束後顯示總題數、答對數、答錯數及本次正確率。

每個單字會保存：

| 欄位         | 說明                                 |
| ------------ | ------------------------------------ |
| `chinese`  | 中文解釋                             |
| `correct`  | 答對次數                             |
| `wrong`    | 答錯次數                             |
| `sentence` | 已生成的例句、挖空句、翻譯及比對資訊 |

目前的學習紀錄存在 Notebook 執行中的記憶體中；重新啟動執行階段後，單字變更、答題統計和例句快取會重設為初始資料。

## 專案檔案

| 檔案                                  | 用途                                                                               |
| ------------------------------------- | ---------------------------------------------------------------------------------- |
| [`VocaBuddy.ipynb`](VocaBuddy.ipynb) | 安裝套件、單字庫核心、挖空演算法、Groq 例句生成器、SentenceQuiz 和 Gradio 使用介面 |
| [`README.md`](README.md)             | 專案介紹、功能、執行方式和資料格式說明                                             |

## Repository

https://github.com/IanWen103026/vocabuddy-group-4
