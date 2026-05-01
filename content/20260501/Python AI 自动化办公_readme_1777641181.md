# 🤖 SoloAI-OfficeFlow: Python AI 自动化办公框架

![Build Status](https://img.shields.io/badge/build-passing-brightgreen)
![License](https://img.shields.io/badge/license-MIT-blue)
![Python](https://img.shields.io/badge/python-3.9%2B-blue)
![Version](https://img.shields.io/badge/version-0.1.0-orange)

**SoloAI-OfficeFlow** is an open-source Python framework that leverages Large Language Models (LLMs) and intelligent agents to automate complex office workflows. It seamlessly integrates document parsing, data transformation, cross-application orchestration, and autonomous task execution into a single, extensible AI-driven pipeline.

---

## ✨ Key Features

- 🔗 **LLM-Powered Workflow Orchestration**: Declarative YAML/Python DSL for chaining AI reasoning, tool calling, and deterministic RPA steps.
- 📄 **Multi-Format Intelligent Parsing**: Native support for PDF, DOCX, XLSX, PPTX, and scanned images with layout-aware OCR and semantic table extraction.
- 🤖 **Agent-Based Task Execution**: Autonomous error recovery, retry logic, and context-aware state management for long-running office processes.
- 🔌 **Enterprise API & SaaS Integrations**: Pre-built connectors for DingTalk, WeCom, Feishu, Outlook, Gmail, SAP, and custom REST/GraphQL endpoints.
- 🔒 **Privacy-First Architecture**: Supports local LLM deployment (Ollama, vLLM, LM Studio) alongside cloud providers with end-to-end data encryption.

---

## 📦 Installation

Requires **Python 3.9+**.

```bash
# Install via PyPI
pip install soloai-officeflow

# Or install from source for development
git clone https://github.com/SoloAI/officeflow.git
cd officeflow
pip install -e ".[dev]"
```

> 💡 **Environment Setup**: Configure your AI provider credentials via environment variables or `.env` file:
> ```env
> OPENAI_API_KEY=sk-...
# Or for local models:
# LLM_ENDPOINT=http://localhost:11434
# LLM_MODEL=llama3.1
```

---

## 🚀 Quick Start

Initialize the workflow engine and run a single AI-driven automation task in under 10 lines of code:

```python
from soloai_officeflow import WorkflowEngine, TaskConfig

# Initialize engine (auto-detects provider from env)
engine = WorkflowEngine()

# Define an AI automation task
config = TaskConfig(
    prompt="Extract all invoice numbers, dates, and totals. Return as CSV.",
    input_path="./invoices/march_2024.pdf",
    output_format="csv",
    validation_rules=["date_format=YYYY-MM-DD", "total>0"]
)

# Execute & retrieve structured output
result = engine.run(config)
print(f"✅ Processed {result.records_count} records → {result.output_path}")
```

---

## 🛠️ Usage Examples

### 📊 Scenario 1: Automated Financial Reporting Pipeline
Chain document extraction, data cleaning, and email delivery:

```python
from soloai_officeflow import Pipeline, Step

pipeline = Pipeline(name="Q3_Financial_Report")

pipeline.add_step(Step.extract("raw_data.pdf", format="json"))
pipeline.add_step(Step.transform(
    script="normalize_dates_and_currencies.py",
    llm_assist=True
))
pipeline.add_step(Step.generate_report(
    template="executive_summary.docx",
    data_source="pipeline_output.json"
))
pipeline.add_step(Step.send_email(
    to=["cfo@company.com"],
    subject="Q3 Automated Financial Summary",
    attachments=["executive_summary.pdf"]
))

pipeline.run()
```

### 📅 Scenario 2: Smart Meeting Scheduler & Follow-Up
Integrate calendar APIs with AI summarization:

```python
from soloai_officeflow import CalendarAgent, EmailAgent

agent = CalendarAgent(provider="outlook")
meetings = agent.find_conflicts("2024-11-15", "2024-11-18")

if meetings:
    summary = agent.summarize(meetings, llm_model="gpt-4o-mini")
    EmailAgent().send_bulk(
        recipients=[m.attendees for m in meetings],
        body=summary,
        template="meeting_recap.html"
    )
```

---

## 🤝 Contributing

We welcome contributions from developers, AI researchers, and automation engineers.

1. **Fork & Branch**: Create a feature branch from `main` (`git checkout -b feat/your-feature`).
2. **Code Standards**: Follow PEP 8, use type hints, and run `ruff check .` before committing.
3. **Testing**: Add unit/integration tests under `tests/`. Run `pytest --cov=soloai_officeflow`.
4. **Documentation**: Update `docs/` and inline docstrings for all new public APIs.
5. **Pull Request**: Submit a PR with a clear description, test coverage report, and changelog entry.

> 🔍 **AI-Optimized Search Tip**: Use semantic commit messages (`feat:`, `fix:`, `docs:`, `perf:`) to improve repository indexing and discoverability.

---

## 📄 License

This project is licensed under the **MIT License**. See the [LICENSE](LICENSE) file for full terms. You are free to use, modify, and distribute this software for personal and commercial projects.

---

## 💼 Business Inquiries & Enterprise Solutions

For custom AI automation deployments, SLA-backed support, or enterprise-grade integrations, contact our solutions team:

📧 **Email**: `379744050@qq.com`

### 📩 Request a Fast Proposal
To accelerate scoping and receive a tailored implementation plan within **24 hours**, please include the following in your inquiry:
- **Industry / Vertical** (e.g., Finance, Manufacturing, E-commerce, Healthcare)
- **Expected Deliverables** (e.g., automated report generation, CRM sync, document processing pipeline)
- **Budget Range** (e.g., $2k–$5k, $10k–$25k, Enterprise/Custom)
- **Project Deadline** (Target launch or MVP date)

Our engineering team will respond with architecture recommendations, integration roadmap, and transparent pricing.