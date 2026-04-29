# 🧠 SoloAI Agent Framework
[![CI Build](https://img.shields.io/github/actions/workflow/status/SoloAI/agent-framework/ci.yml?branch=main&label=build)](https://github.com/SoloAI/agent-framework/actions)
[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](LICENSE)
[![PyPI](https://img.shields.io/pypi/v/soloai-agent.svg)](https://pypi.org/project/soloai-agent/)

A high-performance, modular AI Agent development framework engineered for rapid prototyping, scalable multi-agent orchestration, and enterprise-grade deployment. SoloAI provides a unified abstraction layer over LLMs, tool ecosystems, and state management to accelerate production-ready AI workflows.

## ✨ Key Features
- **LLM-Agnostic Routing**: Seamlessly switch between OpenAI, Anthropic, Mistral, vLLM, or local models via a standardized provider interface.
- **Multi-Agent Orchestration**: Built-in supervisor, swarm, and hierarchical delegation patterns for complex task decomposition and parallel execution.
- **Dynamic Tool Ecosystem**: Auto-generate JSON schemas from Python functions, with native support for MCP, OpenAPI, and custom plugin registries.
- **Persistent Memory & Context**: Vector-backed short/long-term memory with configurable eviction policies, cross-session state sharing, and semantic retrieval.
- **Observability & Telemetry**: OpenTelemetry-native tracing, structured JSON logging, and real-time execution metrics (token usage, latency, tool success rate).
- **Production-Ready Deployment**: Docker/Kubernetes-ready packaging, async execution pipelines, built-in rate limiting, circuit breakers, and retry logic.

## 📦 Installation
Requires Python 3.10+. Install via `pip` or `uv`:
```bash
pip install soloai-agent
# or with uv for faster dependency resolution
uv pip install soloai-agent
```

For full feature support (vector stores, telemetry, async drivers):
```bash
pip install "soloai-agent[full]"
```

## 🚀 Quick Start
Create your first AI agent in under 10 lines of code:
```python
from soloai import Agent, Tool, LLMProvider

# Define a custom tool
@Tool(description="Fetches real-time weather data for a given city")
def get_weather(city: str) -> str:
    # Simulated API call
    return f"Weather in {city}: 22°C, Clear skies"

# Initialize agent
agent = Agent(
    name="WeatherAssistant",
    llm=LLMProvider("openai/gpt-4o"),
    tools=[get_weather],
    system_prompt="You are a helpful weather assistant. Always use the weather tool before answering."
)

# Execute synchronously
response = agent.run("What's the weather like in Tokyo?")
print(response.content)
```

## 🛠 Usage Examples

### Multi-Agent Workflow
Orchestrate specialized agents using a supervisor pattern with automatic handoff:
```python
from soloai.orchestration import Supervisor, AgentRole

researcher = AgentRole("Researcher", tools=[web_search, scrape_page])
analyst = AgentRole("DataAnalyst", tools=[pandas_query, chart_gen])
writer = AgentRole("TechnicalWriter", tools=[markdown_export])

supervisor = Supervisor(
    roles=[researcher, analyst, writer],
    delegation_strategy="hierarchical",
    max_iterations=5,
    timeout=120
)

result = supervisor.execute("Draft a market analysis report on renewable energy trends in 2024.")
print(result.final_output)
```

### Streaming & Async Execution
Handle real-time token streaming and background task processing:
```python
import asyncio
from soloai import Agent

agent = Agent(llm="anthropic/claude-3-5-sonnet")

async def stream_response():
    async for chunk in agent.stream("Explain quantum computing in simple terms"):
        print(chunk.delta, end="", flush=True)

asyncio.run(stream_response())
```

## 🤝 Contributing
We welcome contributions from developers, researchers, and AI engineers. Please follow these guidelines:
1. **Fork & Branch**: Create a feature branch (`feat/your-feature` or `fix/issue-description`).
2. **Code Standards**: Enforce `ruff` linting, `black` formatting, and strict type hints (`mypy`).
3. **Testing**: Add unit/integration tests (`pytest`). Ensure `make test` and `make lint` pass locally.
4. **Documentation**: Update `docs/` and docstrings for all public APIs. Include usage examples for new modules.
5. **Pull Request**: Submit a PR with a clear description, linked issues, and changelog notes following [Conventional Commits](https://www.conventionalcommits.org/).

See [CONTRIBUTING.md](CONTRIBUTING.md) for detailed architecture guidelines, local setup instructions, and CI/CD workflows.

## 📄 License
This project is licensed under the [Apache License 2.0](LICENSE). Commercial usage, modification, and distribution are permitted under the terms of the license. Third-party model providers and external tool integrations remain subject to their respective terms of service.

## 💼 Business & Enterprise Inquiries
For commercial licensing, custom integrations, enterprise support, or white-label solutions, contact our architecture team directly:
📧 **Email**: `379744050@qq.com`

### 📩 Request a Fast Proposal
To accelerate your AI project onboarding, please include the following details in your inquiry:
- **Industry / Vertical**: (e.g., FinTech, Healthcare, E-commerce, SaaS, Manufacturing)
- **Expected Deliverables**: (e.g., Multi-agent workflow, custom toolchain, deployment pipeline, SLA requirements, compliance needs)
- **Budget Range**: (e.g., $5K–$15K, $20K+, Enterprise tier)
- **Target Deadline**: (e.g., MVP in 4 weeks, Production by Q3, Phased rollout)

Our engineering team will respond within 24 hours with a tailored technical proposal, system architecture diagram, and implementation roadmap.