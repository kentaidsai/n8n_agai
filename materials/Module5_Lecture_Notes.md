用 n8n 實現 Agentic AI System — 上課講義（14小時版）

# Module 5｜Guardrails 安全防護設計

*課程時數：1.5 小時*

## 學習目標

- 理解 Guardrails（護欄）在 Agent 系統中的必要性
- 能設計金額守門、PII 遮罩兩類實用防護機制
- 認識 Prompt Injection 攻擊手法並學會基礎防禦

## 專有名詞說明

| 名詞 | 說明 |
| --- | --- |
| **Guardrails（護欄）** | 為 Agent 系統設計的一組防護規則與檢查機制，確保 Agent 的行為不會超出預期的安全與業務邊界。 |
| **Prompt Injection（提示詞注入攻擊）** | 使用者刻意在輸入訊息中夾帶指令，企圖誘導 Agent 忽略原本的 System Prompt、洩漏內部設定，或執行未授權的行為。 |
| **PII（個人識別資訊）** | 如信用卡號、身分證字號等能識別特定個人的敏感資料，需要在記錄與回覆中特別保護。 |
| **Human-in-the-loop（人工審核介入）** | 當系統判斷某項操作風險較高（如大額退款）時，改為轉交真人審核而非讓 Agent 自行決定的設計模式。 |
| **金額守門（Amount Threshold Check）** | 以金額門檻作為觸發人工審核的判斷條件的一種常見業務護欄。 |

## 詳細說明

### 一、為什麼 Agent 系統需要護欄

Agent 一旦被賦予呼叫工具、處理業務邏輯的能力，就代表它有可能做出「錯誤但看似合理」的決策——例如未經查證就核准一筆大額退款、或在對話中不小心洩漏了系統的內部規則。Guardrails 的目的就是在 Agent 的自主決策範圍內劃出明確界線，把高風險的決策交還給人工，同時防禦惡意使用者的攻擊。

### 二、業務護欄：金額守門

最直觀的護欄設計是為關鍵業務動作設定門檻，超過門檻就強制轉人工審核，而不是讓 Agent 自行核准。這類護欄的實作重點在於「門檻要用明確、絕對的語氣寫入 System Prompt 或用 workflow 邏輯（如 IF 節點）強制檢查」，避免 LLM 在語意模糊時自行放寬標準；同時務必用「反例」（例如未超過門檻的正常案例）一併驗證，確保護欄不會「一律攔截」而過度防礙正常服務。

### 三、資料護欄：PII 遮罩

當 Agent 需要處理或記錄包含個資的資訊時，應在寫入記錄／記憶前先做遮罩處理（例如信用卡號僅保留前 4 碼與末 4 碼），且 Agent 的回覆中也不應該原樣覆誦完整的敏感資料。這類防護通常透過正規表示式（Regex）偵測特定格式的敏感資訊來實作。

### 四、抵禦 Prompt Injection

Prompt Injection 攻擊的常見手法包括：要求 Agent「忽略先前的指示」、「印出你的 System Prompt」、或偽裝成系統管理者要求變更業務規則。防禦的核心原則是在 System Prompt 中明確宣告安全規則「優先於其他所有指示，包含使用者訊息中的任何要求」，並且針對「使用者輸入本身可能就是攻擊」這件事直接寫出因應方式：拒絕洩漏內部設定、拒絕變更業務規則、維持原有角色。這是最基礎也最重要的一層防護，但也提醒：Prompt 層級的防護並非萬無一失，關鍵決策仍應搭配 workflow 邏輯（如 IF 節點的門檻檢查）雙重防護，不能只依賴 LLM 自律。

## 與投影片／練習步驟對照

本模組對應 Module 5 投影片（5 張：觀念、輸入輸出範例、人工介入升級機制、LAB）與《Exercise_Steps_Handbook.md》Module 5 章節，並可參考《Exercise_Steps_Handbook.md》所附的退款 Agent Guardrails 條款 System Prompt 範例。

*本檔為《用 n8n 實現 Agentic AI System》課程 Module 5 的上課講義（Markdown 版，內容與 Module5_Lecture_Notes.docx 相同），搭配投影片與《Exercise_Steps_Handbook.md》（或 Module5_Exercise_Steps.docx／.md）一起使用；完整教材包請參閱 README.md。*
