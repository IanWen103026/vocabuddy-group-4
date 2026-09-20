# VocaBuddy — pmπ隊（第 4 組）

## 小組名稱

pmπ隊｜第 4 組（vocabuddy-group-4）

## 組員

| 姓名  | GitHub 帳號                                              | 角色               |
| --- | ------------------------------------------------------ | ---------------- |
| 温世揚 | [@IanWen103026](https://github.com/IanWen103026)       | Repository Owner |
| 翁浩洋 | [@lucasw0908](https://github.com/lucasw0908)           | Developer A      |
| 周裕閎 | [@Watermelon-1234](https://github.com/Watermelon-1234) | Developer B      |
| 鄭向晴 | [@LilyKensa](https://github.com/LilyKensa)             | Developer C      |
| 李承修 | [@LucasLee1221](https://github.com/LucasLee1221)       | Reviewer         |

## 專案簡介

VocaBuddy 是一個使用 Python 撰寫的英文單字學習工具，可在 Google Colab 上執行。

使用者可以透過單字庫進行單字學習與測驗。程式會記錄每個單字的答對與答錯次數，並根據學習紀錄提供正確率、錯題複習與弱項單字等功能。

## 組員分工

1. **温世揚 @IanWen103026（Repository Owner）**：建立 GitHub Repository、邀請 Collaborators、建立 `VocaBuddy.ipynb` 初版
2. **翁浩洋 <@827412318157013002>908（Developer A）**：新增英文單字與中文解釋，建立單字資料
3. **周裕閎 @Watermelon-1234（Developer B）**：新增隨機單字與分類測驗功能
4. **鄭向晴 @LilyKensa（Developer C）**：新增學習紀錄、正確率統計與錯題複習功能
5. **李承修 @LucasLee1221（Reviewer）**：新增弱項單字功能、整理程式與 README，檢查 GitHub commit 紀錄

## 本次新增的單字

本次新增 4 個英文單字：

| 英文單字       | 中文解釋 | 分類 |
| ---------- | ---- | -- |
| startfruit | 楊桃   | 水果 |
| mouse      | 老鼠   | 動物 |
| dog        | 狗    | 動物 |
| cat        | 貓咪   | 動物 |

## 本次新增的功能

* **學習紀錄**：記錄每個單字答對與答錯的次數。
* **正確率統計**：統計整體及個別單字的答題正確率。
* **錯題複習**：列出曾經答錯過的單字，方便重新複習。
* **弱項單字**：根據答題紀錄找出正確率較低、需要加強的單字。
* **隨機單字**：從單字庫中隨機抽取單字進行學習。
* **分類測驗**：可以選擇指定分類進行單字測驗。
* **新增單字**：可以自行加入新的英文單字、中文解釋與分類。
* **刪除單字**：可以刪除單字庫中不需要的單字。

## Google Colab 開啟連結

https://colab.research.google.com/github/IanWen103026/vocabuddy-group-4/blob/main/VocaBuddy.ipynb

## Repository

https://github.com/IanWen103026/vocabuddy-group-4

## 程式執行方式

1. 點擊上方的 Google Colab 連結開啟 `VocaBuddy.ipynb`
2. 選擇上方選單的「執行階段」→「全部執行」
3. 程式會建立 VocaBuddy 單字庫。
4. 可以查看單字總覽與分類。
5. 可以進行隨機單字學習。
6. 可以選擇分類進行單字測驗。
7. 完成測驗後會更新學習紀錄與正確率。
8. 可以查看錯題及需要加強的弱項單字。

## 單字資料格式

新增單字時，可以使用 `add_word()`：

```python
add_word("apple", "蘋果", "水果")
```

程式會自動將單字加入指定分類。

## 學習紀錄

VocaBuddy 會記錄每個單字的答題狀況。

例如：

```text
apple
正確：5 次
錯誤：2 次
正確率：71.4%
```

這些紀錄可以用來找出需要複習的單字。

## 錯題與弱項複習

程式會保留答錯紀錄，並提供錯題複習功能。

另外，也會根據每個單字的答題正確率找出較不熟悉的單字，讓使用者可以優先複習。

## 專案目標

VocaBuddy 希望將原本單純的單字測驗，加入學習紀錄與錯題分析，讓使用者可以更方便地了解自己的學習狀況。