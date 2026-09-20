用 n8n 實現 Agentic AI System — 上課講義（14小時版）

# Module 1｜從聊天工具到 Agentic AI：n8n Agent 架構總覽

*課程時數：1.5 小時*

## 學習目標

- 理解「聊天機器人」與「Agentic AI」的本質差異
- 認識 n8n 作為 Agent 編排引擎的核心元件
- 能運用課堂決策框架判斷該用 Single Agent 或 Multi-Agent

## 專有名詞說明

| 名詞 | 說明 |
| --- | --- |
| **Agent（代理）** | 能感知輸入、自主決策、呼叫外部工具並根據結果採取下一步行動的 AI 程式，不同於單純一問一答的聊天機器人。 |
| **Agentic AI** | 強調 AI 系統具備自主性（autonomy）、工具使用（tool use）與多步驟推理（multi-step reasoning）能力的一類系統設計典範。 |
| **LLM（大型語言模型）** | 如 GPT、Claude 等，作為 Agent 的「大腦」，負責理解輸入、規劃步驟、產生回應。 |
| **Orchestration（編排）** | 協調多個步驟、工具、資料來源共同完成一項任務的過程；n8n 即扮演此編排引擎角色。 |
| **Workflow（工作流程）** | n8n 中由節點（Node）串接而成的自動化流程，是 Agent 運行的容器。 |
| **Single Agent** | 由單一個 AI Agent 節點負責理解與回應所有使用者需求的架構。 |
| **Multi-Agent** | 由多個各司其職的 Agent 協作完成任務的架構，通常搭配一個路由／協調者。 |
| **System Prompt** | 賦予 Agent 角色、規則與行為邊界的一段固定指令，是控制 Agent 行為最重要的機制。 |

## 詳細說明

### 一、從聊天機器人到 Agentic AI 的演進

傳統聊天機器人（Chatbot）多半是「輸入 → 產生文字回覆」的單向流程，本質上是一問一答，無法查詢真實資料、無法執行動作，也無法在多輪對話中維持脈絡。Agentic AI 的關鍵差異在於三件事：（1）能呼叫外部工具取得即時資料或執行動作（Tool Invocation）；（2）能在多輪對話中維持記憶（Memory）；（3）能根據中間結果自主規劃下一步（多步推理）。本課程將帶大家從最基礎的單一 Agent 開始，逐步疊加這三項能力。

### 二、n8n 作為 Agentic AI 的編排引擎

n8n 提供 AI Agent 節點作為 LLM 推理的容器，並透過視覺化的 Workflow 將 Chat Trigger、Tool、Memory 等元件串接起來。相較於直接寫程式呼叫 LLM API，n8n 的優勢在於：可視化除錯、豐富的內建節點（HTTP Request、資料庫、試算表等），以及低程式碼的維護門檻，非常適合快速搭建與迭代 Agent 系統雛形。

### 三、架構決策框架：Single Agent 還是 Multi-Agent？

並非一開始就需要複雜的多代理架構。課堂提供的判斷框架建議先問三個問題：（1）目前的任務職責是否單一、邊界清楚？（2）是否需要平行處理多種截然不同的專業領域？（3）系統的規模與維運複雜度目前是否能負荷多代理的除錯與監控成本？以本課程貫穿範例「全通路智慧客服與工單處理系統」為例，Module 1～3 先以 Single Agent 處理訂單查詢類問題，直到 Module 4 才依實際需求（訂單 vs 退款兩種截然不同的職責）拆分為 Multi-Agent，這正是「先簡單、後複雜」的漸進式架構設計原則的實踐。

### 四、全通路智慧客服範例導入

本課程從 Module 1 到 Module 7，都圍繞同一個情境：一家中型電商／SaaS 公司要用 n8n 打造能自動回覆顧客問題、查詢訂單狀態、處理退換貨，並在複雜案件時轉真人客服的智慧客服系統。每個模組會在同一套系統上疊加一項新能力，最終在 Module 7 整合為完整的 Capstone 成果。建議在課堂一開始就對照練習步驟手冊，理解每個模組「新增了什麼」、「為什麼在這個階段新增」。

## 與投影片／練習步驟對照

本模組對應 Module 1 投影片（5 張：觀念總覽、模式深化、架構決策、LAB 提示）與《Exercise_Steps_Handbook.md》Module 1 章節（動手畫出第一版架構圖）。建議課堂講解本講義的「詳細說明」段落後，直接銜接練習步驟的動手練習。

*本檔為《用 n8n 實現 Agentic AI System》課程 Module 1 的上課講義（Markdown 版，內容與 Module1_Lecture_Notes.docx 相同），搭配投影片與《Exercise_Steps_Handbook.md》（或 Module1_Exercise_Steps.docx／.md）一起使用；完整教材包請參閱 README.md。*
