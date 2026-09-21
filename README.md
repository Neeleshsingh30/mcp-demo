# 🔧 MCP Manual Demo

### *"Under-the-Hood" — see MCP work with zero AI involved*

![Python](https://img.shields.io/badge/Python-3.10+-3776AB?logo=python&logoColor=white)
![FastMCP](https://img.shields.io/badge/FastMCP-Server-4B8BBE)
![No LLM](https://img.shields.io/badge/LLM-None%20needed-lightgrey)
![License](https://img.shields.io/badge/License-MIT-green)

---

## 🎯 What This Demonstrates

This is **Demo 1** of a two-part MCP teaching series. It strips away the LLM entirely so you can see the *raw mechanics* of the Model Context Protocol:

- How an MCP **Server** registers its tools into a schema
- How an MCP **Host/Client** (here, MCP Inspector) discovers that schema
- How a manual `tools/call` triggers real JSON-RPC communication
- How the server executes real logic and returns a real result

> No AI model is involved in this demo — every tool call is triggered **by you, manually**, so the underlying plumbing is fully visible.

---

## 🧰 Tools Exposed by This Server

| Tool | What it does | Example input |
|---|---|---|
| `get_temperature` | Fetches live weather for any city (via wttr.in) | `city: Delhi` |
| `fetch_public_issues` | Lists the top 3 open issues of any public GitHub repo | `owner: langchain-ai`, `repo: langchain` |

---

## 📋 Prerequisites

- **Python 3.10+** — [download here](https://www.python.org/downloads/) (✅ tick "Add python.exe to PATH" on Windows)
- **Node.js (LTS)** — [download here](https://nodejs.org/) (needed only to run `npx` for MCP Inspector)

---

## 🚀 Setup — Step by Step

```bash
# 1. Create and enter the project folder
mkdir mcp_manual_demo
cd mcp_manual_demo

# 2. Create and activate a virtual environment
python -m venv .venv
# Windows:
.venv\Scripts\activate
# Mac/Linux:
source .venv/bin/activate

# 3. Install dependencies
pip install -r requirements.txt
```

> ⚠️ **Windows PowerShell error?**
> If activation fails with `running scripts is disabled on this system`, run this once:
> ```powershell
> Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
> ```

---

## ▶️ Running the Demo

```bash
npx @modelcontextprotocol/inspector python server.py
```

This opens **MCP Inspector** in your browser (usually `http://localhost:6274`).

1. Click **Connect**
2. Open the **Tools** tab — both tools appear automatically, with zero manual wiring
3. Pick a tool, fill in the parameters, hit **Run Tool**
4. Watch the real result come back live

---

## 📁 Project Structure

```
mcp_manual_demo/
├── server.py          # The MCP server — defines and registers both tools
├── requirements.txt   # fastmcp + httpx
└── README.md
```

---

## 💡 The Big Takeaway

Registering a tool (`@mcp.tool()`) and starting the server (`mcp.run()`) are two **separate** jobs. The decorator just builds a schema; `mcp.run()` is what actually opens the door for a client to talk to it over JSON-RPC.

Pair this with **[Demo 2](../mcp_llm_demo)** to see an LLM pick and run tools *on its own*, using a pre-built server instead of a custom one.
