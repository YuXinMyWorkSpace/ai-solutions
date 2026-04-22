# SoloAI Agent Framework

[![Build Status](https://img.shields.io/github/actions/workflow/status/soloai/agent-framework/ci.yml?branch=main)](https://github.com/soloai/agent-framework/actions)
[![License](https://img.shields.io/github/license/soloai/agent-framework)](./LICENSE)

> 一个面向现代 **AI Agent 开发框架** 的开源项目，用于快速构建、编排、部署和扩展智能体应用。  
> SoloAI Agent Framework 提供模块化架构、工具调用、记忆管理与工作流编排能力，帮助开发者高效落地生产级 AI Agent 系统。

---

## Overview

**SoloAI Agent Framework** is an open-source framework for building **AI agents**, **multi-agent workflows**, and **LLM-powered applications** with a clean, extensible, and production-ready architecture. It is designed for developers who need reliable orchestration, tool integration, memory handling, and flexible runtime control for modern agent systems.

## Features

- **Modular Agent Architecture**  
  使用可插拔组件构建 Agent，包括模型、工具、记忆、规划器与执行器。

- **Tool Calling & Function Execution**  
  支持将外部 API、数据库、搜索引擎、业务函数无缝接入智能体能力链路。

- **Workflow Orchestration**  
  支持单 Agent 与多 Agent 协作流程，适用于复杂任务拆解与执行编排。

- **Memory Management**  
  提供短期记忆、长期记忆与上下文管理能力，增强持续对话与任务连续性。

- **Production-Oriented Design**  
  支持日志、配置管理、可观测性、错误处理与扩展接口，便于工程化部署。

- **Developer-Friendly API**  
  简洁直观的 API 设计，帮助团队快速从原型开发过渡到生产环境。

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
git clone https://github.com/soloai/agent-framework.git
cd agent-framework
pip install -e .
```

### Optional dependencies

```bash
pip install "soloai-agent[tools,memory,observability]"
```

---

## Quick Start

下面的示例展示了如何快速创建一个具备工具调用能力的 AI Agent。

```python
from soloai import Agent, Tool, ChatModel

def get_weather(city: str) -> str:
    return f"{city} 的天气为：晴，25°C"

weather_tool = Tool(
    name="weather",
    description="Get weather information for a city",
    func=get_weather
)

model = ChatModel(
    provider="openai",
    model="gpt-4o-mini",
    api_key="YOUR_API_KEY"
)

agent = Agent(
    name="assistant",
    model=model,
    tools=[weather_tool],
    system_prompt="You are a helpful AI assistant."
)

result = agent.run("请帮我查询北京天气，并给出穿衣建议。")
print(result.output)
```

---

## Usage

### 1. Basic Agent

```python
from soloai import Agent, ChatModel

agent = Agent(
    name="basic-agent",
    model=ChatModel(provider="openai", model="gpt-4o-mini"),
    system_prompt="You are a concise technical assistant."
)

response = agent.run("Explain what an AI agent framework is.")
print(response.output)
```

### 2. Agent with Memory

```python
from soloai import Agent, ChatModel, ConversationMemory

memory = ConversationMemory(window_size=10)

agent = Agent(
    name="memory-agent",
    model=ChatModel(provider="openai", model="gpt-4o-mini"),
    memory=memory
)

agent.run("我叫 Alex。")
response = agent.run("你还记得我的名字吗？")
print(response.output)
```

### 3. Workflow Orchestration

```python
from soloai import Agent, Workflow, ChatModel

planner = Agent(
    name="planner",
    model=ChatModel(provider="openai", model="gpt-4o-mini"),
    system_prompt="Break tasks into actionable steps."
)

executor = Agent(
    name="executor",
    model=ChatModel(provider="openai", model="gpt-4o-mini"),
    system_prompt="Execute tasks based on the plan."
)

workflow = Workflow(
    name="research-workflow",
    agents=[planner, executor]
)

result = workflow.run("Research the market trends of AI agents in 2025.")
print(result.output)
```

### 4. Tool Integration

```python
from soloai import Tool

def search_docs(query: str) -> str:
    return f"Search results for: {query}"

doc_tool = Tool(
    name="docs_search",
    description="Search internal technical documentation",
    func=search_docs
)
```

---

## Project Structure

```bash
agent-framework/
├── docs/
├── examples/
├── soloai/
│   ├── agents/
│   ├── memory/
│   ├── tools/
│   ├── workflows/
│   └── models/
├── tests/
├── pyproject.toml
└── README.md
```

---

## Contributing

We welcome contributions from the community.

### How to contribute

1. Fork the repository
2. Create a feature branch

```bash
git checkout -b feat/your-feature-name
```

3. Commit your changes

```bash
git commit -m "feat: add your feature"
```

4. Push to your branch

```bash
git push origin feat/your-feature-name
```

5. Open a Pull Request

### Development setup

```bash
git clone https://github.com/soloai/agent-framework.git
cd agent-framework
python -m venv .venv
source .venv/bin/activate  # Windows: .venv\Scripts\activate
pip install -e ".[dev]"
pre-commit install
```

### Recommended contribution types

- New agent capabilities
- Additional tool integrations
- Workflow improvements
- Performance optimization
- Documentation and examples
- Bug fixes and tests

Please ensure:

- Code follows project style guidelines
- New features include tests
- Documentation is updated when relevant
- Commit messages are clear and conventional

---

## License

This project is licensed under the **MIT License**. See the [LICENSE](./LICENSE) file for details.

---

## Keywords

AI Agent Framework, Agent Orchestration, Multi-Agent System, LLM Framework, Tool Calling, Memory Management, Workflow Engine, Open Source AI Infrastructure, Python AI Agent SDK, SoloAI