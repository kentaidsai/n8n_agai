用 n8n 實現 Agentic AI System — 上課講義（14小時版）

# Module 6｜Observability 與 Evaluation

*課程時數：1.5 小時*

## 學習目標

- 理解 Observability（可觀測性）對維運 Agent 系統的重要性
- 能設計自動化評估流程並解讀通過率報表
- 認識 LLM-as-judge 評估方法的優缺點

## 專有名詞說明

| 名詞 | 說明 |
| --- | --- |
| **Observability（可觀測性）** | 系統能被完整追蹤、記錄、檢視其內部運作狀態（如呼叫了哪些工具、耗時多久、是否觸發護欄）的能力。 |
| **Execution Log（執行紀錄）** | n8n 中記錄每次 workflow 執行細節（節點呼叫鏈、輸入輸出、耗時）的功能，是 Observability 的基礎。 |
| **Evaluation Dataset（評估資料集）** | 一組包含輸入問題與預期正確行為（關鍵字或行為描述）的測試集合，用於系統化驗證 Agent 表現。 |
| **LLM-as-judge（LLM 作為裁判）** | 使用另一個 LLM 節點，依照語意而非逐字比對，判斷 Agent 的實際回覆是否符合預期重點的評估方法。 |
| **Pass Rate（通過率）** | 評估資料集中，Agent 回覆符合預期的題目佔全部題目的比例，是最常用的量化品質指標。 |
| **Regression Testing（回歸測試）** | 每次修改 Agent 的 Prompt 或工具設定後，重新執行整份評估資料集，確保既有功能沒有因改動而變差的做法。 |

## 詳細說明

### 一、為什麼需要 Observability

Agent 系統一旦上線，最怕的就是「不知道它在對話中做了什麼、為什麼做出這個回應」。Observability 讓開發者能回溯每一次對話呼叫了哪些工具、依序為何、各步驟耗時多久，是除錯與持續優化的基礎建設，也是 Module 5 護欄機制是否確實生效的驗證依據。

### 二、設計自動化評估流程

人工一題一題測試 Agent 既耗時又難以規模化，因此需要建置自動化評估 workflow：讀取事先準備好的評估資料集，逐題呼叫 Agent 取得回覆，再用規則比對或 LLM 裁判判斷是否通過，最後將結果彙整為報表。這個機制讓每次修改 Prompt 或工具設定後，都能快速得知「品質有沒有變差」，而不是憑感覺猜測。

### 三、LLM-as-judge：語意而非逐字比對

由於 LLM 的回覆用詞每次可能略有不同，單純比對關鍵字容易誤判。LLM-as-judge 的做法是另外設計一個「評審 Agent」，收到問題、Agent 實際回覆、與預期重點三項資訊後，判斷語意上是否滿足預期，並固定輸出結構化的 JSON 結果方便後續處理。這個方法的優點是能容忍用詞差異，缺點是評審本身也是 LLM，需要嚴格限制其判斷原則（尤其是安全性題目應該從嚴不從寬），否則可能因為 Agent 回覆得體而放水。

### 四、分類型解讀通過率、規劃回歸測試

通過率不該只看整體數字，而應依題型（功能性 vs 安全性、不同業務情境）分組統計，才能精準定位問題所在——例如整體通過率 85% 看似不錯，但若安全性題目通過率只有 60%，代表的風險遠比表面數字嚴重。長期而言，這份評估資料集應該被納入類似 CI/CD 的流程，每次修改 System Prompt 或工具設定後自動重跑，並建立版本比對機制，確保系統品質只會越改越好、不會不知不覺退步。

## 與投影片／練習步驟對照

本模組對應 Module 6 投影片（5 張：觀念、指標設計、評估資料集、LAB）與《Exercise_Steps_Handbook.md》Module 6 章節，並可參考《Exercise_Steps_Handbook.md》所附的 LLM 裁判 System Prompt 範例。

*本檔為《用 n8n 實現 Agentic AI System》課程 Module 6 的上課講義（Markdown 版，內容與 Module6_Lecture_Notes.docx 相同），搭配投影片與《Exercise_Steps_Handbook.md》（或 Module6_Exercise_Steps.docx／.md）一起使用；完整教材包請參閱 README.md。*
