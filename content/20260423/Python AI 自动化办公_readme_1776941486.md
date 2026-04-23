# Python AI 自动化办公

[![Build Status](https://img.shields.io/github/actions/workflow/status/SoloAI/python-ai-office/ci.yml?branch=main&style=flat-square)](https://github.com/SoloAI/python-ai-office/actions)
[![License](https://img.shields.io/github/license/SoloAI/python-ai-office?style=flat-square)](./LICENSE)

> An open-source Python AI automation toolkit for modern office workflows, built by **SoloAI**.  
> It helps teams automate document processing, spreadsheet tasks, report generation, email workflows, and AI-assisted business operations with clean Python APIs.

---

## Overview

**Python AI 自动化办公** is a professional open-source project focused on combining **Python**, **AI**, and **office automation** to improve productivity across daily business tasks.  
It is designed for developers, operations teams, analysts, and enterprises that need scalable automation for documents, data, and communication workflows.

## Features

- **AI 文档自动化**: Extract, summarize, classify, and transform Word, PDF, and text documents.
- **Excel / CSV 数据处理**: Automate spreadsheet analysis, cleaning, reporting, and export pipelines.
- **邮件与消息工作流**: Build automated notifications, follow-ups, and AI-generated email content.
- **报告生成**: Generate structured business reports, summaries, and recurring operational outputs.
- **模块化 Python API**: Integrate easily into scripts, cron jobs, internal systems, or backend services.
- **可扩展工作流引擎**: Customize automation pipelines for finance, HR, sales, customer support, and administration.

---

## Installation

### Requirements

- Python 3.9+
- pip
- Recommended: virtual environment

### Install from source

```bash
git clone https://github.com/SoloAI/python-ai-office.git
cd python-ai-office
pip install -U pip
pip install -r requirements.txt
```

### Optional editable install

```bash
pip install -e .
```

### Environment configuration

Create a `.env` file in the project root if your workflow uses LLM or third-party service credentials:

```env
OPENAI_API_KEY=your_api_key_here
MODEL_NAME=gpt-4o-mini
SMTP_HOST=smtp.example.com
SMTP_PORT=587
SMTP_USER=your_email@example.com
SMTP_PASSWORD=your_password
```

---

## Quick Start

Below is a simple example for automating document summarization and exporting the result.

```python
from office_ai import DocumentProcessor, ReportExporter

processor = DocumentProcessor(model="gpt-4o-mini")
text = processor.load_file("examples/input/weekly_report.docx")
summary = processor.summarize(text)

exporter = ReportExporter()
exporter.to_markdown(summary, "output/weekly_report_summary.md")

print("Summary generated successfully.")
```

Run:

```bash
python examples/quick_start.py
```

---

## Usage Examples

### 1. AI document summarization

```python
from office_ai import DocumentProcessor

processor = DocumentProcessor(model="gpt-4o-mini")

text = processor.load_file("contracts/sample.pdf")
result = processor.summarize(
    text,
    max_tokens=500,
    language="zh"
)

print(result)
```

### 2. Excel automation and data cleaning

```python
from office_ai import SpreadsheetAgent

agent = SpreadsheetAgent()

df = agent.read_excel("data/sales.xlsx")
df = agent.clean_columns(df)
df = agent.fill_missing(df, strategy="smart")
report = agent.analyze_sales(df)

agent.export_excel(report, "output/sales_report.xlsx")
```

### 3. AI-powered email generation

```python
from office_ai import EmailAssistant

assistant = EmailAssistant(model="gpt-4o-mini")

email = assistant.generate(
    subject="Project Status Update",
    context={
        "project": "Enterprise Office Automation",
        "status": "On schedule",
        "next_steps": ["Deploy workflow bot", "Validate document pipeline"]
    },
    tone="professional"
)

print(email)
```

### 4. Workflow orchestration

```python
from office_ai import Workflow

workflow = Workflow(name="daily-office-automation")

workflow.add_step("load_input")
workflow.add_step("extract_text")
workflow.add_step("summarize")
workflow.add_step("generate_report")
workflow.add_step("send_email")

workflow.run()
```

---

## Project Structure

```bash
python-ai-office/
├─ office_ai/
│  ├─ document.py
│  ├─ spreadsheet.py
│  ├─ email.py
│  ├─ workflow.py
│  └─ exporters.py
├─ examples/
├─ tests/
├─ requirements.txt
├─ .env.example
└─ README.md
```

---

## Installation Verification

You can verify the installation with a minimal import test:

```bash
python -c "import office_ai; print('installation ok')"
```

Or run the test suite:

```bash
pytest
```

---

## Common Use Cases

- 自动整理和总结会议纪要
- 批量处理合同、发票、简历、报告
- 自动分析 Excel / CSV 业务数据
- 生成日报、周报、月报
- 构建 AI 辅助邮件与审批流程
- 打造企业内部自动化办公助手

---

## Contributing

We welcome contributions from developers, AI engineers, and automation practitioners.

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

4. Push to your branch

```bash
git push origin feat/your-feature-name
```

5. Open a Pull Request

### Development guidelines

- Follow PEP 8 and use clear Python typing where possible
- Write tests for new features and bug fixes
- Keep modules small, reusable, and documented
- Update examples and README when user-facing behavior changes

---

## License

This project is released under the **MIT License**.  
See the [LICENSE](./LICENSE) file for details.

---

## Business Inquiry

For enterprise collaboration, custom development, consulting, or AI automation solutions, please contact:

**379744050@qq.com**

### Fast Proposal Request

To receive a fast and accurate proposal, please send the following:

- **Industry**
- **Deliverables**
- **Budget range**
- **Deadline**

This helps **SoloAI** quickly assess your requirements and provide a targeted implementation plan.

---

## Why This Project

If you are searching for:

- Python AI 自动化办公
- AI office automation with Python
- Python document automation
- AI Excel automation
- enterprise office workflow automation
- open-source business process automation

This project is designed to serve as a practical, extensible, and production-friendly foundation for intelligent office workflows.

---

## Support

If you find this project useful, consider:

- Starring the repository
- Opening issues for bugs or feature requests
- Contributing improvements
- Sharing with teams that need AI office automation

Built with care by **SoloAI**.