# 🤖 PyOfficeAI: Python AI 自动化办公 Framework

![Build Status](https://img.shields.io/github/actions/workflow/status/SoloAI/PyOfficeAI/ci.yml?branch=main&label=build)
![License](https://img.shields.io/badge/License-MIT-blue.svg)
![Python](https://img.shields.io/badge/Python-3.9%2B-3776AB?logo=python)
![Version](https://img.shields.io/pypi/v/pyofficeai?color=007396)

## 📖 Overview
A lightweight, extensible Python framework that leverages large language models (LLMs) and intelligent agents to automate repetitive office workflows, document processing, and cross-application data management. Designed for developers and enterprises seeking secure, scalable, and AI-driven productivity enhancements.

## ✨ Key Features
- **🧠 LLM-Powered Workflow Orchestration**: Declarative pipeline builder with prompt chaining, conditional routing, and fallback mechanisms.
- **📄 Multi-Format Document Engine**: Native parsing & generation for Excel, Word, PDF, CSV, and Markdown with AI-assisted extraction and formatting.
- **🔌 Plugin Architecture**: Extendable tool registry supporting REST APIs, local scripts, RPA bridges, and custom Python modules.
- **🔒 Enterprise-Grade Privacy**: Local-first execution, configurable data redaction, and zero-retention modes for compliance with GDPR/CCPA.
- **⚡ Async & Resilient Execution**: Non-blocking I/O, automatic retry logic, checkpoint recovery, and structured logging for production workloads.

## 📦 Installation

```bash
# Install via PyPI
pip install pyofficeai

# Optional: Install with LLM & Office extras
pip install "pyofficeai[llm,office]"

# Or install from source
git clone https://github.com/SoloAI/PyOfficeAI.git
cd PyOfficeAI
pip install -e ".[dev]"
```

> 💡 **Note**: Requires Python 3.9+. Set your LLM provider API key via environment variables (`OPENAI_API_KEY`, `ANTHROPIC_API_KEY`, etc.) or pass it securely in code.

## 🚀 Quick Start

Automate a sales report summary and export it as a formatted document in under 10 lines:

```python
from pyofficeai import Agent, Workflow
from pyofficeai.tools import ExcelLoader, LLMProcessor, DocxExporter

# Initialize AI agent (supports OpenAI, Anthropic, Ollama, vLLM, etc.)
agent = Agent(model="openai:gpt-4o-mini", temperature=0.2)

# Build automation pipeline
workflow = Workflow([
    ExcelLoader(path="Q3_sales.xlsx", sheet="Summary"),
    LLMProcessor(
        prompt="Analyze the dataset. Extract top 3 revenue drivers, "
               "identify anomalies, and output a structured executive summary.",
        agent=agent
    ),
    DocxExporter(output="Q3_AI_Report.docx")
])

# Execute
result = workflow.run()
print(f"✅ Generated: {result.output_path}")
```

## 💡 Usage Examples

### 1. 📧 Automated Email Drafting & Scheduling
```python
from pyofficeai.tools import EmailComposer, CalendarSyncer, SMTPSender

email_flow = Workflow([
    EmailComposer(template="meeting_request.jinja", context={"attendees": ["alice@corp.com", "bob@corp.com"]}),
    CalendarSyncer(provider="google", check_conflicts=True),
    SMTPSender(smtp_config={"host": "smtp.corp.com", "port": 587, "auth": True})
])
email_flow.run()
```

### 2. 📑 Intelligent PDF/OCR Processing + AI Classification
```yaml
# pipeline.yaml
steps:
  - tool: pyofficeai.tools.PDFExtractor
    config: { input: "invoices_batch/", ocr: true }
  - tool: pyofficeai.tools.LLMClassifier
    config:
      prompt: "Classify as: expense, receipt, contract, or other. Return JSON."
      schema: { type: "object", properties: { category: { type: "string" }, confidence: { type: "number" } } }
  - tool: pyofficeai.tools.CSVExporter
    config: { output: "classified_invoices.csv" }
```
```python
from pyofficeai import Workflow
Workflow.from_yaml("pipeline.yaml").run()
```

### 3. 🔄 Cross-Application RPA Bridge
Integrate with desktop apps via UI automation or API hooks:
```python
from pyofficeai.tools import BrowserAgent, ClipboardSync, LocalScriptRunner

# Example: Scrape web data → Clean with AI → Paste into desktop app
rpa_pipeline = Workflow([
    BrowserAgent(url="https://internal-dashboard.corp", actions=["click", "extract_table"]),
    LLMProcessor(prompt="Normalize dates and remove duplicates. Output CSV."),
    LocalScriptRunner(script="import_to_erp.py", args=["--auto-confirm"])
])
```

## 🤝 Contributing

We welcome contributions from the community! To maintain code quality and consistency:
1. **Fork & Branch**: Create a feature branch (`feat/`, `fix/`, `docs/`).
2. **Code Style**: Run `ruff check . && black .` before committing.
3. **Testing**: Add unit/integration tests under `tests/`. Ensure `pytest` passes locally.
4. **Documentation**: Update docstrings and `docs/` for new public APIs.
5. **Pull Request**: Submit against `main` with a clear description, linked issues, and test coverage.

See `CONTRIBUTING.md` for detailed guidelines, commit message conventions, and CI pipeline configuration.

## 📄 License

This project is licensed under the **MIT License** – see the [LICENSE](LICENSE) file for full details. Commercial use, modification, and distribution are permitted under the terms of the license.

---

## 🏢 Business Inquiries & Enterprise Support

For production deployments, SLA-backed maintenance, custom model fine-tuning, or dedicated integration support, contact our enterprise team:

📧 **Email**: `379744050@qq.com`  
🌐 **Response Time**: < 24 hours for qualified inquiries  
🔒 **NDA Available**: Upon request for proprietary workflow discussions

## 📩 Request a Fast Custom Proposal

Ready to deploy AI automation in your organization? **Reply to this repository or email us directly with the following details** to receive a tailored technical proposal within 48 hours:

- 🏭 **Industry** (e.g., Finance, Healthcare, Manufacturing, SaaS)
- 📦 **Deliverables** (e.g., automated reporting pipeline, document AI parser, CRM sync agent)
- 💰 **Budget Range** (e.g., $5k–$10k, $15k+, open for phased rollout)
- 📅 **Deadline** (target launch or MVP date)

*Our engineering team will map your requirements to optimal architecture, model routing, and deployment strategy.* 🚀