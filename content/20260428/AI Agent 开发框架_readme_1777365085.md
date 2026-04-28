```markdown
# SoloAI Agent Framework

[![Build Status](https://img.shields.io/github/actions/workflow/status/SoloAI/agent-framework/ci.yml?branch=main)](https://github.com/SoloAI/agent-framework/actions)
[![License](https://img.shields.io/github/license/SoloAI/agent-framework)](./LICENSE)

A modern **AI Agent 开发框架** designed to help developers build, orchestrate, and deploy intelligent agents with modular workflows, tool integration, memory, and production-ready observability.  
Built for teams and open-source contributors who need a scalable foundation for **LLM agents, autonomous workflows, and enterprise AI applications**.

---

## Features

- **Modular Agent Architecture** — Compose agents with reusable planners, tools, memory, and execution pipelines.
- **Multi-Tool Integration** — Connect APIs, databases, search systems, vector stores, and custom function tools.
- **Memory & Context Management** — Support short-term and long-term memory for more capable conversational and task-driven agents.
- **Workflow Orchestration** — Build deterministic or dynamic multi-step agent workflows for automation and decision-making.
- **Observability & Debugging** — Inspect execution traces, prompts, tool calls, and outputs for faster iteration in development and production.
- **Production-Oriented Design** — Designed for local development, server deployment, and integration into real-world AI products.

---

## Installation

### Requirements

- Python 3.10+
- `pip` or `poetry`

### Install with `pip`

```bash
git clone https://github.com/SoloAI/agent-framework.git
cd agent-framework
pip install -r requirements.txt
pip install -e .
```

### Install with `poetry`

```bash
git clone https://github.com/SoloAI/agent-framework.git
cd agent-framework
poetry install
```

### Environment Setup

Create a `.env` file in the project root:

```bash
OPENAI_API_KEY=your_api_key_here
MODEL_NAME=gpt-4o-mini
LOG_LEVEL=INFO
```

---

## Quick Start

The example below shows how to create a simple AI agent with a tool and run a task.

```python
from soloai.agent import Agent
from soloai.tools import tool

@tool
def get_weather(city: str) -> str:
    return f"The weather in {city} is sunny, 26°C."

agent = Agent(
    name="assistant-agent",
    model="gpt-4o-mini",
    instructions="You are a helpful AI assistant that uses tools when needed.",
    tools=[get_weather],
)

response = agent.run("What's the weather in Shanghai today?")
print(response.output)
```

Example output:

```text
The weather in Shanghai is sunny, 26°C.
```

---

## Usage Examples

### 1. Agent with Memory

```python
from soloai.agent import Agent
from soloai.memory import InMemoryStore

memory = InMemoryStore()

agent = Agent(
    name="memory-agent",
    model="gpt-4o-mini",
    instructions="Remember important user preferences.",
    memory=memory,
)

agent.run("My preferred language is Chinese.")
response = agent.run("What language do I prefer?")
print(response.output)
```

### 2. Multi-Step Workflow

```python
from soloai.agent import Agent
from soloai.workflow import Workflow, Step

research_agent = Agent(
    name="researcher",
    model="gpt-4o-mini",
    instructions="Collect relevant information and summarize key facts."
)

writer_agent = Agent(
    name="writer",
    model="gpt-4o-mini",
    instructions="Turn research into a concise technical brief."
)

workflow = Workflow(
    steps=[
        Step(name="research", agent=research_agent),
        Step(name="write", agent=writer_agent),
    ]
)

result = workflow.run("Create a short brief on AI agent observability.")
print(result.output)
```

### 3. Tool-Calling with External APIs

```python
import requests
from soloai.agent import Agent
from soloai.tools import tool

@tool
def search_docs(query: str) -> str:
    resp = requests.get(
        "https://api.example.com/search",
        params={"q": query},
        timeout=10
    )
    return resp.text

agent = Agent(
    name="docs-agent",
    model="gpt-4o-mini",
    instructions="Use the search_docs tool to retrieve documentation when needed.",
    tools=[search_docs],
)

response = agent.run("Find authentication setup instructions.")
print(response.output)
```

### 4. CLI Usage

```bash
python -m soloai run --agent assistant-agent --input "Generate a deployment checklist for an AI agent service"
```

---

## Project Structure

```text
agent-framework/
├── soloai/
│   ├── agent/
│   ├── tools/
│   ├── memory/
│   ├── workflow/
│   ├── observability/
│   └── cli/
├── examples/
├── tests/
├── docs/
├── requirements.txt
├── pyproject.toml
└── README.md
```

---

## Why SoloAI Agent Framework

**SoloAI Agent Framework** is built for developers looking for an extensible **AI Agent 开发框架** that supports:

- AI agent development
- LLM application engineering
- agent workflow orchestration
- tool-augmented reasoning
- memory-driven assistants
- production AI automation

Whether you are building internal copilots, customer support agents, research assistants, or enterprise workflow automation, this framework provides a clean foundation for rapid iteration and scalable deployment.

---

## Contributing

We welcome contributions from the open-source community.

### How to Contribute

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

### Contribution Guidelines

- Follow the existing code style and project structure
- Add tests for new features and bug fixes
- Update documentation for public-facing changes
- Keep pull requests focused and easy to review

For major changes, please open an issue first to discuss your proposal.

---

## License

This project is licensed under the **MIT License**. See the [LICENSE](./LICENSE) file for details.

---

## Business Inquiry

For partnerships, custom development, enterprise deployment, private integration, or consulting related to **AI Agent 开发框架**, please contact:

**379744050@qq.com**

### Fast Proposal Request

To receive a fast and accurate proposal, please send the following details by email:

- **Industry**
- **Deliverables**
- **Budget range**
- **Deadline**

We will review your requirements and respond with a tailored recommendation, technical approach, and estimated implementation plan.

---

## Support

If this project helps you, please consider:

- Starring the repository
- Opening issues for bugs or feature requests
- Contributing code, documentation, or examples

Together, we can build a stronger open-source ecosystem for AI agent development.
```