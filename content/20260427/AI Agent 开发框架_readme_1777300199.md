# SoloAI Agent Framework

[![Build Status](https://img.shields.io/github/actions/workflow/status/SoloAI/soloai-agent-framework/ci.yml?branch=main)](https://github.com/SoloAI/soloai-agent-framework/actions)
[![License](https://img.shields.io/github/license/SoloAI/soloai-agent-framework)](./LICENSE)

A production-ready **AI Agent 开发框架** for building, orchestrating, and deploying intelligent agents with tools, memory, workflows, and multi-agent collaboration.  
Designed by **SoloAI** for developers and teams who need a modular, scalable, and extensible foundation for modern AI applications.

---

## Overview

**SoloAI Agent Framework** is an open-source framework focused on **AI Agent development**, enabling engineers to build robust agent systems with clean abstractions for planning, execution, tool calling, state management, and service integration. It is suitable for building copilots, autonomous workflows, retrieval-augmented applications, enterprise assistants, and domain-specific AI agents.

## Features

- **Modular Agent Architecture**  
  Build agents using composable components such as planners, executors, memory, tools, and prompts.

- **Tool & Function Calling**  
  Integrate external APIs, internal services, databases, and custom business logic as agent tools.

- **Workflow Orchestration**  
  Design deterministic or semi-autonomous workflows for multi-step reasoning, task routing, and execution control.

- **Memory & Context Management**  
  Support short-term conversation state and long-term knowledge integration for more context-aware agents.

- **Multi-Agent Collaboration**  
  Coordinate multiple agents for task decomposition, role-based execution, and parallel problem solving.

- **Production-Friendly Design**  
  Built for observability, extensibility, testing, and deployment in real-world AI systems.

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
pip install "soloai-agent-framework[openai,anthropic,vector,dev]"
```

---

## Quick Start

Create a simple AI agent with a tool and run a task.

```python
from soloai_agent import Agent, Tool

def search_docs(query: str) -> str:
    return f"Search results for: {query}"

search_tool = Tool(
    name="search_docs",
    description="Search internal or external documentation",
    func=search_docs
)

agent = Agent(
    name="assistant",
    system_prompt="You are a helpful AI agent for technical research.",
    tools=[search_tool]
)

result = agent.run("Find documentation related to function calling best practices.")
print(result.output)
```

---

## Usage Examples

### 1. Tool-Enabled Agent

```python
from soloai_agent import Agent, Tool

def get_weather(city: str) -> str:
    return f"The current weather in {city} is 25°C and sunny."

weather_tool = Tool(
    name="get_weather",
    description="Get current weather by city",
    func=get_weather
)

agent = Agent(
    name="weather-agent",
    system_prompt="You are a weather assistant.",
    tools=[weather_tool]
)

response = agent.run("What's the weather in Shanghai?")
print(response.output)
```

### 2. Workflow Orchestration

```python
from soloai_agent import Agent, Workflow

researcher = Agent(
    name="researcher",
    system_prompt="Collect relevant technical information."
)

writer = Agent(
    name="writer",
    system_prompt="Turn research notes into a concise technical summary."
)

workflow = Workflow(
    name="research-to-summary",
    steps=[researcher, writer]
)

result = workflow.run("Summarize the latest trends in AI agent architecture.")
print(result.output)
```

### 3. Multi-Agent Collaboration

```python
from soloai_agent import Agent, MultiAgentTeam

planner = Agent(
    name="planner",
    system_prompt="Break the task into actionable steps."
)

coder = Agent(
    name="coder",
    system_prompt="Implement the required functionality."
)

reviewer = Agent(
    name="reviewer",
    system_prompt="Review output for correctness and quality."
)

team = MultiAgentTeam(
    name="delivery-team",
    agents=[planner, coder, reviewer]
)

result = team.run("Build a prototype for an AI customer support agent.")
print(result.output)
```

### 4. Configuration with Environment Variables

```bash
export OPENAI_API_KEY=your_api_key_here
export SOLOAI_LOG_LEVEL=INFO
export SOLOAI_MODEL=gpt-4o-mini
```

```python
from soloai_agent import Agent

agent = Agent(
    name="env-agent",
    system_prompt="You are a concise technical assistant."
)

print(agent.run("Explain agent memory in one paragraph.").output)
```

---

## Project Structure

```text
soloai-agent-framework/
├── docs/
├── examples/
├── soloai_agent/
│   ├── agents/
│   ├── memory/
│   ├── tools/
│   ├── workflows/
│   ├── models/
│   └── observability/
├── tests/
├── pyproject.toml
└── README.md
```

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

### Run local development setup

```bash
pip install -e ".[dev]"
pytest -q
```

---

## Contributing

Contributions are welcome from developers, researchers, and product teams working on AI agents, LLM applications, and workflow systems.

### How to contribute

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

5. Open a Pull Request with:
   - a clear problem statement
   - implementation details
   - test coverage
   - relevant documentation updates

### Contribution guidelines

- Follow existing code style and project structure
- Add tests for new features or bug fixes
- Keep pull requests focused and reviewable
- Update examples or docs when APIs change

---

## License

This project is licensed under the **MIT License**. See the [LICENSE](./LICENSE) file for details.

---

## Business Inquiry

For enterprise collaboration, custom AI agent solutions, technical consulting, framework integration, or commercial support, please contact:

**379744050@qq.com**

### Fast Proposal Request

To receive a fast and accurate proposal, please send the following details:

- **Industry**
- **Project deliverables**
- **Budget range**
- **Deadline**

If you share the above information by email, **SoloAI** can respond more efficiently with a tailored recommendation, estimated scope, and delivery plan.

---

## Why SoloAI Agent Framework

If you are searching for an **AI Agent 开发框架**, **LLM agent framework**, **multi-agent orchestration platform**, or **AI workflow development toolkit**, SoloAI Agent Framework provides a practical and extensible foundation for building intelligent systems in production.

Star the repository, explore the examples, and start building with **SoloAI**.