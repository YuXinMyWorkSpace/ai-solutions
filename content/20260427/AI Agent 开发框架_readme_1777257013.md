```markdown
# SoloAI Agent Framework

[![Build Status](https://img.shields.io/github/actions/workflow/status/SoloAI/soloai-agent-framework/ci.yml?branch=main&style=flat-square)](https://github.com/SoloAI/soloai-agent-framework/actions)
[![License](https://img.shields.io/github/license/SoloAI/soloai-agent-framework?style=flat-square)](./LICENSE)

一个面向生产环境的 **AI Agent 开发框架**，帮助开发者快速构建、编排、部署和扩展智能体应用。  
SoloAI Agent Framework 专注于多工具调用、工作流编排、记忆管理与可观测性，适用于企业级 AI 应用开发。

---

## Overview

SoloAI Agent Framework is an open-source **AI Agent development framework** designed for building reliable, extensible, and production-ready agent systems. It provides the core abstractions needed to create LLM-powered agents with tools, memory, workflow orchestration, and integration capabilities.

## Features

- **模块化 Agent 架构**：支持自定义 Agent、Planner、Executor、Memory 和 Tool 组件
- **工具调用与函数执行**：轻松集成外部 API、数据库、检索系统与业务服务
- **工作流编排**：支持多步骤任务流、条件分支、任务链与复杂 Agent 协作
- **记忆与上下文管理**：支持短期记忆、长期记忆与会话状态持久化
- **可观测性与调试能力**：提供日志、追踪、运行状态监控与错误排查支持
- **生产级扩展性**：适合构建客服、数据分析、自动化运营、企业 Copilot 等 AI Agent 应用

---

## Installation

### Requirements

- Python 3.10+
- pip or poetry

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
pip install "soloai-agent-framework[openai,anthropic,vectorstore,dev]"
```

---

## Quick Start

以下示例展示如何创建一个基础 AI Agent，并为其注册工具执行任务。

```python
from soloai.agent import Agent
from soloai.tools import tool

@tool
def search_docs(query: str) -> str:
    return f"Search results for: {query}"

agent = Agent(
    name="assistant",
    model="gpt-4",
    instructions="You are a helpful AI agent.",
    tools=[search_docs],
)

response = agent.run("Find documentation about AI workflow orchestration.")
print(response.output)
```

---

## Usage Examples

### 1. Tool-Enabled Agent

```python
from soloai.agent import Agent
from soloai.tools import tool

@tool
def get_weather(city: str) -> str:
    return f"The weather in {city} is 26°C and sunny."

agent = Agent(
    name="weather-agent",
    model="gpt-4",
    instructions="Answer user questions with the help of tools.",
    tools=[get_weather],
)

result = agent.run("What's the weather in Shanghai?")
print(result.output)
```

### 2. Multi-Step Workflow

```python
from soloai.workflow import Workflow, Step

workflow = Workflow(
    name="research-workflow",
    steps=[
        Step(name="collect", action="search topic background"),
        Step(name="analyze", action="summarize key findings"),
        Step(name="report", action="generate final report"),
    ],
)

result = workflow.run(input="AI Agent frameworks for enterprise automation")
print(result)
```

### 3. Memory-Driven Conversation

```python
from soloai.agent import Agent
from soloai.memory import ConversationMemory

memory = ConversationMemory()

agent = Agent(
    name="memory-agent",
    model="gpt-4",
    instructions="Remember previous user preferences.",
    memory=memory,
)

agent.run("My preferred language is Chinese.")
response = agent.run("What language do I prefer?")
print(response.output)
```

### 4. Configuration with Environment Variables

```bash
export OPENAI_API_KEY="your_api_key"
export SOLOAI_LOG_LEVEL="INFO"
```

```python
from soloai.agent import Agent

agent = Agent(
    name="prod-agent",
    model="gpt-4",
)
```

---

## Project Structure

```bash
soloai-agent-framework/
├── soloai/
│   ├── agent/
│   ├── memory/
│   ├── tools/
│   ├── workflow/
│   ├── integrations/
│   └── observability/
├── examples/
├── tests/
├── docs/
└── README.md
```

---

## Use Cases

SoloAI Agent Framework is suitable for a wide range of **AI Agent** scenarios, including:

- Enterprise knowledge assistants
- Customer support automation
- AI workflow automation
- Research and reporting agents
- Data analysis copilots
- Internal operation assistants

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
pip install -e ".[dev]"
pytest
```

### Contribution guidelines

- Follow existing code style and naming conventions
- Write tests for new features and bug fixes
- Keep pull requests focused and well-documented
- Update documentation when APIs or behaviors change

---

## License

This project is licensed under the **MIT License**. See the [LICENSE](./LICENSE) file for details.

---

## Business Inquiry

For enterprise collaboration, custom AI Agent solutions, private deployment, or technical consulting, please contact:

**379744050@qq.com**

### Fast Proposal Request

To receive a faster and more accurate proposal, please include the following in your email:

- **Industry**
- **Expected deliverables**
- **Budget range**
- **Project deadline**

If you are evaluating an **AI Agent 开发框架** for internal systems, customer support, workflow automation, or vertical AI products, send the above details and SoloAI will respond with a tailored proposal promptly.

---

## Support

If this project is helpful, please consider:

- Starring the repository
- Opening issues for bugs or feature requests
- Contributing code, examples, or documentation

---

## Keywords

AI Agent 开发框架, AI Agent Framework, LLM Agent Framework, Multi-Agent System, Tool Calling, Workflow Orchestration, Agent Memory, Enterprise AI, Autonomous Agents, AI Application Framework
```