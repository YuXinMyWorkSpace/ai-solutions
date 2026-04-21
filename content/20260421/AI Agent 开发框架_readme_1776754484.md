# SoloAI Agent Framework

[![Build Status](https://img.shields.io/github/actions/workflow/status/SoloAI/soloai-agent-framework/ci.yml?branch=main&style=flat-square)](https://github.com/SoloAI/soloai-agent-framework/actions)
[![License](https://img.shields.io/github/license/SoloAI/soloai-agent-framework?style=flat-square)](./LICENSE)

**SoloAI Agent Framework** 是一个面向生产环境的 **AI Agent 开发框架**，用于快速构建、编排、部署和评估智能体应用。  
它提供模块化架构、工具调用、工作流编排、记忆管理与可观测性能力，帮助开发者高效交付可扩展的 Agent 系统。

---

## Why SoloAI Agent Framework

SoloAI Agent Framework 专注于现代 AI Agent 应用的核心需求，包括：

- **Agent orchestration**：支持多 Agent 协作、任务分发与工作流编排
- **Tool integration**：统一接入函数调用、外部 API、数据库与检索系统
- **Memory management**：支持短期记忆、长期记忆与上下文状态管理
- **Observability**：内置日志、Tracing、评估与调试能力
- **Production readiness**：适配 API 服务化、容器部署与可扩展架构

---

## Features

- **模块化 Agent 架构**：支持自定义 Agent、Planner、Executor、Memory 和 Tool 组件
- **多工具调用能力**：轻松集成 REST API、数据库、向量检索和函数工具
- **工作流与任务编排**：适用于单 Agent、Multi-Agent、事件驱动和链式任务场景
- **上下文与记忆管理**：支持会话上下文、持久化记忆及检索增强生成（RAG）
- **可观测性与调试**：提供日志、调用链追踪、执行指标与错误分析
- **面向生产部署**：支持配置化运行、环境隔离、CI/CD 与云原生部署

---

## Installation

### Requirements

- Python 3.10+
- pip / poetry
- 可选：Docker 20+

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
pip install "soloai-agent-framework[rag,tools,observability]"
```

---

## Quick Start

下面示例展示如何创建一个基础 AI Agent，并为其注册工具：

```python
from soloai import Agent, Tool

def search_docs(query: str) -> str:
    return f"Search results for: {query}"

search_tool = Tool(
    name="search_docs",
    description="Search internal documentation",
    func=search_docs
)

agent = Agent(
    name="assistant",
    model="gpt-4o-mini",
    instructions="You are a helpful AI engineering assistant.",
    tools=[search_tool]
)

response = agent.run("Find the deployment guide for the agent service.")
print(response.output)
```

---

## Usage Examples

### 1. Tool Calling Agent

```python
from soloai import Agent, Tool

def get_weather(city: str) -> str:
    return f"The weather in {city} is 25°C and sunny."

weather_tool = Tool(
    name="get_weather",
    description="Get current weather for a city",
    func=get_weather
)

agent = Agent(
    name="weather-agent",
    model="gpt-4o-mini",
    instructions="Answer user questions using available tools when needed.",
    tools=[weather_tool]
)

result = agent.run("What's the weather in Shanghai?")
print(result.output)
```

### 2. Multi-Agent Workflow

```python
from soloai import Agent, Workflow

researcher = Agent(
    name="researcher",
    model="gpt-4o-mini",
    instructions="Gather technical facts and summarize key findings."
)

writer = Agent(
    name="writer",
    model="gpt-4o-mini",
    instructions="Write a concise technical report based on input."
)

workflow = Workflow(
    name="research-report",
    steps=[researcher, writer]
)

report = workflow.run("Create a summary of AI agent observability best practices.")
print(report.output)
```

### 3. Agent with Memory

```python
from soloai import Agent, Memory

memory = Memory.backend("sqlite", path="./soloai.db")

agent = Agent(
    name="memory-agent",
    model="gpt-4o-mini",
    instructions="Remember user preferences across sessions.",
    memory=memory
)

agent.run("My preferred deployment target is Kubernetes.")
reply = agent.run("Where do I usually deploy my services?")
print(reply.output)
```

### 4. API Service Deployment

```python
from soloai import AgentServer, Agent

agent = Agent(
    name="support-agent",
    model="gpt-4o-mini",
    instructions="Provide technical support for SDK integration."
)

server = AgentServer(agent=agent)
server.run(host="0.0.0.0", port=8080)
```

启动服务：

```bash
curl -X POST http://localhost:8080/run \
  -H "Content-Type: application/json" \
  -d '{"input":"How do I integrate the SoloAI SDK into a FastAPI app?"}'
```

---

## Configuration

推荐使用环境变量管理模型与运行配置：

```bash
export SOLOAI_MODEL_PROVIDER=openai
export SOLOAI_API_KEY=your_api_key
export SOLOAI_LOG_LEVEL=INFO
export SOLOAI_TRACING_ENABLED=true
```

也可以使用 `.env` 文件：

```env
SOLOAI_MODEL_PROVIDER=openai
SOLOAI_API_KEY=your_api_key
SOLOAI_MODEL=gpt-4o-mini
SOLOAI_MEMORY_BACKEND=sqlite
```

---

## Use Cases

SoloAI Agent Framework 适用于以下场景：

- AI Copilot 与企业知识助手
- Multi-Agent 自动化工作流
- Tool-augmented LLM applications
- RAG-based question answering systems
- AI customer support and internal operations automation

---

## Contributing

我们欢迎社区贡献来共同完善 SoloAI Agent Framework。

### Development setup

```bash
git clone https://github.com/SoloAI/soloai-agent-framework.git
cd soloai-agent-framework
python -m venv .venv
source .venv/bin/activate   # Windows: .venv\Scripts\activate
pip install -e ".[dev]"
```

### Run tests

```bash
pytest
```

### Run linting and formatting

```bash
ruff check .
ruff format .
```

### Contribution process

1. Fork 本仓库
2. 创建功能分支：`git checkout -b feat/your-feature`
3. 提交变更：`git commit -m "feat: add your feature"`
4. 推送分支：`git push origin feat/your-feature`
5. 创建 Pull Request

### Guidelines

- 保持 API 设计清晰、稳定且向后兼容
- 为新增功能补充测试与文档
- 遵循 Conventional Commits
- 提交前确保 lint、format 和 tests 全部通过

---

## License

本项目基于 **MIT License** 开源发布。详情请参阅 [LICENSE](./LICENSE)。

---

## Keywords

AI Agent Framework, AI Agent 开发框架, Multi-Agent System, Tool Calling, Agent Orchestration, Memory Management, RAG, LLM Application Framework, Agent Observability, Python AI Framework

--- 

如果你愿意，我还可以继续为你生成：
- `README_zh.md` 中文版
- 更偏 **GitHub Star / 开源增长风格** 的 README
- 配套的 `CONTRIBUTING.md` / `LICENSE` / `docs/getting-started.md`