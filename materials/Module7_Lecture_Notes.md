用 n8n 實現 Agentic AI System — 上課講義（14小時版）

# Module 7｜整合專題：Capstone

*課程時數：2 小時*

## 學習目標

- 能將 Module 1～6 的所有成果整合為一份完整的架構設計文件
- 能執行上線前檢查清單，確認系統的安全性與品質是否達標
- 能評估如何將這套方法論擴充到客服以外的其他業務情境

## 專有名詞說明

| 名詞 | 說明 |
| --- | --- |
| **Architecture Design Document（架構設計文件）** | 完整描述系統目標、各元件職責、資料流向、安全機制與已知限制的正式文件，是團隊溝通與交接的重要產出。 |
| **Production Readiness（上線就緒度）** | 系統在正式對外服務前，各項安全、監控、品質指標是否都已達到可接受標準的綜合評估。 |
| **Extensibility（可擴充性）** | 系統架構是否容易被複製、調整並套用到其他業務情境的能力。 |

## 詳細說明

### 一、整合思維：從單點能力到完整系統

前六個模組分別練習了架構設計、Tool 與 Memory、MCP 整合、Multi-Agent 協作、Guardrails、Observability 與 Evaluation 六項能力，Module 7 的任務是把這些單點能力整合看待——理解它們彼此如何搭配運作，而不是各自獨立的技術積木。撰寫架構設計文件的過程，正是強迫自己重新檢視整個系統全貌的最好方式。

### 二、上線前檢查清單的意義

在正式對外服務前，應該系統性地確認：Guardrails、Observability、Evaluation 是否都已到位；Module 4 的路由正確率與 Module 6 的評估通過率是否達到可接受的門檻（課程建議至少 80%）。這份檢查清單的價值在於把「感覺應該差不多了」轉換為「有具體數據支持的上線判斷」。

### 三、從客服延伸到其他業務情境

本課程貫穿範例雖然是智慧客服系統，但背後的方法論（Router 判斷、子 Agent 職責切分、Guardrails 護欄、Evaluation 持續驗證）具有高度可遷移性，可以延伸應用到內部 IT 支援、供應商溝通、行政流程審核等其他場景。學員在 Capstone 中應該練習指出：哪些模組（Router／Guardrails／Evaluation）可以直接沿用，哪些需要因應新場景重新設計。

## 與投影片／練習步驟對照

本模組對應 Module 7 投影片（6 張：完整架構、取捨分析、評分規準、LAB）與《Exercise_Steps_Handbook.md》Module 7 章節，是整個課程的總結與驗收模組。

*本檔為《用 n8n 實現 Agentic AI System》課程 Module 7 的上課講義（Markdown 版，內容與 Module7_Lecture_Notes.docx 相同），搭配投影片與《Exercise_Steps_Handbook.md》（或 Module7_Exercise_Steps.docx／.md）一起使用；完整教材包請參閱 README.md。*
