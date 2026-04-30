# 🤖 SoloAI Agent Framework
[![Build Status](https://img.shields.io/github/actions/workflow/status/soloai/agent-framework/ci.yml?branch=main&logo=github)](https://github.com/soloai/agent-framework/actions)
[![License](https://img.shields.io/badge/License-Apache_2.0-blue.svg)](https://opensource.org/licenses/Apache-2.0)
[![Python 3.10+](https://img.shields.io/badge/Python-3.10+-3776AB.svg?logo=python&logoColor=white)](https://www.python.org/)
[![PyPI](https://img.shields.io/pypi/v/soloai-agent.svg)](https://pypi.org/project/soloai-agent/)

SoloAI Agent Framework is a production-grade, modular development framework for designing, orchestrating, and deploying autonomous AI agents. It provides enterprise-ready abstractions for multi-agent workflows, tool integration, persistent memory, and observability, enabling developers to build scalable LLM-powered systems with minimal boilerplate.

---

## ✨ Key Features
- **Modular Architecture**: Pluggable LLM providers, memory backends, and tool executors via standardized interfaces.
- **Multi-Agent Orchestration**: DAG-based workflow engine with built-in routing, fallback strategies, and parallel execution.
- **State & Context Management**: Vector-backed memory, conversation history compression, and cross-session state persistence.
- **Tool/Plugin Ecosystem**: Auto-discovery, sandboxed execution, and JSON-schema validated tool calling for safe external integrations.
- **Observability & Evaluation**: OpenTelemetry-compatible tracing, prompt/version tracking, and automated benchmarking hooks.

---

## 📦 Installation

Requires **Python 3.10+**. Install via `pip`:

```bash
pip install soloai-agent
```

For development with optional dependencies (e.g., OpenAI, LangChain adapters, Redis memory):

```bash
pip install "soloai-agent[full]"
```

---

## 🚀 Quick Start

```python
import asyncio
from soloai import Agent, LLMProvider, MemoryStore

# Initialize core components
llm = LLMProvider("openai/gpt-4o", api_key="YOUR_API_KEY")
memory = MemoryStore("sqlite://./agent_state.db")

# Define a single agent
research_agent = Agent(
    name="TechAnalyst",
    llm=llm,
    memory=memory,
    system_prompt="You are a senior AI research analyst. Provide structured, citation-ready insights."
)

@research_agent.tool
async def search_papers(query: str, limit: int = 5) -> dict:
    """Simulated academic search tool."""
    return {"results": [f"Paper on {query} (2024)"] * limit}

# Execute
async def main():
    response = await research_agent.arun(
        "Summarize recent advancements in multimodal LLMs."
    )
    print(response.content)

asyncio.run(main())
```

---

## 🛠️ Usage Examples

### 1. Multi-Agent Workflow Orchestration
```python
from soloai import Orchestrator, Agent, Role

orchestrator = Orchestrator()

orchestrator.add_agent(
    Agent(name="Planner", role=Role.STRATEGIST, llm=llm),
    Agent(name="Coder", role=Role.DEVELOPER, llm=llm),
    Agent(name="Reviewer", role=Role.AUDITOR, llm=llm)
)

# Define execution graph
orchestrator.define_flow(
    start="Planner",
    edges=[
        ("Planner", "Coder", condition="plan_approved"),
        ("Coder", "Reviewer"),
        ("Reviewer", "Planner", condition="requires_revision", loop=True)
    ]
)

result = orchestrator.run("Build a REST API for user authentication with JWT.")
```

### 2. Custom Tool Registration & Validation
```python
from soloai.tools import ToolRegistry, ToolSchema

@ToolRegistry.register
class DatabaseConnector:
    schema = ToolSchema(
        name="query_db",
        description="Execute read-only SQL queries",
        parameters={"sql": {"type": "string", "description": "SELECT statement"}}
    )

    async def execute(self, sql: str) -> dict:
        # Secure execution logic here
        return {"status": "executed", "rows": []}
```

### 3. Deployment Configuration (Docker)
```dockerfile
FROM python:3.11-slim
WORKDIR /app
COPY requirements.txt .
RUN pip install --no-cache-dir soloai-agent[full]
COPY . .
EXPOSE 8000
CMD ["uvicorn", "soloai.serve:app", "--host", "0.0.0.0", "--port", "8000"]
```

---

## 🤝 Contributing Guidelines

We welcome contributions from developers, researchers, and enterprise teams. To maintain code quality and framework stability:

1. **Fork & Branch**: Create a feature branch from `main` (`git checkout -b feat/your-feature`).
2. **Code Standards**: Follow PEP 8, use type hints, and run `ruff check .` + `mypy .` before committing.
3. **Testing**: All PRs must include unit/integration tests. Run `pytest --cov=soloai` locally.
4. **Documentation**: Update `docs/` and inline docstrings for any public API changes.
5. **Pull Request**: Submit with a clear description, linked issues, and benchmark results (if applicable).

Please review our [CONTRIBUTING.md](CONTRIBUTING.md) and sign the Contributor License Agreement (CLA) before merging.

---

## 📜 License

This project is licensed under the **Apache License 2.0**. See the [LICENSE](LICENSE) file for full terms. Commercial usage is permitted with proper attribution and compliance with the license conditions.

---

## 💼 Business Inquiries & Enterprise Support

For custom integrations, SLA-backed deployments, or white-label solutions, contact our engineering team directly:

📧 **Email**: `379744050@qq.com`

📩 **Request a Fast Proposal**:  
To accelerate scoping and pricing, please include the following in your inquiry:
- Target **industry** / use case
- Expected **deliverables** (e.g., custom agents, orchestration pipelines, UI/dashboard, deployment)
- **Budget range**
- Project **deadline**

Our solutions architects will respond within 24 business hours with a tailored technical roadmap and commercial proposal.