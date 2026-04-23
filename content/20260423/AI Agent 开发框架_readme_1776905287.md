# SoloAI Agent Framework

[![Build Status](https://img.shields.io/github/actions/workflow/status/SoloAI/soloai-agent-framework/ci.yml?branch=main&style=flat-square)](https://github.com/SoloAI/soloai-agent-framework/actions)
[![License](https://img.shields.io/github/license/SoloAI/soloai-agent-framework?style=flat-square)](./LICENSE)

**SoloAI Agent Framework** 是一个面向生产环境的 **AI Agent 开发框架**，用于快速构建、编排、部署和扩展基于大语言模型（LLM）的智能代理系统。  
它提供模块化架构、工具调用、工作流编排、记忆管理与多 Agent 协作能力，帮助开发者高效落地企业级 AI 应用。

---

## Why SoloAI Agent Framework

SoloAI Agent Framework 专注于 **AI Agent engineering**, **LLM application orchestration**, **tool calling**, **memory management**, 和 **multi-agent workflow design**。  
无论你是在构建客服机器人、企业 Copilot、自动化任务执行器，还是复杂的多步骤推理系统，该框架都能提供清晰、可扩展、可观测的开发体验。

---

## Features

- **模块化 Agent 架构**  
  支持自定义 Agent、Prompt、Tools、Memory、Planner 和 Executor，便于快速组合复杂能力。

- **工具调用与函数执行**  
  内置 Tool 接口，支持 API、数据库、文件系统、搜索引擎及自定义函数集成。

- **多 Agent 协作编排**  
  轻松构建 Supervisor、Planner、Worker 等多 Agent 协作模式，满足复杂任务拆解需求。

- **工作流与状态管理**  
  支持任务流转、上下文共享、持久化状态和长流程执行，适合生产级 Agent 系统。

- **可观测性与调试能力**  
  提供日志、执行追踪、事件流和中间结果输出，帮助定位 Agent 推理和工具调用问题。

- **面向生产部署**  
  支持本地开发、容器化部署、CI/CD 集成与可扩展服务化架构。

---

## Installation

### Requirements

- Python 3.10+
- `pip` or `poetry`
- OpenAI-compatible or other supported LLM provider API key

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
pip install "soloai-agent-framework[tools,vector,server]"
```

### Environment setup

Create a `.env` file:

```env
OPENAI_API_KEY=your_api_key
SOLOAI_MODEL=gpt-4o-mini
SOLOAI_LOG_LEVEL=INFO
```

---

## Quick Start

以下示例展示了如何使用 SoloAI Agent Framework 创建一个具备工具调用能力的基础 AI Agent。

```python
from soloai import Agent, Tool
from soloai.models import ChatModel

def get_weather(city: str) -> str:
    return f"{city} 当前天气晴，温度 26°C"

weather_tool = Tool(
    name="get_weather",
    description="根据城市名称查询天气信息",
    func=get_weather
)

model = ChatModel(
    provider="openai",
    model="gpt-4o-mini",
    temperature=0.2
)

agent = Agent(
    name="assistant",
    model=model,
    tools=[weather_tool],
    system_prompt="你是一个专业且简洁的 AI 助手。"
)

response = agent.run("请帮我查询上海天气，并给出穿衣建议。")
print(response.output)
```

---

## Usage

### 1. Basic Agent

适用于问答、文本生成、结构化输出等基础场景。

```python
from soloai import Agent
from soloai.models import ChatModel

agent = Agent(
    name="qa-agent",
    model=ChatModel(provider="openai", model="gpt-4o-mini"),
    system_prompt="你是企业知识库助手，请基于事实回答问题。"
)

result = agent.run("请总结 AI Agent 开发框架的核心组成部分。")
print(result.output)
```

---

### 2. Agent with Memory

通过记忆模块实现多轮上下文保持与会话管理。

```python
from soloai import Agent
from soloai.memory import ConversationMemory
from soloai.models import ChatModel

memory = ConversationMemory(session_id="demo-session")

agent = Agent(
    name="memory-agent",
    model=ChatModel(provider="openai", model="gpt-4o-mini"),
    memory=memory,
    system_prompt="你是一个能够记住上下文的智能助手。"
)

agent.run("我叫 Alex，我在构建一个金融风控 Agent。")
result = agent.run("请记住我的项目方向，并给我一些下一步建议。")

print(result.output)
```

---

### 3. Multi-Agent Workflow

构建任务拆解与执行型多 Agent 工作流。

```python
from soloai import Agent, Workflow
from soloai.models import ChatModel

planner = Agent(
    name="planner",
    model=ChatModel(provider="openai", model="gpt-4o-mini"),
    system_prompt="你负责拆解任务并制定执行计划。"
)

executor = Agent(
    name="executor",
    model=ChatModel(provider="openai", model="gpt-4o-mini"),
    system_prompt="你负责根据计划执行具体步骤。"
)

workflow = Workflow(
    name="research-workflow",
    agents=[planner, executor]
)

result = workflow.run("调研 AI Agent 开发框架在企业知识管理中的落地方案。")
print(result.output)
```

---

### 4. Custom Tool Integration

将内部系统或第三方服务接入 Agent 工具链。

```python
from soloai import Tool

def query_crm(customer_id: str) -> dict:
    return {
        "customer_id": customer_id,
        "name": "Acme Corp",
        "plan": "Enterprise",
        "status": "active"
    }

crm_tool = Tool(
    name="query_crm",
    description="查询 CRM 客户信息",
    func=query_crm
)
```

---

## Project Structure

```text
soloai-agent-framework/
├── soloai/
│   ├── agents/
│   ├── models/
│   ├── memory/
│   ├── tools/
│   ├── workflows/
│   ├── observability/
│   └── server/
├── examples/
├── tests/
├── docs/
├── pyproject.toml
└── README.md
```

---

## Use Cases

SoloAI Agent Framework 可广泛用于以下场景：

- **企业知识库问答与 Copilot**
- **客户支持自动化**
- **任务执行型智能体**
- **研究型 Agent 与信息检索**
- **多步骤业务流程自动化**
- **Agent 平台与 AI 原生应用开发**

---

## Contributing

欢迎社区贡献代码、文档、示例和最佳实践。

### How to contribute

1. Fork this repository
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

```bash
git commit -m "feat: add new tool execution hook"
```

6. Push your branch and open a Pull Request

### Contribution guidelines

- 保持代码风格一致，并通过 lint / test
- 为新增功能补充测试与文档
- 优先提交小而清晰的 PR
- 对重大改动请先创建 Issue 讨论设计方案

---

## Roadmap

- [ ] 支持更多 LLM providers
- [ ] 增强 Agent tracing 与 observability
- [ ] 图形化工作流编排能力
- [ ] 向量检索与长期记忆增强
- [ ] 分布式多 Agent 执行支持

---

## License

This project is licensed under the **MIT License**.  
See the [LICENSE](./LICENSE) file for details.

---

## Keywords

AI Agent 开发框架, AI Agent Framework, LLM Orchestration, Multi-Agent System, Tool Calling, Agent Workflow, Memory Management, AI Automation, Open Source AI Infrastructure