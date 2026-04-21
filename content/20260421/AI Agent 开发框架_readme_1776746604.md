```markdown
# SoloAI Agent Framework

[![Build Status](https://img.shields.io/github/actions/workflow/status/SoloAI/soloai-agent-framework/ci.yml?branch=main)](https://github.com/SoloAI/soloai-agent-framework/actions)
[![License](https://img.shields.io/github/license/SoloAI/soloai-agent-framework)](./LICENSE)

**SoloAI Agent Framework** 是一个面向 **AI Agent 开发框架** 场景的开源基础设施，帮助开发者快速构建、编排、测试与部署可扩展的智能体系统。  
它提供模块化 Agent 架构、工具调用、记忆管理、工作流编排与多模型接入能力，适用于企业级 AI 应用与自动化场景。

---

## Why SoloAI Agent Framework

现代 AI Agent 开发不仅需要调用大语言模型，还需要具备**任务拆解、工具执行、上下文记忆、流程编排、可观测性与生产部署能力**。  
SoloAI Agent Framework 专注于为开发者提供一个简洁、稳定、可扩展的框架，用于构建：

- Autonomous AI Agents
- Multi-Agent Systems
- Tool-Using LLM Applications
- RAG + Agent Workflows
- Enterprise AI Automation Pipelines

---

## Features

- **模块化 Agent 架构**：支持自定义 Agent、Planner、Executor、Memory、Tools 等核心组件
- **多模型接入**：兼容 OpenAI、Azure OpenAI、Anthropic 及本地/私有化模型
- **工具调用与函数执行**：轻松集成搜索、数据库、API、文件系统等外部工具
- **工作流与多智能体编排**：支持复杂任务流、角色协作和任务路由
- **记忆与上下文管理**：提供短期记忆、长期记忆与向量检索能力
- **可观测性与生产就绪**：内置日志、Tracing、配置管理与可测试开发模式

---

## Installation

### Requirements

- Python 3.10+
- `pip` or `poetry`

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
pip install "soloai-agent-framework[openai]"
pip install "soloai-agent-framework[anthropic]"
pip install "soloai-agent-framework[vector]"
```

### Environment variables

创建 `.env` 文件：

```bash
OPENAI_API_KEY=your_openai_api_key
ANTHROPIC_API_KEY=your_anthropic_api_key
SOLOAI_LOG_LEVEL=INFO
```

---

## Quick Start

下面的示例展示如何使用 SoloAI Agent Framework 创建一个具备工具调用能力的基础 AI Agent。

```python
from soloai import Agent, Tool
from soloai.models import OpenAIChatModel

def get_weather(city: str) -> str:
    return f"{city} 当前天气晴朗，温度 26°C。"

weather_tool = Tool(
    name="weather",
    description="Get current weather by city name",
    func=get_weather
)

agent = Agent(
    name="assistant",
    model=OpenAIChatModel(model="gpt-4o-mini"),
    tools=[weather_tool],
    system_prompt="You are a helpful AI agent that can use tools when necessary."
)

response = agent.run("请帮我查询北京天气，并给出出行建议。")
print(response.output)
```

---

## Usage Examples

### 1. Basic Agent

```python
from soloai import Agent
from soloai.models import OpenAIChatModel

agent = Agent(
    name="qa-agent",
    model=OpenAIChatModel(model="gpt-4o-mini"),
    system_prompt="Answer questions clearly and concisely."
)

result = agent.run("什么是 AI Agent？")
print(result.output)
```

### 2. Agent with Memory

```python
from soloai import Agent
from soloai.memory import ConversationMemory
from soloai.models import OpenAIChatModel

memory = ConversationMemory()

agent = Agent(
    name="memory-agent",
    model=OpenAIChatModel(model="gpt-4o-mini"),
    memory=memory,
    system_prompt="Remember important facts from the conversation."
)

agent.run("我的名字是 Alex。")
result = agent.run("你还记得我的名字吗？")
print(result.output)
```

### 3. Multi-Agent Workflow

```python
from soloai import Agent, Workflow
from soloai.models import OpenAIChatModel

researcher = Agent(
    name="researcher",
    model=OpenAIChatModel(model="gpt-4o-mini"),
    system_prompt="Research the topic and summarize key facts."
)

writer = Agent(
    name="writer",
    model=OpenAIChatModel(model="gpt-4o-mini"),
    system_prompt="Write a polished article based on the research summary."
)

workflow = Workflow(
    name="content-pipeline",
    steps=[researcher, writer]
)

result = workflow.run("撰写一篇关于 AI Agent 开发框架趋势的短文。")
print(result.output)
```

### 4. Tool Calling with External API

```python
import requests
from soloai import Agent, Tool
from soloai.models import OpenAIChatModel

def search_docs(query: str) -> str:
    response = requests.get(
        "https://api.example.com/search",
        params={"q": query},
        timeout=10
    )
    return response.text

search_tool = Tool(
    name="docs_search",
    description="Search internal technical documentation",
    func=search_docs
)

agent = Agent(
    name="support-agent",
    model=OpenAIChatModel(model="gpt-4o-mini"),
    tools=[search_tool],
    system_prompt="Use the docs_search tool when the user asks product questions."
)

result = agent.run("如何配置 Agent 的 memory 模块？")
print(result.output)
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
│   └── tracing/
├── tests/
├── pyproject.toml
└── README.md
```

---

## Common Use Cases

SoloAI Agent Framework 适用于以下 AI 应用开发场景：

- 企业知识库问答与检索增强生成（RAG）
- 智能客服与自动化支持系统
- 具备工具调用能力的任务执行 Agent
- 多角色协作的 Multi-Agent 系统
- AI 工作流自动化与业务流程编排
- 面向生产环境的 AI Agent 平台开发

---

## Development

### Run tests

```bash
pytest
```

### Lint and format

```bash
ruff check .
ruff format .
```

### Start local development

```bash
pip install -e ".[dev]"
pytest -q
```

---

## Contributing

欢迎社区贡献代码、文档和建议。为了确保协作高效，请在提交前遵循以下规范：

1. Fork 本仓库并创建功能分支：
   ```bash
   git checkout -b feat/your-feature-name
   ```
2. 提交清晰、原子化的 commit
3. 为新功能补充测试用例与必要文档
4. 确保本地通过 lint、format 和 test
5. 提交 Pull Request，并在描述中说明变更背景、设计思路与验证方式

### Commit Convention

建议使用 Conventional Commits：

```text
feat: add multi-agent routing support
fix: resolve memory serialization bug
docs: improve quick start examples
```

### Reporting Issues

提交 Issue 时请尽量包含：

- 运行环境
- 安装方式
- 复现步骤
- 预期行为
- 实际行为
- 错误日志或截图

---

## Roadmap

- [ ] 支持更多 LLM Provider
- [ ] 图形化 Agent Workflow 编排
- [ ] 分布式任务调度
- [ ] 更完善的 Observability 与 Tracing
- [ ] 企业级权限与安全控制

---

## License

本项目基于 **MIT License** 开源发布。详情请参阅 [LICENSE](./LICENSE)。

---

## Keywords

AI Agent Framework, AI Agent 开发框架, LLM Agent, Multi-Agent System, Tool Calling, Agent Workflow, RAG, Autonomous Agent, Python AI Framework, AI Automation

```