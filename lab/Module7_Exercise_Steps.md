用 n8n 實現 Agentic AI System — 練習步驟手冊（14小時版・加深版）

# Module 7｜整合專題：Capstone

**目標**：完成個人版「智慧客服 Agent System」架構設計文件，整合 Module 1～6 的所有成果。

**所需資料**：無新增資料檔；請彙整 Module 2～6 使用過的 `data/` 全部檔案與各模組測試結果，作為文件附錄佐證

**通用前置準備**
- n8n 環境已可建立與執行 workflow（self-hosted 或 n8n Cloud 皆可）
- 已取得 LLM API Key（OpenAI 或 Anthropic 等），並在 n8n Credentials 中設定完成
- 建議另開一個「練習用」資料夾／專案，避免與既有 workflow 混淆
- 下載本教材包 data/ 資料夾內所有練習用資料檔，並記住其存放路徑

**步驟**

1. 回顧 Module 1～6 完成的所有 workflow，畫出最終版系統架構圖（建議標示：Router、訂單 Agent、退款 Agent、MCP Server、Guardrails 檢查點、記錄與評估流程，以及各節點使用的資料來源）。
2. 撰寫一頁式架構設計文件，包含：
   - 系統目標與適用情境
   - 各模組（Agent）職責與呼叫關係
   - 使用的工具／MCP／記憶機制，並列出對應的資料檔（如 `orders_mock.json`、`mcp_server_tools.json`）
   - Guardrails 清單，附上 `guardrail_test_cases.csv` 的測試結果摘要
   - Observability／Evaluation 機制，附上 `evaluation_dataset.csv` 的最終通過率
   - 已知限制與後續優化方向
3. 檢查上線前清單：Guardrails、Observability、Evaluation 是否都已到位，Module 4 的路由正確率與 Module 6 的評估通過率是否達到可接受的門檻（建議至少 80%）。
4. 說明如何將這套架構擴充到客服以外的業務情境（如內部 IT 支援、供應商溝通、行政流程），列出至少 1 個具體例子，並指出哪些模組（Router／Guardrails／Evaluation）可以直接沿用、哪些需要重新設計。
5. （時間允許時）與其他學員互相簡報 5 分鐘，互相提問與回饋，特別聚焦在對方的 Guardrails 設計與評估結果是否有遺漏的邊界案例。

**驗收標準**：架構設計文件內容完整，能清楚回答「這套系統做什麼、怎麼做、如何確保安全與品質」；文件中的關鍵指標（路由正確率、評估通過率）皆有數據佐證，而非空泛敘述。

*本檔為完整教材包《Exercise_Steps_Handbook.md》的 Module 7 獨立版本；完整手冊與全部練習用資料檔（data/ 資料夾）請參閱教材包 README.md。*
