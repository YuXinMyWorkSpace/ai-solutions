# SoloAI Agent Framework

[![Build Status](https://img.shields.io/github/actions/workflow/status/SoloAI/soloai-agent/ci.yml?branch=main)](https://github.com/SoloAI/soloai-agent/actions)
[![License](https://img.shields.io/github/license/SoloAI/soloai-agent)](./LICENSE)

**SoloAI Agent Framework** 是一个面向生产环境的 **AI Agent 开发框架**，用于快速构建、编排、测试与部署具备工具调用、记忆管理和多步骤推理能力的智能代理系统。  
它帮助开发者以模块化方式集成 LLM、工具链、工作流和外部系统，适用于自动化助手、企业 Copilot、任务执行代理和多智能体协作场景。

---

## Features

- **模块化 Agent 架构**：支持任务规划、推理、工具调用、记忆、上下文管理等核心能力解耦。
- **多模型与多提供商接入**：兼容 OpenAI、Azure OpenAI、Anthropic、本地模型及自定义推理后端。
- **工具与工作流编排**：支持 Function Calling、插件扩展、外部 API 调用及复杂工作流设计。
- **可观测性与调试能力**：内置日志、追踪、事件回放和执行链路分析，便于调优和排障。
- **生产级部署支持**：适合构建可扩展、高可用、可测试的 AI Agent 服务。
- **面向 RAG 与企业集成**：可与向量数据库、知识库、检索服务和业务系统无缝结合。

---

## Installation

### Requirements

- Python 3.10+
- `pip` or `poetry`
- A valid LLM provider API key (optional for local model usage)

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

### Environment setup

```bash
export OPENAI_API_KEY=your_api_key
export SOLOAI_MODEL=gpt-4o-mini
```

For Windows PowerShell:

```powershell
$env:OPENAI_API_KEY="your_api_key"
$env:SOLOAI_MODEL="gpt-4o-mini"
```

---

## Quick Start

以下示例展示如何创建一个具备基础对话与工具调用能力的 AI Agent：

```python
from soloai import Agent, Tool

def get_weather(city: str) -> str:
    return f"{city} 当前天气：晴，25°C"

weather_tool = Tool(
    name="get_weather",
    description="Get current weather information for a city",
    func=get_weather
)

agent = Agent(
    name="assistant",
    model="gpt-4o-mini",
    system_prompt="You are a helpful AI assistant.",
    tools=[weather_tool]
)

response = agent.run("请告诉我北京今天天气如何？")
print(response.output)
```

---

## Usage Examples

### 1. Basic Chat Agent

```python
from soloai import Agent

agent = Agent(
    name="chat-agent",
    model="gpt-4o-mini",
    system_prompt="You are an expert technical assistant."
)

result = agent.run("Explain what an AI agent framework is.")
print(result.output)
```

### 2. Agent with Memory

```python
from soloai import Agent, Memory

memory = Memory()

agent = Agent(
    name="memory-agent",
    model="gpt-4o-mini",
    memory=memory,
    system_prompt="Remember key user preferences and use them in future responses."
)

agent.run("My preferred programming language is Python.")
result = agent.run("What programming language do I prefer?")
print(result.output)
```

### 3. Tool Calling and Task Automation

```python
from soloai import Agent, Tool

def search_docs(query: str) -> str:
    return f"Top documentation results for: {query}"

def create_ticket(title: str) -> str:
    return f"Ticket created: {title}"

tools = [
    Tool(name="search_docs", description="Search internal docs", func=search_docs),
    Tool(name="create_ticket", description="Create a support ticket", func=create_ticket),
]

agent = Agent(
    name="ops-agent",
    model="gpt-4o-mini",
    tools=tools,
    system_prompt="Resolve user issues with available tools."
)

result = agent.run("Search docs for deployment failure causes and create a ticket.")
print(result.output)
```

### 4. Workflow-Oriented Agent

```python
from soloai import Agent, Workflow

workflow = Workflow(name="research-workflow")

agent = Agent(
    name="research-agent",
    model="gpt-4o-mini",
    workflow=workflow,
    system_prompt="Break down complex tasks into clear steps and execute them."
)

result = agent.run("Research AI agent frameworks and summarize key differences.")
print(result.output)
```

---

## Architecture Overview

SoloAI Agent Framework is designed for developers building **AI-native applications**, **autonomous agents**, and **LLM orchestration systems**. A typical architecture includes:

- **LLM Layer**: OpenAI, Anthropic, Azure OpenAI, local LLMs
- **Agent Core**: planning, reasoning, tool execution, memory, guardrails
- **Knowledge Layer**: vector stores, RAG pipelines, document retrieval
- **Integration Layer**: REST APIs, databases, enterprise services, SaaS tools
- **Observability Layer**: tracing, logs, evaluation, runtime metrics

This makes SoloAI suitable for:

- AI Copilot platforms
- Enterprise automation assistants
- Customer support agents
- Research and analysis agents
- Multi-agent orchestration systems

---

## Installation for Development

```bash
git clone https://github.com/SoloAI/soloai-agent.git
cd soloai-agent
pip install -e ".[dev]"
pre-commit install
pytest
```

---

## Contributing

We welcome contributions from the open-source community.

### How to contribute

1. Fork the repository
2. Create a feature branch

```bash
git checkout -b feature/amazing-feature
```

3. Commit your changes

```bash
git commit -m "feat: add amazing feature"
```

4. Push to your branch

```bash
git push origin feature/amazing-feature
```

5. Open a Pull Request

### Contribution guidelines

- Follow PEP 8 and project linting rules
- Add tests for new features and bug fixes
- Update documentation when changing public APIs
- Use clear, conventional commit messages
- Discuss major changes via GitHub Issues before implementation

### Local quality checks

```bash
ruff check .
pytest
```

---

## License

This project is licensed under the **MIT License**. See the [LICENSE](./LICENSE) file for details.

---

## Keywords

AI Agent Framework, LLM Orchestration, Multi-Agent System, Tool Calling, RAG, Memory, Workflow Engine, Function Calling, Autonomous Agents, Python AI Framework

--- 

If you want, I can also generate:
- a **Chinese-only README**
- a **bilingual README (中文 + English)**
- a **more product-oriented version for GitHub landing page conversion**