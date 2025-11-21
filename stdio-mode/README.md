# Python MCP Server (Stdio 模式)

## 開發 MCP Server

### 說明
本教學將依循官方範例，使用 FastMCP 函式庫實現一個簡單的 Python MCP Server，並透過 Stdio 模式進行測試。
- 官方參考：https://modelcontextprotocol.io/docs/develop/build-server#python

### 🔧 步驟一：環境準備與 uv 安裝
uv 是用來執行和管理 Python 專案的工具，可以安裝套件、管理環境和執行腳本
1. 安裝指令：
    ```shell
    curl -LsSf https://astral.sh/uv/install.sh | sh
    ```

2. 初始化專案
    ```shell
    # 建立並進入虛擬環境
    uv venv
    source .venv/bin/activate
    
    # 初始化 uv 專案
    uv init
    ```
    執行 uv init 後，會在當前資料夾下生成專案所需的核心檔案：
    - .gitignore
    - .python-version
    - pyproject.toml
    - README.md

### 📦 步驟二：安裝必要套件
> 💡 對 Stdio 模式的 MCP Server 來說，只有 `"mcp[cli]"` 是必要的。`httpx` 則是範例中用來處理網路請求的額外套件。
```shell
uv add "mcp[cli]" httpx
```

### 📝 步驟三：實現 MCP Server 邏輯
建立 weather.py，參考 [weather.py](weather.py) 內容 <br/>

主要重點說明：
```python
# 初始化 MCP server
mcp = FastMCP("weather")

# 建立 MCP Tool
@mcp.tool()
async def get_alerts(state: str) -> str:
    """
    撰寫說明
    """

    # 撰寫業務邏輯，並回傳結果
    return f"Fetching alerts for {state}..."

# 運行 mcp server (預設使用 STDIO 模式)
if __name__ == "__main__":
    mcp.run()
```


### 🧪 步驟四：測試 MCP Server (使用 Inspector)
使用 mcp dev 指令啟動 Inspector 工具，它會以 Stdio 模式執行你的 `weather.py`，並透過 Proxy 將資料傳輸到瀏覽器介面。

1. 啟動 MCP inspector，並指定運行 `weather.py`
    ```shell
    uv run mcp dev weather.py
    ```
2. 確認 Inspector 啟動資訊，Console 會顯示以下資訊，並自動打開瀏覽器：
    ```text
    Starting MCP inspector...
    ⚙️ Proxy server listening on localhost:6277
    🔑 Session token: ada07a3c319d499a3cd65f6ec6f50....
       Use this token to authenticate requests or set DANGEROUSLY_OMIT_AUTH=true to disable auth
    
    🚀 MCP Inspector is up and running at:
       http://localhost:6274/?MCP_PROXY_AUTH_TOKEN=ada07a3c319d499a3cd65f6ec6f50....
    ```
3. 進行連線：選擇 STDIO Mode → 點 Connect
    ![stdio.png](imgs/stdio.png)
4. 進行測試：切換到 Tools 分頁 → 選擇 List Tools 即可看到您定義工具清單 → 選擇要測試的 Tool → 輸入參數進行測試
    ![test-tools.png](imgs/test-tools.png)
