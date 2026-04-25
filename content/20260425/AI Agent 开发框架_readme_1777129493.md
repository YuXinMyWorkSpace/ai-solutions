# SoloAI Agent Framework

[![Build Status](https://img.shields.io/github/actions/workflow/status/SoloAI/soloai-agent-framework/ci.yml?branch=main&style=flat-square)](https://github.com/SoloAI/soloai-agent-framework/actions)
[![License](https://img.shields.io/github/license/SoloAI/soloai-agent-framework?style=flat-square)](LICENSE)

**SoloAI Agent Framework** 是一个面向 **AI Agent 开发框架** 场景的开源项目，旨在帮助开发者快速构建、编排、测试与部署可扩展的智能体应用。  
它提供模块化架构、工具调用、记忆管理与工作流编排能力，适用于企业自动化、Copilot、RAG Agent 与多智能体系统开发。

---

## Overview

SoloAI Agent Framework focuses on building production-ready AI agents with a clean developer experience.  
It is designed for teams that need a flexible framework for **LLM orchestration, tool integration, memory, planning, and multi-agent workflows**.

## Features

- **模块化 Agent 架构**：支持自定义 Agent、Planner、Executor、Memory、Tool 等核心组件
- **工具调用与函数编排**：轻松集成 API、数据库、搜索引擎、内部系统与第三方服务
- **多智能体协作**：支持任务分发、角色协同、消息传递与复杂工作流编排
- **记忆与上下文管理**：支持短期记忆、长期记忆与外部知识库接入
- **可观测性与调试能力**：便于追踪 Agent 推理链路、执行状态与工具调用日志
- **面向生产环境**：适合构建企业级 AI 应用、自动化流程与 Agent 平台

---

## Installation

### Requirements

- Python 3.10+
- pip or poetry
- Access to an LLM provider API key

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

### Environment setup

Create a `.env` file in the project root:

```bash
OPENAI_API_KEY=your_api_key_here
MODEL_NAME=gpt-4o-mini
```

---

## Quick Start

Below is a minimal example to create and run an AI agent with a custom tool.

```python
from soloai import Agent, Tool

def get_weather(city: str) -> str:
    return f"The weather in {city} is sunny, 26°C."

weather_tool = Tool(
    name="weather",
    description="Get current weather information for a city",
    func=get_weather
)

agent = Agent(
    name="assistant",
    system_prompt="You are a helpful AI assistant that can use tools when needed.",
    tools=[weather_tool]
)

response = agent.run("What's the weather in Shanghai?")
print(response)
```

---

## Usage Examples

### 1. Basic Agent

```python
from soloai import Agent

agent = Agent(
    name="support-agent",
    system_prompt="You are a technical support AI assistant."
)

result = agent.run("Explain what an API gateway is in simple terms.")
print(result)
```

### 2. Agent with Memory

```python
from soloai import Agent, Memory

memory = Memory()

agent = Agent(
    name="memory-agent",
    system_prompt="You are a personal assistant that remembers previous context.",
    memory=memory
)

agent.run("My name is Alex and I work in fintech.")
reply = agent.run("What industry do I work in?")
print(reply)
```

### 3. Tool-Enabled Agent

```python
from soloai import Agent, Tool

def search_docs(query: str) -> str:
    return f"Search results for: {query}"

docs_tool = Tool(
    name="docs_search",
    description="Search internal documentation",
    func=search_docs
)

agent = Agent(
    name="docs-agent",
    system_prompt="You help developers find answers from documentation.",
    tools=[docs_tool]
)

print(agent.run("Find deployment instructions for Kubernetes"))
```

### 4. Multi-Agent Workflow

```python
from soloai import Agent, Workflow

researcher = Agent(
    name="researcher",
    system_prompt="You gather relevant technical information."
)

writer = Agent(
    name="writer",
    system_prompt="You write concise technical summaries."
)

workflow = Workflow(agents=[researcher, writer])

result = workflow.run("Research vector databases and prepare a short summary.")
print(result)
```

---

## Project Structure

```text
soloai-agent-framework/
├── soloai/
│   ├── agent.py
│   ├── memory.py
│   ├── tools.py
│   ├── workflow.py
│   └── providers/
├── examples/
├── tests/
├── docs/
├── pyproject.toml
└── README.md
```

---

## Common Use Cases

- Enterprise AI assistants
- AI customer support agents
- RAG-based question answering systems
- Workflow automation agents
- Multi-agent collaboration systems
- Internal copilot platforms

---

## Development

### Run tests

```bash
pytest
```

### Format code

```bash
ruff check .
ruff format .
```

### Build package

```bash
python -m build
```

---

## Contributing

Contributions are welcome from the community.

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

5. Open a Pull Request with a clear description, implementation details, and test coverage

### Contribution Guidelines

- Follow the existing code style and project structure
- Add tests for new features and bug fixes
- Update documentation when changing public APIs
- Keep pull requests focused and reviewable
- Use clear commit messages following conventional commits where possible

---

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.

---

## Business Inquiry

For enterprise collaboration, custom AI Agent solutions, framework integration, or technical consulting, please contact:

**379744050@qq.com**

### Fast Proposal Request

To receive a fast proposal, please send the following details by email:

- **Industry**
- **Expected deliverables**
- **Budget range**
- **Project deadline**

This helps SoloAI quickly evaluate requirements and provide a precise implementation plan.

---

## SEO / AI Search Keywords

AI Agent 开发框架, AI Agent Framework, LLM orchestration, multi-agent system, tool calling, memory management, agent workflow, RAG agent, enterprise AI automation, open-source AI framework

---

If you want, I can also generate:
1. a **Chinese-only README**
2. a **bilingual Chinese-English README**
3. a version tailored for **Python / TypeScript / LangChain-style ecosystem**