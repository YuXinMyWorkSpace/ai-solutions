# 🤖 SoloAI Agent Framework

![Build Status](https://img.shields.io/github/actions/workflow/status/SoloAI/agent-framework/ci.yml?branch=main&label=Build)
![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)
![Python](https://img.shields.io/badge/Python-3.10%2B-blue)
![PyPI](https://img.shields.io/pypi/v/soloai-agent)

A production-grade, modular framework for building, orchestrating, and deploying autonomous AI agents. Designed for enterprise and developer workflows, SoloAI Agent Framework provides standardized LLM routing, stateful memory management, multi-agent coordination, and enterprise observability out of the box.

---

## ✨ Key Features

| Feature | Description |
|---------|-------------|
| 🔌 **Plugin-First Architecture** | Decoupled tool, memory, and LLM provider interfaces with hot-swappable adapters |
| 🌐 **Multi-Agent Orchestration** | Native support for hierarchical, peer-to-peer, and swarm-based agent workflows |
| 🧠 **Stateful Context & Memory** | Vector-backed short/long-term memory with session isolation and retrieval optimization |
| 📊 **Enterprise Observability** | Built-in tracing, latency metrics, token tracking, and OpenTelemetry-compatible logging |
| ⚡ **Async & Type-Safe SDK** | Fully typed Python API with `asyncio`-first execution and runtime validation |
| 🚀 **Cross-Platform Deployment** | One-command packaging for Docker, Kubernetes, AWS Lambda, and serverless runtimes |

---

## 📦 Installation

### Via PyPI
```bash
pip install soloai-agent
```

### From Source (Development)
```bash
git clone https://github.com/SoloAI/agent-framework.git
cd agent-framework
python -m venv .venv && source .venv/bin/activate
pip install -e ".[dev]"
```

---

## 🚀 Quick Start

Create a single autonomous agent with tool binding and memory in under 10 lines:

```python
from soloai import Agent, Tool, Memory
from soloai.llm import OpenAIProvider

# 1. Configure LLM backend
llm = OpenAIProvider(api_key="your-api-key", model="gpt-4o")

# 2. Register a custom tool
@Tool.register
def fetch_market_data(symbol: str) -> dict:
    return {"symbol": symbol, "price": 182.45, "trend": "bullish"}

# 3. Initialize & execute agent
agent = Agent(
    name="MarketAnalyst",
    llm=llm,
    memory=Memory(session_id="demo_001", backend="sqlite"),
    tools=[fetch_market_data]
)

response = agent.run("Analyze the current trend for AAPL and recommend next steps.")
print(response.output)
```

---

## 🛠️ Usage Examples

### Multi-Agent Workflow (Supervisor + Workers)
```python
from soloai.orchestration import MultiAgentWorkflow, SupervisorAgent, WorkerAgent

supervisor = SupervisorAgent(
    llm=llm,
    strategy="hierarchical",
    planning_prompt="Break down tasks and delegate to specialized workers."
)

coder = WorkerAgent(llm=llm, role="BackendEngineer", tools=[code_executor])
reviewer = WorkerAgent(llm=llm, role="QAReviewer", tools=[linter, test_runner])

workflow = MultiAgentWorkflow(
    supervisor=supervisor,
    workers=[coder, reviewer],
    max_iterations=3,
    timeout_sec=120
)

result = workflow.execute("Implement and validate a rate-limited FastAPI endpoint.")
print(f"✅ Final Output: {result.final_output}")
print(f"📊 Execution Trace: {workflow.get_trace_summary()}")
```

### Streaming & Event Hooks
```python
from soloai.events import EventStream

stream = EventStream()
stream.on("tool_call", lambda ev: print(f"🔧 Calling: {ev.tool_name}"))
stream.on("llm_token", lambda ev: print(ev.token, end="", flush=True))

agent = Agent(llm=llm, memory=Memory(), stream=stream)
agent.run_stream("Generate a step-by-step deployment guide for Kubernetes.")
```

---

## 🤝 Contributing

We welcome contributions from developers, researchers, and AI engineers.

1. **Fork & Clone** the repository
2. Create a feature branch: `git checkout -b feat/your-feature`
3. Install dev dependencies: `pip install -e ".[dev]"`
4. Run tests & linting: `pytest && ruff check .`
5. Commit using [Conventional Commits](https://www.conventionalcommits.org/)
6. Open a Pull Request with a clear description, test coverage, and benchmark results (if applicable)

📖 Full guidelines: [`CONTRIBUTING.md`](CONTRIBUTING.md)

---

## 📜 License

This project is licensed under the **Apache License 2.0**. See the [`LICENSE`](LICENSE) file for details. Commercial usage, modification, and distribution are permitted under the terms of the license.

---

## 💼 Business Inquiries & Enterprise Support

For enterprise licensing, custom integrations, SLA-backed support, or on-premise deployment assistance, please contact our solutions team:

📧 **379744050@qq.com**

---

## 📩 Request a Custom Proposal

🚀 **Need a tailored AI agent solution for your organization?**  
To receive a fast, customized proposal within **24 hours**, please email us with:
- **Industry / Vertical** (e.g., FinTech, Healthcare, E-commerce, SaaS)
- **Expected Deliverables** (e.g., autonomous customer support agent, data pipeline orchestrator, internal workflow bot)
- **Budget Range**
- **Project Deadline**

Our engineering team will respond with architecture recommendations, implementation timelines, and pricing tailored to your requirements.