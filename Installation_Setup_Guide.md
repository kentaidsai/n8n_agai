# 用 n8n 實現 Agentic AI System — 軟體安裝與環境設定指南

*14 小時課程・課前準備手冊*

本手冊協助學員在課程開始前完成以下環境設定：

- n8n 執行環境（self-hosted 或 n8n Cloud 擇一）
- LLM API Key 申請與在 n8n Credentials 中設定
- Module 3 練習用 MCP Server 範例環境
- 課程練習用資料檔下載與擺放

*建議在課程開始前至少 1～2 天完成本手冊全部步驟，並在課前確認「驗收檢查表」（見文末）的每一項都能打勾。*

---

## 一、n8n 執行環境設定

n8n 有兩種常見的使用方式：n8n Cloud（雲端託管，免安裝）與 self-hosted（自行架設，可用 Docker 或 npm）。課程練習兩種方式皆可，擇一完成即可，建議依自己的環境熟悉度選擇；若不確定，建議選擇 n8n Cloud 的免費試用，設定最快。

### 方式 A：n8n Cloud（建議新手使用）

1. 開啟瀏覽器，前往 n8n 官方網站（https://n8n.io），點選「Get started」或「Start for free」。
2. 以 Email 或 Google／GitHub 帳號註冊一個新帳號。
3. 完成註冊精靈（workspace 名稱可自訂，例如「n8n-agentic-course」）。
4. 進入後台後，確認可以看到「Workflows」總覽頁，並能點選「+ Create Workflow」建立一個空白 workflow。
5. 在空白 workflow 中新增一個 Manual Trigger 節點並執行一次，確認整體介面運作正常（執行後應顯示綠色勾勾）。

> **提示：** n8n Cloud 提供免費試用期，試用期間功能已足夠支援本課程全部 7 個模組的練習；若試用期在課程結束前到期，可申請延長或改用 self-hosted 方式。

### 方式 B：Self-hosted（Docker，建議已有 Docker 經驗者使用）

1. 確認電腦已安裝 Docker Desktop（Windows／Mac）或 Docker Engine（Linux）；可在終端機執行以下指令確認版本：

   ```
   docker --version
   ```

2. 在終端機執行以下指令啟動 n8n 容器（會將資料保存在本機的 `~/.n8n` 資料夾，重啟後資料不會遺失）：

   ```
   docker run -it --rm \
     --name n8n \
     -p 5678:5678 \
     -v ~/.n8n:/home/node/.n8n \
     docker.n8n.io/n8nio/n8n
   ```

3. 開啟瀏覽器，前往 http://localhost:5678，依畫面指示建立第一組管理員帳號（Email／密碼）。
4. 登入後，同方式 A 步驟 4～5，建立一個空白 workflow 並執行一次 Manual Trigger 節點，確認運作正常。

> **注意：** 若之後要長時間保留 workflow（例如課程期間持續使用），建議將 `docker run` 指令中的 `--rm` 拿掉，並改用 `docker start` / `docker stop` 管理容器的啟停，避免容器移除後資料跟著消失（雖然 `-v` 掛載的資料夾本身不會被刪除，但仍建議熟悉 Docker 操作的學員才使用 `--rm` 之外的長駐方式）。

### 方式 C：Self-hosted（npm，適合已安裝 Node.js 的開發者）

1. 確認已安裝 Node.js 18 版以上：

   ```
   node --version
   ```

2. 全域安裝 n8n：

   ```
   npm install -g n8n
   ```

3. 啟動 n8n：

   ```
   n8n start
   ```

4. 終端機顯示啟動完成後，開啟瀏覽器前往 http://localhost:5678，同方式 B 完成帳號建立與測試。

### 三種方式比較

| 方式 | 優點 | 適合對象 |
| --- | --- | --- |
| n8n Cloud | 免安裝、免維護，開箱即用 | 初學者、想專注在課程內容的學員 |
| Self-hosted（Docker） | 資料完全在本機、容器化易於重置環境 | 已熟悉 Docker 的學員 |
| Self-hosted（npm） | 與本機 Node.js 開發環境整合度高 | 習慣終端機操作的開發者 |

## 二、LLM API Key 申請與設定

課程練習需要呼叫 LLM（大型語言模型）API 作為 AI Agent 節點的 Chat Model。以下以 OpenAI 與 Anthropic 兩家常見供應商為例，擇一申請即可；已有其他相容供應商（如 Azure OpenAI）的 API Key 也可以直接使用。

### 申請 OpenAI API Key

1. 前往 https://platform.openai.com，註冊或登入帳號。
2. 進入左側選單「API keys」頁面（或直接前往 https://platform.openai.com/api-keys）。
3. 點選「Create new secret key」，為 Key 命名（例如 `n8n-agentic-course`），建立後立即複製並妥善保存——這組 Key 只會顯示一次。
4. 確認帳號已綁定付款方式或有足夠額度（「Billing」頁面可查看），本課程練習用量極低，一般在幾美元額度內即可完成全部模組。

### 申請 Anthropic（Claude）API Key

1. 前往 https://console.anthropic.com，註冊或登入帳號。
2. 進入「API Keys」頁面，點選「Create Key」，命名後建立並複製保存。
3. 確認帳號已有可用額度（「Plans & Billing」頁面可查看或加值）。

### 在 n8n 中設定 Credential

1. 登入 n8n 後台，點選左側選單「Credentials」，再點選右上角「+ Add Credential」。
2. 搜尋並選擇對應的 Credential 類型（例如「OpenAi API」或「Anthropic API」）。
3. 將剛才申請到的 API Key 貼入對應欄位，Credential 名稱建議填寫容易辨識的名字（例如 `course-openai-key`）。
4. 點選「Save」，若畫面顯示連線測試成功（或無錯誤訊息），即代表設定完成。
5. 之後在 AI Agent 節點的 Chat Model 欄位中，即可從下拉選單選擇剛才建立的 Credential。

> **注意：** API Key 等同於帳號密碼，請勿分享給他人、勿上傳到公開的程式碼倉庫（GitHub 等），也不建議直接寫死在 workflow 的節點參數中——一律透過 n8n Credentials 機制管理。

## 三、Module 3 練習用 MCP Server 環境

Module 3 會練習串接一個 MCP（Model Context Protocol）Server，暴露 `get_order_status`、`get_inventory`、`search_faq` 三個工具供 Agent 呼叫。以下提供一個以 Node.js 建置的最小可行範例，供課前先行準備環境；實際工具邏輯與模擬資料在課堂中會依 `data/mcp_server_tools.json` 帶著大家一起完成。

### 先決條件

- 已安裝 Node.js 18 版以上（可與方式 C 的 n8n npm 安裝共用同一份 Node.js 環境）。
- 下載本教材包 `data/` 資料夾中的 `mcp_server_tools.json`，供課堂練習時參考三個工具的 schema 與模擬回應。

### 建立最小可行的 MCP Server 專案骨架

1. 建立一個新資料夾並初始化 Node.js 專案：

   ```
   mkdir mcp-server-course && cd mcp-server-course
   npm init -y
   ```

2. 安裝 MCP 官方 SDK（課堂會示範如何用它快速暴露工具）：

   ```
   npm install @modelcontextprotocol/sdk
   ```

3. 建立 `server.js` 檔案，作為課堂上實作 `get_order_status`／`get_inventory`／`search_faq` 三個工具的起點（課堂中會提供完整範例程式碼，此處僅需確認以下最小骨架能夠執行不報錯）：

   ```js
   // server.js（課前先確認可執行，工具邏輯課堂中完成）
   const { McpServer } = require("@modelcontextprotocol/sdk/server/mcp.js");

   const server = new McpServer({ name: "course-mock-server", version: "1.0.0" });

   console.log("MCP server skeleton loaded. 課堂中將在此加入三個工具。");
   ```

4. 執行以下指令確認骨架可以正常執行、不會報錯：

   ```
   node server.js
   ```

> **提示：** 若課堂改用其他語言（如 Python）的 MCP SDK 示範，步驟原理相同：安裝對應語言的 MCP SDK、建立最小可執行的 Server 骨架即可，實際工具實作會在課堂中一起完成，課前不需要先寫好三個工具的完整邏輯。

5. 確認 n8n 的 MCP Client Tool 節點在你的 n8n 版本中可以正常新增（在新增節點的搜尋框輸入「MCP」應能看到「MCP Client Tool」節點）；若搜尋不到，請確認 n8n 版本是否為近期版本，或依 n8n 官方文件安裝對應的 community node。

## 四、課程練習用資料檔

請於課前下載本教材包 `data/` 資料夾內全部練習用資料檔，並記住存放路徑（課堂練習步驟中會直接引用檔名）。

| 檔案 | 用途 | 使用模組 |
| --- | --- | --- |
| `orders_mock.json` | 10 筆模擬訂單資料 | Module 2、3 |
| `mcp_server_tools.json` | MCP Server 三個工具的 schema 與模擬回應 | Module 3 |
| `routing_test_cases.csv` | 8 題路由測試問題 | Module 4 |
| `guardrail_test_cases.csv` | 6 題安全防護測試案例 | Module 5 |
| `evaluation_dataset.csv` | 20 題自動化評估測試集 | Module 6 |

> **提示：** 所有資料檔為固定格式的模擬資料，各模組練習步驟中會標明對應的確切檔名，請勿自行更名，以免與《Exercise_Steps_Handbook.md》的引用不一致。

## 五、課前驗收檢查表

完成以下所有項目後，即代表課前環境準備完成，可以直接進入 Module 1 的課程內容。

- [ ] n8n 已可正常開啟後台，並能建立一個空白 workflow、執行 Manual Trigger 節點成功
- [ ] 已申請至少一組 LLM API Key（OpenAI 或 Anthropic 或其他相容供應商）
- [ ] 已在 n8n Credentials 中設定好該 API Key，且顯示連線成功
- [ ] 已安裝 Node.js 18+，並能執行 `node --version` 顯示版本號
- [ ] 已建立 MCP Server 練習專案骨架，並能以 `node server.js` 執行不報錯
- [ ] 已下載 `data/` 資料夾全部 5 份練習用資料檔，並確認存放路徑
- [ ] 已閱讀《Exercise_Steps_Handbook.md》或對應模組的 Word 檔，了解 Module 1 的練習內容

*若上述任一項目無法完成，請於課前與講師聯繫協助排除，避免影響課堂練習進度。*


