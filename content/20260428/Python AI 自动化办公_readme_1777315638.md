# SoloAI · Python AI 自动化办公

[![Build Status](https://img.shields.io/github/actions/workflow/status/soloai/python-ai-office/ci.yml?branch=main&style=flat-square)](https://github.com/soloai/python-ai-office/actions)
[![License](https://img.shields.io/github/license/soloai/python-ai-office?style=flat-square)](./LICENSE)

> An open-source Python framework for **AI-powered office automation**.  
> Built by **SoloAI**, this project helps teams automate repetitive办公 workflows such as document generation, spreadsheet processing, email handling, report creation, and intelligent task orchestration.

---

## Overview

**Python AI 自动化办公** is designed for developers, operations teams, and businesses that want to combine **Python automation**, **LLM/AI capabilities**, and **office productivity workflows** into one practical toolkit. It provides modular components for integrating AI into document pipelines, Excel automation, data extraction, scheduling, and business process automation.

## Features

- **AI-driven document automation**  
  Generate, summarize, rewrite, and classify Word, PDF, and text-based documents.

- **Excel and data workflow automation**  
  Read, clean, analyze, and export spreadsheet data with Python-based automation pipelines.

- **Email and notification integration**  
  Automate email drafting, sending, parsing, and workflow-triggered notifications.

- **Task orchestration for office processes**  
  Chain multi-step business workflows such as reporting, approvals, reminders, and document routing.

- **Pluggable LLM and API integration**  
  Connect with OpenAI-compatible models, local models, or enterprise AI services.

- **Developer-friendly architecture**  
  Modular Python package structure, CLI support, environment-based configuration, and extensible adapters.

---

## Installation

### Requirements

- Python 3.9+
- `pip` or `poetry`
- Optional: API key for your preferred LLM provider

### Install from source

```bash
git clone https://github.com/soloai/python-ai-office.git
cd python-ai-office
pip install -r requirements.txt
```

### Install in editable mode

```bash
pip install -e .
```

### Environment configuration

Create a `.env` file in the project root:

```env
AI_PROVIDER=openai
AI_API_KEY=your_api_key_here
MODEL_NAME=gpt-4o-mini
SMTP_HOST=smtp.example.com
SMTP_PORT=587
SMTP_USER=your_email@example.com
SMTP_PASSWORD=your_password
```

---

## Quick Start

Below is a minimal example showing how to automate a simple office task: summarize a document and export the result.

```python
from soloai_office import OfficeAgent

agent = OfficeAgent(
    provider="openai",
    model="gpt-4o-mini"
)

result = agent.process_document(
    input_path="data/weekly_report.txt",
    task="Summarize the report into 5 bullet points and extract action items."
)

print(result.summary)
print(result.action_items)

agent.export_text("output/weekly_summary.md", result.summary)
```

Run:

```bash
python examples/quick_start.py
```

---

## Usage Examples

### 1. Excel automation with AI insights

```python
from soloai_office import ExcelAgent

excel = ExcelAgent()

report = excel.analyze(
    input_file="data/sales.xlsx",
    sheet_name="Q1",
    prompt="Identify top-performing products, revenue trends, and anomalies."
)

print(report.insights)
excel.export_report("output/sales_insights.xlsx", report)
```

### 2. Automated email drafting

```python
from soloai_office import MailAgent

mailer = MailAgent(provider="openai", model="gpt-4o-mini")

email = mailer.generate_email(
    context="""
    Write a professional follow-up email to a client.
    Include project status, next steps, and a request for feedback.
    """,
    tone="professional"
)

print(email.subject)
print(email.body)
```

### 3. Batch document processing

```python
from soloai_office import BatchProcessor

processor = BatchProcessor(provider="openai", model="gpt-4o-mini")

results = processor.run(
    input_dir="documents/",
    task="Extract contract dates, company names, obligations, and risks."
)

for item in results:
    print(item.filename, item.extracted_fields)
```

### 4. Workflow orchestration

```python
from soloai_office import Workflow

workflow = Workflow("monthly_reporting")

workflow.add_step("load_excel")
workflow.add_step("analyze_kpis_with_ai")
workflow.add_step("generate_summary_doc")
workflow.add_step("send_email_to_management")

workflow.run()
```

---

## Project Structure

```text
python-ai-office/
├── soloai_office/
│   ├── agents/
│   ├── workflows/
│   ├── integrations/
│   ├── utils/
│   └── cli.py
├── examples/
├── tests/
├── requirements.txt
├── .env.example
└── README.md
```

---

## Installation Options for Development

### Create a virtual environment

```bash
python -m venv .venv
source .venv/bin/activate
```

On Windows:

```bash
.venv\Scripts\activate
```

### Install development dependencies

```bash
pip install -r requirements.txt
pip install -r requirements-dev.txt
```

### Run tests

```bash
pytest
```

### Run linting

```bash
ruff check .
```

---

## Contributing

Contributions are welcome from developers, automation engineers, and AI practitioners.

### How to contribute

1. Fork the repository
2. Create a feature branch

```bash
git checkout -b feature/your-feature-name
```

3. Make your changes
4. Run tests and lint checks
5. Commit with clear messages

```bash
git commit -m "feat: add intelligent Excel anomaly detection"
```

6. Push your branch and open a Pull Request

### Contribution guidelines

- Follow Python best practices and PEP 8
- Write clear docstrings and type hints where possible
- Add or update tests for new functionality
- Keep modules focused and reusable
- Document user-facing changes in the README or docs

---

## Roadmap

- Support for more enterprise document formats
- Local/offline LLM integration
- Workflow templates for HR, finance, and operations
- OCR-enhanced document understanding
- Web dashboard for managing automation jobs

---

## License

This project is licensed under the **MIT License**.  
See the [LICENSE](./LICENSE) file for details.

---

## Business Inquiry

For enterprise collaboration, custom AI automation solutions, technical consulting, or implementation support, please contact:

**379744050@qq.com**

### Fast Proposal Request

To receive a fast and accurate proposal, please send the following:

- **Industry**
- **Project deliverables**
- **Budget range**
- **Deadline**

If you share your **industry, deliverables, budget range, and deadline**, SoloAI can respond faster with a more targeted technical solution and implementation proposal.

---

## Why This Project

This repository is built for teams searching for:

- Python AI automation for office work
- AI office workflow automation
- Python document automation
- Excel AI analysis tools
- LLM-powered business process automation
- Open-source AI办公 automation framework

If your goal is to streamline repetitive office tasks with **Python + AI**, this project provides a practical, extensible starting point.

---

## Support

If this project helps you, please consider:

- Starring the repository
- Opening issues for bugs or feature requests
- Submitting pull requests
- Sharing use cases with the community

**Build smarter office workflows with SoloAI.**