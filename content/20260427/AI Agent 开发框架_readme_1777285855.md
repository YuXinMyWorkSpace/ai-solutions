# SoloAI Agent Framework

[![Build Status](https://img.shields.io/github/actions/workflow/status/soloai/soloai-agent-framework/ci.yml?branch=main&style=flat-square)](https://github.com/soloai/soloai-agent-framework/actions)
[![License](https://img.shields.io/github/license/soloai/soloai-agent-framework?style=flat-square)](./LICENSE)

A production-oriented **AI Agent 开发框架** by **SoloAI** for building, orchestrating, and deploying LLM-powered agents with tools, memory, workflows, and observability.  
Designed for developers and teams who need a modular, extensible, and enterprise-ready foundation for agentic AI applications.

---

## Overview

SoloAI Agent Framework is an open-source framework for developing intelligent AI agents that can reason, call tools, manage context, and execute multi-step tasks. It helps teams rapidly build agent systems for customer support, internal copilots, automation pipelines, RAG applications, and domain-specific AI assistants.

## Features

- **Modular Agent Architecture**  
  Build reusable agents with pluggable models, prompts, tools, memory, and execution policies.

- **Tool Calling and Workflow Orchestration**  
  Connect agents to APIs, databases, search systems, and business services for real-world task execution.

- **Memory and Context Management**  
  Support for short-term session memory and long-term knowledge integration for more reliable multi-turn interactions.

- **RAG and Knowledge Base Integration**  
  Combine vector search, document retrieval, and grounded generation for accurate domain-aware responses.

- **Observability and Debugging**  
  Trace agent reasoning steps, tool invocations, latency, and failures to improve reliability in production.

- **Flexible Deployment**  
  Run locally for development or deploy to cloud and container environments for scalable AI workloads.

---

## Installation

### Requirements

- Python 3.10+
- `pip` or `poetry`
- Access to an LLM provider API key

### Install with pip

```bash
pip install soloai-agent-framework
```

### Install from source

```bash
git clone https://github.com/soloai/soloai-agent-framework.git
cd soloai-agent-framework
pip install -e .
```

### Environment setup

Create a `.env` file in the project root:

```env
OPENAI_API_KEY=your_api_key_here
MODEL_NAME=gpt-4o-mini
```

---

## Quick Start

```python
from soloai import Agent, Tool

def get_weather(city: str) -> str:
    return f"The weather in {city} is sunny, 26°C."

weather_tool = Tool(
    name="weather",
    description="Get current weather for a city",
    func=get_weather
)

agent = Agent(
    name="assistant",
    model="gpt-4o-mini",
    tools=[weather_tool],
    system_prompt="You are a helpful AI assistant."
)

response = agent.run("What's the weather in Shanghai today?")
print(response.output)
```

Expected output:

```text
The weather in Shanghai is sunny, 26°C.
```

---

## Usage Examples

### 1. Create an AI agent with custom tools

```python
from soloai import Agent, Tool

def search_docs(query: str) -> str:
    return f"Top results for: {query}"

def create_ticket(title: str) -> str:
    return f"Ticket created: {title}"

agent = Agent(
    name="support-agent",
    model="gpt-4o-mini",
    tools=[
        Tool(name="search_docs", description="Search internal documentation", func=search_docs),
        Tool(name="create_ticket", description="Create support ticket", func=create_ticket),
    ],
    system_prompt="You are an enterprise IT support agent."
)

result = agent.run("Search VPN setup guide and create a ticket if missing.")
print(result.output)
```

### 2. Add memory for multi-turn conversations

```python
from soloai import Agent, Memory

memory = Memory.session()

agent = Agent(
    name="sales-assistant",
    model="gpt-4o-mini",
    memory=memory,
    system_prompt="You are a concise B2B sales assistant."
)

agent.run("Our company sells AI automation solutions.")
reply = agent.run("What does our company sell?")
print(reply.output)
```

### 3. RAG-based knowledge assistant

```python
from soloai import Agent, KnowledgeBase, Retriever

kb = KnowledgeBase.from_documents("./docs")
retriever = Retriever(vector_store="faiss", top_k=5)

agent = Agent(
    name="knowledge-agent",
    model="gpt-4o-mini",
    retriever=retriever,
    knowledge_base=kb,
    system_prompt="Answer only based on retrieved company knowledge."
)

response = agent.run("Summarize the deployment policy.")
print(response.output)
```

### 4. Run an agent workflow

```python
from soloai import AgentWorkflow

workflow = AgentWorkflow([
    "analyze_request",
    "retrieve_context",
    "call_tools",
    "generate_response"
])

result = workflow.run("Prepare an onboarding checklist for a new DevOps engineer.")
print(result)
```

---

## Common Use Cases

- **Enterprise AI Copilot**
- **Customer Support Automation**
- **Internal Knowledge Assistant**
- **Document Q&A and RAG Systems**
- **Workflow Automation Agents**
- **Multi-agent Task Execution**

---

## Project Structure

```text
soloai-agent-framework/
├── soloai/
│   ├── agents/
│   ├── tools/
│   ├── memory/
│   ├── workflows/
│   ├── retrieval/
│   └── observability/
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
git clone https://github.com/soloai/soloai-agent-framework.git
cd soloai-agent-framework
python -m venv .venv
source .venv/bin/activate
pip install -e ".[dev]"
pytest
```

### Contribution guidelines

- Follow consistent code style and naming conventions
- Add tests for new features and bug fixes
- Update documentation for API or behavior changes
- Keep pull requests focused and reviewable
- Use clear commit messages following conventional commits when possible

---

## License

This project is released under the **MIT License**.  
See the [LICENSE](./LICENSE) file for full details.

---

## Business Inquiry

For consulting, implementation, custom AI agent solutions, or enterprise collaboration, please contact:

**379744050@qq.com**

### Fast Proposal Request

To receive a faster and more accurate proposal, please send the following details in your email:

- **Industry**
- **Project deliverables**
- **Budget range**
- **Deadline**

Whether you need an AI Agent 开发框架 customization, an enterprise-grade agent platform, or end-to-end AI solution delivery, SoloAI can help evaluate requirements and provide a practical implementation plan quickly.

---

## Why SoloAI Agent Framework

If you are searching for an **AI agent development framework**, **AI Agent 开发框架**, **LLM agent orchestration platform**, or **open-source agent framework for RAG and tool calling**, SoloAI Agent Framework provides a strong technical foundation for modern agent engineering.

If this project is useful to you, please consider:

- Starring the repository
- Opening issues for feedback or feature requests
- Contributing code or documentation
- Reaching out for business collaboration

--- 

## Star History

If you find this project valuable, give it a star to support future development.