用 n8n 實現 Agentic AI System — 練習步驟手冊（14小時版・加深版）

# Module 4｜Multi-Agent 協作方法論與實作

**目標**：把客服 Agent 拆分為 Router + 多個子 Agent 協作系統，並用 8 題路由測試案例驗證正確率。

**所需資料**：`data/routing_test_cases.csv`（8 題路由測試問題，含預期分類與預期轉交對象）

**通用前置準備**
- n8n 環境已可建立與執行 workflow（self-hosted 或 n8n Cloud 皆可）
- 已取得 LLM API Key（OpenAI 或 Anthropic 等），並在 n8n Credentials 中設定完成
- 建議另開一個「練習用」資料夾／專案，避免與既有 workflow 混淆
- 下載本教材包 data/ 資料夾內所有練習用資料檔，並記住其存放路徑

**步驟**

1. 將 Module 2/3 完成的 Agent 邏輯，分別複製為兩個獨立 workflow：「訂單 Agent」「退款 Agent」，各自透過 **Execute Workflow Trigger** 開放給主流程呼叫。
2. 為每個子 Agent 精簡其 System Prompt，使其只專注於單一職責（訂單 Agent 只處理查詢／庫存；退款 Agent 只處理退款與退貨申請，範例見下方）。
3. 新建主流程「Router Agent」：
   - 加入一個 AI Agent 節點作為路由判斷者，System Prompt 說明其任務是「判斷顧客問題類型，並回傳應轉交的 Agent 名稱：訂單 Agent、退款 Agent，或『一般諮詢』」（範例見下方）
   - 或改用 **Switch** 節點依關鍵字／分類結果路由，兩種做法可各自實作後比較差異
4. 用 **Execute Workflow** 節點，將 Router 判斷後的請求轉交給對應的子 Agent workflow，並將子 Agent 的回覆帶回主流程。
5. 針對 `routing_test_cases.csv` 中「一般諮詢」類的題目（如 R07、R08），設計 Router 的處理方式：不轉交子 Agent，而是由 Router 直接安撫回覆或引用知識庫回答，並記錄下來。
6. 整合子 Agent 的回覆，統一格式後回傳給顧客。
7. 依序執行 `routing_test_cases.csv` 的全部 8 題測試問題（R01～R08），對每一題記錄：Agent 實際判斷的分類、實際轉交的對象，並與 CSV 中的 `expected_category`／`expected_agent` 欄位比對是否一致。
8. 計算 8 題中的路由正確率，挑出判斷錯誤或邊界模糊的題目（特別留意 R06 取消訂單、R08 情緒性客訴這類邊界情境），討論可能原因（分類定義不清、System Prompt 描述不足）與改善方向，並嘗試調整後重新測試該題。

> **System Prompt 範例（Module 4 Router + 子 Agent）**
>
> **Router Agent（判斷分類，不直接回答顧客問題）**
>
> ```
> 你是客服系統的路由判斷者，不負責直接回答顧客問題。
> 
> 你的任務：閱讀顧客訊息，判斷應該轉交給哪一個處理單位，只能回傳以下三者之一（純文字，不要加其他說明）：
> - order_agent：訂單查詢、物流、庫存相關問題
> - refund_agent：退款、退貨、換貨相關問題
> - general：無法歸類的一般諮詢、情緒性抱怨、或需要人工協助的問題
> 
> 判斷原則：
> - 若訊息同時包含多種意圖，以顧客當下最主要的訴求為準。
> - 若無法確定，回傳 general，不要猜測或硬套分類。
> - 情緒強烈的客訴（如威脅、辱罵、重複投訴）一律回傳 general，交由人工判斷。
> ```
>
> **訂單 Agent（精簡自 Module 2/3 的骨架，只保留訂單相關職責）**
>
> ```
> 你是「訂單 Agent」，只負責訂單查詢、物流與庫存相關問題。
> 所有資料必須透過 get_order_status、get_inventory 工具取得，不可憑空猜測。
> 若顧客的問題其實是退款/退貨，告知「這部分將由退款專責窗口協助」，不要自己處理。
> ```
>
> **退款 Agent（精簡自同一骨架，只保留退款相關職責）**
>
> ```
> 你是「退款 Agent」，只負責退款與退貨申請相關問題。
> 所有訂單資料必須透過 get_order_status 工具確認後才能受理退款申請，不可憑空猜測訂單是否符合退貨資格。
> 若顧客的問題其實是查訂單物流，告知「這部分將由訂單查詢窗口協助」，不要自己處理。
> ```
>
> 撰寫要點：Router 的 Prompt 只做「分類」，明確限制輸出格式（只能回傳固定的幾個值之一），避免它自己嘗試回答問題；子 Agent 的 Prompt 則是從 Module 2/3 的骨架「裁切」而來，刻意縮小職責範圍，並加上「不是我的職責時怎麼辦」的退場規則，避免子 Agent 之間互相搶答或掉球。

**驗收標準**：8 題路由測試案例中，至少 6 題（75%）判斷結果與 `expected_category`／`expected_agent` 一致；子 Agent 回覆內容正確；能具體說出判斷錯誤題目的可能原因與至少一個改善方向。

*本檔為完整教材包《Exercise_Steps_Handbook.md》的 Module 4 獨立版本；完整手冊與全部練習用資料檔（data/ 資料夾）請參閱教材包 README.md。*
