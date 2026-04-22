# SoloAI Python AI 自动化办公

[![Build Status](https://img.shields.io/github/actions/workflow/status/SoloAI/python-ai-office/ci.yml?branch=main&style=flat-square)](https://github.com/SoloAI/python-ai-office/actions)
[![License](https://img.shields.io/github/license/SoloAI/python-ai-office?style=flat-square)](./LICENSE)

> An open-source Python framework for AI-powered office automation, designed to streamline document processing, spreadsheet workflows, email tasks, and business operations with extensible automation pipelines.

**SoloAI Python AI 自动化办公** helps developers and teams build intelligent office automation solutions using Python, AI models, and workflow integrations for modern productivity environments.

---

## Features

- **AI 文档自动化**: Parse, summarize, classify, and generate Word, PDF, and text-based office documents.
- **Excel / 表格智能处理**: Automate spreadsheet analysis, report generation, data cleaning, and KPI summarization.
- **邮件与消息自动化**: Trigger AI-assisted email drafting, routing, notifications, and office workflow alerts.
- **可扩展工作流引擎**: Build custom automation pipelines with modular Python components and AI service integrations.
- **多场景办公集成**: Connect with common office systems, APIs, databases, and internal enterprise tools.
- **开发者友好**: Clean Python APIs, CLI support, configuration-based execution, and easy deployment.

---

## Installation

### Requirements

- Python 3.9+
- `pip` or `poetry`
- Optional: API key for your preferred AI provider

### Install from PyPI

```bash
pip install soloai-office
```

### Install from source

```bash
git clone https://github.com/SoloAI/python-ai-office.git
cd python-ai-office
pip install -e .
```

### Optional dependencies

```bash
pip install "soloai-office[excel,email,pdf]"
```

---

## Quick Start

```python
from soloai_office import OfficeAgent

agent = OfficeAgent(
    provider="openai",
    api_key="YOUR_API_KEY"
)

result = agent.run(
    task="读取 sales_report.xlsx，生成本周销售总结，并输出为 markdown 文件"
)

print(result.output_text)
print(result.output_path)
```

Run from CLI:

```bash
soloai-office run \
  --task "读取 contracts 文件夹中的 PDF，提取关键信息并汇总到 Excel" \
  --provider openai
```

---

## Usage Examples

### 1. Intelligent Excel Analysis

```python
from soloai_office import ExcelAutomation

excel = ExcelAutomation()
report = excel.analyze(
    file_path="data/monthly_sales.xlsx",
    prompt="识别异常销售数据，生成管理层摘要，并输出图表建议"
)

print(report.summary)
```

### 2. Document Summarization and Extraction

```python
from soloai_office import DocumentAutomation

docs = DocumentAutomation()
result = docs.process(
    input_path="docs/contracts/",
    actions=["extract_entities", "summarize", "classify"],
    output_format="json"
)

print(result)
```

### 3. AI Email Drafting

```python
from soloai_office import EmailAutomation

mailer = EmailAutomation(provider="openai", api_key="YOUR_API_KEY")
draft = mailer.generate_reply(
    subject="Project Status Update",
    context="客户希望了解当前项目交付进度以及下阶段计划。",
    tone="professional"
)

print(draft.body)
```

### 4. Workflow Pipeline Automation

```python
from soloai_office import Workflow

workflow = Workflow(name="daily-office-automation")

workflow.add_step("load_excel", file="input/tasks.xlsx")
workflow.add_step("summarize_tasks", ai_prompt="汇总今日待办并按优先级分类")
workflow.add_step("draft_email", template="daily_summary")
workflow.add_step("export_report", format="pdf")

result = workflow.execute()
print(result.status)
```

---

## Project Structure

```text
python-ai-office/
├── soloai_office/
│   ├── agents/
│   ├── automation/
│   ├── integrations/
│   ├── workflows/
│   └── cli/
├── examples/
├── tests/
├── docs/
├── README.md
└── pyproject.toml
```

---

## Configuration

You can configure the project using environment variables:

```bash
export SOLOAI_PROVIDER=openai
export SOLOAI_API_KEY=your_api_key
export SOLOAI_LOG_LEVEL=INFO
```

Example `.env` file:

```env
SOLOAI_PROVIDER=openai
SOLOAI_API_KEY=your_api_key
SOLOAI_OUTPUT_DIR=./outputs
```

---

## Contributing

Contributions are welcome from the open-source community.

### How to contribute

1. Fork the repository
2. Create a feature branch

```bash
git checkout -b feat/your-feature-name
```

3. Install development dependencies

```bash
pip install -e ".[dev]"
```

4. Run tests

```bash
pytest
```

5. Run formatting and linting

```bash
ruff check .
black .
```

6. Commit your changes

```bash
git commit -m "feat: add new office automation module"
```

7. Push and open a Pull Request

### Contribution guidelines

- Follow PEP 8 and project linting rules
- Add tests for new features and bug fixes
- Keep PRs focused and well-documented
- Update documentation and examples when needed

---

## License

This project is licensed under the **MIT License**. See the [LICENSE](./LICENSE) file for details.

---

## Keywords

Python AI 自动化办公, office automation, AI workflow automation, intelligent document processing, Excel automation, email automation, enterprise productivity, Python automation framework, AI agent for office tasks

---

## Maintainer

Developed and maintained by **SoloAI**.