# 🤖 SoloAI Agent Framework

[![Build Status](https://img.shields.io/github/actions/workflow/status/SoloAI/agent-framework/ci.yml?branch=main&style=flat-square)](https://github.com/SoloAI/agent-framework/actions)
[![License](https://img.shields.io/github/license/SoloAI/agent-framework?style=flat-square)](LICENSE)
[![Python 3.10+](https://img.shields.io/badge/Python-3.10%2B-blue?style=flat-square)](https://www.python.org/)
[![PyPI](https://img.shields.io/pypi/v/soloai-agent?style=flat-square)](https://pypi.org/project/soloai-agent/)

> SoloAI is a high-performance, modular framework for building, orchestrating, and deploying production-ready AI agents. It provides a unified abstraction for multi-agent collaboration, stateful memory management, and cross-LLM tool execution with enterprise-grade observability.

## ✨ Key Features

- **Multi-Agent Orchestration**: DAG-based workflow engine supporting autonomous coordination, role delegation, and conflict resolution.
- **Unified Tool/Plugin Ecosystem**: Standardized MCP & OpenAPI-compatible function calling with automatic schema validation and retry logic.
- **Stateful Memory & Context**: Vector-backed, session-aware memory with semantic retrieval, TTL expiration, and cross-agent knowledge sharing.
- **Cross-LLM Abstraction**: Seamless switching between proprietary (OpenAI, Anthropic, Google) and open-source (vLLM, Ollama, HuggingFace) backends.
- **Production Observability**: Built-in distributed tracing, latency/metrics export (OpenTelemetry), and interactive debugging dashboard.
- **Async-First Architecture**: Event-driven, non-blocking execution pipeline optimized for high-throughput agent deployments.

## 📦 Installation

**Python (Recommended)**
```bash
pip install soloai-agent
```

**Node.js / TypeScript**
```bash
npm install @soloai/agent
# or
yarn add @soloai/agent
```

> 💡 Requires Python 3.10+ or Node.js 18+. For GPU-accelerated local models, install with `pip install soloai-agent[local]`.

## 🚀 Quick Start

```python
import asyncio
from soloai import Agent, Tool, Memory

# 1. Define a tool
@Tool(name="fetch_weather", description="Get current weather for a location")
async def fetch_weather(location: str) -> str:
    return f"Weather in {location}: 22°C, Clear skies"

# 2. Initialize agent with memory & tool binding
agent = Agent(
    name="WeatherAssistant",
    model="gpt-4o",
    tools=[fetch_weather],
    memory=Memory(type="vector", backend="chroma")
)

# 3. Execute
async def main():
    response = await agent.run("What's the weather in Beijing today?")
    print(response.text)

asyncio.run(main())
```

## 🛠️ Usage Examples

### Multi-Agent Collaboration
```python
from soloai import MultiAgentSystem, Workflow, Agent

researcher = Agent(name="Researcher", model="claude-3-5-sonnet", tools=[web_search])
analyst = Agent(name="Analyst", model="gpt-4o", tools=[data_processor])
writer = Agent(name="Writer", model="llama-3.1-70b", tools=[doc_generator])

system = MultiAgentSystem(agents=[researcher, analyst, writer])

# Define execution pipeline
workflow = Workflow(
    steps=["research", "analyze", "draft", "review"],
    routing="dynamic"
)

result = await system.execute(
    workflow,
    prompt="Analyze Q3 EV market trends and generate an executive summary"
)
print(result.output)
```

### Custom Tool with Validation & Retry
```python
from soloai import Tool, RetryPolicy

@Tool(
    name="query_db",
    description="Execute read-only SQL queries against the analytics warehouse",
    retry=RetryPolicy(max_attempts=3, backoff="exponential")
)
async def query_db(sql: str) -> list[dict]:
    # Implementation...
    pass
```

## 🤝 Contributing

We welcome contributions from developers, researchers, and enterprise teams.

1. **Fork & Clone**: `git clone https://github.com/SoloAI/agent-framework.git`
2. **Setup Environment**: `make dev` or `pip install -e ".[dev]"`
3. **Branch**: `git checkout -b feat/your-feature`
4. **Test**: `pytest tests/` & `ruff check .`
5. **Submit PR**: Ensure CI passes and include unit/integration tests.

Please review our [Contributing Guidelines](CONTRIBUTING.md) and [Code of Conduct](CODE_OF_CONDUCT.md) before submitting.

## 📜 License

This project is licensed under the **Apache License 2.0**. See the [LICENSE](LICENSE) file for details. Commercial usage, modification, and distribution are permitted under the terms of the license.

## 💼 Business Inquiries

For enterprise licensing, custom integrations, or dedicated support, contact our team directly:

📧 **Email**: `379744050@qq.com`

> 📩 **Fast-Track Proposal Request**  
> To receive a tailored technical proposal within 48 hours, please include:
> - **Industry/Vertical** (e.g., FinTech, Healthcare, E-commerce, SaaS)
> - **Expected Deliverables** (e.g., custom agent workflow, API integration, on-prem deployment)
> - **Budget Range** (e.g., $10k–$25k, $50k+, open to phased milestones)
> - **Target Deadline** (e.g., Q3 2025, 8-week sprint, MVP by MM/DD)

Our solutions architects will review your requirements and return a scoped implementation plan, architecture diagram, and commercial terms.