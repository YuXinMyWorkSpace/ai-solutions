# 🤖 SoloAgent Framework
[![Build Status](https://github.com/SoloAI/solo-agent/actions/workflows/ci.yml/badge.svg)](https://github.com/SoloAI/solo-agent/actions/workflows/ci.yml)
[![License](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![Python](https://img.shields.io/badge/Python-3.9%2B-blue)](https://www.python.org/)
[![PyPI version](https://badge.fury.io/py/solo-agent.svg)](https://pypi.org/project/solo-agent/)

**SoloAgent** is a lightweight, production-grade AI Agent development framework designed for rapid prototyping, orchestration, and deployment of autonomous LLM-driven systems. It provides a unified API for tool integration, stateful memory management, and multi-agent collaboration with built-in observability.

## ✨ Key Features
- **🧩 Modular Agent Architecture**: Pluggable LLM backends (OpenAI, Anthropic, vLLM, Ollama) with standardized `BaseAgent` interfaces and provider-agnostic routing.
- **🧠 Hierarchical Memory System**: Short-term context windows, long-term vector-backed retrieval, and session-aware state persistence with automatic eviction policies.
- **🔗 Declarative Tool Integration**: Auto-generated JSON schemas, async/sync execution, structured output parsing, and built-in fallback/retry mechanisms.
- **🌐 Multi-Agent Orchestration**: Native support for supervisor-worker, debate, and router patterns with deterministic message-passing protocols.
- **📊 Production Observability**: OpenTelemetry-compatible tracing, structured logging, latency metrics, and deterministic evaluation pipelines for agent regression testing.

## 📦 Installation
Install the core package via PyPI:
```bash
pip install solo-agent
```

Optional provider extras:
```bash
# Cloud LLM providers (OpenAI, Anthropic, Google)
pip install solo-agent[cloud-llms]

# Local inference engines (vLLM, Ollama, llama.cpp)
pip install solo-agent[local-llms]

# Full development stack (testing, linting, docs)
pip install solo-agent[dev]
```

*Requirements*: Python 3.9+, `pip`, and valid API keys or local model endpoints for your chosen LLM provider.

## 🚀 Quick Start
Initialize and execute a tool-augmented agent in under 10 lines:
```python
from solo_agent import Agent, Tool, Memory

@Tool(name="calculate", description="Evaluate a mathematical expression safely")
def math_eval(expr: str) -> str:
    # In production, use ast.literal_eval or a safe parser
    return str(eval(expr, {"__builtins__": {}}))

agent = Agent(
    name="MathSolver",
    llm="openai:gpt-4o",
    tools=[math_eval],
    memory=Memory(type="ephemeral", max_tokens=8192)
)

response = agent.run("What is 128 * 42 divided by 3?")
print(response.content)
```

## 📖 Usage Examples

### Multi-Agent Collaboration
Orchestrate specialized agents using a supervisor routing pattern:
```python
from solo_agent import Supervisor, Agent, Tool

researcher = Agent(name="Researcher", llm="anthropic:claude-3-5-sonnet", tools=[web_search])
coder = Agent(name="Engineer", llm="openai:gpt-4o", tools=[code_interpreter])

supervisor = Supervisor(
    name="ProjectLead",
    agents=[researcher, coder],
    strategy="router",  # Intent-based delegation
    max_iterations=5,
    verbose=True
)

task = "Build a Python script to scrape and analyze crypto prices from CoinGecko."
result = supervisor.run(task)
print(result.final_output)
```

### Async Execution & Streaming
Leverage async I/O for low-latency applications and real-time UI updates:
```python
import asyncio
from solo_agent import Agent

async def run_streaming_agent():
    agent = Agent(name="Assistant", llm="openai:gpt-4o-mini")
    
    async for chunk in agent.stream("Explain quantum entanglement in 3 sentences."):
        print(chunk.delta, end="", flush=True)

asyncio.run(run_streaming_agent())
```

## 🤝 Contributing
We welcome contributions from developers, researchers, and AI engineers. Please follow these guidelines:
1. **Fork & Branch**: Fork the repository and create a descriptive branch (`git checkout -b feat/your-feature`).
2. **Code Standards**: Follow PEP 8, enforce type hints, and run `ruff check . && mypy solo_agent/` before committing.
3. **Testing**: Add unit/integration tests under `tests/`. Mock LLM responses using `solo_agent.testing.MockLLM` to ensure deterministic CI runs.
4. **Pull Request**: Submit a PR with a clear description, linked issues, and updated documentation. Include benchmark results if modifying core execution paths.
5. **Code of Conduct**: All contributors must adhere to our [Code of Conduct](CODE_OF_CONDUCT.md).

For architectural discussions, RFCs, or plugin proposals, open a [GitHub Discussion](https://github.com/SoloAI/solo-agent/discussions).

## 📜 License
This project is licensed under the **MIT License** - see the [LICENSE](LICENSE) file for full terms and conditions.

---
*Built by [SoloAI](https://github.com/SoloAI) | Documentation: [docs.solo-agent.ai](https://docs.solo-agent.ai) | Report Issues: [GitHub Issues](https://github.com/SoloAI/solo-agent/issues)*