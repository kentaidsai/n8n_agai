用 n8n 實現 Agentic AI System — 上課講義（14小時版）

# Module 4｜Multi-Agent 協作方法論與實作

*課程時數：2.5 小時*

## 學習目標

- 理解何時該將 Single Agent 拆分為 Multi-Agent
- 能設計 Router（路由判斷者）與子 Agent 的職責邊界
- 能用測試案例驗證路由正確率並持續優化

## 專有名詞說明

| 名詞 | 說明 |
| --- | --- |
| **Multi-Agent System（多代理系統）** | 由多個各自負責不同職責的 Agent 協作，共同完成單一 Agent 難以有效處理的複雜任務。 |
| **Router / Orchestrator（路由／協調者）** | Multi-Agent 架構中負責判斷使用者意圖、並將請求轉交給對應子 Agent 的角色，本身通常不直接回答業務問題。 |
| **Sub-agent（子代理）** | 職責範圍被刻意縮小、只專注單一領域任務的 Agent（如訂單 Agent、退款 Agent）。 |
| **Execute Workflow / Execute Workflow Trigger** | n8n 中用於讓一個 workflow 呼叫另一個 workflow 的機制，是實作 Router 轉交子 Agent 的技術基礎。 |
| **Single Responsibility（單一職責原則）** | 每個子 Agent 應只負責一件定義清楚的事，避免多個 Agent 之間職責重疊或互相搶答。 |
| **Handoff（轉交）** | Router 判斷完成後，將對話控制權與必要上下文轉交給對應子 Agent 的過程。 |

## 詳細說明

### 一、何時該拆分為 Multi-Agent

當單一 Agent 需要同時精通多種截然不同的業務領域（如訂單查詢的資料邏輯 與 退款政策的審核邏輯），System Prompt 會變得又長又複雜，容易顧此失彼、判斷準確率下降。這時候的解法不是把 Prompt 寫得更長，而是拆分職責：讓每個 Agent 只專注一個定義清楚的領域，並由一個 Router 負責判斷「這個問題該交給誰」。這正是 Module 4 要練習的核心方法論。

### 二、Router 的兩種設計模式

Router 可以用兩種方式實作：（1）用一個 AI Agent 節點做語意分類，System Prompt 明確限制只能輸出固定的幾個分類值之一（如 order_agent／refund_agent／general），避免它自己嘗試回答問題；（2）用 n8n 的 Switch 節點依關鍵字或規則直接路由，優點是速度快、成本低、行為完全可預測，缺點是難以應付語意複雜或多重意圖的訊息。實務上兩者可以搭配：先用 Switch 做粗篩，語意不明確的案例才交給 AI Router 細分。

### 三、子 Agent 的職責邊界設計

子 Agent 的 System Prompt 應該從原本 Single Agent 的骨架「裁切」而來，刻意縮小職責範圍，並且明確加入「這不是我的職責時該怎麼辦」的退場規則（例如訂單 Agent 遇到退款問題時，應告知「這部分將由退款專責窗口協助」而非自己嘗試處理）。這個退場規則正是避免子 Agent 之間互相搶答或掉球的關鍵設計。

### 四、用測試案例驗證與迭代路由正確率

Router 的判斷不會一次到位，需要用涵蓋各種情境（含邊界模糊案例）的測試集反覆驗證。本課程提供的 8 題路由測試案例中，特別包含「一般諮詢」與情緒性客訴等邊界情境，用意是訓練學員辨識「哪些問題不該勉強分類」，以及如何根據錯誤案例反推 System Prompt 或分類定義需要補強之處。

## 與投影片／練習步驟對照

本模組對應 Module 4 投影片（5 張：觀念、我們的架構、取捨分析、LAB）與《Exercise_Steps_Handbook.md》Module 4 章節，並可直接參考《Exercise_Steps_Handbook.md》所附的 Router／訂單 Agent／退款 Agent 三份 System Prompt 範例。

*本檔為《用 n8n 實現 Agentic AI System》課程 Module 4 的上課講義（Markdown 版，內容與 Module4_Lecture_Notes.docx 相同），搭配投影片與《Exercise_Steps_Handbook.md》（或 Module4_Exercise_Steps.docx／.md）一起使用；完整教材包請參閱 README.md。*
