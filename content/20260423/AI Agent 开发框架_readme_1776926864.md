# SoloAI Agent Framework

[![Build Status](https://img.shields.io/github/actions/workflow/status/SoloAI/soloai-agent/ci.yml?branch=main&style=for-the-badge)](https://github.com/SoloAI/soloai-agent/actions)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg?style=for-the-badge)](./LICENSE)

> 一个面向现代 **AI Agent 开发框架** 的开源项目，帮助开发者快速构建、编排、运行和扩展具备工具调用、记忆、工作流与多代理协作能力的智能体应用。  
> SoloAI Agent Framework 专注于生产级 AI Agent engineering，适用于 LLM 应用开发、自动化任务执行、RAG 集成以及企业级 Agent 系统落地。

---

## Overview

**SoloAI Agent Framework** is an open-source framework for building **AI Agents** with modular architecture, tool integration, memory management, workflow orchestration, and multi-agent collaboration. It is designed for developers and teams who need a scalable, extensible, and production-ready foundation for agent-based applications.

### Why SoloAI Agent Framework?

AI Agent systems are evolving from simple prompt chains to complex, stateful, tool-using applications. SoloAI provides the core abstractions and developer experience needed to build reliable agentic systems with clean interfaces, observability, and extensibility.

---

## Features

- **Modular Agent Architecture**  
  Build reusable agents with pluggable components such as planners, memory modules, tools, and model providers.

- **Tool Calling & Function Execution**  
  Seamlessly integrate external APIs, internal business logic, databases, and custom tools for action-oriented AI workflows.

- **Memory & Context Management**  
  Support short-term and long-term memory strategies for contextual conversations and persistent task execution.

- **Workflow Orchestration**  
  Define deterministic or dynamic agent workflows for multi-step reasoning, task routing, and human-in-the-loop processes.

- **Multi-Agent Collaboration**  
  Create cooperative agent systems where specialized agents communicate, delegate, and solve complex tasks together.

- **Production-Ready Developer Experience**  
  Designed for testing, logging, observability, extensibility, and deployment in real-world AI applications.

---

## Installation

### Requirements

- Python 3.10+
- pip or poetry
- Access to an LLM provider API key such as OpenAI, Anthropic, or compatible endpoints

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
pip install "soloai-agent[tools,rag,dev]"
```

### Environment setup

Create a `.env` file in the project root:

```env
OPENAI_API_KEY=your_api_key_here
ANTHROPIC_API_KEY=your_api_key_here
SOLOAI_LOG_LEVEL=INFO
```

---

## Quick Start

Below is a minimal example showing how to create and run a simple AI agent.

```python
from soloai import Agent, Tool
from soloai.models import OpenAIChatModel

def get_weather(city: str) -> str:
    return f"The current weather in {city} is sunny, 26°C."

weather_tool = Tool(
    name="get_weather",
    description="Get the current weather for a city",
    func=get_weather
)

agent = Agent(
    name="assistant",
    model=OpenAIChatModel(model="gpt-4o-mini"),
    tools=[weather_tool],
    system_prompt="You are a helpful AI assistant that uses tools when needed."
)

response = agent.run("What's the weather in Shanghai?")
print(response.output)
```

---

## Usage Examples

### 1. Agent with Memory

```python
from soloai import Agent
from soloai.memory import ConversationMemory
from soloai.models import OpenAIChatModel

memory = ConversationMemory()

agent = Agent(
    name="memory-agent",
    model=OpenAIChatModel(model="gpt-4o-mini"),
    memory=memory,
    system_prompt="You are a conversational assistant with memory."
)

agent.run("My name is Alice.")
result = agent.run("What's my name?")
print(result.output)
```

### 2. Workflow-Oriented Agent

```python
from soloai import Agent, Workflow
from soloai.models import OpenAIChatModel

research_agent = Agent(
    name="researcher",
    model=OpenAIChatModel(model="gpt-4o-mini"),
    system_prompt="Research the topic and summarize key facts."
)

writer_agent = Agent(
    name="writer",
    model=OpenAIChatModel(model="gpt-4o-mini"),
    system_prompt="Write a concise technical summary based on provided research."
)

workflow = Workflow(
    name="research-to-summary",
    steps=[research_agent, writer_agent]
)

result = workflow.run("Explain AI agent orchestration frameworks.")
print(result.output)
```

### 3. Multi-Agent Collaboration

```python
from soloai import Agent, Team
from soloai.models import OpenAIChatModel

planner = Agent(
    name="planner",
    model=OpenAIChatModel(model="gpt-4o-mini"),
    system_prompt="Break down the task into actionable steps."
)

executor = Agent(
    name="executor",
    model=OpenAIChatModel(model="gpt-4o-mini"),
    system_prompt="Execute the plan and provide the final result."
)

team = Team(
    name="task-force",
    agents=[planner, executor]
)

result = team.run("Create a launch checklist for a SaaS AI product.")
print(result.output)
```

### 4. Registering a Custom Tool

```python
from soloai import Tool

def search_docs(query: str) -> str:
    return f"Top documentation result for: {query}"

doc_tool = Tool(
    name="search_docs",
    description="Search internal documentation",
    func=search_docs
)
```

---

## Project Structure

```bash
soloai-agent/
├── soloai/
│   ├── agents/
│   ├── memory/
│   ├── models/
│   ├── tools/
│   ├── workflows/
│   └── teams/
├── examples/
├── tests/
├── docs/
├── pyproject.toml
└── README.md
```

---

## Common Use Cases

- **AI Agent application development**
- **Tool-using LLM systems**
- **Autonomous workflow automation**
- **RAG + Agent integrations**
- **Customer support copilots**
- **Research assistants and internal productivity tools**
- **Enterprise agent orchestration platforms**

---

## Contributing

We welcome contributions from the open-source community.

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

6. Commit your changes using clear commit messages
7. Open a Pull Request with a detailed description of the change

### Contribution Guidelines

- Keep PRs focused and atomic
- Add tests for new features and bug fixes
- Update documentation when behavior changes
- Follow the existing code style and naming conventions
- Discuss major architecture changes via Issues before implementation

---

## Development

### Run the test suite

```bash
pytest -q
```

### Run type checking

```bash
mypy soloai
```

### Local documentation

```bash
mkdocs serve
```

---

## Roadmap

- [ ] More model provider integrations
- [ ] Visual workflow builder
- [ ] Advanced memory backends
- [ ] Native observability dashboard
- [ ] Enterprise authentication and permissions
- [ ] Distributed multi-agent runtime

---

## License

This project is licensed under the **MIT License**. See the [LICENSE](./LICENSE) file for details.

---

## Keywords

**AI Agent Framework**, **AI Agent 开发框架**, **LLM Agent**, **Agent Orchestration**, **Multi-Agent System**, **Tool Calling**, **Agent Memory**, **Workflow Automation**, **RAG Agent**, **Open Source AI Framework**

If you want, I can also generate:
- a **中文版 README**
- a **bilingual README (Chinese + English)**
- a **more product-focused README for GitHub landing page conversion**