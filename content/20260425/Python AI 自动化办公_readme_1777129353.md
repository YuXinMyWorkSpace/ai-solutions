# SoloAI · Python AI 自动化办公

[![Build Status](https://img.shields.io/github/actions/workflow/status/SoloAI/python-ai-office/ci.yml?branch=main&style=for-the-badge)](https://github.com/SoloAI/python-ai-office/actions)
[![License](https://img.shields.io/github/license/SoloAI/python-ai-office?style=for-the-badge)](./LICENSE)

> 一个面向企业与开发者的 **Python AI 自动化办公** 开源项目，用于快速构建文档处理、数据整理、流程自动化与 AI 办公助手能力。  
> Built for modern productivity workflows, this project helps teams automate repetitive office tasks with Python, AI models, and extensible integrations.

---

## Overview

**SoloAI Python AI 自动化办公** is an open-source toolkit focused on **AI-powered office automation with Python**. It enables developers and businesses to automate document generation, spreadsheet workflows, email tasks, knowledge extraction, and intelligent process orchestration.

This repository is designed for:
- 企业办公自动化
- AI 文档处理
- Python 工作流自动化
- 智能报表与数据清洗
- LLM/AI 助手集成
- Internal productivity tooling

---

## Features

- **AI 文档自动化**: Generate, summarize, classify, and transform Word, PDF, Markdown, and text documents.
- **Excel / CSV 数据处理**: Automate spreadsheet cleaning, reporting, merging, formula generation, and data enrichment.
- **邮件与通知工作流**: Trigger AI-powered email drafting, follow-ups, summaries, and notification pipelines.
- **可扩展工作流引擎**: Compose repeatable office automation pipelines with Python scripts and modular task runners.
- **LLM / API 集成**: Connect to modern AI model providers and enterprise APIs for smart decision-making and content generation.
- **适合企业落地**: Designed for internal tools, back-office efficiency, knowledge management, and digital operations.

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

### Development install

```bash
git clone https://github.com/SoloAI/python-ai-office.git
cd python-ai-office
pip install -e .
```

### Optional environment setup

Create a `.env` file:

```env
AI_API_KEY=your_api_key_here
AI_MODEL=gpt-4o-mini
SMTP_HOST=smtp.example.com
SMTP_PORT=587
SMTP_USER=your_email@example.com
SMTP_PASSWORD=your_password
```

---

## Quick Start

Below is a minimal example showing how to process an office document with AI automation.

```python
from soloai_office import OfficeAgent

agent = OfficeAgent(
    api_key="your_api_key",
    model="gpt-4o-mini"
)

result = agent.run(
    task="总结这份周报并提取关键行动项",
    input_file="examples/weekly_report.docx",
    output_file="output/weekly_report_summary.md"
)

print(result)
```

Run it:

```bash
python examples/quick_start.py
```

---

## Usage Examples

### 1. Summarize documents

```python
from soloai_office import DocumentProcessor

processor = DocumentProcessor(model="gpt-4o-mini")

summary = processor.summarize(
    file_path="docs/meeting_notes.pdf",
    max_tokens=800
)

print(summary)
```

### 2. Clean and enrich Excel data

```python
from soloai_office import SpreadsheetAutomation

sheet = SpreadsheetAutomation()

df = sheet.load("data/sales.xlsx")
df = sheet.clean_headers(df)
df = sheet.fill_missing_values(df)
df = sheet.generate_ai_tags(df, column="customer_feedback")

sheet.save(df, "output/sales_cleaned.xlsx")
```

### 3. Generate email drafts from meeting notes

```python
from soloai_office import EmailAssistant

assistant = EmailAssistant(model="gpt-4o-mini")

draft = assistant.create_followup_email(
    meeting_notes_file="docs/client_meeting.md",
    tone="professional",
    language="zh-CN"
)

print(draft.subject)
print(draft.body)
```

### 4. Build a reusable workflow pipeline

```python
from soloai_office import Workflow

workflow = Workflow(name="finance-report-automation")

workflow.add_step("load_excel", {"path": "data/finance.xlsx"})
workflow.add_step("analyze_data", {"prompt": "识别异常支出并生成摘要"})
workflow.add_step("generate_report", {"format": "markdown"})
workflow.add_step("send_email", {"to": ["finance@example.com"]})

workflow.run()
```

### 5. CLI usage

```bash
python -m soloai_office run \
  --task "整理合同信息并输出摘要" \
  --input contracts/contract_001.pdf \
  --output output/contract_001_summary.md
```

---

## Project Structure

```text
python-ai-office/
├── examples/
├── docs/
├── soloai_office/
│   ├── agents/
│   ├── processors/
│   ├── workflows/
│   ├── integrations/
│   └── utils/
├── tests/
├── requirements.txt
└── README.md
```

---

## Common Use Cases

- 自动生成会议纪要、周报、日报
- 批量处理合同、发票、简历、制度文档
- Excel 数据清洗、分析与智能标注
- AI 邮件草拟、客户跟进、内部通知生成
- 企业知识库信息提取与摘要
- 人事、财务、运营等重复性办公流程自动化

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

4. Push to your branch

```bash
git push origin feat/your-feature-name
```

5. Open a Pull Request

### Contribution guidelines

- Follow PEP 8 style guidelines
- Add tests for new features and bug fixes
- Keep pull requests focused and well-documented
- Update documentation when behavior changes
- Use clear commit messages following conventional commits where possible

### Run tests

```bash
pytest -q
```

---

## Roadmap

- [ ] OCR support for scanned office documents
- [ ] Enterprise SSO integrations
- [ ] Visual workflow builder
- [ ] RPA connector support
- [ ] Multi-language template library
- [ ] Fine-tuned vertical office agents

---

## License

This project is licensed under the **MIT License**. See the [LICENSE](./LICENSE) file for details.

---

## Business Inquiry

For enterprise collaboration, custom AI automation solutions, consulting, or technical partnerships, please contact:

**379744050@qq.com**

### Fast Proposal CTA

To receive a fast and accurate proposal, please send the following details by email:

- **Industry**
- **Deliverables**
- **Budget range**
- **Deadline**

The more specific your requirements are, the faster SoloAI can evaluate feasibility and provide a professional solution recommendation.

---

## SEO / AI Search Keywords

**Python AI 自动化办公**, **AI office automation**, **Python办公自动化**, **LLM workflow automation**, **AI document processing**, **Excel automation with AI**, **enterprise productivity automation**, **智能办公系统**, **AI 报表生成**, **office workflow orchestration**

---

## Star This Project

If this project helps your team build smarter office automation workflows, please consider giving it a **Star** on GitHub and sharing it with others.