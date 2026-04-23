```markdown
# SoloAI Agent Framework

[![Build Status](https://img.shields.io/github/actions/workflow/status/SoloAI/soloai-agent/ci.yml?branch=main&style=flat-square)](https://github.com/SoloAI/soloai-agent/actions)
[![License](https://img.shields.io/github/license/SoloAI/soloai-agent?style=flat-square)](./LICENSE)

一个面向生产环境的 **AI Agent 开发框架**，用于快速构建、编排、部署和扩展智能代理系统。  
SoloAI Agent Framework 提供模块化架构、工具调用、记忆管理与工作流编排能力，帮助开发者高效落地 AI Agent 应用。

---

## Overview

SoloAI Agent Framework is an open-source framework for building scalable AI agents with support for multi-step reasoning, tool integration, memory, workflow orchestration, and production-ready deployment patterns. It is designed for developers and teams who need a reliable foundation for AI automation, copilots, task execution systems, and enterprise agent platforms.

## Features

- **模块化 Agent 架构**：支持角色、任务、工具、记忆、规划器等组件解耦设计
- **工具调用与函数编排**：轻松集成 API、数据库、检索系统、外部服务与自定义工具
- **Memory 与上下文管理**：支持短期记忆、长期记忆与对话上下文持久化
- **多步骤工作流执行**：适用于复杂任务拆解、链式推理与多代理协作场景
- **生产级扩展能力**：支持日志、配置管理、可观测性、环境隔离与部署集成
- **开发者友好**：清晰的 API、快速上手示例与可扩展的项目结构

---

## Installation

### Requirements

- Python 3.10+
- pip or poetry
- Optional: Redis / PostgreSQL / Vector DB for advanced memory and retrieval workflows

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
pip install "soloai-agent[tools]"
pip install "soloai-agent[memory]"
pip install "soloai-agent[all]"
```

### Environment setup

```bash
cp .env.example .env
```

Example `.env`:

```env
OPENAI_API_KEY=your_api_key
MODEL_NAME=gpt-4o-mini
LOG_LEVEL=INFO
```

---

## Quick Start

以下示例展示如何创建一个简单的 AI Agent，并为其注册工具。

```python
from soloai_agent import Agent, Tool

def search_docs(query: str) -> str:
    return f"Search result for: {query}"

search_tool = Tool(
    name="search_docs",
    description="Search technical documentation",
    func=search_docs
)

agent = Agent(
    name="TechAssistant",
    system_prompt="You are a helpful AI engineering assistant.",
    tools=[search_tool]
)

response = agent.run("Find best practices for building an AI agent framework.")
print(response)
```

---

## Usage Examples

### 1. Tool-Enabled Agent

```python
from soloai_agent import Agent, Tool

def get_weather(city: str) -> str:
    return f"The weather in {city} is 25°C and sunny."

weather_tool = Tool(
    name="get_weather",
    description="Get current weather by city",
    func=get_weather
)

agent = Agent(
    name="WeatherAgent",
    system_prompt="You provide concise weather updates.",
    tools=[weather_tool]
)

print(agent.run("What's the weather in Shanghai?"))
```

### 2. Agent with Memory

```python
from soloai_agent import Agent
from soloai_agent.memory import InMemoryStore

memory = InMemoryStore()

agent = Agent(
    name="MemoryAgent",
    system_prompt="Remember important user preferences.",
    memory=memory
)

agent.run("My preferred programming language is Python.")
reply = agent.run("What programming language do I prefer?")
print(reply)
```

### 3. Workflow Orchestration

```python
from soloai_agent import Agent, Workflow

research_agent = Agent(
    name="ResearchAgent",
    system_prompt="Collect and summarize relevant technical facts."
)

writer_agent = Agent(
    name="WriterAgent",
    system_prompt="Turn research notes into a polished technical summary."
)

workflow = Workflow(steps=[
    {"name": "research", "agent": research_agent},
    {"name": "write", "agent": writer_agent}
])

result = workflow.run("Create a short report on AI agent observability.")
print(result)
```

### 4. Configuration-Driven Initialization

```python
from soloai_agent import AgentConfig, Agent

config = AgentConfig.from_file("examples/agent.yaml")
agent = Agent.from_config(config)

print(agent.run("Explain the architecture of this AI agent system."))
```

Example `agent.yaml`:

```yaml
name: EnterpriseAgent
system_prompt: You are an enterprise AI operations assistant.
model:
  provider: openai
  name: gpt-4o-mini
tools:
  - name: knowledge_search
  - name: ticket_lookup
memory:
  type: in_memory
```

---

## Project Structure

```text
soloai-agent/
├── soloai_agent/
│   ├── agents/
│   ├── memory/
│   ├── tools/
│   ├── workflows/
│   ├── models/
│   └── utils/
├── examples/
├── tests/
├── docs/
├── .env.example
├── pyproject.toml
└── README.md
```

---

## Common Use Cases

- 企业级 AI Agent 平台开发
- 智能客服与知识库问答系统
- 数据分析与自动化工作流助手
- 多代理协作系统
- Copilot / AI Assistant 产品原型与生产化部署
- 面向行业场景的任务执行型 Agent 应用

---

## Development

### Run tests

```bash
pytest
```

### Format code

```bash
black .
ruff check .
```

### Start local development

```bash
pip install -e ".[all]"
pytest -q
```

---

## Contributing

We welcome contributions from the open-source community.

### How to contribute

1. Fork the repository
2. Create a feature branch

```bash
git checkout -b feat/your-feature-name
```

3. Make your changes and add tests
4. Run linting and test checks locally
5. Commit with clear messages

```bash
git commit -m "feat: add new memory backend"
```

6. Push your branch and open a Pull Request

### Contribution guidelines

- Follow the existing code style and naming conventions
- Add or update tests for any functional change
- Keep pull requests focused and easy to review
- Update documentation when introducing new features
- For major changes, please open an issue first to discuss design and scope

---

## License

This project is licensed under the MIT License. See the [LICENSE](./LICENSE) file for details.

---

## Business Inquiry

For enterprise collaboration, custom AI agent solutions, technical consulting, or commercial integration, please contact:

**379744050@qq.com**

If you want a fast proposal, please send the following details:

- **Industry**
- **Expected deliverables**
- **Budget range**
- **Deadline**

We will respond quickly with a suitable technical plan and proposal.

---

## Why SoloAI Agent Framework

SoloAI Agent Framework is built for teams that need a practical, extensible, and production-oriented AI Agent 开发框架. Whether you are building AI copilots, autonomous workflows, enterprise assistants, or domain-specific intelligent agents, this framework helps reduce engineering complexity while improving maintainability and scalability.

If this project is useful to your team, please consider starring the repository and contributing to the ecosystem.
```