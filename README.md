# python-mcp-server

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

執行完，會產生以下檔案：
- .gitignore
- .python-version
- main.py
- pyproject.toml
- README.md

## 安裝套件
```shell
uv add "mcp[cli]"
```

## Ref
- https://modelcontextprotocol.io/docs/develop/build-server#python
