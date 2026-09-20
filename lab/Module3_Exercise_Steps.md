用 n8n 實現 Agentic AI System — 練習步驟手冊（14小時版・加深版）

# Module 3｜MCP Server/Client 整合實作

**目標**：串接一個 MCP Server，讓 Agent 透過 MCP Client 呼叫工具取得資料，並比較與直接 API 呼叫的差異。

**所需資料**：`data/mcp_server_tools.json`（MCP Server 三個工具的 schema 與模擬回應：get_order_status、get_inventory、search_faq）

**通用前置準備**
- n8n 環境已可建立與執行 workflow（self-hosted 或 n8n Cloud 皆可）
- 已取得 LLM API Key（OpenAI 或 Anthropic 等），並在 n8n Credentials 中設定完成
- 建議另開一個「練習用」資料夾／專案，避免與既有 workflow 混淆
- 下載本教材包 data/ 資料夾內所有練習用資料檔，並記住其存放路徑

**步驟**

1. 參考 `data/mcp_server_tools.json` 中三個工具的 `input_schema` 與 `mock_examples`，用課前提供的簡易 MCP Server 範例（或任何支援 MCP 協定的框架）建置一個本機或雲端可存取的 MCP Server，暴露這三個工具：
   - `get_order_status`：查訂單狀態（可重用 Module 2 的模擬資料邏輯）
   - `get_inventory`：查商品庫存，輸入 SKU（如 `SKU-1001`、`SKU-4005`），回傳庫存數量與補貨預估日
   - `search_faq`：以關鍵字查詢客服知識庫，回傳最相關的 1～3 筆 FAQ
2. 在 n8n 中加入 **MCP Client Tool** 節點，設定 MCP Server 的連線位址與認證資訊，並確認節點能列出上一步暴露的三個工具。
3. 將 MCP Client Tool 掛載到 Module 2 的 AI Agent 節點上（可與既有的 HTTP Request Tool 並存，方便對照）。
4. 用 `mcp_server_tools.json` 內建的 `mock_examples` 逐一測試：
   - 訂單查詢：「訂單 A12345 到了嗎？」→ 驗證透過 MCP 取得與 Module 2 一致的結果
   - 庫存查詢：「SKU-4005 這台螢幕現在有貨嗎？」→ 驗證 Agent 能正確轉述「目前無庫存，預估 2026-10-05 補貨」
   - 知識庫查詢：「退貨要幾天？」→ 驗證 Agent 能引用 FAQ 回答退貨審核與退款時程
   - 查無資料情境：用 `search_faq` 的「外星人入侵怎麼辦」測試，驗證 Agent 在知識庫查無資料時的回應方式
5. 比較直接呼叫 API（HTTP Request Tool，Module 2 做法）與透過 MCP 呼叫（本模組做法）的差異：設定方式、工具描述與 schema 的可重用性、跨專案／跨 Agent 共用的維護成本。將比較結果整理成一張簡表。
6. （進階，時間允許時）嘗試把 `get_inventory` 或 `search_faq` 其中一個工具，改用你熟悉的方式（如簡易 Express/FastAPI 服務）包裝成 MCP Server 雛形，理解 MCP 協定如何對外暴露工具的 schema 與呼叫介面。

> **System Prompt 調整重點（Module 3）**
>
> 本模組沿用 Module 2 的 System Prompt 骨架，只需要在「資料來源規則」段落擴充，讓 Agent 知道現在有更多工具可用：
>
> ```
> （沿用 Module 2 的角色與語氣設定，資料來源規則擴充為：）
> 
> 你現在可以使用以下工具，所有資料都必須透過工具取得，不可憑空猜測：
> - get_order_status：查詢訂單狀態
> - get_inventory：查詢商品庫存與補貨預估日
> - search_faq：查詢客服知識庫，回答一般政策類問題（如退貨天數、保固規則）
> 
> 若 search_faq 查無相關資料，誠實告知顧客「這個問題我需要進一步確認，稍後由專人回覆」，不可以自行編造政策內容。
> ```
>
> 重點是：新增工具時，System Prompt 只需要「補充資料來源規則」，角色定義與語氣格式通常不必重寫——這也是 Module 4 之後每個子 Agent 都能共用同一套骨架的原因。

**驗收標準**：Agent 能透過 MCP Client 成功取得三個工具回傳的資料，且結果與 `mcp_server_tools.json` 的 mock 範例一致；能寫出至少三點「MCP vs 直接 API 呼叫」的差異；查無資料情境有被正確處理。

*本檔為完整教材包《Exercise_Steps_Handbook.md》的 Module 3 獨立版本；完整手冊與全部練習用資料檔（data/ 資料夾）請參閱教材包 README.md。*
