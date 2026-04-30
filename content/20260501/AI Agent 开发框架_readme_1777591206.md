# 🤖 SoloAI Agent Framework

[![Build Status](https://img.shields.io/github/actions/workflow/status/SoloAI/agent-framework/ci.yml?branch=main&label=build)](https://github.com/SoloAI/agent-framework/actions)
[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](https://opensource.org/licenses/Apache-2.0)
[![Python](https://img.shields.io/badge/Python-3.9%2B-3776AB.svg)](https://www.python.org/)
[![PyPI](https://img.shields.io/pypi/v/soloai-agent-framework.svg)](https://pypi.org/project/soloai-agent-framework/)

A production-ready, modular framework for designing, orchestrating, and deploying autonomous AI agents. SoloAI Agent Framework abstracts LLM routing, tool integration, state management, and multi-agent coordination into a unified, enterprise-grade SDK optimized for scalability, observability, and rapid iteration.

---

## ✨ Key Features

| Feature | Description |
|---------|-------------|
| 🔀 **Dynamic LLM Routing & Fallback** | Seamlessly switch between OpenAI, Anthropic, open-weight, or on-prem models with automatic latency/cost optimization and graceful degradation. |
| 🧩 **Modular Tool & API Integration** | Native support for REST, GraphQL, MCP, and custom Python functions. Auto-generate JSON schemas for reliable LLM tool calling. |
| 🌐 **Multi-Agent Orchestration** | Supervisor/worker, peer-to-peer, and hierarchical patterns with shared memory, conflict resolution, and deterministic execution graphs. |
| 📊 **Built-in Observability & Tracing** | OpenTelemetry-compliant spans, structured logging, token/cost tracking, and automated evaluation pipelines (RAGAS, LangSmith compatible). |
| 🛡️ **Enterprise Security & Compliance** | Role-based access control (RBAC), PII redaction, prompt injection mitigation, audit trails, and SOC 2-ready deployment templates. |

---

## 📦 Installation

Requires **Python 3.9+**. Install via `pip` or `poetry`:

```bash
# Standard installation
pip install soloai-agent-framework

# With optional observability & cloud deployment extras
pip install "soloai-agent-framework[observability,deploy]"
```

> 💡 **Note:** Set your provider API keys via environment variables (`OPENAI_API_KEY`, `ANTHROPIC_API_KEY`, etc.) before initialization.

---

## 🚀 Quick Start

Create and run your first AI agent in under 10 lines of code:

```python
from soloai import Agent, LLMRouter, ToolRegistry

# 1. Configure LLM routing with automatic fallback
router = LLMRouter(
    primary="openai:gpt-4o",
    fallbacks=["anthropic:claude-3-5-sonnet", "ollama:llama-3-70b"],
    fallback_threshold_ms=2000
)

# 2. Register a typed tool
@ToolRegistry.register(description="Fetches real-time weather data for a given city")
def get_weather(city: str) -> dict:
    # Replace with actual API call
    return {"city": city, "temp_c": 22, "condition": "Sunny"}

# 3. Initialize and run the agent
agent = Agent(
    name="WeatherAssistant",
    llm=router,
    tools=[get_weather],
    memory="ephemeral"
)

response = agent.run("What's the current weather in Tokyo?")
print(response.output)  # Agent autonomously calls tool & formats answer
```

---

## 🛠️ Advanced Usage

### Multi-Agent Collaboration Pattern
```python
from soloai.orchestration import Supervisor, WorkerAgent, MessageBus

# Define specialized workers
researcher = WorkerAgent(name="Researcher", role="Web search & data extraction")
coder = WorkerAgent(name="Developer", role="Python script generation & validation")

# Supervisor coordinates execution flow
supervisor = Supervisor(
    agents=[researcher, coder],
    routing_strategy="task_decomposition",
    max_iterations=5
)

# Execute complex workflow
result = supervisor.run("Build a Python script that scrapes and visualizes GitHub trending repos.")
print(result.final_output)
```

### Persistent Memory & Evaluation Hook
```python
from soloai.memory import VectorMemory
from soloai.eval import MetricTracker

# Attach long-term vector memory
agent.memory = VectorMemory(provider="chromadb", collection="agent_context")

# Attach evaluation pipeline
tracker = MetricTracker(metrics=["accuracy", "latency_ms", "cost_usd"])
response = agent.run("Analyze Q3 financial trends and summarize key risks.", tracker=tracker)

print(tracker.summary())
```

---

## 🤝 Contributing

We welcome contributions from developers, researchers, and AI engineers. Please follow our workflow:

1. **Fork & Branch**: Create a feature branch from `main` (`git checkout -b feat/your-feature`).
2. **Code Standards**: Follow PEP 8, use `ruff` for linting, and `mypy` for type checking.
3. **Testing**: Ensure all new features include unit/integration tests (`pytest tests/`). Maintain ≥90% coverage.
4. **Documentation**: Update `docs/` and inline docstrings. Use Google-style docstrings.
5. **Pull Request**: Submit via GitHub with a clear description, linked issues, and test results.

See `CONTRIBUTING.md` for detailed guidelines, commit conventions, and architecture diagrams.

---

## 📜 License

This project is licensed under the **Apache License 2.0**. See the [LICENSE](LICENSE) file for full terms. Commercial usage, modification, and distribution are permitted under the conditions outlined in the license.

---

## 📩 Business Inquiries & Custom Solutions

For enterprise deployments, custom agent architectures, SLA-backed support, or white-label integrations, contact our solutions team directly:

📧 **Email:** `379744050@qq.com`

### 🚀 Get a Fast Proposal
To accelerate scoping and receive a tailored technical proposal within 24 hours, please include the following details in your inquiry:
- **Industry / Vertical** (e.g., FinTech, Healthcare, E-commerce, SaaS)
- **Expected Deliverables** (e.g., Multi-agent workflow, RAG pipeline, API gateway, UI dashboard)
- **Budget Range** (e.g., $5K–$10K, $10K–$50K, Enterprise/Custom)
- **Target Deadline** (e.g., MVP in 4 weeks, Production rollout by Q3)

Our engineering team will respond with architecture recommendations, timeline breakdowns, and transparent pricing. Let's build intelligent, scalable AI systems together.