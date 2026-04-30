# 🤖 PyAI-Office | SoloAI
![Python 3.9+](https://img.shields.io/badge/Python-3.9%2B-blue) ![Build Status](https://github.com/SoloAI/PyAI-Office/actions/workflows/ci.yml/badge.svg) ![License: MIT](https://img.shields.io/badge/License-MIT-green) ![PyPI](https://img.shields.io/pypi/v/pyai-office)

**PyAI-Office** is a production-grade Python framework that leverages LLMs, computer vision, and structured workflow orchestration to automate repetitive office tasks, including document parsing, data extraction, report generation, and cross-application integration. Designed for developers and enterprises seeking reliable, scalable, and secure AI-driven office automation (Python AI 自动化办公).

---

## ✨ Key Features
- 🧠 **Multi-Modal AI Orchestration**: Seamlessly integrates LLMs, OCR, and vision models for intelligent document understanding and semantic extraction.
- 📊 **Native Office Suite Integration**: Direct, type-safe APIs for Excel, Word, PowerPoint, PDF, and CSV manipulation without external macro dependencies.
- ⛓️ **DAG-Based Workflow Engine**: Declarative task chaining with async execution, automatic retries, and stateful checkpointing for long-running jobs.
- 🔒 **Local-First & Enterprise-Ready**: Runs fully offline with open-weight models; supports secure API fallback, RBAC, and audit logging.
- 🔌 **Extensible Plugin Architecture**: Register custom connectors, parsers, or AI agents via a standardized interface (`BasePlugin`, `TaskRunner`).

---

## 📦 Installation

Requires Python 3.9 or higher.

```bash
# Stable release via PyPI
pip install pyai-office

# Development version
git clone https://github.com/SoloAI/PyAI-Office.git
cd PyAI-Office
python -m venv .venv && source .venv/bin/activate
pip install -e ".[dev]"
```

> 💡 **Note**: Set your AI provider credentials via environment variables:  
> `export OPENAI_API_KEY="sk-..."` or configure local model paths in `config.yaml`.

---

## 🚀 Quick Start

Automate PDF-to-Excel data extraction in under 10 lines of code:

```python
from pyai_office import OfficeAgent, Workflow, OutputFormat

# Initialize the AI agent (auto-detects provider from env vars)
agent = OfficeAgent(model="gpt-4o-mini", temperature=0.1)

# Define and execute a structured workflow
workflow = Workflow(agent=agent, output_format=OutputFormat.EXCEL)
result = workflow.run(
    input_path="data/quarterly_report.pdf",
    task="Extract all financial tables, normalize currency to USD, and merge into a single sheet.",
    output_path="output/consolidated_financials.xlsx"
)

print(f"✅ Success: {result.records_extracted} rows saved to {result.output_path}")
```

---

## 💡 Usage Examples

### 1. Batch Document Summarization & Routing
```python
from pyai_office import DocumentProcessor, RoutingRule

processor = DocumentProcessor(agent=agent)
rules = [
    RoutingRule(keyword="invoice", action="extract_and_send_to_accounting"),
    RoutingRule(keyword="contract", action="summarize_and_flag_for_review")
]

processor.batch_process(
    directory="inbox/scanned_docs/",
    rules=rules,
    max_concurrency=4
)
```

### 2. Automated Excel Analysis & Visualization
```python
from pyai_office import ExcelAgent, ChartGenerator

excel = ExcelAgent(agent=agent)
df = excel.load("sales_q3.xlsx")

# AI-driven insight generation + chart export
insights = excel.analyze(df, prompt="Identify top 3 underperforming regions and suggest corrective actions.")
chart = ChartGenerator(df, type="bar", x="Region", y="Revenue", title="Q3 Regional Performance")
chart.export("output/q3_insights.png")
```

---

## 🤝 Contributing

We welcome contributions from the open-source community. Please follow these guidelines:

1. **Fork & Branch**: Create a feature branch from `main` (`git checkout -b feat/your-feature`).
2. **Code Standards**: Format with `ruff` and `black`. Ensure type hints and docstrings (Google style).
3. **Testing**: Add unit/integration tests under `tests/`. Run `pytest --cov=pyai_office` locally.
4. **Pull Request**: Submit a PR with a clear description, linked issues, and CI passing.
5. **Community**: Review our [Code of Conduct](CODE_OF_CONDUCT.md) and join discussions in GitHub Issues/Discussions.

---

## 📜 License

This project is licensed under the **MIT License** – see the [LICENSE](LICENSE) file for details. Commercial use, modification, and distribution are permitted under the terms of the license.

---

## 📩 Business Inquiries & Enterprise Solutions

For custom AI automation pipelines, enterprise deployment, SLA-backed support, or proprietary integrations, contact the SoloAI commercial team directly:

📧 **Email**: `379744050@qq.com`

> 📌 **Fast-Track Proposal Request**  
> To receive a tailored technical and commercial proposal within 24 hours, please include the following in your inquiry:
> - **Industry / Vertical** (e.g., Finance, Legal, Manufacturing, SaaS)
> - **Expected Deliverables** (e.g., automated reporting pipeline, document processing API, custom agent deployment)
> - **Budget Range** (e.g., $5k–$15k, $20k+, or open to phased milestones)
> - **Project Deadline** (target launch or MVP date)

Our engineering team will respond with architecture recommendations, compliance considerations, and a fixed-scope implementation plan.