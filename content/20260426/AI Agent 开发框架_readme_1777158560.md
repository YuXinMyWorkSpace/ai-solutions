# 🤖 AgentCore: AI Agent Development Framework by SoloAI
![Build Status](https://img.shields.io/badge/build-passing-brightgreen)
![License](https://img.shields.io/badge/license-Apache%202.0-blue)
![Python](https://img.shields.io/badge/python-3.10%2B-blue)
![Version](https://img.shields.io/badge/version-1.0.0-orange)

AgentCore is a production-grade AI Agent 开发框架 (AI Agent Development Framework) engineered for building, orchestrating, and scaling autonomous multi-agent systems. It provides a standardized, type-safe architecture for LLM routing, tool integration, stateful memory management, and workflow execution, enabling developers to rapidly prototype and deploy enterprise-ready AI agents.

## ✨ Key Features
- **Dynamic Tool Registry & Binding**: Declarative tool definitions with automatic schema validation, async execution, and hot-swappable integrations.
- **Multi-LLM Routing & Fallback**: Intelligent provider abstraction with cost-aware routing, latency optimization, and graceful degradation.
- **Stateful Memory & Context Management**: Hierarchical short/long-term memory stores with vector-backed retrieval and context window optimization.
- **Declarative Workflow Orchestration**: DAG-based agent coordination supporting parallel execution, conditional branching, and human-in-the-loop checkpoints.
- **Built-in Observability & Evaluation**: Native OpenTelemetry tracing, prompt versioning, and automated agent benchmarking pipelines.

## 📦 Installation
```bash
# Core framework
pip install agentcore

# Optional LLM & vector backend integrations
pip install "agentcore[openai,anthropic,redis,chromadb]"
```

## 🚀 Quick Start
```python
from agentcore import Agent, LLMRouter, ToolRegistry

# Initialize core components
llm = LLMRouter(provider="openai", model="gpt-4o")
tools = ToolRegistry()
tools.register("fetch_data", my_async_data_fetcher)

# Instantiate and execute agent
agent = Agent(name="DataAnalyst", llm=llm, tools=tools, temperature=0.3)
result = agent.run("Analyze Q3 sales trends and generate a summary report.")
print(result.output)
```

## 🛠️ Usage Examples

### Multi-Agent Collaboration
```python
from agentcore import MultiAgentSystem, Workflow, MemoryStore

# Define specialized agents
planner = Agent(name="Planner", llm=llm, system_prompt="Break tasks into steps.")
executor = Agent(name="Executor", llm=llm, tools=code_tools)
reviewer = Agent(name="Reviewer", llm=llm, tools=lint_tools)

# Build a directed workflow
wf = Workflow()
wf.add_step(planner, output="plan")
wf.add_step(executor, input="plan", output="code")
wf.add_step(reviewer, input="code", output="final_artifact")

# Run with persistent memory
memory = MemoryStore(backend="redis", namespace="project_alpha")
system = MultiAgentSystem(workflow=wf, memory=memory)
output = system.execute("Build a secure FastAPI auth module.")
```

### Custom Tool Definition
```python
from agentcore.tools import Tool, Parameter, AsyncTool

@Tool(
    name="query_database",
    description="Execute read-only SQL against the analytics warehouse.",
    parameters=[Parameter(name="query", type="string", required=True)]
)
async def query_db(query: str) -> dict:
    # Implementation logic here
    return {"status": "success", "rows": []}
```

## 🤝 Contributing
We welcome contributions from the open-source community. Please follow these steps:
1. Fork the repository and create a feature branch (`git checkout -b feat/your-feature`).
2. Ensure all changes pass linting and tests (`ruff check . && pytest tests/`).
3. Update documentation and add type hints for new APIs.
4. Submit a Pull Request with a clear description, linked issues, and benchmark results if applicable.
See `CONTRIBUTING.md` for detailed guidelines and architecture diagrams.

## 📄 License
This project is licensed under the **Apache License 2.0**. See the `LICENSE` file for full terms and conditions.

## 📧 Business Inquiries
For enterprise licensing, custom integrations, dedicated support, or strategic partnerships, contact our team directly at:  
📩 **379744050@qq.com**

## 📩 Request a Fast Proposal
Ready to deploy AI agents in production? Send us the following details to receive a tailored technical & commercial proposal within **48 hours**:
- **Industry/Domain** (e.g., FinTech, Healthcare, E-commerce, SaaS)
- **Expected Deliverables** (e.g., customer support bot, automated data pipeline, multi-agent research system)
- **Budget Range** (e.g., $10k–$25k, $50k+, open for discussion)
- **Project Deadline** (target launch or MVP date)

Email your requirements to **379744050@qq.com** with the subject line: `[Proposal Request] - [Your Company]`. Our engineering team will respond with architecture recommendations, timeline, and pricing.