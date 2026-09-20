用 n8n 實現 Agentic AI System — 上課講義（14小時版）

# Module 2｜Single Agent 實作：Tool Invocation 與 Memory Management

*課程時數：3 小時*

## 學習目標

- 理解 Tool Invocation（工具呼叫）的運作原理
- 能設計清楚的工具描述（Tool Description）與輸入 Schema
- 理解 Memory 機制如何讓 Agent 維持多輪對話脈絡
- 認識「幻覺」問題並學會用工具強制 Grounding

## 專有名詞說明

| 名詞 | 說明 |
| --- | --- |
| **Tool / Function Calling（工具呼叫）** | LLM 根據使用者輸入與工具描述，自主判斷是否需要、以及該呼叫哪一個外部工具，並自動組裝呼叫參數的機制。 |
| **Tool Schema（工具輸入結構）** | 定義一個工具需要哪些輸入參數、型別與是否必填的規格，讓 LLM 知道如何正確組裝呼叫請求。 |
| **Chat Trigger** | n8n 中作為對話入口的節點，接收使用者的訊息。 |
| **AI Agent 節點** | n8n 中承載 LLM 推理迴圈的核心節點，負責串接 Chat Model、Tool、Memory 三種子元件。 |
| **HTTP Request Tool** | 以呼叫外部 HTTP API 的方式實作的工具類型，是最基礎、最常見的 Tool 實作方式。 |
| **Memory（記憶）／Window Buffer Memory** | 讓 Agent 記得先前對話內容的機制，Window Buffer Memory 只保留最近 N 輪對話，避免上下文過長。 |
| **Grounding（落地／根據事實）** | 強制 Agent 的回答必須根據工具回傳的真實資料，而非憑 LLM 自身訓練知識或機率猜測作答。 |
| **Hallucination（幻覺）** | LLM 在缺乏真實依據時，生成看似合理但實際錯誤或憑空捏造的內容，是 Agent 系統最需要防範的風險之一。 |

## 詳細說明

### 一、Tool Invocation 的運作原理

當 Agent 收到使用者訊息後，LLM 會根據 System Prompt 中的角色設定與掛載工具的描述（Tool Description）與 Schema，判斷「這個問題是否需要呼叫工具」以及「該呼叫哪一個工具、帶入哪些參數」。這個判斷完全依賴工具描述寫得是否清楚：描述越明確（例如「查詢訂單狀態，輸入訂單編號，回傳狀態、品項與到貨日；查無此訂單會回傳 found=false」），LLM 就越能正確判斷呼叫時機與方式。這也是為什麼本課程在 Module 2 的練習中特別強調工具描述的撰寫細節。

### 二、為什麼需要 Memory

真實的客服對話往往是多輪的：顧客先問「我的訂單到了嗎」，接著追問「那大概什麼時候到」，這時 Agent 必須記得上一輪提到的訂單編號，否則就需要顧客不斷重複輸入。Window Buffer Memory 這類機制讓 Agent 在有限的視窗內（例如最近 5 輪）保留對話歷史，兼顧脈絡連貫性與 Token 成本控制。

### 三、對抗幻覺：用工具結果強制 Grounding

LLM 在沒有明確資料依據時，容易「編」出一個聽起來合理但錯誤的答案（例如編造一個不存在的到貨日期）。防範方法是在 System Prompt 中明確規定「所有訂單資訊必須透過工具取得，不可以憑記憶或猜測回答」，並且明確定義工具查無資料時（found=false）該如何誠實回應，而不是讓 LLM 自由發揮。這也是 Module 2 練習中「查無資料情境」測試案例存在的原因——刻意驗證 Agent 在缺乏資料時是否會說謊。

### 四、錯誤處理設計

工具呼叫本身也可能失敗（逾時、服務中斷等），一個成熟的 Agent 系統需要在 System Prompt 或工具描述中明確定義失敗時的因應方式（如實告知系統暫時無法查詢），而不是讓 Agent 假裝呼叫成功或給出錯誤資訊。

## 與投影片／練習步驟對照

本模組對應 Module 2 投影片（7 張，含 Tool 與 Memory 兩組觀念＋範例對照頁）與《Exercise_Steps_Handbook.md》Module 2 章節；並可對照《Exercise_Steps_Handbook.md》Module 2 小節所附的 System Prompt 範例動手實作。

*本檔為《用 n8n 實現 Agentic AI System》課程 Module 2 的上課講義（Markdown 版，內容與 Module2_Lecture_Notes.docx 相同），搭配投影片與《Exercise_Steps_Handbook.md》（或 Module2_Exercise_Steps.docx／.md）一起使用；完整教材包請參閱 README.md。*
