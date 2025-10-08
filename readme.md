# 🌤️ MCP Weather Assistant
## Introduction
This project demonstrates how to build a **tool-augmented conversational AI** using **Model Context Protocol (MCP)**.  
It connects an **Anthropic Claude** model to a **custom weather MCP server** that retrieves real-time weather alerts and forecasts from the **U.S. National Weather Service (NWS API)**.

## 🚀 Features
- **FastMCP Server** (`weather.py`)
  - Exposes tools like:
    - `get_alerts(state)` → Fetches active weather alerts by U.S. state.
    - `get_forecast(latitude, longitude)` → Fetches detailed weather forecasts for a given location.
  - Uses the official [NWS API](https://www.weather.gov/documentation/services-web-api).

- **MCP Client** (`client.py`)
  - Launches the MCP server and connects via stdio.
  - Integrates with **Anthropic Claude** (`claude-sonnet-4-5-20250929`).
  - Lets Claude **automatically call weather tools** when responding to user queries.
  - Provides an **interactive chat loop** where users can type queries like:
    > “Show me the weather alerts in California”  
    > “What’s the forecast near 37.77, -122.42?”

- **.env Support**
  - Loads your Anthropic API key automatically via `dotenv`.


### 🧠 System Flow
```text
User Query  →  MCP Client  →  Claude Model (via Anthropic API)
                    ↓
              MCP Server Tools
              ↙︎               ↘︎
    get_alerts(state)     get_forecast(lat, lon)
```

## 🧠 How It Works

### Architecture Overview
1. **`weather.py`** runs a FastMCP server that defines callable weather tools.
2. **`client.py`** launches the MCP server and initializes an MCP session.
3. When you ask Claude a question, it can decide to **call a tool**.
4. The result is sent back to Claude for reasoning and response generation.