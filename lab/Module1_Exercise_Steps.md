用 n8n 實現 Agentic AI System — 練習步驟手冊（14小時版・加深版）

# Module 1｜從聊天工具到 Agentic AI：n8n Agent 架構總覽

**目標**：畫出智慧客服 Agent 的第一版架構藍圖，決定何處用 Single Agent，並練習用課堂教授的決策框架做出架構選擇。

**所需資料**：無（僅需紙筆／白板；可搭配投影片「架構決策：Single 還是 Multi-Agent？」對照）

**通用前置準備**
- n8n 環境已可建立與執行 workflow（self-hosted 或 n8n Cloud 皆可）
- 已取得 LLM API Key（OpenAI 或 Anthropic 等），並在 n8n Credentials 中設定完成
- 建議另開一個「練習用」資料夾／專案，避免與既有 workflow 混淆
- 下載本教材包 data/ 資料夾內所有練習用資料檔，並記住其存放路徑

**步驟**

1. 在白板或紙上列出客服系統要處理的三種問題類型：訂單查詢、退換貨、技術支援，並各自寫下 1～2 個具體顧客提問範例（例如訂單查詢：「我的訂單到了嗎？」）。
2. 針對每種問題類型，標註：需要呼叫哪些外部資料（訂單系統、庫存系統、知識庫），以及該資料來源目前是否已有 API 或需要模擬。
3. 對照投影片「適合 Single Agent／適合 Multi-Agent」的判斷標準表，逐條打勾：目前的三種問題類型，單一職責程度如何？是否需要平行處理？
4. 畫出第一版架構圖：一個 Single Agent 接收顧客訊息 → 依需要呼叫工具 → 回覆顧客。標示出 Agent、工具、資料來源三個區塊與其連線關係。
5. 用第 3 步的決策框架，寫下兩個理由，說明「為什麼 Module 1～3 適合先做 Single Agent，等到 Module 4 才拆分為 Multi-Agent」。
6. 標註「這個模組先做」與「留到後續模組」的功能（例如 Multi-Agent 拆分、Guardrails、Evaluation 先不做），確保範圍邊界清楚。
7. 與鄰座交換架構草圖，用 2 分鐘互相說明設計理由，並記錄一個對方提出的建議或質疑。

**驗收標準**：架構圖能清楚說明 Agent 會呼叫的工具與資料來源；能用決策框架的語言解釋為何現階段選擇 Single Agent；明確標示範圍邊界。

*本檔為完整教材包《Exercise_Steps_Handbook.md》的 Module 1 獨立版本；完整手冊與全部練習用資料檔（data/ 資料夾）請參閱教材包 README.md。*
