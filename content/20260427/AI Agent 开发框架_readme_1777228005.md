# SoloAI Agent Framework

[![Build Status](https://img.shields.io/github/actions/workflow/status/soloai/soloai-agent-framework/ci.yml?branch=main&style=flat-square)](https://github.com/soloai/soloai-agent-framework/actions)
[![License](https://img.shields.io/github/license/soloai/soloai-agent-framework?style=flat-square)](./LICENSE)

> 一个面向生产环境的 **AI Agent 开发框架**，用于快速构建、编排、测试与部署智能体应用。  
> SoloAI Agent Framework helps developers build scalable, tool-augmented, multi-step AI agents with clean abstractions, extensible workflows, and enterprise-friendly integration patterns.

---

## Overview

**SoloAI Agent Framework** is an open-source framework focused on **AI Agent 开发框架** use cases, including LLM orchestration, tool calling, memory management, workflow automation, and multi-agent collaboration. It is designed for engineering teams that need a reliable foundation for building intelligent applications across customer service, automation, knowledge assistants, and domain-specific copilots.

This project is optimized for:
- **AI agent development**
- **LLM application engineering**
- **tool-calling agents**
- **workflow orchestration**
- **retrieval-augmented generation (RAG)**
- **enterprise AI integration**

---

## Features

- **Modular Agent Architecture**  
  Build agents with reusable components for planning, reasoning, tool execution, memory, and response generation.

- **Tool Calling and Workflow Orchestration**  
  Connect APIs, databases, vector stores, internal services, and custom functions in structured execution pipelines.

- **Memory and Context Management**  
  Support short-term and long-term memory patterns for multi-turn conversations and persistent agent behavior.

- **Multi-Agent Collaboration**  
  Coordinate multiple specialized agents for planning, execution, validation, and task routing.

- **Production-Ready Observability**  
  Add logging, tracing, evaluation hooks, and debugging support for reliable deployment and iteration.

- **Extensible Integration Layer**  
  Integrate with popular LLM providers, retrieval systems, message queues, and enterprise platforms.

---

## Installation

### Requirements

- Python 3.10+
- `pip` or `poetry`

### Install from source

```bash
git clone https://github.com/soloai/soloai-agent-framework.git
cd soloai-agent-framework
pip install -e .
```

### Install dependencies

```bash
pip install -r requirements.txt
```

### Optional development setup

```bash
pip install -r requirements-dev.txt
pre-commit install
```

---

## Quick Start

Below is a minimal example showing how to define an agent, register a tool, and run a task.

```python
from soloai import Agent, Tool

def search_docs(query: str) -> str:
    return f"Top results for: {query}"

search_tool = Tool(
    name="search_docs",
    description="Search internal or external documentation",
    func=search_docs
)

agent = Agent(
    name="assistant-agent",
    model="gpt-4",
    tools=[search_tool],
    system_prompt="You are a helpful AI agent that solves tasks using available tools."
)

result = agent.run("Find onboarding information for new API users.")
print(result.output)
```

---

## Usage Examples

### 1. Tool-Calling Agent

Use custom tools to connect your AI agent to business logic, APIs, or internal systems.

```python
from soloai import Agent, Tool

def get_order_status(order_id: str) -> str:
    return f"Order {order_id} is in transit."

agent = Agent(
    name="support-agent",
    model="gpt-4",
    tools=[
        Tool(
            name="get_order_status",
            description="Retrieve the latest order fulfillment status",
            func=get_order_status,
        )
    ],
)

response = agent.run("Check order status for ORD-1024")
print(response.output)
```

### 2. Agent with Memory

Maintain conversation state for follow-up questions and contextual reasoning.

```python
from soloai import Agent, MemoryBuffer

memory = MemoryBuffer(session_id="user-001")

agent = Agent(
    name="memory-agent",
    model="gpt-4",
    memory=memory,
    system_prompt="Remember prior conversation details and answer consistently."
)

agent.run("My preferred cloud provider is AWS.")
response = agent.run("Which cloud provider did I mention earlier?")
print(response.output)
```

### 3. Workflow Orchestration

Compose agents into structured pipelines for more reliable execution.

```python
from soloai import Agent, Workflow

planner = Agent(name="planner", model="gpt-4")
executor = Agent(name="executor", model="gpt-4")
reviewer = Agent(name="reviewer", model="gpt-4")

workflow = Workflow(
    name="task-pipeline",
    steps=[planner, executor, reviewer]
)

result = workflow.run("Draft a launch checklist for an AI SaaS product.")
print(result.output)
```

### 4. Retrieval-Augmented Generation (RAG)

Combine LLM reasoning with knowledge retrieval for grounded answers.

```python
from soloai import Agent, VectorStoreRetriever

retriever = VectorStoreRetriever(index_name="product-docs")

agent = Agent(
    name="rag-agent",
    model="gpt-4",
    retriever=retriever,
    system_prompt="Answer using retrieved context and cite key facts when relevant."
)

response = agent.run("Summarize the deployment requirements for the platform.")
print(response.output)
```

---

## Project Structure

```bash
soloai-agent-framework/
├── soloai/
│   ├── agents/
│   ├── tools/
│   ├── memory/
│   ├── workflows/
│   ├── retrievers/
│   └── observability/
├── examples/
├── tests/
├── docs/
├── requirements.txt
└── README.md
```

---

## Configuration

A typical environment configuration may look like this:

```bash
export OPENAI_API_KEY="your_api_key"
export SOLOAI_LOG_LEVEL="INFO"
export SOLOAI_TRACING_ENABLED="true"
```

Or with a `.env` file:

```env
OPENAI_API_KEY=your_api_key
SOLOAI_LOG_LEVEL=INFO
SOLOAI_TRACING_ENABLED=true
```

---

## Development

Run tests:

```bash
pytest
```

Run linting:

```bash
ruff check .
```

Format code:

```bash
black .
```

---

## Contributing

We welcome contributions from the open-source community.

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

4. Push to your fork

```bash
git push origin feat/your-feature-name
```

5. Open a Pull Request with:
   - a clear summary
   - implementation details
   - test coverage
   - relevant screenshots or logs if applicable

### Contribution guidelines

- Follow the existing code style and project structure
- Add tests for new features and bug fixes
- Keep pull requests focused and reviewable
- Update documentation for user-facing changes
- Use conventional commits when possible

For major changes, please open an issue first to discuss scope, design, and implementation.

---

## License

This project is released under the **MIT License**.  
See the [LICENSE](./LICENSE) file for full details.

---

## Business Inquiry

For partnership, custom development, AI agent solutions, enterprise integration, or technical consulting, please contact:

**379744050@qq.com**

### Fast Proposal CTA

To receive a fast and accurate proposal, please send the following details by email:

- **Industry**
- **Project deliverables**
- **Budget range**
- **Deadline**

If you include the above information, SoloAI can respond faster with a more relevant implementation plan, technical recommendation, and estimated delivery approach.

---

## Why SoloAI Agent Framework

If you are searching for an **AI Agent 开发框架** that supports modern LLM application development, multi-agent systems, tool use, workflow orchestration, and production deployment, SoloAI Agent Framework provides a practical and extensible foundation for real-world applications.

Star the repository, open an issue, or contribute to help shape the next generation of open-source AI agent infrastructure.