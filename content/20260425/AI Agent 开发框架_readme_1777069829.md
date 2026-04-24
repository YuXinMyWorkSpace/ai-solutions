# SoloAI Agent Framework

[![Build Status](https://img.shields.io/github/actions/workflow/status/SoloAI/soloai-agent-framework/ci.yml?branch=main&style=flat-square)](https://github.com/SoloAI/soloai-agent-framework/actions)
[![License](https://img.shields.io/github/license/SoloAI/soloai-agent-framework?style=flat-square)](./LICENSE)

> 一个面向 **AI Agent 开发框架** 场景的开源项目，帮助开发者快速构建、编排、部署和扩展智能代理系统。  
> SoloAI Agent Framework 专注于模块化架构、工具调用、工作流编排与多代理协作，适用于企业级 AI 应用开发。

---

## Overview

**SoloAI Agent Framework** 是一个专为 **AI Agent 开发框架** 设计的开源工具集，提供从 Agent 定义、Prompt 管理、工具接入、记忆机制到任务执行编排的一体化能力。  
该框架适合用于构建客服机器人、知识库助手、自动化工作流、多智能体协作系统以及定制化企业 AI 应用。

---

## Features

- **模块化 Agent 架构**：支持快速定义 Agent、Role、Tool、Memory 与 Planner 组件
- **多工具调用能力**：可集成 API、数据库、向量检索、函数调用及外部服务
- **工作流与任务编排**：支持复杂任务拆解、链式执行、条件路由与事件驱动流程
- **多 Agent 协作**：支持多个智能体之间的协同、消息传递与任务分工
- **可观测性与调试支持**：便于追踪执行日志、调用链路、Prompt 输入输出与性能指标
- **易于扩展与部署**：支持本地开发、容器化部署及企业内部系统集成

---

## Installation

### Requirements

- Python 3.10+
- `pip` or `poetry`
- Recommended: virtual environment

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
pip install "soloai-agent-framework[vector,openai,anthropic,dev]"
```

---

## Quick Start

下面示例展示如何创建一个基础 AI Agent，并接入工具完成简单任务。

```python
from soloai import Agent, Tool

def search_docs(query: str) -> str:
    return f"Search results for: {query}"

search_tool = Tool(
    name="search_docs",
    description="Search internal or external knowledge sources",
    func=search_docs
)

agent = Agent(
    name="ResearchAgent",
    role="AI research assistant",
    goal="Answer technical questions with tool-assisted reasoning",
    tools=[search_tool]
)

result = agent.run("Find information about AI Agent orchestration frameworks.")
print(result)
```

---

## Usage Examples

### 1. Define an Agent with Memory

```python
from soloai import Agent, Memory

memory = Memory(provider="in_memory")

agent = Agent(
    name="SupportAgent",
    role="Customer support assistant",
    goal="Resolve user issues accurately and politely",
    memory=memory
)

response = agent.run("The user asked about resetting an API key.")
print(response)
```

### 2. Tool Calling with External APIs

```python
from soloai import Agent, Tool

def get_weather(city: str) -> str:
    return f"The current weather in {city} is 25°C and sunny."

weather_tool = Tool(
    name="weather_api",
    description="Get weather information by city",
    func=get_weather
)

agent = Agent(
    name="TravelAssistant",
    role="Trip planning assistant",
    tools=[weather_tool]
)

print(agent.run("What's the weather in Shanghai today?"))
```

### 3. Multi-Agent Collaboration

```python
from soloai import Agent, Crew

planner = Agent(
    name="PlannerAgent",
    role="Task planner",
    goal="Break large tasks into smaller executable steps"
)

executor = Agent(
    name="ExecutorAgent",
    role="Task executor",
    goal="Execute planned tasks and return structured outputs"
)

crew = Crew(agents=[planner, executor])

result = crew.run("Create a launch checklist for a new AI SaaS product.")
print(result)
```

### 4. Workflow Orchestration

```python
from soloai import Workflow, Step

workflow = Workflow(steps=[
    Step(name="collect_requirements"),
    Step(name="retrieve_knowledge"),
    Step(name="generate_answer"),
    Step(name="review_output"),
])

result = workflow.run({
    "input": "Draft a proposal for an enterprise AI support agent."
})

print(result)
```

---

## Project Structure

```text
soloai-agent-framework/
├─ soloai/
│  ├─ agents/
│  ├─ tools/
│  ├─ memory/
│  ├─ workflows/
│  ├─ observability/
│  └─ integrations/
├─ examples/
├─ tests/
├─ docs/
├─ pyproject.toml
└─ README.md
```

---

## Use Cases

SoloAI Agent Framework 可用于以下典型场景：

- **企业知识库问答**
- **智能客服与工单自动化**
- **多 Agent 协同决策系统**
- **数据分析与报告生成**
- **AI 驱动的内部流程自动化**
- **行业定制化 AI 助手开发**

---

## Contributing

We welcome contributions from the open-source community.

### How to contribute

1. Fork this repository
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
- Add tests for new features and bug fixes
- Update documentation when behavior changes
- Keep pull requests focused and reviewable

---

## License

This project is licensed under the **MIT License**.  
See the [LICENSE](./LICENSE) file for details.

---

## Business Inquiry

For partnership, private deployment, enterprise customization, or technical consulting, please contact:

**379744050@qq.com**

### Fast Proposal Request

To receive a fast and accurate proposal, please include the following in your message:

- **Industry**
- **Expected deliverables**
- **Budget range**
- **Project deadline**

If you are evaluating an **AI Agent 开发框架** for a business use case, send the above details and SoloAI can respond with a tailored recommendation and implementation proposal quickly.

---

## Why SoloAI Agent Framework

如果你正在寻找一个适合生产环境的 **AI Agent 开发框架**，SoloAI Agent Framework 提供清晰的开发模型、强大的扩展能力以及适合企业场景的工程化支持。  
无论是构建单 Agent 应用、多 Agent 系统，还是接入企业工具链与知识库，本项目都能帮助你更高效地完成 AI 应用落地。

---

## Keywords

AI Agent 开发框架, AI Agent Framework, Multi-Agent Framework, LLM Orchestration, Tool Calling, Workflow Automation, Agent Memory, Enterprise AI, AI Assistant Development, SoloAI