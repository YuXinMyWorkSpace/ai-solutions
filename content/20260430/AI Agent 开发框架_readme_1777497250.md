# 🤖 SoloAI Agent Framework

[![Build Status](https://img.shields.io/github/actions/workflow/status/SoloAI/agent-framework/ci.yml?branch=main&label=build&logo=github)](https://github.com/SoloAI/agent-framework/actions) [![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](https://opensource.org/licenses/Apache-2.0) [![Python](https://img.shields.io/badge/Python-3.9%2B-blue?logo=python)](https://www.python.org/)

SoloAI Agent Framework is a production-ready, modular architecture for designing, orchestrating, and deploying autonomous AI agents. It provides a unified Python SDK for LLM integration, tool routing, stateful memory management, and multi-agent collaboration, optimized for enterprise scalability and low-latency inference.

---

## 🚀 Key Features

1. **Framework-Agnostic LLM Routing** – Seamlessly switch between OpenAI, Anthropic, Mistral, or self-hosted models with zero code refactoring.
2. **Declarative Tool & Plugin System** – Register Python functions, REST APIs, or MCP servers as agent tools with automatic schema validation and type safety.
3. **Stateful Memory & Context Management** – Built-in short-term, long-term, and vector-backed memory with automatic context window pruning and summarization.
4. **Multi-Agent Orchestration** – Native support for supervisor, swarm, and hierarchical routing patterns with conflict resolution and task delegation.
5. **Production Observability** – Integrated tracing, token accounting, latency profiling, and OpenTelemetry-compatible export for enterprise monitoring.
6. **Async & Streaming Execution** – Fully asynchronous runtime with token-level streaming, cancellation support, and graceful error recovery.

---

## 📦 Installation

```bash
# Create and activate a virtual environment (recommended)
python -m venv .venv && source .venv/bin/activate

# Install core package
pip install soloai-agent

# Install with full LLM adapters, vector memory, and observability extras
pip install "soloai-agent[full]"
```

> 💡 Requires Python 3.9+. For GPU-accelerated local inference, install the optional `torch` and `vllm` dependencies separately.

---

## ⚡ Quick Start

```python
from soloai.agent import Agent
from soloai.tools import WebSearch, Calculator
from soloai.memory import PersistentMemory

# Initialize a single agent with tools and memory
agent = Agent(
    name="MarketAnalyst",
    model="openai:gpt-4o",
    tools=[WebSearch(), Calculator()],
    memory=PersistentMemory(backend="sqlite", path="./agent_memory.db")
)

# Execute a task
response = agent.run(
    "Find the current stock price of Apple and calculate a 12% increase."
)

print(response.content)
```

---

## 🛠️ Usage Examples

### 1. Custom Tool Definition
```python
from soloai.tools import Tool
from pydantic import BaseModel, Field

class QueryParams(BaseModel):
    ticker: str = Field(..., description="Stock ticker symbol")

@Tool.register(
    name="fetch_stock_price",
    description="Retrieves real-time price for a given ticker",
    input_schema=QueryParams
)
def fetch_stock_price(ticker: str) -> float:
    # Simulated API call
    return {"AAPL": 189.50, "MSFT": 412.30}.get(ticker.upper(), 0.0)
```

### 2. Multi-Agent Supervisor Pattern
```python
from soloai.orchestration import Supervisor, Agent

researcher = Agent(name="Researcher", model="anthropic:claude-3-sonnet", tools=[WebSearch()])
analyst = Agent(name="Analyst", model="openai:gpt-4o", tools=[Calculator()])

supervisor = Supervisor(
    name="ResearchPipeline",
    agents=[researcher, analyst],
    routing_strategy="dynamic_delegation",
    max_iterations=5
)

result = supervisor.run("Analyze Q3 earnings trends for NVIDIA and summarize key risks.")
print(result.final_output)
```

### 3. Streaming & Observability Hook
```python
from soloai.callbacks import TokenStreamCallback
from soloai.tracing import OpenTelemetryTracer

agent = Agent(
    name="StreamBot",
    model="mistral:mistral-large",
    callbacks=[TokenStreamCallback(), OpenTelemetryTracer()]
)

async for chunk in agent.run_async("Explain transformer architecture step-by-step."):
    print(chunk.delta, end="", flush=True)
```

---

## 🤝 Contributing

We welcome contributions from the open-source community. Please follow these guidelines:

1. **Fork & Branch**: Fork the repository and create a feature branch (`feat/your-feature` or `fix/issue-#`).
2. **Code Standards**: Follow PEP 8, use type hints, and run `ruff check . && mypy .` before committing.
3. **Testing**: Add unit/integration tests under `tests/`. Ensure 100% coverage for new modules. Run `pytest --cov=soloai`.
4. **Pull Request**: Submit a PR with a clear description, linked issues, and benchmark results (if applicable).
5. **Documentation**: Update `docs/` and docstrings for any public API changes.

All contributions are subject to the project's Code of Conduct and require signed DCO (Developer Certificate of Origin).

---

## 📄 License

This project is licensed under the **Apache License 2.0**. See the [LICENSE](LICENSE) file for full terms. You may use, modify, and distribute this software for commercial and non-commercial purposes in compliance with the license.

---

## 💼 Business Inquiries & Enterprise Solutions

For custom AI agent development, enterprise licensing, SLA-backed support, or on-premise deployment, contact our solutions team:

📧 **379744050@qq.com**

📝 **Request a Fast Proposal**  
To accelerate your project timeline, please include the following details in your initial inquiry:
- 🏢 **Target Industry** (e.g., FinTech, Healthcare, SaaS, Manufacturing)
- 📦 **Expected Deliverables** (e.g., custom agent workflows, API integrations, deployment pipelines, UI/UX)
- 💰 **Budget Range** (e.g., $10k–$25k, $50k+, or custom)
- 📅 **Project Deadline** (Target launch or MVP date)

Our engineering team will review your requirements and respond within **24 hours** with a tailored technical architecture and commercial proposal.