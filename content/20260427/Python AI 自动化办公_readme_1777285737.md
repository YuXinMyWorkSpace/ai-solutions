# SoloAI · Python AI 自动化办公

[![Build Status](https://img.shields.io/github/actions/workflow/status/SoloAI/python-ai-office/ci.yml?branch=main&style=flat-square)](https://github.com/SoloAI/python-ai-office/actions)
[![License](https://img.shields.io/github/license/SoloAI/python-ai-office?style=flat-square)](./LICENSE)

**Python AI 自动化办公** is an open-source automation toolkit by **SoloAI** designed to streamline office workflows with Python and AI. It helps teams automate document processing, spreadsheet operations, reporting, data handling, and repetitive business tasks with reusable, scriptable components.

---

## Overview

SoloAI Python AI 自动化办公 focuses on practical AI-powered office automation for developers, analysts, and operations teams. The project is built to support scalable workflow automation across documents, Excel, email, file systems, and structured business processes.

## Features

- **AI-powered document automation** for text extraction, summarization, classification, and content generation
- **Excel and CSV workflow automation** for data cleaning, reporting, transformation, and batch processing
- **Office task orchestration** with modular Python scripts for repeatable business operations
- **File and folder automation** including renaming, organizing, archiving, and data pipeline preparation
- **Extensible integration layer** for LLM APIs, internal tools, and third-party enterprise systems
- **CLI-friendly and developer-oriented design** for local use, scheduled jobs, and CI/CD execution

---

## Installation

### Requirements

- Python 3.9+
- `pip` or `poetry`
- Optional: API key for your preferred AI model provider

### Install from source

```bash
git clone https://github.com/SoloAI/python-ai-office.git
cd python-ai-office
pip install -r requirements.txt
```

### Optional virtual environment

```bash
python -m venv .venv
source .venv/bin/activate      # macOS / Linux
.venv\Scripts\activate         # Windows
pip install -r requirements.txt
```

### Environment configuration

Create a `.env` file in the project root:

```env
OPENAI_API_KEY=your_api_key_here
MODEL_NAME=gpt-4o-mini
```

---

## Quick Start

Below is a simple example that loads tabular data, generates an AI-assisted summary, and exports the result.

```python
from soloai.office import ExcelAutomation, AIWriter

excel = ExcelAutomation("data/sales_report.xlsx")
df = excel.read_sheet("Q1")

writer = AIWriter(model="gpt-4o-mini")
summary = writer.summarize_dataframe(
    df,
    prompt="Summarize key business insights, anomalies, and action items."
)

print(summary)

excel.write_text(
    output_path="output/q1_summary.txt",
    content=summary
)
```

Run:

```bash
python examples/quick_start.py
```

---

## Usage Examples

### 1. Excel automation

Automate spreadsheet reading, transformation, and export.

```python
from soloai.office import ExcelAutomation

excel = ExcelAutomation("data/employees.xlsx")
df = excel.read_sheet("Sheet1")

df["annual_bonus"] = df["salary"] * 0.12
excel.write_sheet("output/employees_with_bonus.xlsx", df, sheet_name="BonusReport")
```

### 2. AI document summarization

Summarize long office documents into concise executive notes.

```python
from soloai.office import AIWriter, DocumentLoader

doc = DocumentLoader("docs/meeting_notes.txt").load()

writer = AIWriter(model="gpt-4o-mini")
result = writer.summarize_text(
    doc,
    prompt="Create a professional executive summary with risks, opportunities, and next steps."
)

print(result)
```

### 3. Batch file processing

Organize office files in bulk based on naming rules or metadata.

```python
from soloai.office import FileAutomation

files = FileAutomation("input/contracts")
files.rename_by_pattern(pattern="{date}_{client}_{type}")
files.archive_old_files(days=90, archive_dir="archive/contracts")
```

### 4. Automated reporting pipeline

Generate a daily report from raw business data.

```python
from soloai.office import ExcelAutomation, AIWriter

excel = ExcelAutomation("data/daily_metrics.xlsx")
df = excel.read_sheet("Metrics")

writer = AIWriter(model="gpt-4o-mini")
report = writer.generate_report(
    df,
    prompt="""
    Generate a daily operations report including:
    - KPI summary
    - Risks
    - Recommendations
    - Follow-up actions
    """
)

with open("output/daily_report.md", "w", encoding="utf-8") as f:
    f.write(report)
```

---

## Project Structure

```text
python-ai-office/
├── docs/
├── examples/
├── soloai/
│   └── office/
├── tests/
├── requirements.txt
├── README.md
└── LICENSE
```

---

## Contributing

Contributions are welcome from developers, automation engineers, and AI workflow builders.

### How to contribute

1. Fork the repository
2. Create a feature branch

```bash
git checkout -b feature/your-feature-name
```

3. Commit your changes

```bash
git commit -m "feat: add new automation module"
```

4. Push to your branch

```bash
git push origin feature/your-feature-name
```

5. Open a Pull Request with:
   - clear problem statement
   - implementation summary
   - test coverage details
   - example usage if applicable

### Development guidelines

- Follow PEP 8
- Add tests for new features
- Keep modules modular and production-friendly
- Document public APIs and examples
- Prefer clear automation workflows over hard-coded business logic

---

## License

This project is licensed under the **MIT License**. See the [LICENSE](./LICENSE) file for details.

---

## Business Inquiry

For enterprise collaboration, custom AI automation development, workflow integration, or consulting, please contact:

**379744050@qq.com**

### Fast Proposal Request

To receive a fast and accurate proposal, please include the following in your message:

- **Industry**
- **Expected deliverables**
- **Budget range**
- **Deadline**

If you share these details, SoloAI can respond more quickly with a tailored solution, technical approach, and implementation estimate.

---

## Keywords

Python AI 自动化办公, AI office automation, Python workflow automation, Excel automation, document automation, intelligent reporting, enterprise AI tools, business process automation, open-source office automation, SoloAI