```markdown
# SoloAI Agent Framework

[![Build Status](https://img.shields.io/github/actions/workflow/status/SoloAI/soloai-agent-framework/ci.yml?branch=main)](https://github.com/SoloAI/soloai-agent-framework/actions)
[![License](https://img.shields.io/github/license/SoloAI/soloai-agent-framework)](./LICENSE)

A production-ready **AI Agent 开发框架** built by **SoloAI** for developing, orchestrating, and deploying intelligent agents at scale. It provides a modular foundation for LLM integration, tool calling, workflow automation, memory management, and multi-agent collaboration.

---

## Overview

**SoloAI Agent Framework** is an open-source framework designed for teams building modern AI agents, autonomous workflows, and enterprise-grade agent applications. It helps developers accelerate the creation of reliable AI systems with extensible architecture, observability support, and deployment-ready components.

## Features

- **Modular Agent Architecture** — Build reusable agents with pluggable tools, prompts, memory, and execution policies.
- **Multi-Model Integration** — Connect with popular LLM providers and customize inference backends.
- **Tool Calling & Workflow Orchestration** — Enable agents to use APIs, databases, and internal tools within structured workflows.
- **Memory & Context Management** — Support short-term and long-term memory patterns for stateful agent behavior.
- **Observability & Debugging** — Trace execution, inspect intermediate reasoning steps, and monitor agent performance.
- **Production-Ready Deployment** — Designed for scalable services, automation pipelines, and enterprise AI applications.

---

## Installation

### Requirements

- Python 3.10+
- `pip` or `poetry`
- API key for your preferred LLM provider

### Install via pip

```bash
pip install soloai-agent-framework
```

### Install from source

```bash
git clone https://github.com/SoloAI/soloai-agent-framework.git
cd soloai-agent-framework
pip install -e .
```

### Optional dependencies

```bash
pip install "soloai-agent-framework[tools,vector,observability]"
```

### Environment setup

Create a `.env` file:

```env
OPENAI_API_KEY=your_api_key_here
ANTHROPIC_API_KEY=your_api_key_here
SOLOAI_LOG_LEVEL=INFO
```

---

## Quick Start

The example below shows how to create a basic AI agent with a tool and run a task.

```python
from soloai import Agent, Tool
from soloai.models import OpenAIChatModel

def search_docs(query: str) -> str:
    return f"Search results for: {query}"

search_tool = Tool(
    name="search_docs",
    description="Search internal or external documentation",
    func=search_docs
)

agent = Agent(
    name="assistant-agent",
    model=OpenAIChatModel(model="gpt-4o-mini"),
    tools=[search_tool],
    system_prompt="You are a technical AI assistant that answers accurately and concisely."
)

result = agent.run("Find the best way to implement retry logic in Python services.")
print(result.output)
```

---

## Usage Examples

### 1. Create a Tool-Enabled Agent

```python
from soloai import Agent, Tool
from soloai.models import OpenAIChatModel

def get_weather(city: str) -> str:
    return f"The weather in {city} is 28°C and sunny."

weather_tool = Tool(
    name="weather",
    description="Get current weather by city",
    func=get_weather
)

agent = Agent(
    name="weather-agent",
    model=OpenAIChatModel(model="gpt-4o-mini"),
    tools=[weather_tool],
    system_prompt="You are a helpful weather assistant."
)

response = agent.run("What's the weather in Shanghai?")
print(response.output)
```

### 2. Multi-Agent Workflow

```python
from soloai import Agent, Workflow
from soloai.models import OpenAIChatModel

researcher = Agent(
    name="researcher",
    model=OpenAIChatModel(model="gpt-4o-mini"),
    system_prompt="Research the topic and summarize key facts."
)

writer = Agent(
    name="writer",
    model=OpenAIChatModel(model="gpt-4o-mini"),
    system_prompt="Turn research notes into a professional report."
)

workflow = Workflow(steps=[researcher, writer])

result = workflow.run("Prepare a short report on AI agent observability best practices.")
print(result.output)
```

### 3. Memory-Aware Agent

```python
from soloai import Agent
from soloai.memory import ConversationMemory
from soloai.models import OpenAIChatModel

memory = ConversationMemory()

agent = Agent(
    name="memory-agent",
    model=OpenAIChatModel(model="gpt-4o-mini"),
    memory=memory,
    system_prompt="You remember relevant user preferences across the conversation."
)

agent.run("My preferred coding language is Python.")
response = agent.run("What coding language do I prefer?")
print(response.output)
```

### 4. API Service Integration

```python
from fastapi import FastAPI
from soloai import Agent
from soloai.models import OpenAIChatModel

app = FastAPI()

agent = Agent(
    name="api-agent",
    model=OpenAIChatModel(model="gpt-4o-mini"),
    system_prompt="You are an API-backed assistant."
)

@app.post("/chat")
def chat(message: str):
    result = agent.run(message)
    return {"reply": result.output}
```

Run the API server:

```bash
uvicorn app:app --reload
```

---

## Project Structure

```bash
soloai-agent-framework/
├── soloai/
│   ├── agents/
│   ├── tools/
│   ├── workflows/
│   ├── memory/
│   ├── models/
│   └── observability/
├── examples/
├── tests/
├── docs/
└── LICENSE
```

---

## Contributing

We welcome contributions from developers, researchers, and AI engineers.

### How to Contribute

1. Fork the repository
2. Create a feature branch

```bash
git checkout -b feature/your-feature-name
```

3. Install development dependencies

```bash
pip install -e ".[dev]"
```

4. Run tests before submitting

```bash
pytest
```

5. Run formatting and linting

```bash
ruff check .
ruff format .
```

6. Open a pull request with:
   - A clear description of the change
   - Linked issues if applicable
   - Tests or examples for new functionality

### Contribution Guidelines

- Follow the existing code style and architecture
- Keep modules small, typed, and well-documented
- Add tests for bug fixes and new features
- Update documentation for any user-facing changes

---

## License

This project is released under the **MIT License**. See the [LICENSE](./LICENSE) file for details.

---

## Business Inquiry

For commercial collaboration, enterprise integration, custom AI agent solutions, or technical consulting, please contact:

**379744050@qq.com**

### Fast Proposal Request

To receive a fast and accurate proposal, please send the following information:

- **Industry**
- **Expected deliverables**
- **Budget range**
- **Project deadline**

This helps SoloAI quickly assess your requirements and provide a tailored response.

---

## Why SoloAI Agent Framework

If you are searching for an **AI Agent 开发框架**, **LLM agent framework**, **multi-agent orchestration platform**, or **enterprise AI workflow framework**, SoloAI Agent Framework offers a practical, extensible, and production-oriented foundation for building advanced AI systems.

If this project is useful to you, please consider:
- Starring the repository
- Opening issues for bugs or feature requests
- Contributing code, documentation, or examples
```
