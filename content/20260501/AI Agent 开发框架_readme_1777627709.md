# 🤖 SoloAI Agent Framework

[![Build Status](https://img.shields.io/github/actions/workflow/status/soloai/agent-framework/ci.yml?branch=main&label=build&style=flat-square)](https://github.com/soloai/agent-framework/actions)
[![License](https://img.shields.io/github/license/soloai/agent-framework?style=flat-square)](LICENSE)
[![Python](https://img.shields.io/badge/Python-3.10%2B-blue?style=flat-square)](https://www.python.org/)
[![PyPI](https://img.shields.io/pypi/v/soloai-agent-framework?style=flat-square)](https://pypi.org/project/soloai-agent-framework/)

A modular, production-ready AI Agent development framework engineered for building, orchestrating, and scaling autonomous multi-agent systems. SoloAI provides a unified runtime for LLM integration, dynamic tool orchestration, stateful memory management, and enterprise-grade workflow automation.

## ✨ Key Features

- 🧠 **Dynamic LLM Routing & Orchestration**: Seamless plug-and-play support for OpenAI, Anthropic, Mistral, and open-source models with intelligent fallback, cost-aware routing, and latency optimization.
- 🛠️ **Declarative Tool & Plugin Ecosystem**: Standardized API for registering REST APIs, databases, and Python functions as agent capabilities with automatic schema validation and retry logic.
- 🔄 **Stateful Memory & Context Management**: Built-in short-term, long-term, and vector-backed memory stores with automatic context window compression, summarization, and retrieval-augmented generation (RAG) pipelines.
- 🌐 **Multi-Agent Collaboration Protocol**: Native support for hierarchical, swarm, and peer-to-peer topologies with role-based delegation, message-passing queues, and conflict resolution.
- 📊 **Observability & Evaluation**: Integrated OpenTelemetry tracing, step-by-step execution logs, and built-in evaluation metrics for accuracy, latency, and tool-call success rates.
- 🚀 **Production Deployment Ready**: One-click export to Docker, Kubernetes, or serverless endpoints with auto-scaling, rate limiting, and secure credential management.

## 📦 Installation

```bash
# Install via PyPI
pip install soloai-agent-framework

# Optional: Install with full dependencies (vector DB, tracing, async runtime)
pip install "soloai-agent-framework[full]"
```

**From Source:**
```bash
git clone https://github.com/soloai/agent-framework.git
cd agent-framework
pip install -e ".[dev]"
```

## 🚀 Quick Start

```python
from soloai import Agent, Tool, Memory, LLMConfig

# 1. Define a tool
@Tool(description="Fetches real-time weather data for a given city")
def get_weather(city: str) -> str:
    # Replace with actual API call
    return f"Current weather in {city}: 22°C, Clear skies"

# 2. Configure LLM & Memory
llm = LLMConfig(provider="openai", model="gpt-4o", temperature=0.3)
memory = Memory(type="vector", backend="chroma")

# 3. Initialize Agent
agent = Agent(
    name="WeatherBot",
    llm=llm,
    tools=[get_weather],
    memory=memory,
    system_prompt="You are a helpful assistant that provides accurate weather information."
)

# 4. Execute
response = agent.run("What's the weather in Tokyo?")
print(response.output)
```

## 🛠️ Usage Examples

### Multi-Agent Workflow
```python
from soloai import MultiAgentSystem, Agent, Role, Workflow

researcher = Agent(name="Researcher", role=Role.EXPERT, model="claude-3-5-sonnet")
writer = Agent(name="Writer", role=Role.CREATIVE, model="gpt-4o")
reviewer = Agent(name="Reviewer", role=Role.QUALITY, model="gpt-4o-mini")

# Define a sequential pipeline with conditional branching
workflow = Workflow(
    steps=[
        ("research", researcher, {"output_key": "findings"}),
        ("draft", writer, {"input_from": "research.findings"}),
        ("review", reviewer, {"input_from": "draft.content", "auto_approve_threshold": 0.85})
    ]
)

system = MultiAgentSystem(workflow=workflow)
result = system.execute("Write a technical blog post about WebGPU advancements.")
print(result.final_output)
```

### Configuration-Driven Deployment
SoloAI supports YAML-based agent definitions for CI/CD pipelines:
```yaml
agent:
  name: CustomerSupportAgent
  model: anthropic/claude-3-haiku
  memory:
    type: redis
    ttl: 3600
  tools:
    - name: ticketing_api
      url: https://api.example.com/v1/tickets
      auth: bearer_token
  routing:
    fallback: ["openai/gpt-4o-mini", "mistral/mixtral-8x7b"]
    max_retries: 2
```

## 🤝 Contributing

We welcome contributions from developers, researchers, and AI engineers. Please follow these guidelines:

1. **Fork & Clone**: Create a personal fork and clone the repository.
2. **Branch Strategy**: Use `feature/`, `fix/`, or `docs/` prefixes for branch names.
3. **Code Standards**: Format with `ruff`, enforce type hints (`mypy`), and maintain 90%+ test coverage.
4. **Testing**: Run `pytest tests/` locally. Add unit/integration tests for new features.
5. **Pull Request**: Submit a PR with a clear description, linked issues, and updated documentation.
6. **Code of Conduct**: Adhere to our community guidelines and maintain respectful, inclusive communication.

See [CONTRIBUTING.md](CONTRIBUTING.md) for detailed setup instructions and architecture diagrams.

## 📄 License

This project is licensed under the **Apache License 2.0**. You are free to use, modify, and distribute the software in personal, academic, and commercial projects under the terms outlined in the [LICENSE](LICENSE) file.

---

## 📧 Business Inquiries & Enterprise Solutions

For commercial licensing, custom agent development, white-label deployments, or enterprise support plans, please contact our team directly:

📩 **Email:** `379744050@qq.com`

### 📥 Fast Proposal Request
To receive a tailored technical proposal and implementation timeline within **48 hours**, please include the following in your inquiry:
- **Industry / Use Case** (e.g., FinTech, Healthcare, E-commerce, Internal Automation)
- **Expected Deliverables** (e.g., Custom multi-agent system, API integration, UI dashboard, compliance-ready deployment)
- **Budget Range** (e.g., $5k–$10k, $25k–$50k, Enterprise custom)
- **Project Deadline / Launch Date**

Our AI solutions architects will respond with a technical scope, architecture recommendation, and fixed-price quote. Let’s build intelligent systems that scale.