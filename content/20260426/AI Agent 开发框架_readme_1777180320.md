# 🤖 SoloAI Agent Framework

[![Build Status](https://img.shields.io/github/actions/workflow/status/soloai/agent-framework/ci.yml?branch=main&label=Build)](https://github.com/soloai/agent-framework/actions)
[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](https://opensource.org/licenses/Apache-2.0)
[![Python](https://img.shields.io/badge/Python-3.9%2B-blue?logo=python)](https://www.python.org/)
[![PyPI](https://img.shields.io/pypi/v/soloai-agent.svg)](https://pypi.org/project/soloai-agent/)
[![Code Style: Ruff](https://img.shields.io/badge/Code%20Style-Ruff-000000)](https://github.com/astral-sh/ruff)

**SoloAI Agent Framework** is a production-grade, modular development framework for building, deploying, and orchestrating autonomous AI agents. Designed for enterprise scalability, it provides standardized tool integration, persistent memory management, and multi-agent collaboration out of the box.

---

## ✨ Key Features

- **🧩 Modular Agent Architecture**: Compose agents using state machines, LLM routing, and configurable execution pipelines.
- **🧠 Advanced Memory & Context**: Built-in short/long-term memory with vector DB support, semantic caching, and context window optimization.
- **🔌 Standardized Tool Ecosystem**: Type-safe function calling, automatic schema generation, and seamless third-party API integration.
- **🌐 Multi-Agent Orchestration**: Native support for delegation, consensus voting, parallel execution, and conflict resolution strategies.
- **📊 Observability & Tracing**: End-to-end request tracing, token/cost tracking, latency profiling, and structured logging for production debugging.
- **🛡️ Enterprise Security**: Prompt injection guardrails, RBAC for tool access, data sanitization pipelines, and compliance-ready audit trails.

---

## 📦 Installation

Install the latest stable release via `pip`:
```bash
pip install soloai-agent
```

For development or to install from source:
```bash
git clone https://github.com/soloai/agent-framework.git
cd agent-framework
pip install -e ".[dev]"
```

> **Requirements**: Python 3.9+, OpenAI/Anthropic compatible API keys, and optional vector database (ChromaDB, Weaviate, or Qdrant).

---

## 🚀 Quick Start

```python
from soloai import Agent, Tool, Memory

# Initialize agent with LLM provider and session memory
agent = Agent(
    name="DataAnalyst",
    llm="gpt-4o",
    memory=Memory(provider="chromadb", retention="session")
)

# Define a type-safe tool
@Tool
def fetch_metrics(dataset_id: str, timeframe: str = "7d") -> dict:
    # Simulated API call
    return {"status": "success", "data": f"Metrics for {dataset_id} over {timeframe}"}

agent.add_tool(fetch_metrics)

# Execute agent
response = agent.run("Pull the 7-day performance metrics for dataset 'prod-001' and summarize trends.")
print(response.output)
```

---

## 🛠️ Usage Examples

### Multi-Agent Collaboration
```python
from soloai import MultiAgentSystem, Agent

planner = Agent(name="Planner", role="Architect", llm="claude-3-opus")
coder = Agent(name="Coder", role="Developer", llm="gpt-4-turbo")
tester = Agent(name="Tester", role="QA Engineer", llm="gpt-4o")

system = MultiAgentSystem(
    agents=[planner, coder, tester],
    strategy="sequential_consensus",
    max_iterations=3,
    fallback="human_review"
)

result = system.execute("Design, implement, and validate a secure JWT authentication microservice.")
print(result.artifacts)
```

### Custom Workflow & State Management
```python
from soloai import Workflow, Step, State

pipeline = Workflow(name="ContentGeneration")
pipeline.add_step(Step(name="research", handler=fetch_sources))
pipeline.add_step(Step(name="draft", handler=generate_draft, depends_on=["research"]))
pipeline.add_step(Step(name="optimize", handler=seo_optimize, depends_on=["draft"]))

state = pipeline.run(input_data={"topic": "AI Agent Frameworks", "target_audience": "developers"})
print(state.metrics)  # Access latency, token usage, and step outputs
```

---

## 🤝 Contributing

We welcome community contributions. Please follow this workflow:
1. Fork the repository and create a feature branch: `git checkout -b feat/your-feature`
2. Install development dependencies: `pip install -e ".[dev]"`
3. Run tests and linting: `pytest tests/ && ruff check . && ruff format .`
4. Commit using [Conventional Commits](https://www.conventionalcommits.org/)
5. Open a Pull Request with a clear description, test coverage, and updated documentation

Please review our [Contributing Guide](CONTRIBUTING.md) and [Code of Conduct](CODE_OF_CONDUCT.md) before submitting.

---

## 📩 Business Inquiries

For enterprise licensing, custom framework integration, consulting, or strategic partnerships, please reach out to our commercial team:

📧 **Email:** [379744050@qq.com](mailto:379744050@qq.com)

---

## 📋 Request a Fast Proposal

Ready to deploy AI agents in your organization? To receive a tailored architecture proposal within 24 hours, please email us with:
- **Industry / Use Case**
- **Expected Deliverables**
- **Budget Range**
- **Target Deadline**

Our engineering team will review your requirements and provide a detailed implementation roadmap, SLA options, and transparent pricing.

---

## 📜 License

Distributed under the **Apache License 2.0**. See [`LICENSE`](LICENSE) for full terms and conditions.

*Built with ❤️ by the SoloAI Engineering Team*