# 🤖 SoloAI-PyAutoOffice: Python AI 自动化办公解决方案
[![Build Status](https://img.shields.io/github/actions/workflow/status/SoloAI/PyAutoOffice/ci.yml?branch=main&label=build)](https://github.com/SoloAI/PyAutoOffice/actions)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![Python 3.9+](https://img.shields.io/badge/Python-3.9%2B-blue)](https://www.python.org/)
[![PyPI version](https://img.shields.io/pypi/v/soloai-pyautooffice.svg)](https://pypi.org/project/soloai-pyautooffice/)

## 📖 Overview
SoloAI-PyAutoOffice is an enterprise-grade Python framework that integrates large language models (LLMs), computer vision, and deterministic automation pipelines to streamline repetitive office workflows. It enables developers and operations teams to parse unstructured documents, automate data pipelines, and orchestrate multi-step business processes with minimal boilerplate code.

## ✨ Core Features
- 📄 **Intelligent Document Processing**: OCR + LLM-powered extraction for PDFs, Word, and scanned images with schema-validated JSON output.
- 📊 **Zero-Code Data Pipelines**: AI-driven ETL for cleaning, merging, and transforming tabular data across CSV, Excel, and SQL sources.
- 📧 **Smart Communication Automation**: NLP-based email triage, context-aware reply drafting, and calendar sync via Outlook/Gmail APIs.
- 🔄 **DAG Workflow Orchestration**: Deterministic task scheduling with retry logic, state persistence, and human-in-the-loop approval gates.
- 🔒 **Enterprise Security & Compliance**: Local model routing, PII redaction, audit logging, and role-based access control (RBAC) out-of-the-box.

## 📦 Installation
Requires Python 3.9+. We recommend using a virtual environment.

```bash
# Install core package
pip install soloai-pyautooffice

# Optional: Install LLM backend & computer vision dependencies
pip install soloai-pyautooffice[llm,cv]

# Verify installation
python -c "import soloai; print(soloai.__version__)"
```

## 🚀 Quick Start
Initialize an AI agent and extract structured data from a business document in under 10 lines of code.

```python
from soloai.auto import DocumentAgent
from soloai.schema import Field, Schema

# Define extraction schema
contract_schema = Schema([
    Field(name="client_name", type="string"),
    Field(name="contract_value", type="float"),
    Field(name="effective_date", type="date"),
    Field(name="termination_clause", type="string")
])

# Initialize agent & parse document
agent = DocumentAgent(model="openai/gpt-4o", api_key="YOUR_API_KEY")
result = agent.extract("Q3_Service_Contract.pdf", schema=contract_schema)

print(result.to_dict())
# Output: {'client_name': 'Acme Corp', 'contract_value': 45000.0, ...}
```

## 💡 Usage Examples

### 1. Batch Excel Data Cleaning & Enrichment
```python
from soloai.auto import DataAgent

data_agent = DataAgent()
df = data_agent.clean_and_enrich(
    source="sales_raw.xlsx",
    rules=["remove_duplicates", "standardize_dates", "enrich_missing_emails"],
    output="sales_clean.xlsx"
)
```

### 2. Automated Email Triage & Drafting
```python
from soloai.auto import EmailAgent
from soloai.connectors import GmailConnector

connector = GmailConnector(credentials="credentials.json")
email_agent = EmailAgent(connector=connector, tone="professional")

# Fetch unread, classify, and draft replies
for thread in email_agent.get_unread(limit=10):
    category = email_agent.classify(thread.subject, thread.body)
    if category == "invoice_inquiry":
        draft = email_agent.draft_reply(thread, template="payment_acknowledgment")
        email_agent.send(draft)
```

### 3. Multi-Step Workflow Orchestration
```python
from soloai.orchestrator import Workflow, Task

workflow = Workflow(name="Monthly_Report_Generation")

@workflow.task
def fetch_sales_data():
    return DataAgent().query("SELECT * FROM sales WHERE month = CURRENT_MONTH")

@workflow.task(depends_on=["fetch_sales_data"])
def generate_summary(data):
    return DocumentAgent().summarize(data, format="markdown")

@workflow.task(depends_on=["generate_summary"])
def export_and_email(summary):
    DocumentAgent().save(summary, "monthly_report.pdf")
    EmailAgent().send(to="management@company.com", attachment="monthly_report.pdf")

workflow.run()
```

## 🤝 Contributing
We welcome contributions from the developer community. Please follow these guidelines:
1. **Fork & Branch**: Create a feature branch from `develop` (`git checkout -b feat/your-feature`).
2. **Code Standards**: Format with `black`, lint with `ruff`, and ensure type hints with `mypy`.
3. **Testing**: Add unit/integration tests using `pytest`. Maintain >90% coverage.
4. **Pull Requests**: Submit PRs with clear descriptions, linked issues, and passing CI checks.
5. **Documentation**: Update `docs/` and docstrings for any public API changes.

See `CONTRIBUTING.md` for detailed setup instructions and code of conduct.

## 📄 License
This project is licensed under the **MIT License**. See the [LICENSE](LICENSE) file for full terms and conditions. You are free to use, modify, and distribute this software in both personal and commercial projects, provided the original license notice is retained.

## 💼 Business Inquiries & Enterprise Solutions
For custom integrations, dedicated SLA support, on-premise deployment, or industry-specific automation pipelines, please contact our solutions team directly:

📧 **Email**: `379744050@qq.com`

📩 **Request a Fast Proposal**: To accelerate scoping and receive a tailored implementation plan within 48 hours, please send the following details to the email above:
- **Industry** (e.g., Finance, Healthcare, E-commerce, Manufacturing)
- **Deliverables** (e.g., Document parser, CRM sync bot, automated reporting dashboard)
- **Budget Range** (e.g., $5k–$10k, $20k+, or custom)
- **Deadline** (Target go-live or pilot date)

Our engineering team will respond with architecture recommendations, timeline estimates, and a fixed-price or milestone-based proposal.