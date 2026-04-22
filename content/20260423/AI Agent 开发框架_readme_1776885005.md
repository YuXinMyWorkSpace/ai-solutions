# SoloAI Agent Framework

[![Build Status](https://img.shields.io/github/actions/workflow/status/SoloAI/soloai-agent/ci.yml?branch=main&style=flat-square)](https://github.com/SoloAI/soloai-agent/actions)
[![License](https://img.shields.io/github/license/SoloAI/soloai-agent?style=flat-square)](./LICENSE)

> An open-source **AI Agent 开发框架** designed for building, orchestrating, and deploying production-ready autonomous agents and multi-agent workflows.  
> SoloAI Agent Framework helps developers create scalable LLM-powered applications with modular tools, memory, planning, and runtime observability.

---

## Overview

**SoloAI Agent Framework** is a modern framework for **AI Agent development**, focused on modular architecture, extensibility, and developer productivity. It provides the building blocks needed to create intelligent agents capable of reasoning, tool calling, workflow automation, and multi-step task execution.

This project is optimized for teams building:

- LLM applications
- Autonomous AI agents
- Multi-agent systems
- Tool-using copilots
- Workflow automation platforms
- Retrieval-augmented AI systems

---

## Features

- **Modular Agent Architecture** — Build agents with pluggable memory, tools, planners, and executors.
- **Multi-Agent Orchestration** — Coordinate multiple specialized agents for complex tasks and collaborative reasoning.
- **Tool Calling & Function Execution** — Integrate APIs, databases, search engines, and custom business logic as agent tools.
- **Memory & Context Management** — Support short-term context, long-term memory, and retrieval-based knowledge access.
- **Observability & Debugging** — Trace agent steps, inspect decisions, and monitor execution flows for production environments.
- **Production-Ready Integration** — Designed for APIs, cloud deployment, automation backends, and enterprise AI applications.

---

## Installation

### Requirements

- Python 3.10+
- `pip` or `poetry`

### Install with pip

```bash
pip install soloai-agent
```

### Install from source

```bash
git clone https://github.com/SoloAI/soloai-agent.git
cd soloai-agent
pip install -e .
```

### Optional dependencies

```bash
pip install "soloai-agent[openai]"
pip install "soloai-agent[anthropic]"
pip install "soloai-agent[dev]"
```

---

## Quick Start

Create and run a simple AI agent with a tool:

```python
from soloai import Agent, Tool
from soloai.models import OpenAIChatModel

def weather_tool(city: str) -> str:
    return f"The weather in {city} is sunny, 25°C."

agent = Agent(
    name="assistant",
    model=OpenAIChatModel(model="gpt-4o-mini"),
    tools=[
        Tool.from_function(
            weather_tool,
            name="get_weather",
            description="Get weather information for a given city"
        )
    ],
    system_prompt="You are a helpful AI agent."
)

result = agent.run("What's the weather in Shanghai?")
print(result.output)
```

### Environment setup

```bash
export OPENAI_API_KEY=your_api_key_here
```

---

## Usage Examples

### 1. Basic Agent

```python
from soloai import Agent
from soloai.models import OpenAIChatModel

agent = Agent(
    name="qa-agent",
    model=OpenAIChatModel(model="gpt-4o-mini"),
    system_prompt="Answer questions clearly and accurately."
)

response = agent.run("Explain AI agents in one paragraph.")
print(response.output)
```

---

### 2. Agent with Memory

```python
from soloai import Agent
from soloai.memory import ConversationMemory
from soloai.models import OpenAIChatModel

memory = ConversationMemory()

agent = Agent(
    name="memory-agent",
    model=OpenAIChatModel(model="gpt-4o-mini"),
    memory=memory,
    system_prompt="Remember user preferences across the conversation."
)

agent.run("My favorite programming language is Python.")
response = agent.run("What is my favorite programming language?")
print(response.output)
```

---

### 3. Multi-Agent Workflow

```python
from soloai import Agent, AgentTeam
from soloai.models import OpenAIChatModel

researcher = Agent(
    name="researcher",
    model=OpenAIChatModel(model="gpt-4o-mini"),
    system_prompt="Research the topic and summarize key points."
)

writer = Agent(
    name="writer",
    model=OpenAIChatModel(model="gpt-4o-mini"),
    system_prompt="Turn research notes into a polished technical summary."
)

team = AgentTeam(
    agents=[researcher, writer],
    strategy="sequential"
)

result = team.run("Create a short overview of AI agent frameworks.")
print(result.output)
```

---

### 4. Tool-Integrated Workflow

```python
from soloai import Agent, Tool
from soloai.models import OpenAIChatModel

def search_docs(query: str) -> str:
    return f"Search results for: {query}"

agent = Agent(
    name="docs-agent",
    model=OpenAIChatModel(model="gpt-4o-mini"),
    tools=[
        Tool.from_function(
            search_docs,
            name="search_docs",
            description="Search internal documentation"
        )
    ],
    system_prompt="Use tools when needed to answer accurately."
)

response = agent.run("Find documentation about agent memory.")
print(response.output)
```

---

## Project Structure

```text
soloai-agent/
├── soloai/
│   ├── agents/
│   ├── tools/
│   ├── memory/
│   ├── models/
│   ├── orchestration/
│   └── observability/
├── examples/
├── tests/
├── docs/
└── README.md
```

---

## Contributing

Contributions are welcome from the community. Whether you want to improve documentation, fix bugs, add integrations, or enhance the agent runtime, we’d love your help.

### How to contribute

1. Fork the repository
2. Create a feature branch

```bash
git checkout -b feat/your-feature-name
```

3. Install development dependencies

```bash
pip install -e ".[dev]"
```

4. Run tests

```bash
pytest
```

5. Run formatting and linting

```bash
ruff check .
ruff format .
```

6. Commit your changes with clear messages
7. Open a Pull Request describing:
   - the problem being solved
   - implementation details
   - testing performed
   - any breaking changes

### Development principles

- Write clear, maintainable, typed Python code
- Add tests for new features and bug fixes
- Keep APIs consistent and well documented
- Prefer composable modules over tightly coupled implementations

---

## License

This project is licensed under the **MIT License**. See the [LICENSE](./LICENSE) file for details.

---

## Keywords

**AI Agent Framework**, **AI Agent 开发框架**, **LLM Agent**, **Autonomous Agents**, **Multi-Agent System**, **Tool Calling**, **Agent Memory**, **LLM Orchestration**, **RAG**, **AI Workflow Automation**

---

## Maintainer

Developed and maintained by **SoloAI**.  
If this project helps you, consider starring the repository to support future development.