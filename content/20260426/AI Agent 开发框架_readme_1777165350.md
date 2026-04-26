# 🤖 SoloAI Agent Framework

[![CI/CD Build](https://img.shields.io/badge/build-passing-brightgreen?logo=github)](https://github.com/SoloAI/agent-framework/actions)
[![License](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![Python 3.10+](https://img.shields.io/badge/python-3.10%2B-blue?logo=python)](https://www.python.org/)

A production-grade, modular **AI Agent Development Framework** engineered for building, orchestrating, and scaling autonomous multi-agent systems. SoloAI abstracts LLM complexity while providing enterprise-ready toolchains, stateful memory, and full observability out of the box.

---

## ✨ Key Features

| Capability | Description |
|------------|-------------|
| 🔌 **Unified LLM Abstraction** | Plug-and-play routing for OpenAI, Anthropic, Mistral, local vLLM/Ollama, and custom fine-tuned models via a single API contract. |
| 🕸️ **Multi-Agent Orchestration** | Native support for hierarchical, swarm, debate, and supervisor-worker patterns with built-in conflict resolution and consensus voting. |
| 🧠 **Stateful Memory & Context** | Hybrid short/long-term memory with vector indexing, automatic context-window optimization, and semantic retrieval. |
| 🛠️ **Extensible Tool Ecosystem** | Type-safe function calling, REST/gRPC integration, sandboxed Python/JS execution, and dynamic tool discovery. |
| 📊 **Production Observability** | OpenTelemetry-compliant tracing, latency/cost profiling, automated evaluation pipelines, and real-time agent telemetry. |
| 🚀 **Zero-Config Deployment** | Docker, Kubernetes, and serverless-ready with health checks, auto-scaling hooks, and CI/CD pipeline templates. |

---

## 📦 Installation

**Via PyPI (Recommended)**
```bash
pip install soloai-agent
```

**From Source (Latest Features)**
```bash
git clone https://github.com/SoloAI/agent-framework.git
cd agent-framework
pip install -e ".[dev,deploy]"
```

> 💡 *Requires Python 3.10+. For GPU acceleration, install `torch` and `vllm` separately.*

---

## 🚀 Quick Start

Create and run a single autonomous agent in under 10 lines of code:

```python
from soloai import Agent, Memory, ToolRegistry
from soloai.models import OpenAIModel

# 1. Configure model & memory
llm = OpenAIModel(api_key="sk-...", model="gpt-4o")
memory = Memory(type="vector", backend="chromadb", retention="7d")

# 2. Initialize agent with toolchain
agent = Agent(
    name="DataAnalyst",
    model=llm,
    memory=memory,
    tools=ToolRegistry(["web_search", "python_interpreter", "csv_parser"])
)

# 3. Execute task
response = await agent.run("Fetch Q3 2024 SaaS revenue data, clean it, and output a markdown summary.")
print(response.output)
```

---

## 🛠️ Usage Examples

### 🔹 Multi-Agent Swarm Orchestration
```python
from soloai.orchestration import SwarmOrchestrator
from soloai.agents import Planner, Executor, Reviewer

agents = [
    Planner(name="Architect", role="system_design"),
    Executor(name="Engineer", role="code_implementation"),
    Reviewer(name="QA", role="testing_validation")
]

swarm = SwarmOrchestrator(
    agents=agents,
    strategy="hierarchical",
    max_iterations=5,
    consensus_threshold=0.8
)

result = await swarm.execute("Design and implement a rate-limited authentication microservice.")
print(result.artifacts)  # Returns structured code, tests, and deployment config
```

### 🔹 Custom Tool Integration
```python
from soloai.tools import Tool, Parameter
from pydantic import BaseModel

class WeatherParams(BaseModel):
    city: str
    unit: str = "celsius"

@Tool.register(name="get_weather", description="Fetch real-time weather data")
async def fetch_weather(params: WeatherParams) -> dict:
    # Simulated API call
    return {"city": params.city, "temp": 22, "unit": params.unit}

# Tool is automatically available to any agent using ToolRegistry()
```

### 🔹 YAML-Driven Production Config
```yaml
# agent_config.yaml
agent:
  name: "CustomerSupportBot"
  model: "anthropic/claude-3-sonnet"
  memory:
    type: "redis_vector"
    ttl_hours: 48
  orchestration:
    type: "supervisor"
    fallback_on_error: true
  observability:
    tracing: "otel"
    log_level: "INFO"
```
```python
from soloai.config import load_config
config = load_config("agent_config.yaml")
agent = Agent.from_config(config)
```

---

## 🤝 Contributing

We welcome contributions from developers, researchers, and AI engineers. Please follow our workflow:

1. **Fork & Branch:** Create a feature branch (`feat/`, `fix/`, `docs/`)
2. **Code Standards:** Run `ruff check .` and `mypy .` before committing
3. **Testing:** Add unit/integration tests (`pytest tests/`) and ensure `coverage >= 90%`
4. **Documentation:** Update `docs/` and docstrings for all public APIs
5. **Pull Request:** Submit with a clear description, linked issue, and benchmark results (if performance-related)

📖 See `CONTRIBUTING.md` for detailed guidelines, architecture diagrams, and local dev setup.

---

## 📄 License

This project is licensed under the **MIT License** – see the [LICENSE](LICENSE) file for details. You are free to use, modify, and distribute this framework for commercial and open-source projects.

---

## 💼 Business Inquiries & Custom Solutions

SoloAI offers enterprise-grade customization, dedicated support, and white-label AI agent deployments tailored to your infrastructure and compliance requirements.

📧 **Contact:** `379744050@qq.com`

🚀 **Fast-Track Proposal Request**  
To receive a customized technical proposal within 24 hours, please email us with the following details:
- **Industry / Vertical** (e.g., FinTech, Healthcare, E-commerce, SaaS)
- **Expected Deliverables** (e.g., multi-agent workflow, RAG pipeline, API integration, on-prem deployment)
- **Budget Range** (e.g., $5k–$10k, $10k–$25k, Enterprise/Custom)
- **Target Deadline** (e.g., MVP in 4 weeks, Full rollout by Q2 2025)

Our engineering team will respond with architecture recommendations, implementation timelines, and transparent pricing.