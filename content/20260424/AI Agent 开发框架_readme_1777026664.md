# SoloAI Agent Framework

[![Build Status](https://img.shields.io/github/actions/workflow/status/SoloAI/soloai-agent-framework/ci.yml?branch=main&style=flat-square)](https://github.com/SoloAI/soloai-agent-framework/actions)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg?style=flat-square)](./LICENSE)

A production-ready **AI Agent 开发框架** designed by **SoloAI** for building, orchestrating, and deploying intelligent agents with modular workflows, tool calling, memory, and multi-agent collaboration.  
It helps developers create scalable AI applications faster with a clean architecture, extensible components, and deployment-friendly interfaces.

---

## Overview

**SoloAI Agent Framework** is an open-source framework focused on modern **AI agent development**, enabling teams to build robust agent systems for automation, copilots, enterprise workflows, retrieval-augmented generation, and domain-specific reasoning tasks.

It is optimized for:
- **LLM application development**
- **AI agent orchestration**
- **tool integration and function calling**
- **memory and context management**
- **multi-agent workflow execution**
- **production deployment for enterprise AI systems**

---

## Features

- **Modular Agent Architecture**  
  Build agents with reusable components such as planners, executors, memory modules, tools, and evaluators.

- **Tool Calling & Workflow Orchestration**  
  Integrate APIs, databases, search engines, vector stores, and custom business systems into structured agent workflows.

- **Memory & Context Management**  
  Support short-term and long-term memory patterns for conversational AI, task continuity, and stateful execution.

- **Multi-Agent Collaboration**  
  Coordinate multiple agents for planning, reasoning, delegation, and task execution across complex pipelines.

- **Extensible Provider Integration**  
  Connect with popular LLM providers, embedding services, vector databases, and observability platforms.

- **Production-Ready Developer Experience**  
  Includes clear abstractions, configurable runtime settings, logging, testing support, and deployment-friendly patterns.

---

## Installation

### Prerequisites

- Python 3.10+
- `pip` or `poetry`
- Access to an LLM API provider

### Install with pip

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
pip install "soloai-agent-framework[openai]"
pip install "soloai-agent-framework[anthropic]"
pip install "soloai-agent-framework[vector]"
pip install "soloai-agent-framework[dev]"
```

### Environment configuration

Create a `.env` file:

```bash
OPENAI_API_KEY=your_api_key_here
ANTHROPIC_API_KEY=your_api_key_here
MODEL_NAME=gpt-4o-mini
```

---

## Quick Start

Below is a minimal example for creating an AI agent with a tool and running a task.

```python
from soloai import Agent, Tool, Memory
from soloai.providers import OpenAIChatModel

def search_docs(query: str) -> str:
    return f"Search results for: {query}"

tool = Tool(
    name="search_docs",
    description="Search internal or public documentation",
    func=search_docs,
)

model = OpenAIChatModel(
    model="gpt-4o-mini",
    temperature=0.2,
)

memory = Memory()

agent = Agent(
    name="assistant-agent",
    model=model,
    tools=[tool],
    memory=memory,
    system_prompt="You are a helpful AI agent for technical research and execution."
)

result = agent.run("Find best practices for building a retrieval-augmented AI assistant.")
print(result.output)
```

---

## Usage Examples

### 1. Tool-Enabled Agent

```python
from soloai import Agent, Tool
from soloai.providers import OpenAIChatModel

def get_weather(city: str) -> str:
    return f"The weather in {city} is sunny, 28°C."

weather_tool = Tool(
    name="get_weather",
    description="Get weather information for a city",
    func=get_weather
)

agent = Agent(
    name="weather-agent",
    model=OpenAIChatModel(model="gpt-4o-mini"),
    tools=[weather_tool],
    system_prompt="Use tools when needed and provide concise answers."
)

response = agent.run("What is the weather in Shanghai?")
print(response.output)
```

### 2. Agent with Memory

```python
from soloai import Agent, Memory
from soloai.providers import OpenAIChatModel

memory = Memory()

agent = Agent(
    name="memory-agent",
    model=OpenAIChatModel(model="gpt-4o-mini"),
    memory=memory,
    system_prompt="You are a stateful assistant that remembers prior context."
)

agent.run("My company is building an AI customer support copilot.")
response = agent.run("What kind of product am I building?")
print(response.output)
```

### 3. Multi-Agent Workflow

```python
from soloai import Agent, Workflow
from soloai.providers import OpenAIChatModel

planner = Agent(
    name="planner",
    model=OpenAIChatModel(model="gpt-4o-mini"),
    system_prompt="Break tasks into actionable steps."
)

researcher = Agent(
    name="researcher",
    model=OpenAIChatModel(model="gpt-4o-mini"),
    system_prompt="Research technical options and constraints."
)

writer = Agent(
    name="writer",
    model=OpenAIChatModel(model="gpt-4o-mini"),
    system_prompt="Create a polished technical summary."
)

workflow = Workflow(agents=[planner, researcher, writer])

result = workflow.run("Create a proposal for an enterprise AI knowledge assistant.")
print(result.output)
```

### 4. API Service Integration

```python
from fastapi import FastAPI
from soloai import Agent
from soloai.providers import OpenAIChatModel

app = FastAPI()

agent = Agent(
    name="api-agent",
    model=OpenAIChatModel(model="gpt-4o-mini"),
    system_prompt="You are an enterprise AI assistant."
)

@app.post("/chat")
def chat(message: str):
    result = agent.run(message)
    return {"output": result.output}
```

Run the service:

```bash
uvicorn app:app --reload
```

---

## Project Structure

```text
soloai-agent-framework/
├── soloai/
│   ├── agents/
│   ├── memory/
│   ├── tools/
│   ├── workflows/
│   ├── providers/
│   └── utils/
├── examples/
├── tests/
├── docs/
├── pyproject.toml
└── README.md
```

---

## Common Use Cases

- Enterprise AI assistants
- AI copilots for operations and support
- Knowledge base Q&A systems
- Retrieval-augmented generation (RAG)
- Multi-agent research pipelines
- Workflow automation with LLMs
- Internal tool automation and API orchestration

---

## Contributing

We welcome contributions from the open-source community.

### How to contribute

1. Fork the repository
2. Create a feature branch

```bash
git checkout -b feature/your-feature-name
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
black .
```

6. Commit your changes with clear messages
7. Open a Pull Request describing:
   - the problem
   - the proposed solution
   - implementation details
   - test coverage

### Contribution guidelines

- Follow the existing project structure and coding conventions
- Write tests for new features and bug fixes
- Keep PRs focused and reviewable
- Update documentation when behavior changes
- Be respectful and constructive in code reviews and discussions

---

## Roadmap

- [ ] Visual workflow builder
- [ ] Native RAG pipeline templates
- [ ] Agent evaluation and tracing dashboard
- [ ] More provider integrations
- [ ] Distributed task execution support
- [ ] Enterprise deployment examples

---

## License

This project is licensed under the **MIT License**.  
See the [LICENSE](./LICENSE) file for details.

---

## Business Inquiry

For commercial collaboration, custom AI agent solutions, enterprise integration, or technical consulting, please contact:

**379744050@qq.com**

### Fast Proposal CTA

If you would like a fast project proposal, please send the following information by email:

- **Industry**
- **Expected deliverables**
- **Budget range**
- **Deadline**

With these details, SoloAI can quickly evaluate requirements and provide a more accurate proposal for your AI agent project.

---

## Why SoloAI Agent Framework

If you are searching for an **AI Agent 开发框架**, **AI agent framework**, **LLM orchestration framework**, or **multi-agent development platform**, SoloAI Agent Framework provides a strong technical foundation for building modern, scalable, production-grade AI systems.

Star the repository, open an issue, or contribute to help shape the future of open-source AI agent engineering.