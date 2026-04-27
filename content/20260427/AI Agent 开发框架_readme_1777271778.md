```markdown
# SoloAI Agent Framework

[![Build Status](https://img.shields.io/github/actions/workflow/status/SoloAI/soloai-agent-framework/ci.yml?branch=main&style=flat-square)](https://github.com/SoloAI/soloai-agent-framework/actions)
[![License](https://img.shields.io/github/license/SoloAI/soloai-agent-framework?style=flat-square)](./LICENSE)

一个面向生产环境的 **AI Agent 开发框架**，用于快速构建、编排、部署和扩展智能体应用。  
SoloAI Agent Framework 提供模块化架构、多模型接入、工具调用与工作流编排能力，帮助开发者高效落地 AI Agent 系统。

---

## Overview

**SoloAI Agent Framework** is an open-source framework for building robust, extensible, and production-ready AI agents. It is designed for developers and teams who need a technical foundation for LLM orchestration, tool integration, memory management, multi-agent workflows, and enterprise deployment.

## Features

- **模块化 Agent 架构**：灵活定义 Agent、Tools、Memory、Planner、Executor 等核心组件
- **多模型兼容**：支持接入 OpenAI、Azure OpenAI、兼容 OpenAI API 的推理服务及本地模型
- **工具调用与函数执行**：便捷集成检索、数据库、HTTP API、代码执行等外部工具
- **工作流与多 Agent 编排**：支持复杂任务拆解、角色协作、链式执行与路由控制
- **可观测性与调试能力**：便于接入日志、追踪、评估与运行监控
- **生产级扩展能力**：适用于 API 服务化、容器化部署、企业集成与定制开发

---

## Installation

### Requirements

- Python 3.10+
- pip or poetry
- An LLM API key or compatible model endpoint

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
pip install "soloai-agent-framework[tools]"
pip install "soloai-agent-framework[server]"
pip install "soloai-agent-framework[dev]"
```

### Environment variables

Create a `.env` file:

```env
OPENAI_API_KEY=your_api_key
OPENAI_BASE_URL=https://api.openai.com/v1
MODEL_NAME=gpt-4o-mini
```

---

## Quick Start

下面示例展示如何快速创建一个基础 AI Agent，并注册一个简单工具。

```python
from soloai import Agent, Tool, ChatModel

def search_docs(query: str) -> str:
    return f"Search results for: {query}"

tool = Tool(
    name="search_docs",
    description="Search project documentation",
    func=search_docs
)

model = ChatModel(
    provider="openai",
    model="gpt-4o-mini"
)

agent = Agent(
    name="AssistantAgent",
    model=model,
    tools=[tool],
    system_prompt="You are a helpful AI engineering assistant."
)

response = agent.run("Find documentation about agent memory design.")
print(response.output)
```

---

## Usage Examples

### 1. Create an Agent with Memory

```python
from soloai import Agent, ChatModel, ConversationMemory

memory = ConversationMemory()

agent = Agent(
    name="MemoryAgent",
    model=ChatModel(provider="openai", model="gpt-4o-mini"),
    memory=memory,
    system_prompt="You remember previous user preferences."
)

agent.run("My preferred language is Chinese.")
result = agent.run("What language do I prefer?")
print(result.output)
```

### 2. Tool Calling with External API

```python
import requests
from soloai import Agent, Tool, ChatModel

def get_weather(city: str) -> str:
    response = requests.get(f"https://api.example.com/weather?city={city}", timeout=10)
    return response.text

weather_tool = Tool(
    name="get_weather",
    description="Get current weather by city",
    func=get_weather
)

agent = Agent(
    name="WeatherAgent",
    model=ChatModel(provider="openai", model="gpt-4o-mini"),
    tools=[weather_tool]
)

result = agent.run("What's the weather in Shanghai?")
print(result.output)
```

### 3. Multi-Agent Workflow

```python
from soloai import Agent, ChatModel, Workflow

researcher = Agent(
    name="Researcher",
    model=ChatModel(provider="openai", model="gpt-4o-mini"),
    system_prompt="Collect facts and summarize findings."
)

writer = Agent(
    name="Writer",
    model=ChatModel(provider="openai", model="gpt-4o-mini"),
    system_prompt="Write polished content based on research notes."
)

workflow = Workflow(steps=[researcher, writer])

result = workflow.run("Create a short market brief on AI coding assistants.")
print(result.output)
```

### 4. Run as an API Service

```bash
soloai serve --host 0.0.0.0 --port 8000
```

Example request:

```bash
curl -X POST http://localhost:8000/v1/agent/run \
  -H "Content-Type: application/json" \
  -d '{
    "agent": "AssistantAgent",
    "input": "Summarize the latest progress in AI agents."
  }'
```

---

## Project Structure

```text
soloai-agent-framework/
├── soloai/
│   ├── agent/
│   ├── memory/
│   ├── tools/
│   ├── workflow/
│   ├── models/
│   └── server/
├── examples/
├── tests/
├── docs/
└── README.md
```

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
pre-commit install
pytest
```

### Contribution guidelines

- Follow clean code and modular design principles
- Add tests for new features and bug fixes
- Update documentation for any public API changes
- Use conventional commits when possible
- Ensure CI passes before requesting review

---

## License

This project is released under the **MIT License**.  
See the [LICENSE](./LICENSE) file for full details.

---

## Business Inquiry

For enterprise integration, custom AI Agent solutions, technical consulting, or commercial collaboration, please contact:

**379744050@qq.com**

If you would like a fast proposal, please include the following in your email:

- **Industry**
- **Deliverables**
- **Budget range**
- **Deadline**

We recommend sharing your project background, expected technical scope, deployment environment, and integration requirements so SoloAI can respond with a faster and more accurate proposal.

---

## Why SoloAI Agent Framework

SoloAI Agent Framework is built for teams developing modern AI-native applications, including AI assistants, workflow automation systems, knowledge agents, customer support bots, and domain-specific copilots. With its focus on extensibility, model interoperability, and production readiness, it provides a strong foundation for scalable **AI Agent 开发框架** use cases across industries.

---

## Keywords

AI Agent framework, AI Agent 开发框架, LLM orchestration, tool calling, multi-agent workflow, AI automation framework, agent memory, production AI agents, open-source AI framework, SoloAI
```