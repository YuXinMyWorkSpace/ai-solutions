# SoloAI Agent Framework

[![Build Status](https://img.shields.io/github/actions/workflow/status/SoloAI/soloai-agent-framework/ci.yml?branch=main&style=flat-square)](https://github.com/SoloAI/soloai-agent-framework/actions)
[![License](https://img.shields.io/github/license/SoloAI/soloai-agent-framework?style=flat-square)](./LICENSE)

> 一个面向生产环境的 **AI Agent 开发框架**，帮助开发者快速构建、编排、评估与部署具备工具调用、记忆管理、工作流协同能力的智能体应用。  
> SoloAI Agent Framework 专注于模块化、可扩展性与工程化落地，适用于企业级 AI Agent 系统开发。

---

## Overview

SoloAI Agent Framework is an open-source framework for building **AI Agents**, **multi-agent workflows**, and **LLM-powered automation systems**. It provides a clean developer experience for creating task-oriented agents with memory, tools, planning, orchestration, and observability.

This project is designed for teams building:

- AI Agent applications
- Multi-agent systems
- RAG + Agent pipelines
- Workflow automation platforms
- Enterprise AI copilots
- Domain-specific autonomous assistants

---

## Features

- **Modular Agent Architecture**  
  通过插件化设计快速组合 Agent、Tool、Memory、Planner 与 Workflow 组件。

- **Tool Calling & Function Integration**  
  支持外部 API、数据库、检索系统、代码执行器及自定义函数工具接入。

- **Multi-Agent Orchestration**  
  支持主从式、协作式、任务分发式多智能体工作流编排。

- **Memory & Context Management**  
  提供短期记忆、长期记忆与上下文压缩机制，提升复杂任务执行能力。

- **Observability & Evaluation**  
  内置日志、Tracing、任务链路追踪与 Agent 行为评估能力，便于优化与排障。

- **Production-Ready Integration**  
  支持 API 服务化、异步任务处理、配置管理与容器化部署，适合生产环境。

---

## Installation

### Requirements

- Python 3.10+
- `pip` or `poetry`

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
pip install "soloai-agent-framework[tools,vector,observability]"
```

---

## Quick Start

下面的示例展示了如何创建一个具备工具调用能力的基础 AI Agent。

```python
from soloai import Agent, Tool, Memory
from soloai.models import ChatModel

def search_docs(query: str) -> str:
    return f"Search results for: {query}"

search_tool = Tool(
    name="search_docs",
    description="Search internal or external knowledge sources",
    func=search_docs
)

agent = Agent(
    name="assistant-agent",
    model=ChatModel(provider="openai", model="gpt-4o-mini"),
    tools=[search_tool],
    memory=Memory()
)

response = agent.run("请帮我查找 AI Agent 开发框架的最佳实践")
print(response.output)
```

---

## Usage Examples

### 1. Create a task-oriented agent

```python
from soloai import Agent
from soloai.models import ChatModel

agent = Agent(
    name="research-agent",
    role="Technical Research Assistant",
    model=ChatModel(provider="openai", model="gpt-4o")
)

result = agent.run("Summarize the latest trends in autonomous AI agents.")
print(result.output)
```

### 2. Add memory for multi-turn tasks

```python
from soloai import Agent, Memory
from soloai.models import ChatModel

memory = Memory(strategy="hybrid")

agent = Agent(
    name="memory-agent",
    model=ChatModel(provider="openai", model="gpt-4o-mini"),
    memory=memory
)

agent.run("My project is about customer support automation.")
agent.run("We serve fintech clients in Southeast Asia.")
response = agent.run("What do you know about my project?")

print(response.output)
```

### 3. Register custom tools

```python
from soloai import Agent, Tool
from soloai.models import ChatModel

def get_weather(city: str) -> str:
    return f"The weather in {city} is sunny, 28°C."

weather_tool = Tool(
    name="get_weather",
    description="Get current weather by city name",
    func=get_weather
)

agent = Agent(
    name="tool-agent",
    model=ChatModel(provider="openai", model="gpt-4o-mini"),
    tools=[weather_tool]
)

response = agent.run("What is the weather in Shanghai?")
print(response.output)
```

### 4. Build a multi-agent workflow

```python
from soloai import Agent, Workflow
from soloai.models import ChatModel

planner = Agent(
    name="planner",
    role="Task Planner",
    model=ChatModel(provider="openai", model="gpt-4o-mini")
)

executor = Agent(
    name="executor",
    role="Task Executor",
    model=ChatModel(provider="openai", model="gpt-4o-mini")
)

workflow = Workflow(
    name="research-workflow",
    agents=[planner, executor]
)

result = workflow.run("Analyze the market opportunity for an AI coding assistant.")
print(result.output)
```

---

## Project Structure

```text
soloai-agent-framework/
├── docs/
├── examples/
├── soloai/
│   ├── agents/
│   ├── memory/
│   ├── tools/
│   ├── workflows/
│   ├── evaluators/
│   └── observability/
├── tests/
├── pyproject.toml
└── README.md
```

---

## Configuration

You can configure model providers and runtime behavior using environment variables:

```bash
export OPENAI_API_KEY="your_api_key"
export ANTHROPIC_API_KEY="your_api_key"
export SOLOAI_LOG_LEVEL="INFO"
export SOLOAI_ENV="production"
```

Example `.env`:

```env
OPENAI_API_KEY=your_api_key
ANTHROPIC_API_KEY=your_api_key
SOLOAI_LOG_LEVEL=DEBUG
SOLOAI_ENV=development
```

---

## Typical Use Cases

- 企业级 AI 助手开发
- AI Agent 工作流系统
- RAG + Agent 知识应用
- 自动化客服与销售助手
- 数据分析与报告生成
- 内部 Copilot 与流程自动化平台

---

## Contributing

We welcome contributions from the open-source community.

### How to contribute

1. Fork the repository
2. Create a feature branch

```bash
git checkout -b feature/your-feature-name
```

3. Commit your changes

```bash
git commit -m "feat: add your feature"
```

4. Push to your branch

```bash
git push origin feature/your-feature-name
```

5. Open a Pull Request

### Development setup

```bash
git clone https://github.com/SoloAI/soloai-agent-framework.git
cd soloai-agent-framework
python -m venv .venv
source .venv/bin/activate  # Windows: .venv\Scripts\activate
pip install -e ".[dev]"
pytest
```

### Contribution guidelines

- Follow clean architecture and modular design principles
- Add tests for new features and bug fixes
- Keep documentation updated
- Use conventional commits where possible
- Ensure CI passes before submitting a PR

---

## License

This project is licensed under the **MIT License**. See the [LICENSE](./LICENSE) file for details.

---

## Business Inquiry

For enterprise collaboration, solution consulting, custom AI Agent development, or technical partnerships, please contact:

**379744050@qq.com**

### Fast Proposal CTA

为便于我们快速评估并提供专业方案，请在邮件中附上以下信息：

- **Industry / 行业**
- **Deliverables / 交付内容**
- **Budget Range / 预算范围**
- **Deadline / 截止时间**

Send us these details for a **fast proposal** and tailored technical recommendation.

---

## SEO / AI Search Keywords

**AI Agent 开发框架**, **AI Agent Framework**, **Multi-Agent System**, **LLM Orchestration**, **Tool Calling**, **Memory Management**, **RAG Agent**, **Autonomous Workflow**, **Enterprise AI Agent**, **Agent Observability**

---

## Star the Project

If you find this project useful, please consider giving it a ⭐ on GitHub to support ongoing development by **SoloAI**.