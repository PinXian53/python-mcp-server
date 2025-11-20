# python-mcp-server

## 說明
本專案依照官方範例，使用 python 實現 mcp server
- https://modelcontextprotocol.io/docs/develop/build-server#python

## 安裝 uv
uv 是用來執行和管理 Python 專案的工具，可以安裝套件、管理環境和執行腳本

安裝指令：
```shell
curl -LsSf https://astral.sh/uv/install.sh | sh
```

## 初始化專案
```shell
uv init
```

執行完，會在當前資料夾下，產生以下檔案：
- .gitignore
- .python-version
- main.py
- pyproject.toml
- README.md

## 安裝套件
> 💡 對 mcp server 來說只有 `"mcp[cli]"` 是必要的，`httpx` 是範例中為了查詢天氣另外加的
```shell
uv add "mcp[cli]" httpx
```

## 建立 MCP Server
```python
# 引入 FastMCP
from mcp.server.fastmcp import FastMCP

# 初始化 MCP server，並給予名稱
mcp = FastMCP("weather")

# 建立 MCP Tool
@mcp.tool()
async def get_alerts(state: str) -> str:
    """Get weather alerts for a US state.

    Args:
        state: Two-letter US state code (e.g. CA, NY)
    """

    # TODO 撰寫邏輯，並回傳結果
    
    return state

@mcp.tool()
async def get_forecast(latitude: float, longitude: float) -> str:
    """Get weather forecast for a location.

    Args:
        latitude: Latitude of the location
        longitude: Longitude of the location
    """

    # TODO 撰寫邏輯，並回傳結果

    return f"{latitude},{longitude}"
```
