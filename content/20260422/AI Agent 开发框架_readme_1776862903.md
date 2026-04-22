# SoloAI Agent Framework

[![Build Status](https://img.shields.io/github/actions/workflow/status/soloai/soloai-agent-framework/ci.yml?branch=main)](https://github.com/soloai/soloai-agent-framework/actions)
[![License](https://img.shields.io/github/license/soloai/soloai-agent-framework)](./LICENSE)

**SoloAI Agent Framework** 是一个面向生产环境的 **AI Agent 开发框架**，用于快速构建、编排、测试与部署具备工具调用、记忆管理和多步骤推理能力的智能体系统。  
它为开发者提供模块化架构、可扩展接口与工程化工作流，适用于构建 LLM 应用、自动化代理、多智能体协作系统和企业级 AI 工作流。

---

## Features

- **Modular Agent Architecture**  
  通过可插拔组件构建 Agent，包括模型层、工具层、记忆层、任务规划层和执行层。

- **Tool Calling & Workflow Orchestration**  
  支持函数调用、外部 API 集成、任务链路编排和复杂工作流自动化。

- **Memory & Context Management**  
  提供短期记忆、长期记忆与上下文压缩机制，提升多轮交互与任务连续性。

- **Multi-Agent Collaboration**  
  支持多个 Agent 的角色分工、消息传递与协作执行，适用于复杂问题求解。

- **Observability & Evaluation**  
  内置日志、追踪、调试和评测接口，便于分析 Agent 行为和优化系统性能。

- **Production-Ready Deployment**  
  支持本地开发、容器化部署和云端集成，适合从原型验证到生产落地。

---

## Installation

### Requirements

- Python 3.10+
- `pip` or `poetry`
- Optional: Docker for containerized deployment

### Install via pip

```bash
pip install soloai-agent-framework
```

### Install from source

```bash
git clone https://github.com/soloai/soloai-agent-framework.git
cd soloai-agent-framework
pip install -e .
```

### Install with Poetry

```bash
git clone https://github.com/soloai/soloai-agent-framework.git
cd soloai-agent-framework
poetry install
```

---

## Quick Start

下面示例展示如何创建一个基础 AI Agent，并为其注册一个工具函数。

```python
from soloai import Agent, Tool
from soloai.models import OpenAIChatModel

def search_docs(query: str) -> str:
    return f"Search results for: {query}"

agent = Agent(
    name="assistant",
    model=OpenAIChatModel(
        model="gpt-4o-mini",
        api_key="YOUR_API_KEY"
    ),
    tools=[
        Tool.from_function(search_docs)
    ],
    system_prompt="You are a helpful AI agent that solves developer tasks."
)

response = agent.run("Find documentation about vector databases.")
print(response.output)
```

---

## Usage Examples

### 1. Agent with Memory

为 Agent 启用记忆能力，以支持多轮上下文管理。

```python
from soloai import Agent
from soloai.memory import InMemoryStore
from soloai.models import OpenAIChatModel

memory = InMemoryStore()

agent = Agent(
    name="memory-agent",
    model=OpenAIChatModel(model="gpt-4o-mini", api_key="YOUR_API_KEY"),
    memory=memory,
    system_prompt="Remember user preferences and conversation context."
)

agent.run("My favorite programming language is Python.")
response = agent.run("What programming language do I like?")
print(response.output)
```

### 2. Tool Calling for External APIs

将外部服务封装为工具，供 Agent 自动调用。

```python
import requests
from soloai import Agent, Tool
from soloai.models import OpenAIChatModel

def get_weather(city: str) -> str:
    data = requests.get(f"https://api.example.com/weather?city={city}").json()
    return f"{city}: {data['temp']}°C, {data['condition']}"

agent = Agent(
    name="weather-agent",
    model=OpenAIChatModel(model="gpt-4o-mini", api_key="YOUR_API_KEY"),
    tools=[Tool.from_function(get_weather)],
    system_prompt="You are a weather assistant. Use tools when needed."
)

response = agent.run("What's the weather in Shanghai?")
print(response.output)
```

### 3. Multi-Agent Workflow

通过多个 Agent 协作完成更复杂的任务。

```python
from soloai import Agent, Workflow
from soloai.models import OpenAIChatModel

researcher = Agent(
    name="researcher",
    model=OpenAIChatModel(model="gpt-4o-mini", api_key="YOUR_API_KEY"),
    system_prompt="Research the topic and gather facts."
)

writer = Agent(
    name="writer",
    model=OpenAIChatModel(model="gpt-4o-mini", api_key="YOUR_API_KEY"),
    system_prompt="Write a concise technical summary based on research notes."
)

workflow = Workflow(agents=[researcher, writer])

result = workflow.run("Explain the benefits of retrieval-augmented generation.")
print(result.output)
```

### 4. Run a Local Development Server

如果框架提供 API 或调试面板，可使用以下方式启动本地服务：

```bash
soloai serve --host 0.0.0.0 --port 8080
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
│   ├── models/
│   ├── tools/
│   ├── workflows/
│   └── telemetry/
├── tests/
├── pyproject.toml
└── README.md
```

---

## Why SoloAI Agent Framework

SoloAI Agent Framework 专注于 **AI Agent framework**, **LLM agent orchestration**, **multi-agent systems**, **tool use**, **memory management**, 和 **production AI automation** 等核心能力。  
对于希望构建可观测、可维护、可扩展的 AI Agent 应用的开发团队，它提供了一套清晰、工程化且面向未来的技术基础设施。

---

## Contributing

We welcome contributions from the community.

### How to Contribute

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

### Development Setup

```bash
git clone https://github.com/soloai/soloai-agent-framework.git
cd soloai-agent-framework
pip install -e ".[dev]"
pre-commit install
pytest
```

### Contribution Guidelines

- Follow existing code style and project conventions
- Add tests for new features and bug fixes
- Update documentation when changing public APIs
- Use clear commit messages
- Keep pull requests focused and reviewable

---

## License

This project is licensed under the **MIT License**. See the [LICENSE](./LICENSE) file for details.

---

## Keywords

AI Agent 开发框架, AI Agent Framework, LLM Agent, Multi-Agent System, Tool Calling, Agent Memory, Workflow Orchestration, AI Automation, Open Source AI Framework, SoloAI