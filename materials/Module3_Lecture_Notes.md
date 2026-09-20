用 n8n 實現 Agentic AI System — 上課講義（14小時版）

# Module 3｜MCP Server/Client 整合實作

*課程時數：2 小時*

## 學習目標

- 理解 MCP（Model Context Protocol）的設計目的與運作模式
- 能比較 MCP 與直接 API 呼叫（HTTP Request Tool）的差異
- 能將既有工具透過 MCP Server 對外暴露

## 專有名詞說明

| 名詞 | 說明 |
| --- | --- |
| **MCP（Model Context Protocol）** | 一套開放協定，用於標準化 AI 應用（Client）與外部工具／資料來源（Server）之間的溝通方式，讓工具可以被不同 AI 應用共用而不必重複開發串接程式。 |
| **MCP Server** | 對外暴露一組工具（含名稱、描述、輸入 Schema）供 AI 應用呼叫的服務端程式。 |
| **MCP Client** | n8n 中的 MCP Client Tool 節點，負責連接 MCP Server、列出並呼叫其暴露的工具。 |
| **Input Schema** | MCP 工具規格中定義輸入參數結構的部分，功能上與 HTTP Request Tool 的 Schema 類似，但格式標準化。 |
| **標準化（Standardization）** | MCP 的核心價值主張——同一個工具實作一次，即可被多個不同的 Agent 應用重複使用，無需為每個應用客製一次串接邏輯。 |

## 詳細說明

### 一、為什麼需要 MCP

在 Module 2 中，我們透過 HTTP Request Tool 直接呼叫一個自建的模擬 API，這種做法簡單直接，但有明顯限制：每個 Agent 應用都得重新設定一次工具描述與 Schema；工具邏輯若要被多個專案共用，就得複製貼上或各自維護；缺乏統一的權限與版本管理機制。MCP 的出現就是為了解決這類「重複造輪子」與「難以共用」的問題——工具只需要在 MCP Server 端實作與暴露一次，任何支援 MCP 協定的 AI 應用（不限 n8n）都能直接發現並呼叫。

### 二、MCP 的架構：Client-Server 模式

MCP 採用 Client-Server 架構：MCP Server 負責定義並執行實際的工具邏輯（如查訂單、查庫存、查 FAQ），並以標準化的方式描述每個工具的名稱、用途與輸入格式；MCP Client（在 n8n 中即為 MCP Client Tool 節點）負責連線到 Server、列出可用工具，並將其掛載到 Agent 身上，讓 Agent 像使用一般 Tool 一樣呼叫它們。

### 三、MCP vs 直接 API 呼叫的比較

兩者在「讓 Agent 能查到資料」這件事上效果相同，差異主要在維護面：直接 API 呼叫的設定與工具描述綁定在單一 workflow 中，難以重複使用；MCP 的工具定義與實作集中在 Server 端，一次修改、所有 Client 端受益，跨專案、跨 Agent 共用的維護成本明顯較低。因此，當工具需要被多個 Agent 或多個專案共用時，優先考慮 MCP；若只是單一 workflow 內的一次性需求，直接 API 呼叫仍然是更輕量的選項。

### 四、何時導入 MCP

實務上的判斷原則是：工具的重用需求越高、供多個團隊或多個 Agent 共用的機率越大，就越值得投入建置 MCP Server 的初期成本；反之，若只是暫時性、實驗性的單一用途，直接 API 呼叫仍然是合理的起點——這也呼應 Module 1「先簡單、後複雜」的漸進式架構設計原則。

## 與投影片／練習步驟對照

本模組對應 Module 3 投影片（5 張：觀念、與直接 API 呼叫比較、Server 端工具介紹、LAB）與《Exercise_Steps_Handbook.md》Module 3 章節，並可參考《Exercise_Steps_Handbook.md》所附的 System Prompt 調整重點，理解在新增 MCP 工具時 System Prompt 該如何最小幅度調整。

*本檔為《用 n8n 實現 Agentic AI System》課程 Module 3 的上課講義（Markdown 版，內容與 Module3_Lecture_Notes.docx 相同），搭配投影片與《Exercise_Steps_Handbook.md》（或 Module3_Exercise_Steps.docx／.md）一起使用；完整教材包請參閱 README.md。*
