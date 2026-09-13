# LangChain Serve & LangSmith Integration

A production-ready application framework designed to build, monitor, and deploy Large Language Model (LLM) applications. This repository implements **LangChain** orchestration logic, seamlessly integrated with **LangSmith** for full-stack observability, tracking, and debugging, alongside **LangServe** to expose your chains as production-ready web APIs.

## 🚀 Key Features
* **Production Deployment:** Easily wraps LangChain computational graphs into ready-to-use HTTP REST APIs via LangServe.
* **Full Observability:** Out-of-the-box tracking with LangSmith to monitor latency, track token usage, visualize prompt inputs/outputs, and debug agent execution steps.
* **Streamlined Integration:** Provides unified handling of API request/response validation using Pydantic schemas standard in LangServe endpoints.

## 🏗️ System Architecture

The workflow follows a standard enterprise deployment and observability pipeline:

🛠️ Build (LangChain)        🚀 Deploy (LangServe)       📊 Monitor (LangSmith)+-----------------------+     +--------------------+     +-----------------------+|  LLM Prompt Templates |     |   FastAPI App /    |     | Real-time Tracing     ||           +           | --->|   Serve Endpoints  | --->| Token Usage Analysis  ||  LCEL Component Chains|     |  (/invoke, /stream)|     | Step-by-Step Debugging|+-----------------------+     +----------+---------+     +-----------------------+|v📡 Exposed REST API


1. **Build:** Logic is chained using LangChain Expression Language (LCEL).
2. **Deploy:** `serve.py` uses LangServe to expose the application through a high-performance framework (like FastAPI), generating automatic API documentation.
3. **Monitor:** Every run, trace, and chain variable is securely logged to the LangSmith cloud backend for performance profiling.

## 🛠️ Tech Stack
* **Orchestration:** LangChain
* **API Service:** LangServe (FastAPI under the hood)
* **LLM Ops / Tracing:** LangSmith
* **Language:** Python 3.10+

## 📁 Repository Structure
* `serve.py`: The core application server file. It instantiates the LangChain components, establishes the LangSmith environment variables, hooks up the routing middleware, and spins up the live API server.

## ⚙️ Getting Started

### 1. Clone the Repository
```bash
git clone https://github.com
cd langchain-serve
```

### 2. Set Up a Virtual Environment
```bash
python -m venv venv
# On Windows:
venv\Scripts\activate
# On macOS/Linux:
source venv/bin/activate
```

### 3. Install Dependencies
```bash
pip install langchain langserve langsmith fastapi uvicorn python-dotenv
```

### 4. Configure Environment Variables
Create a `.env` file in your root directory to link your LangSmith account and provide your LLM API credentials:
```env
# LangSmith Configuration
LANGCHAIN_TRACING_V2=true
LANGCHAIN_ENDPOINT="https://langchain.com"
LANGCHAIN_API_KEY=your_langsmith_api_key_here
LANGCHAIN_PROJECT="your-project-name"

# Model Provider Configuration
OPENAI_API_KEY=your_openai_api_key_here
# OR if using Groq
GROQ_API_KEY=your_groq_api_key_here
```

### 5. Launch the Server
```bash
python serve.py
```
Your API endpoints will now be hosted locally (typically at `http://localhost:8000`). You can visit `http://localhost:8000/docs` to view the interactive Swagger API documentation, or go to `http://localhost:8000/[your-chain-endpoint]/playground` to test the chain directly in a web UI.

## 📝 License
This project is open-source and available under the MIT License.
