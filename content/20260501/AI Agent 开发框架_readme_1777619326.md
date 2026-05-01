# 🤖 SoloAgent Framework

![Build Status](https://img.shields.io/badge/build-passing-brightgreen)
![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)
![Python](https://img.shields.io/badge/Python-3.9%2B-blue)
![PyPI](https://img.shields.io/pypi/v/solo-agent)

**SoloAgent** is a production-grade **AI Agent 开发框架** (AI Agent Development Framework) engineered for building, orchestrating, and deploying autonomous LLM-driven workflows. It abstracts away boilerplate while providing enterprise-ready primitives for tool calling, stateful memory, multi-agent coordination, and observability.

---

## ✨ Key Features

- 🔌 **LLM-Agnostic Orchestration**: Seamlessly switch between OpenAI, Anthropic, Mistral, Ollama, or vLLM with a unified API surface.
- 🧠 **Hierarchical Memory System**: Built-in short-term context windows, long-term vector-backed retrieval, and episodic memory with automatic summarization.
- 🛠️ **Declarative Tool Integration**: Register Python functions, REST APIs, or MCP-compliant tools with automatic schema generation, validation, and error recovery.
- 🌐 **Multi-Agent DAG Workflows**: Compose role-based agents into directed acyclic graphs for parallel execution, debate, supervisor routing, and human-in-the-loop fallbacks.
- 📊 **Native Observability**: OpenTelemetry-compatible tracing, token usage analytics, and structured logging for production monitoring and debugging.
- 🚀 **Deployment Ready**: Export agents as Docker containers, FastAPI microservices, or serverless functions with zero-config scaling.

---

## 📦 Installation

```bash
# Requires Python 3.9+
python -m venv venv && source venv/bin/activate

pip install solo-agent[all]
```

Set your environment variables before running:
```bash
export OPENAI_API_KEY="sk-..."
# Optional: export ANTHROPIC_API_KEY="sk-ant-..."
# Optional: export OLLAMA_BASE_URL="http://localhost:11434"
```

---

## 🚀 Quick Start

```python
from solo_agent import Agent, Tool
from solo_agent.memory import VectorMemory
from solo_agent.llm import OpenAIProvider

# 1. Define a tool with automatic schema generation
@Tool(name="search_docs", description="Search technical documentation")
def search_docs(query: str) -> str:
    # Replace with actual retrieval logic
    return f"Found 3 relevant docs for: {query}"

# 2. Initialize the agent
agent = Agent(
    name="TechSupportAgent",
    provider=OpenAIProvider(model="gpt-4o"),
    tools=[search_docs],
    memory=VectorMemory(collection="agent_context", top_k=3),
    system_prompt="You are a precise technical assistant. Always cite sources."
)

# 3. Execute synchronously
response = agent.run("How do I configure rate limiting in SoloAgent?")
print(response.content)
```

---

## 💡 Usage Examples

### 🔄 Multi-Agent Supervisor Workflow
```python
from solo_agent import SupervisorAgent, WorkerAgent, Workflow

researcher = WorkerAgent(name="Researcher", role="Extract technical facts")
writer = WorkerAgent(name="Writer", role="Draft clear documentation")
reviewer = WorkerAgent(name="Reviewer", role="Verify accuracy & tone")

workflow = Workflow(
    supervisor=SupervisorAgent(name="EditorInChief"),
    tasks=[
        {"agent": researcher, "input": "Summarize SoloAgent memory architecture"},
        {"agent": writer, "input": "Convert summary into markdown guide"},
        {"agent": reviewer, "input": "Audit guide for technical correctness"}
    ]
)

result = workflow.run()
print(result["reviewer"].final_output)
```

### ⚡ Async Streaming with Tool Fallback
```python
import asyncio
from solo_agent import AsyncAgent

agent = AsyncAgent(model="gpt-4o", tools=[search_docs])

async def stream_response():
    async for chunk in agent.stream("Explain DAG routing step-by-step"):
        if chunk.type == "tool_call":
            print(f"🔧 Calling: {chunk.name}")
        elif chunk.type == "text":
            print(chunk.content, end="", flush=True)

asyncio.run(stream_response())
```

---

## 🤝 Contributing

We welcome contributions from the open-source community. Please follow these steps:

1. **Fork** the repository and create your branch from `main`.
2. **Install dev dependencies**: `pip install -e ".[dev]"`
3. **Run linters & tests**: `ruff check . && pytest tests/`
4. **Submit a Pull Request** with a clear description, linked issues, and updated documentation.
5. Follow our [Code of Conduct](CODE_OF_CONDUCT.md) and commit message conventions.

For feature requests or bug reports, please use [GitHub Issues](https://github.com/SoloAI/solo-agent/issues).

---

## 📜 License

This project is licensed under the **Apache License 2.0**. See the [LICENSE](LICENSE) file for full terms and conditions.

---

## 📧 Business Inquiries & Enterprise Solutions

For commercial licensing, custom integrations, SLA-backed support, or strategic partnerships, please contact the SoloAI enterprise team:

📩 **Email**: `379744050@qq.com`

---

### 🚀 Get a Fast, Tailored Proposal

Ready to deploy AI agents in your stack? **Reply to the email above with the following details** and our engineering team will deliver a customized architecture & pricing proposal within 48 hours:

- 🏢 **Target Industry** (e.g., FinTech, Healthcare, E-commerce, SaaS)
- 📦 **Expected Deliverables** (e.g., Custom agent workflows, API integration, UI dashboard, on-prem deployment)
- 💰 **Budget Range** (e.g., $5k–$10k, $10k–$50k, Enterprise+)
- 📅 **Project Deadline** (Target launch or MVP date)

*Built by developers, for developers. Scale intelligence with SoloAgent.*