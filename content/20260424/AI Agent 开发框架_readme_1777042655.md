# SoloAI Agent Framework 🤖
![Build Status](https://img.shields.io/badge/Build-Passing-brightgreen)
![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)
![Python](https://img.shields.io/badge/Python-3.10%2B-blue)

SoloAI Agent Framework is a high-performance, modular development toolkit for building, orchestrating, and deploying production-ready AI agents. Designed for developers and enterprises, it streamlines LLM integration, tool calling, memory management, and multi-agent collaboration through a unified, type-safe API.

## ✨ Key Features
- **Declarative Agent Definition**: Define agents, roles, and workflows using Python decorators or YAML configuration with full type safety.
- **Advanced Tool & Plugin Ecosystem**: Auto-discover, validate, and execute external APIs, databases, and custom functions with built-in schema enforcement.
- **Stateful Memory & Context Optimization**: Hybrid short/long-term memory with vector-backed retrieval and dynamic context window compression.
- **Multi-Agent Orchestration**: Native support for supervisor-worker patterns, debate routing, and parallel execution with conflict resolution.
- **Built-in Observability & Evaluation**: Integrated tracing, latency/metrics logging, and automated benchmarking for agent reliability.

## 📦 Installation
Requires Python 3.10+. Install via pip:
```bash
pip install soloai-agent
```

Install optional provider integrations:
```bash
# OpenAI, Anthropic, Local LLMs, Vector DBs
pip install soloai-agent[openai,anthropic,local,chromadb]
```

## 🚀 Quick Start
```python
from soloai import Agent, Tool, LLMProvider

@Tool(name="fetch_weather", description="Retrieve current weather data for a given city")
def fetch_weather(city: str) -> str:
    # Simulated tool execution
    return f"Current conditions in {city}: 22°C, Clear Sky"

agent = Agent(
    name="WeatherAssistant",
    llm=LLMProvider("openai", model="gpt-4o"),
    tools=[fetch_weather],
    memory="short_term"
)

response = agent.run("What's the weather like in Tokyo?")
print(response.output)
```

## 🛠️ Usage Examples

### Multi-Agent Collaboration
```python
from soloai.orchestration import SupervisorAgent, WorkerAgent

researcher = WorkerAgent(name="Researcher", role="web_search", tools=[search_tool])
analyst = WorkerAgent(name="Analyst", role="data_processing", tools=[pandas_tool])

supervisor = SupervisorAgent(
    agents=[researcher, analyst],
    strategy="dynamic_routing",
    max_turns=5,
    fallback_agent="analyst"
)

result = supervisor.run("Analyze Q3 AI adoption metrics across healthcare and finance sectors.")
print(result.summary)
```

### Production Configuration
```yaml
# agent_config.yaml
agent:
  name: EnterpriseSupportBot
  llm:
    provider: anthropic
    model: claude-3-sonnet
    temperature: 0.2
  memory:
    type: vector_db
    backend: chroma
    retention_days: 30
  observability:
    tracing: true
    metrics_exporter: prometheus
  deployment:
    runtime: docker
    replicas: 3
```
Load configuration:
```python
from soloai.config import load_config
agent = load_config("agent_config.yaml").build()
```

## 🤝 Contributing
We welcome contributions from the open-source community. Please follow these guidelines:
1. Fork the repository and create a feature branch (`git checkout -b feat/your-feature`)
2. Install development dependencies: `pip install -e ".[dev]"`
3. Run linting, formatting, and tests: `make lint && make format && make test`
4. Follow [Conventional Commits](https://www.conventionalcommits.org/) for commit messages
5. Submit a Pull Request with a clear description, test coverage, and documentation updates

All contributions must adhere to our [Code of Conduct](CODE_OF_CONDUCT.md) and [Contributing Guide](CONTRIBUTING.md).

## 📩 Business Inquiries
For enterprise licensing, custom agent development, SLA support, or strategic partnerships, contact our solutions team at:  
📧 **379744050@qq.com**

🚀 **Ready to deploy your AI agent solution?**  
Send us a brief outlining your **industry**, **expected deliverables**, **budget range**, and **project deadline**. Our engineering team will review your requirements and deliver a tailored technical proposal within 24 hours.

## 📜 License
This project is licensed under the Apache License 2.0. See the [LICENSE](LICENSE) file for full terms and conditions.