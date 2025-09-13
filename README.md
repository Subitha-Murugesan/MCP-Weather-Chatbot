# MCP Weather Chatbot

**MCP Weather Chatbot** is a Generative AI project that exposes real-time **weather data and alerts** as an MCP (Model Context Protocol) server.
It demonstrates how to build MCP tools that can be accessed by different clients using both **SSE** (Server-Sent Events over HTTP) and **stdio** transport.

The backend integrates with the **US National Weather Service (NWS) API** to provide accurate, structured weather alerts and forecasts.

---

## Quick Start

Clone the repo and set up the environment using **uv**:

```bash
# Initialize venv
uv venv
source .venv/bin/activate

# Install dependencies
uv add mcp httpx nest_asyncio
```

Run the MCP Weather server:

```bash
uv run server.py
```

Run a client (stdio or SSE):

```bash
uv run client_stdio.py
# or
uv run client_sse.py
```

---

##  Workflow Overview

```
User -> Client (stdio / SSE) -> MCP Weather Server -> NWS API
```

* **Weather MCP Server (`server.py`)**

  * Tools:

    * `get_alerts(state)` → Fetches weather alerts for a given U.S. state
    * `get_forecast(lat, lon)` → Returns a detailed forecast for a location
  * Supports **stdio** and **SSE (HTTP)** transports
  * Runs locally or in Docker

* **Clients**

  * `client_stdio.py` → Connects via **stdio**
  * `client_sse.py` → Connects via **SSE** (`http://localhost:8000/sse`)

---

## User Experience

1. Start the server:

   ```bash
   uv run server.py
   ```
   <img width="2772" height="1670" alt="image" src="https://github.com/user-attachments/assets/3cd0e1c7-7ee9-4603-8924-b94be54e94b6" />


2. Run the SSE client:

   ```bash
   uv run client_sse.py
   ```
<img width="2772" height="1670" alt="image" src="https://github.com/user-attachments/assets/13a10a35-ae96-4862-b4c8-8e0fdab16581" />

3. Or run the stdio client:

   ```bash
   uv run client_stdio.py
   ```

4. Example interaction:

You: provide me the weather state of NC
<img width="1726" height="1016" alt="image" src="https://github.com/user-attachments/assets/86de6a60-6312-4208-bace-9dc89d7d0e33" />


---

## Running with Docker

Build and run the containerized server:

```bash
docker build -t mcp-weather .
docker run -p 8000:8000 mcp-weather
```
<img width="1726" height="1016" alt="image" src="https://github.com/user-attachments/assets/b71000c2-7b35-4ce5-ad6c-7b8141fc5622" />
<img width="1726" height="274" alt="image" src="https://github.com/user-attachments/assets/3e1d8667-622f-4d65-ba5f-cf9bbccc2256" />


This starts the MCP Weather Server with **SSE** enabled and exposes it on `localhost:8000`.

---

## Testing the MCP Weather Server

You can test the server in **three different ways**:

### MCP Inspector

```bash
uv run mcp dev server/weather.py
```
<img width="1980" height="1124" alt="image" src="https://github.com/user-attachments/assets/7a31561c-dec0-4a1f-bd0e-478cf97c46c9" />
<img width="2872" height="1678" alt="image" src="https://github.com/user-attachments/assets/f525e098-779a-4779-933a-ead29e4489dd" />


---

### Claude Desktop

Install the MCP server:

```bash
uv run mcp install server/weather.py
```
<img width="2342" height="1678" alt="image" src="https://github.com/user-attachments/assets/f90d2c84-85c6-4e98-8a4a-47611e9df687" />


---

### Cursor IDE

1. Open **Cursor → Settings → MCP & Integrations**
2. Add a **Custom MCP Server**
3. Insert your server config (`server/weather.py`)
4. Save → Chat with weather tools directly in Cursor

<img width="2342" height="1670" alt="image" src="https://github.com/user-attachments/assets/a95a9984-0954-4c37-8480-0adfc602b069" />

