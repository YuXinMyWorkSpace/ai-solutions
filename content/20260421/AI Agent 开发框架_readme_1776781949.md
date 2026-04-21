# SoloAI Agent Framework

[![Build Status](https://img.shields.io/github/actions/workflow/status/soloai/agent-framework/ci.yml?branch=main&style=flat-square)](https://github.com/soloai/agent-framework/actions)
[![License](https://img.shields.io/github/license/soloai/agent-framework?style=flat-square)](./LICENSE)

> 一个面向生产环境的 **AI Agent 开发框架**，用于快速构建、编排、测试与部署智能体应用。  
> SoloAI Agent Framework 提供模块化架构、工具调用、记忆管理与工作流编排能力，帮助开发者高效落地 LLM / Agent 系统。

---

## Overview

**SoloAI Agent Framework** is an open-source framework for building modern AI agents with reusable components, structured workflows, and production-ready integrations. It is designed for developers and teams who need a scalable foundation for **LLM applications**, **tool-using agents**, **multi-step reasoning workflows**, and **autonomous task execution**.

---

## Features

- **Modular Agent Architecture**  
  使用可组合组件构建 Agent，包括模型、工具、记忆、规划器与执行器。

- **Tool Calling & Function Execution**  
  原生支持工具注册、函数调用与外部 API 集成，便于构建具备行动能力的 AI Agent。

- **Workflow Orchestration**  
  支持多步骤任务流、链式调用与复杂业务逻辑编排，适用于自动化和 Copilot 场景。

- **Memory & Context Management**  
  提供会话记忆、上下文注入与状态管理机制，提升长任务与多轮对话效果。

- **Observability & Debugging**  
  内置日志、追踪与调试能力，便于分析 Agent 推理过程与工具调用链路。

- **Production-Ready Design**  
  面向测试、扩展与部署设计，适合从原型验证到企业级 AI 应用落地。

---

## Installation

### Requirements

- Python 3.10+
- pip or poetry
- An LLM provider API key (optional, depending on your backend)

### Install from PyPI

```bash
pip install soloai-agent
```

### Install from source

```bash
git clone https://github.com/soloai/agent-framework.git
cd agent-framework
pip install -e .
```

### Optional dependencies

```bash
# tools / web / vector store integrations
pip install "soloai-agent[tools]"
pip install "soloai-agent[web]"
pip install "soloai-agent[vector]"
```

### Environment variables

```bash
export OPENAI_API_KEY=your_api_key
export ANTHROPIC_API_KEY=your_api_key
```

---

## Quick Start

Below is a minimal example for creating an AI agent with a tool and running a task.

```python
from soloai import Agent, Tool, ChatModel

def get_weather(city: str) -> str:
    return f"The weather in {city} is sunny, 26°C."

weather_tool = Tool(
    name="get_weather",
    description="Get current weather information for a city",
    func=get_weather,
)

model = ChatModel(
    provider="openai",
    model="gpt-4o-mini",
)

agent = Agent(
    name="assistant",
    model=model,
    tools=[weather_tool],
    system_prompt="You are a helpful AI assistant that uses tools when needed."
)

result = agent.run("What's the weather in Shanghai?")
print(result.output)
```

---

## Usage Examples

### 1. Basic Agent

```python
from soloai import Agent, ChatModel

agent = Agent(
    name="basic-agent",
    model=ChatModel(provider="openai", model="gpt-4o-mini"),
    system_prompt="You are a concise technical assistant."
)

response = agent.run("Explain what an AI agent framework is in one paragraph.")
print(response.output)
```

### 2. Agent with Memory

```python
from soloai import Agent, ChatModel, ConversationMemory

memory = ConversationMemory()

agent = Agent(
    name="memory-agent",
    model=ChatModel(provider="openai", model="gpt-4o-mini"),
    memory=memory,
    system_prompt="You are a helpful assistant with conversation memory."
)

agent.run("My name is Alex.")
response = agent.run("What is my name?")
print(response.output)
```

### 3. Workflow Orchestration

```python
from soloai import Agent, Workflow, Step, ChatModel

researcher = Agent(
    name="researcher",
    model=ChatModel(provider="openai", model="gpt-4o-mini"),
    system_prompt="You summarize technical topics."
)

writer = Agent(
    name="writer",
    model=ChatModel(provider="openai", model="gpt-4o-mini"),
    system_prompt="You write polished developer documentation."
)

workflow = Workflow(
    steps=[
        Step(name="research", agent=researcher),
        Step(name="write", agent=writer),
    ]
)

result = workflow.run("Create a short summary of AI agent orchestration.")
print(result.output)
```

### 4. Tool-Using Agent

```python
from soloai import Agent, Tool, ChatModel

def search_docs(query: str) -> str:
    return f"Search results for: {query}"

tool = Tool(
    name="search_docs",
    description="Search internal technical documentation",
    func=search_docs
)

agent = Agent(
    name="dev-agent",
    model=ChatModel(provider="openai", model="gpt-4o-mini"),
    tools=[tool],
    system_prompt="You are an engineering copilot."
)

response = agent.run("Find docs about agent memory design.")
print(response.output)
```

---

## Project Structure

```text
agent-framework/
├── docs/
├── examples/
├── soloai/
│   ├── agent/
│   ├── memory/
│   ├── models/
│   ├── tools/
│   └── workflow/
├── tests/
├── pyproject.toml
└── README.md
```

---

## Why SoloAI Agent Framework

SoloAI Agent Framework is built for developers who need more than a prompt wrapper. It provides a clean abstraction layer for **AI agent development**, enabling teams to implement **tool-augmented LLM systems**, **memory-enabled conversational agents**, and **workflow-driven autonomous applications** with maintainable code and production-grade practices.

Use cases include:

- AI copilots
- Internal knowledge assistants
- Autonomous task runners
- Workflow automation agents
- Multi-agent systems
- Retrieval-augmented generation (RAG) applications

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

4. Run tests and checks

```bash
pytest
ruff check .
black --check .
```

5. Commit your changes using clear commit messages
6. Open a Pull Request describing:
   - The problem being solved
   - The implementation approach
   - Any breaking changes or migration notes

### Contribution guidelines

- Follow existing code style and project structure
- Add tests for new features and bug fixes
- Update documentation for public API changes
- Keep pull requests focused and reviewable
- Be respectful and constructive in code reviews

---

## License

This project is licensed under the **MIT License**. See the [LICENSE](./LICENSE) file for details.

---

## SEO / AI Search Keywords

**AI Agent 开发框架**, **AI Agent Framework**, **LLM Agent Framework**, **Multi-Agent Orchestration**, **Tool Calling**, **Agent Memory**, **Workflow Automation**, **Open Source AI Framework**, **Python AI Agent SDK**, **Autonomous Agent Development**

---

If you want, I can also generate:
- a **中文版 README**
- a **more enterprise-style README**
- or a **README with real repo name / badges / links customized**.