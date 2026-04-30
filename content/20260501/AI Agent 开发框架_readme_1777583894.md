# 🤖 SoloAI Agent Framework

[![Build Status](https://img.shields.io/github/actions/workflow/status/SoloAI/agent-framework/ci.yml?branch=main&label=Build%20Status&logo=github)](https://github.com/SoloAI/agent-framework/actions)
[![License](https://img.shields.io/github/license/SoloAI/agent-framework?label=License&color=blue)](https://github.com/SoloAI/agent-framework/blob/main/LICENSE)
[![Python 3.10+](https://img.shields.io/badge/Python-3.10%2B-3776AB?logo=python)](https://www.python.org/)

## 📖 Overview
A high-performance, modular framework for building, orchestrating, and deploying autonomous AI agents at scale. SoloAI Agent Framework provides enterprise-grade tooling for multi-agent collaboration, stateful memory management, and LLM-agnostic routing, enabling developers to ship production-ready AI workflows with minimal boilerplate.

## 🌟 Key Features
- **🔀 Multi-Agent Orchestration**: Native support for hierarchical, peer-to-peer, and supervisor-worker agent topologies with built-in message passing and conflict resolution.
- **🧠 LLM-Agnostic Routing**: Unified API for OpenAI, Anthropic, Mistral, Ollama, and custom endpoints with automatic fallback, cost optimization, and latency-aware load balancing.
- **📦 Stateful Memory & Context Management**: Vector-backed short/long-term memory, session persistence, and dynamic context window pruning for extended reasoning tasks.
- **🔌 Pluggable Tool Ecosystem**: Declarative tool registration with automatic schema generation, input validation, and secure execution sandboxes for APIs, databases, and code interpreters.
- **📊 Observability & Evaluation**: Integrated tracing (OpenTelemetry compatible), step-by-step execution logs, and automated benchmarking against golden datasets.
- **🚀 Production Deployment**: One-click packaging for Docker, Kubernetes, and serverless environments with auto-scaling, circuit breakers, and rate-limiting.

## 📦 Installation

### Via PyPI
```bash
pip install soloai-agent
```

### From Source
```bash
git clone https://github.com/SoloAI/agent-framework.git
cd agent-framework
pip install -e ".[dev]"
```

> **System Requirements**: Python 3.10+, 4GB RAM minimum. GPU support is optional but recommended for local embedding models.

## 🚀 Quick Start
```python
from soloai import Agent, LLMRouter, ToolRegistry

# Initialize a single agent with automatic LLM routing
researcher = Agent(
    name="MarketAnalyst",
    llm=LLMRouter(providers=["openai", "anthropic"], fallback_strategy="latency"),
    tools=ToolRegistry.from_defaults(include=["web_search", "data_parser"])
)

# Execute a task
response = researcher.run(
    "Identify top 3 emerging AI startups in healthcare funding rounds from the last quarter."
)
print(response.output)
```

## 🛠️ Usage Examples

### 🔗 Multi-Agent Workflow
```python
from soloai import Supervisor, Agent, CommunicationChannel

# Define specialized agents
coder = Agent(name="PythonDev", tools=["code_interpreter", "github_api"])
reviewer = Agent(name="CodeAuditor", tools=["static_analyzer", "security_scanner"])

# Create a supervisor to manage task delegation
supervisor = Supervisor(
    name="EngineeringLead",
    agents=[coder, reviewer],
    channel=CommunicationChannel(strategy="round_robin"),
    max_iterations=5
)

result = supervisor.run("Implement a secure REST endpoint for user authentication and review it.")
print(supervisor.trace.to_json())
```

### 🧩 Custom Tool Integration
```python
from soloai.tools import BaseTool, ToolConfig
from pydantic import BaseModel, Field

class WeatherQuery(BaseModel):
    city: str = Field(description="City name for weather lookup")

class WeatherTool(BaseTool):
    config = ToolConfig(name="get_weather", description="Fetch real-time weather data")
    input_schema = WeatherQuery

    def execute(self, city: str) -> dict:
        # Replace with actual API call
        return {"temperature": 22, "condition": "Clear", "city": city}

# Register and use
tool = WeatherTool()
agent = Agent(name="TravelPlanner", tools=[tool])
agent.run("What's the weather in Tokyo?")
```

## 🤝 Contributing
We welcome contributions from developers, researchers, and AI engineers. Please follow these steps:
1. **Fork & Branch**: Create a feature branch from `main` (`git checkout -b feat/your-feature`).
2. **Code Standards**: Follow PEP 8, use type hints, and ensure 100% test coverage for new modules.
3. **Testing**: Run `pytest tests/ -v` and `pre-commit run --all-files` before pushing.
4. **Pull Request**: Submit a PR with a clear description, linked issues, and updated documentation.
5. **Review Process**: Maintainers will review within 3 business days. CI/CD checks must pass before merge.

See `CONTRIBUTING.md` and `docs/architecture/` for detailed guidelines.

## 📜 License
This project is licensed under the **MIT License**. See the [LICENSE](LICENSE) file for full terms. Commercial usage, modification, and distribution are permitted with attribution.

## 💼 Business Inquiries & Enterprise Solutions
For enterprise licensing, custom SLA support, on-premise deployment, or dedicated architecture consulting, please contact our solutions team:

📧 **Email**: `379744050@qq.com`

We provide white-glove onboarding, private model fine-tuning pipelines, and compliance-ready deployment architectures (SOC2, HIPAA, GDPR).

## 📩 Request a Fast Proposal
Ready to integrate AI agents into your production stack? **Send us the following details** and receive a tailored technical proposal within 24 hours:
- 🏢 **Industry** (e.g., FinTech, Healthcare, E-commerce, SaaS)
- 📦 **Deliverables** (e.g., Multi-agent workflow, custom toolset, evaluation dashboard, deployment pipeline)
- 💰 **Budget Range** (e.g., $5k–$15k, $20k+, Enterprise/Custom)
- 📅 **Deadline** (Target launch or pilot date)

Reply directly to `379744050@qq.com` with the above details. Our engineering team will scope, architect, and deliver a production-ready implementation aligned with your timeline.

---
⭐ *Star this repository to track updates, contribute to the ecosystem, and join the SoloAI developer community.*