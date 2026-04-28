# 🤖 SoloAI Agent Framework

[![Build Status](https://github.com/SoloAI/agent-framework/actions/workflows/ci.yml/badge.svg)](https://github.com/SoloAI/agent-framework/actions/workflows/ci.yml)
[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](https://opensource.org/licenses/Apache-2.0)

## 📖 Overview
A production-ready, modular **AI Agent Development Framework** designed for building, orchestrating, and deploying autonomous LLM-driven agents at scale. SoloAI provides standardized memory management, tool execution pipelines, and multi-agent coordination to accelerate enterprise-grade AI system development.

## ✨ Core Features
- **Modular Architecture**: Decoupled components for LLM routing, state management, and tool execution with hot-swappable backends.
- **Multi-Agent Orchestration**: Native support for hierarchical, swarm, and debate-based agent collaboration with conflict resolution protocols.
- **Stateful Memory & Context Control**: Vector-backed short/long-term memory with automatic context window pruning and semantic caching.
- **Enterprise Observability**: Built-in OpenTelemetry-compatible tracing, structured logging, and deterministic evaluation metrics.
- **Standardized Tool Integration**: JSON Schema-driven API wrappers, RAG pipeline connectors, and secure Python/JS function execution.
- **Cloud-Native Deployment**: Docker-optimized, Kubernetes-ready, and serverless export templates for AWS Lambda, GCP Cloud Run, and Azure Functions.

## 📦 Installation
```bash
# Install via PyPI
pip install soloai-agent-framework

# Or install from source for development
git clone https://github.com/SoloAI/agent-framework.git
cd agent-framework
pip install -e ".[dev]"
```
> **Requirements**: Python 3.9+, `uv` or `pip` package manager, and an active LLM API key (OpenAI, Anthropic, vLLM, or local Ollama).

## 🚀 Quick Start
```python
from soloai import Agent, Memory, Tool

# Initialize agent with model, memory backend, and custom tools
agent = Agent(
    model="openai/gpt-4o",
    memory=Memory(type="vector_store", backend="chromadb", retention="7d"),
    tools=[Tool.from_function(query_database)]
)

# Execute a single autonomous task
response = agent.run("Analyze Q3 sales trends and generate a 3-bullet executive summary.")
print(response.output)
print(f"🔍 Tokens used: {response.usage.total_tokens}")
```

## 🛠️ Usage Examples

### 🔗 Multi-Agent Workflow Orchestration
```python
from soloai.orchestration import SupervisorAgent, WorkerAgent, Strategy

# Define specialized worker agents
researcher = WorkerAgent(role="Market Researcher", tools=[web_search_tool])
quant = WorkerAgent(role="Quantitative Analyst", tools=[pandas_tool, stats_tool])

# Supervisor coordinates task delegation & synthesis
supervisor = SupervisorAgent(
    workers=[researcher, quant],
    strategy=Strategy.HIERARCHICAL,
    max_iterations=5
)

result = supervisor.execute("Forecast next quarter's churn rate based on competitor pricing shifts.")
print(result.synthesis)
```

### 📊 Observability & Evaluation
```python
from soloai.observability import TraceRecorder, Evaluator

# Enable automatic tracing
with TraceRecorder(project="sales-agent-v1"):
    response = agent.run("Identify top 3 upsell opportunities.")

# Run deterministic evaluation
metrics = Evaluator().assess(
    output=response,
    ground_truth=expected_output,
    criteria=["factual_accuracy", "actionability", "latency"]
)
print(metrics.to_json())
```

## 🤝 Contributing
We welcome contributions from the AI engineering community. Please follow these guidelines:
1. **Fork & Branch**: Create a feature branch from `main` (`git checkout -b feat/your-feature`).
2. **Code Standards**: Format with `ruff` and `black`. Ensure type hints (`mypy --strict`).
3. **Testing**: All PRs must include `pytest` coverage (`>85%`). Run `make test` before pushing.
4. **Pull Requests**: Use the provided PR template. Link related issues and document breaking changes.
5. **Review Process**: Maintainers will review within 3 business days. CI must pass before merge.

Detailed guidelines are available in `CONTRIBUTING.md`.

## 📄 License
This project is licensed under the **Apache License 2.0**. See the `LICENSE` file for full terms and conditions. Commercial use, modification, and distribution are permitted under the license requirements.

## 🏢 Business Inquiries & Enterprise Solutions
For enterprise licensing, SLA-backed support, custom model fine-tuning, or on-premise deployment consulting, contact our solutions team:

📧 **Email**: `379744050@qq.com`

## 📩 Request a Fast Custom Proposal
Accelerate your AI agent deployment. To receive a tailored architecture proposal and implementation timeline within 24 hours, please reply with:
- **Industry / Vertical** (e.g., FinTech, Healthcare, E-commerce, SaaS)
- **Expected Deliverables** (e.g., multi-agent workflow, RAG pipeline, autonomous customer support, internal ops bot)
- **Budget Range** (e.g., $5k–$15k, $15k–$50k, Enterprise/Custom)
- **Target Deadline** (e.g., MVP in 4 weeks, Q3 launch, flexible)

Our engineering team will map your requirements to a production-ready SoloAI deployment blueprint.