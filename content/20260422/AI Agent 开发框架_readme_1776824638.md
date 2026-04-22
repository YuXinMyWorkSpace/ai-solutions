# SoloAI Agent Framework

[![Build Status](https://img.shields.io/github/actions/workflow/status/SoloAI/soloai-agent/ci.yml?branch=main&style=flat-square)](https://github.com/SoloAI/soloai-agent/actions)
[![License](https://img.shields.io/github/license/SoloAI/soloai-agent?style=flat-square)](./LICENSE)

**SoloAI Agent Framework** 是一个面向生产环境的 **AI Agent 开发框架**，用于快速构建、编排、部署和扩展基于大语言模型（LLM）的智能体应用。  
它提供模块化 Agent 架构、工具调用、工作流编排、记忆管理与可观测性能力，帮助开发者高效打造可维护、可扩展的 AI Native 系统。

---

## Why SoloAI Agent Framework

SoloAI Agent Framework 专为现代 AI Agent 应用设计，支持从简单问答助手到多智能体协作系统的完整开发生命周期。  
无论你是在构建任务执行 Agent、企业知识助手、自动化工作流，还是面向 SaaS 的 AI 能力平台，本框架都能提供统一、工程化的基础设施支持。

---

## Features

- **模块化 Agent 架构**：支持自定义 Agent、Planner、Executor、Memory、Tool 等核心组件
- **多工具调用能力**：可无缝集成 API、数据库、搜索引擎、代码执行环境等外部工具
- **工作流与任务编排**：支持链式任务、条件分支、多步骤推理与多 Agent 协作
- **Memory 与上下文管理**：支持短期记忆、长期记忆、会话上下文压缩与检索增强
- **可观测性与调试**：内置日志、追踪、Agent 行为分析，便于调试与性能优化
- **生产级部署支持**：适用于 API 服务、异步任务系统、企业内部平台与云原生部署场景

---

## Installation

### Requirements

- Python 3.10+
- `pip` or `poetry`
- OpenAI / compatible LLM API key

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
pip install "soloai-agent[tools,vector,observability]"
```

### Environment variables

```bash
export OPENAI_API_KEY="your_api_key"
export SOLOAI_LOG_LEVEL="INFO"
```

---

## Quick Start

下面的示例展示了如何使用 SoloAI Agent Framework 创建一个最小可运行的 AI Agent。

```python
from soloai_agent import Agent
from soloai_agent.llms import OpenAIChatModel

model = OpenAIChatModel(
    model="gpt-4o-mini",
    temperature=0.2
)

agent = Agent(
    name="assistant",
    model=model,
    system_prompt="You are a helpful AI agent for technical tasks."
)

response = agent.run("Summarize the benefits of AI agent frameworks in 3 bullet points.")
print(response.output)
```

运行后，你将获得一个具备基础推理能力的智能体，可用于构建更复杂的任务执行流程。

---

## Usage Examples

### 1. Agent with Tools

为 Agent 注册工具，使其可以调用外部函数完成任务。

```python
from soloai_agent import Agent, tool
from soloai_agent.llms import OpenAIChatModel

@tool
def search_docs(query: str) -> str:
    """Search internal documentation."""
    return f"Results for: {query}"

agent = Agent(
    name="doc-assistant",
    model=OpenAIChatModel(model="gpt-4o-mini"),
    tools=[search_docs],
    system_prompt="You can use tools to answer documentation questions."
)

result = agent.run("Find information about deployment architecture.")
print(result.output)
```

---

### 2. Multi-step Workflow

使用工作流将复杂任务拆解为多个阶段执行。

```python
from soloai_agent import Agent, Workflow
from soloai_agent.llms import OpenAIChatModel

researcher = Agent(
    name="researcher",
    model=OpenAIChatModel(model="gpt-4o-mini"),
    system_prompt="Research the topic and collect key points."
)

writer = Agent(
    name="writer",
    model=OpenAIChatModel(model="gpt-4o-mini"),
    system_prompt="Write a concise technical summary based on the input."
)

workflow = Workflow(
    steps=[researcher, writer]
)

result = workflow.run("AI Agent frameworks for enterprise automation")
print(result.output)
```

---

### 3. Memory-enabled Agent

为 Agent 增加记忆能力，适用于持续对话与上下文追踪场景。

```python
from soloai_agent import Agent
from soloai_agent.llms import OpenAIChatModel
from soloai_agent.memory import ConversationMemory

memory = ConversationMemory(session_id="demo-user-001")

agent = Agent(
    name="memory-assistant",
    model=OpenAIChatModel(model="gpt-4o-mini"),
    memory=memory,
    system_prompt="Remember user preferences and maintain context."
)

agent.run("My preferred programming language is Python.")
response = agent.run("What programming language do I prefer?")
print(response.output)
```

---

### 4. API Service Integration

可将 Agent 快速集成为服务接口，用于 Web、SaaS 或内部平台。

```python
from fastapi import FastAPI
from pydantic import BaseModel
from soloai_agent import Agent
from soloai_agent.llms import OpenAIChatModel

app = FastAPI()

agent = Agent(
    name="api-agent",
    model=OpenAIChatModel(model="gpt-4o-mini"),
    system_prompt="Answer user requests accurately."
)

class ChatRequest(BaseModel):
    message: str

@app.post("/chat")
def chat(req: ChatRequest):
    result = agent.run(req.message)
    return {"output": result.output}
```

启动服务：

```bash
uvicorn app:app --reload
```

---

## Project Structure

```text
soloai-agent/
├── soloai_agent/
│   ├── agents/
│   ├── workflows/
│   ├── tools/
│   ├── memory/
│   ├── llms/
│   └── observability/
├── examples/
├── tests/
├── docs/
└── README.md
```

---

## Use Cases

SoloAI Agent Framework 适用于以下典型场景：

- **AI Assistant**：企业知识助手、客服机器人、研发助手
- **Task Automation**：自动生成报告、数据处理、工单流转
- **Multi-Agent Systems**：研究、规划、执行、审校等角色协作
- **RAG Applications**：结合向量数据库与知识检索的增强生成系统
- **Developer Tools**：代码助手、文档助手、CI/CD 智能自动化

---

## Contributing

我们欢迎社区贡献，共同完善 SoloAI Agent Framework。

### How to contribute

1. Fork 本仓库
2. 创建功能分支

```bash
git checkout -b feat/your-feature-name
```

3. 安装开发依赖

```bash
pip install -e ".[dev]"
```

4. 运行测试

```bash
pytest
```

5. 提交代码并发起 Pull Request

```bash
git add .
git commit -m "feat: add your feature"
git push origin feat/your-feature-name
```

### Contribution guidelines

- 遵循清晰的模块边界与工程规范
- 为新增功能补充测试用例
- 使用规范化提交信息，如 `feat:`, `fix:`, `docs:`
- 提交前确保格式化与静态检查通过

示例：

```bash
ruff check .
black .
pytest
```

如果你计划提交较大改动，建议先创建 Issue 讨论设计方案。

---

## License

本项目基于 **MIT License** 开源发布。详情请参阅 [LICENSE](./LICENSE)。

---

## Keywords

AI Agent Framework, LLM Agent Development, Multi-Agent Workflow, Tool Calling, Agent Memory, RAG Framework, AI Automation, Python AI Framework, Agent Orchestration, Production AI Agents

--- 

如果你愿意，我还可以继续为你补充：
- `README` 的 **中英双语版本**
- 更像真实开源项目的 **目录徽章、Stars/Forks 徽章**
- 配套生成 `CONTRIBUTING.md` / `LICENSE` / `docs/quickstart.md`