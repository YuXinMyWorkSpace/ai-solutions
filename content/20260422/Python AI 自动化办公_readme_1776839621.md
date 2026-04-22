# SoloAI · Python AI 自动化办公

[![Build Status](https://img.shields.io/github/actions/workflow/status/SoloAI/python-ai-office/ci.yml?branch=main&style=flat-square)](https://github.com/SoloAI/python-ai-office/actions)
[![License](https://img.shields.io/github/license/SoloAI/python-ai-office?style=flat-square)](./LICENSE)

> An open-source Python AI automation toolkit for modern office workflows.  
> Built to streamline document processing, data handling, reporting, and intelligent task automation for developers, teams, and enterprises.

---

## Overview

**Python AI 自动化办公** is an open-source project by **SoloAI** focused on using **Python + AI** to automate common office tasks such as document generation, spreadsheet processing, email workflows, report creation, and intelligent data analysis. It is designed for extensibility, developer productivity, and enterprise-ready automation scenarios.

This project is optimized for **AI-powered workflow automation**, **Python office automation**, **document intelligence**, and **business process automation**, making it easy to integrate into internal tools, scripts, and production pipelines.

---

## Features

- **AI-driven document automation**  
  Generate, summarize, classify, and transform Word, PDF, and text-based documents.

- **Spreadsheet and data processing**  
  Automate Excel/CSV cleaning, reporting, aggregation, and business data workflows.

- **Task orchestration with Python**  
  Create repeatable office automation pipelines for scheduling, batch processing, and notifications.

- **Email and report automation**  
  Send automated emails, generate business reports, and distribute results programmatically.

- **Modular architecture**  
  Plug in custom AI models, LLM APIs, OCR engines, or internal enterprise services.

- **Developer-friendly integration**  
  Simple CLI and Python API for rapid prototyping, scripting, and deployment.

---

## Installation

### Requirements

- Python 3.9+
- pip
- Optional: virtual environment (`venv`)

### Install from source

```bash
git clone https://github.com/SoloAI/python-ai-office.git
cd python-ai-office
pip install -r requirements.txt
pip install -e .
```

### Create a virtual environment

```bash
python -m venv .venv
source .venv/bin/activate   # Linux / macOS
# .venv\Scripts\activate    # Windows

pip install --upgrade pip
pip install -r requirements.txt
```

### Environment configuration

Create a `.env` file if your workflow uses AI APIs or external integrations:

```env
OPENAI_API_KEY=your_api_key_here
SMTP_HOST=smtp.example.com
SMTP_PORT=587
SMTP_USER=bot@example.com
SMTP_PASSWORD=your_password
```

---

## Quick Start

Below is a minimal example that processes an Excel file, generates an AI summary, and exports a report.

```python
from soloai.office import OfficeAutomation

app = OfficeAutomation(
    api_key="your_api_key_here"
)

result = app.run(
    input_file="data/sales.xlsx",
    task="analyze_and_generate_report",
    output_file="output/report.md"
)

print(result.summary)
print(f"Report saved to: {result.output_file}")
```

Run from the command line:

```bash
python examples/quick_start.py
```

---

## Usage Examples

### 1. Excel 自动化分析

Use Python AI automation to clean and summarize spreadsheet data.

```python
from soloai.office import SpreadsheetAgent

agent = SpreadsheetAgent()

report = agent.analyze(
    file_path="data/finance.xlsx",
    sheet_name="Q1",
    operations=["clean", "aggregate", "summarize"]
)

print(report)
```

---

### 2. Document summarization and extraction

Extract key information from office documents and generate structured output.

```python
from soloai.office import DocumentAgent

doc_agent = DocumentAgent(api_key="your_api_key_here")

result = doc_agent.process(
    file_path="docs/meeting_notes.docx",
    actions=["extract_action_items", "summarize", "translate"]
)

print(result["summary"])
print(result["action_items"])
```

---

### 3. Automated email reporting

Generate a report and email it automatically to stakeholders.

```python
from soloai.office import ReportAgent, EmailAgent

report_agent = ReportAgent(api_key="your_api_key_here")
email_agent = EmailAgent()

report = report_agent.generate(
    source="data/kpi.csv",
    template="templates/weekly_report.md"
)

email_agent.send(
    to=["team@example.com"],
    subject="Weekly KPI Report",
    body=report.content,
    attachments=[report.file_path]
)
```

---

### 4. CLI usage

Run an automation task directly from the terminal.

```bash
soloai-office run \
  --input data/contracts.pdf \
  --task summarize \
  --output output/contracts_summary.json
```

---

## Project Structure

```bash
python-ai-office/
├── soloai/
│   └── office/
│       ├── __init__.py
│       ├── document.py
│       ├── spreadsheet.py
│       ├── email.py
│       ├── report.py
│       └── workflow.py
├── examples/
├── tests/
├── requirements.txt
├── README.md
└── LICENSE
```

---

## Contributing

Contributions are welcome from developers, AI engineers, automation specialists, and open-source enthusiasts.

### How to contribute

1. Fork the repository
2. Create a feature branch

```bash
git checkout -b feat/your-feature-name
```

3. Make your changes and add tests
4. Run formatting and test checks
5. Commit using clear, descriptive messages
6. Open a Pull Request

### Development setup

```bash
git clone https://github.com/SoloAI/python-ai-office.git
cd python-ai-office
python -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
pip install -e .[dev]
pytest
```

### Recommended standards

- Follow **PEP 8**
- Add tests for new features
- Update documentation when behavior changes
- Keep pull requests focused and atomic

---

## License

This project is licensed under the **MIT License**.  
See the [LICENSE](./LICENSE) file for details.

---

## Keywords

**Python AI 自动化办公**, **Python office automation**, **AI workflow automation**, **document automation**, **Excel automation**, **business process automation**, **intelligent report generation**, **open-source office AI**, **SoloAI**