# 上課講義（各章節）— 用 n8n 實現 Agentic AI System

本資料夾收錄「用 n8n 實現 Agentic AI System」14 小時課程的**上課講義**，依 7 個模組拆分，每個模組各一份 Word 檔（`.docx`）與內容相同的 Markdown 檔（`.md`），供講師與學員選擇習慣的格式使用。

## 這份講義是什麼、不是什麼

投影片以精簡條列呈現重點，方便課堂口頭講解；《Exercise_Steps_Handbook.md》聚焦在動手操作的具體步驟。本講義補上兩者之間的空白：**專有名詞的正式定義**與**觀念背後的原理、設計取捨與實務判斷依據**，用完整段落說明「為什麼要這樣設計」，而不只是「該怎麼做」。適合作為課前預習、課堂補充講解，或課後複習查閱之用。

## 檔案清單

| 檔案 | 模組主題 | 時數 |
| --- | --- | --- |
| `Module1_Lecture_Notes.docx` / `.md` | 從聊天工具到 Agentic AI：n8n Agent 架構總覽 | 1.5h |
| `Module2_Lecture_Notes.docx` / `.md` | Single Agent 實作：Tool Invocation 與 Memory Management | 3h |
| `Module3_Lecture_Notes.docx` / `.md` | MCP Server/Client 整合實作 | 2h |
| `Module4_Lecture_Notes.docx` / `.md` | Multi-Agent 協作方法論與實作 | 2.5h |
| `Module5_Lecture_Notes.docx` / `.md` | Guardrails 安全防護設計 | 1.5h |
| `Module6_Lecture_Notes.docx` / `.md` | Observability 與 Evaluation | 1.5h |
| `Module7_Lecture_Notes.docx` / `.md` | 整合專題：Capstone | 2h |

`.docx` 與 `.md` 兩種格式內容完全相同：`.docx` 版本有標題樣式、術語表格與 n8n 配色，適合列印或直接分發；`.md` 版本為純文字 Markdown，適合貼入 Notion、GitHub 或其他純文字／Markdown 環境使用。

## 每份講義的結構

1. **學習目標**：本模組結束後，學員應該能做到的 3～4 件具體事情。
2. **專有名詞說明**：以表格列出本模組會用到的關鍵術語（多為英文縮寫或技術名詞），逐一給出繁體中文定義，避免課堂中因為術語理解落差而卡住。
3. **詳細說明**：以 3～4 個小節、完整段落展開本模組的核心觀念，包含原理說明、設計模式的取捨比較、與常見的實務判斷原則（例如「什麼時候該拆分 Multi-Agent」「什麼時候該導入 MCP」）。
4. **與投影片／練習步驟對照**：說明本講義對應到哪幾張投影片、哪一章練習步驟，方便講師安排課堂節奏，也方便學員在動手練習前後回頭查閱背景知識。

## 建議使用方式

- **課前**：學員可先讀過對應模組的講義，尤其是「專有名詞說明」段落，減少課堂上因術語不熟悉而打斷進度。
- **課堂中**：投影片講到相關頁面、或學員提問「這個名詞是什麼意思」時，直接翻開對應段落展開講解；「詳細說明」段落也可作為課堂口頭講解的逐字稿骨架。
- **課後**：搭配《Exercise_Steps_Handbook.md》（或對應模組的 `Module{n}_Exercise_Steps.docx`／`.md`）動手練習時，遇到不確定「為什麼這樣做」的地方，回頭查閱本講義的「詳細說明」。

