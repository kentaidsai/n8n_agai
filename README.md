# 用 n8n 實現 Agentic AI System｜14 小時課程總覽

*Building Agentic AI Systems with n8n — 從 Single Agent 到 Multi-Agent 架構的實戰工作坊，14 小時完整整合 MCP、Guardrails、Observability 與 Evaluation。*

`Single → Multi-Agent` · `MCP Server/Client` · `Guardrails` · `Observability` · `Evaluation`

| 時數 | 模組數 | 建議天數 | 貫穿範例 |
| --- | --- | --- | --- |
| 14 小時 | 7 個 | 2 天 | 智慧客服 Agent |

---

## 課程目標

本課程是一堂以 n8n 為核心的實戰 LAB，目標是讓學員把 AI Agent 從「單一聊天機器人」升級為能自主呼叫工具、串接標準化協定（MCP）、多代理人協作、具備安全防護與可觀測性的企業級 Agentic AI 系統。

- **架構判斷**：判斷情境該用 Single 或 Multi-Agent，並說明理由
- **工具與記憶**：為 Agent 掛載工具、設計短期／長期記憶
- **MCP 整合**：建立並串接 MCP Server／Client，工具跨專案共用
- **多代理協作**：設計並實作 Router、Orchestrator-Worker 等協作系統
- **安全防護**：為系統加上 Guardrails，降低誤用與風險
- **監控與評估**：建立 Observability 與 Evaluation，持續改善品質

## 貫穿範例

全通路智慧客服與工單處理 Agent System — 全程以同一套系統為主線，從只會回答問題的 Single Agent，逐步疊加工具、記憶、MCP、多代理協作、安全防護與監控機制。

```
顧客訊息 → Router Agent → ┬ 訂單 Agent（查詢／退換貨）
                          ├ 退款 Agent（金額守門）
                          └ 技術支援 Agent（轉真人）
```

## 適合對象

- 已有 n8n 基本操作經驗，想進一步打造 AI Agent 自動化流程的自動化顧問與工程師
- 想將公司內部客服、工單、行政流程升級為 Agentic AI 系統的系統整合工程師
- 企業主管、PM、顧問，想評估 Agentic AI 導入可行性並建立可複製的架構藍圖
- 技術型專案經理，需要規劃 AI Agent 專案的架構、風險與驗收標準
- 已會使用 ChatGPT/Claude，想進一步學會 Multi-Agent、MCP、Guardrails 與 Evaluation 的學員
- 培訓經理與企業內訓規劃者，需設計 Agentic AI 相關課程
- 想導入標準化工具協定（MCP），讓多個 AI 專案共用工具的開發團隊
- RPA/流程自動化工程師，想將既有流程升級為具備推理與工具呼叫能力的 Agent

## 課程大綱

7 個模組，14 小時，一個貫穿範例。

| 模組 | 主題 | 時數 |
| --- | --- | --- |
| Module 1 | Agentic AI 基礎與架構設計方法論 | 1.5h |
| Module 2 | Single Agent 實作：Tool Invocation 與 Memory Management | 3h |
| Module 3 | MCP Server/Client 整合 | 2h |
| Module 4 | Multi-Agent 協作方法論與實作 | 2.5h |
| Module 5 | Guardrails 安全防護設計 | 1.5h |
| Module 6 | Observability 與 Evaluation | 1.5h |
| Module 7 | Architecture Design 與 Capstone 專題 | 2h |
| **總計** | | **14h** |

## 學會技能

1. 能說明 Agentic AI 與傳統 Workflow 自動化的差異，並解釋 ReAct、Plan-and-Execute、Reflection 等常見設計模式
2. 能判斷特定業務情境該用 Single Agent 或 Multi-Agent 架構，並說明理由
3. 能在 n8n 中為 Agent 掛載自訂工具，包含 HTTP Request Tool、Code Tool 與 Sub-workflow Tool
4. 能設計適當的短期與長期記憶機制，讓 Agent 記住對話脈絡與使用者偏好
5. 能說明 MCP 解決的問題，並在 n8n 中以 MCP Client 呼叫既有工具
6. 能將既有工具包裝為可跨專案共用的 MCP Server 雛形
7. 能說明 Router、Orchestrator-Worker、Hierarchical、Handoff 等 Multi-Agent 協作模式的差異
8. 能在 n8n 中實作具備路由與協調能力的多代理人協作系統
9. 能為 Agent 系統設計輸入與輸出 Guardrails，降低 Prompt Injection 與幻覺風險
10. 能設計業務規則守門（如金額上限）與 Human-in-the-loop 升級機制
11. 能為 Agent 系統建立執行紀錄與追蹤儀表板，監控呼叫鏈與 Token 成本
12. 能建立黃金測試資料集並設計自動化 Evaluation Workflow
13. 能評估不同架構設計在 Scalability、Cost、Latency 上的取捨
14. 能整合前述所有能力，產出一套完整的 Agentic AI 系統架構設計文件
15. 能將此課程的方法論與 workflow 範本，應用於客服以外的業務情境（如內部 IT 支援、供應商溝通、行政流程）

## 課前準備

請於上課前先完成下列帳號申請與軟體安裝，以利課堂 LAB 操作。

1. **n8n 環境**：建議安裝 Docker Desktop 並準備一組可用的 n8n（self-hosted 或 n8n Cloud 帳號皆可），確保能建立與執行 workflow。
2. **LLM API Key**：至 OpenAI 或 Anthropic（或其他相容供應商）申請 API Key，課堂 LAB 將用於呼叫語言模型。
3. **資料庫（選用）**：若可行，安裝 Docker 版 Postgres 或 Redis，供 Memory Management 單元練習使用；未安裝者可於課堂中臨時建置。
4. **上課環境**：不限作業系統，僅需能執行 Docker 與瀏覽器；課程設計以 n8n 雲端或地端實例為核心，可依企業內部環境調整。

---

*用 n8n 實現 Agentic AI System · 14 小時版課程總覽頁（Markdown 版，內容與 `course-overview.html` 相同）；完整教材包請參閱 `README.md`。*
