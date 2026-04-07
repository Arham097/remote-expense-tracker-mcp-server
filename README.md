# Expense Tracker MCP Server

A local MCP server for tracking expenses and income using SQLite.

## Features

- Add, list, update, delete expense records
- Add, list, update, delete income records
- Summarize expenses and income by date range and optional category
- Exposes categories via MCP resource: `expense://categories`

## Requirements

- Python 3.11+
- An MCP client such as Claude Desktop or Claude Code

## Install

From the project folder:

```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
pip install -e .
```

## Run (Local Test)

```powershell
.\.venv\Scripts\Activate.ps1
python main.py
```

The server runs over stdio, which is what MCP clients expect.

## Claude Desktop Setup

Add this server to your Claude Desktop MCP config file.

Typical Windows config path:

`%APPDATA%\Claude\claude_desktop_config.json`

Example config:

```json
{
  "mcpServers": {
    "expense-tracker": {
      "command": "C:\\Users\\arham\\OneDrive\\Desktop\\expense-tracker-mcp-server\\.venv\\Scripts\\python.exe",
      "args": [
        "C:\\Users\\arham\\OneDrive\\Desktop\\expense-tracker-mcp-server\\main.py"
      ]
    }
  }
}
```

After saving, restart Claude Desktop.

## Claude Code Example

Once connected, you can ask Claude Code:

```text
Add an expense on 2026-04-07 for 18.5 in category "Food", subcategory "Lunch", note "Office canteen".
Then list expenses from 2026-04-01 to 2026-04-30.
Then summarize expenses from 2026-04-01 to 2026-04-30.
```

You can also query the categories resource:

```text
Read the MCP resource expense://categories
```

## Available MCP Tools

- `add_expense(date, amount, category, subcategory="", note="")`
- `list_expenses(start_date, end_date)`
- `summarize(start_date, end_date, category=None)`
- `update_expense(expense_id, date=None, amount=None, category=None, subcategory=None, note=None)`
- `delete_expense(expense_id)`
- `add_income(date, amount, category, subcategory="", note="")`
- `list_income(start_date, end_date)`
- `summarize_income(start_date, end_date, category=None)`
- `update_income(income_id, date=None, amount=None, category=None, subcategory=None, note=None)`
- `delete_income(income_id)`

## Data Files

- `expenses.db` is created automatically when the server starts.
- `categories.json` is served as the `expense://categories` resource.
