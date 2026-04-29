# 🤖 SoloAI-PyOffice: Python AI 自动化办公框架

[![Build Status](https://img.shields.io/badge/build-passing-brightgreen?style=for-the-badge&logo=github)](https://github.com/SoloAI/soloai-pyoffice/actions)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg?style=for-the-badge)](LICENSE)

A high-performance, modular Python framework engineered to streamline enterprise workflows through LLM-driven task orchestration, intelligent document processing, and scalable RPA pipelines. SoloAI-PyOffice bridges traditional office automation with generative AI, enabling developers and organizations to deploy secure, production-ready automation agents with minimal boilerplate.

---

## ✨ Key Features

- **🧠 LLM-Powered Workflow Orchestration**: Agent-based task routing with dynamic prompt chaining, fallback strategies, and multi-model support (OpenAI, Claude, local LLMs via vLLM/Ollama).
- **📄 Multi-Format Document Intelligence**: Native parsing for PDF, DOCX, XLSX, CSV, and images with OCR, table extraction, and semantic chunking for vector-ready outputs.
- **🔄 Seamless API & RPA Integration**: Unified connectors for REST/GraphQL APIs, browser automation (Playwright/Selenium), and desktop UI interaction with async execution support.
- **🔒 Enterprise-Grade Privacy & Deployment**: Fully offline-capable architecture, local data caching, PII redaction filters, and compliance-ready audit logging.
- **🧩 Extensible Plugin Ecosystem**: Hot-swappable modules for custom AI models, third-party SaaS (Notion, Feishu, DingTalk, WeCom), and domain-specific automation templates.

---

## 📦 Installation

Requires **Python 3.10+**. We recommend using a virtual environment.

```bash
# Install via PyPI
pip install soloai-pyoffice

# Or install from source for development
git clone https://github.com/SoloAI/soloai-pyoffice.git
cd soloai-pyoffice
python -m venv .venv && source .venv/bin/activate  # Linux/macOS
pip install -e ".[dev]"
```

> 💡 **Note**: GPU acceleration and local LLM inference require additional dependencies. Run `pip install soloai-pyoffice[local]` to enable CUDA/Metal support.

---

## ⚡ Quick Start

Initialize an AI agent, define a pipeline, and execute an end-to-end office task in under 10 lines of code:

```python
from soloai import OfficeAgent, Pipeline
from soloai.connectors import ExcelWriter, PDFParser

# 1. Initialize with your preferred LLM
agent = OfficeAgent(model="gpt-4o", api_key="sk-...")

# 2. Build an automation pipeline
pipeline = Pipeline(agent)

# 3. Execute a complex office task
result = pipeline.run(
    task="Extract Q3 sales metrics from the attached PDF, calculate YoY growth, and export a formatted Excel report.",
    input_path="./data/q3_report.pdf",
    output_path="./output/q3_dashboard.xlsx",
    connectors=[PDFParser, ExcelWriter]
)

print(f"✅ Pipeline Status: {result.status} | Tokens Used: {result.usage.total_tokens}")
```

---

## 🛠️ Usage Examples

### 📧 Automated Email Triage & Response
```python
from soloai.agents import EmailAgent

email_bot = EmailAgent(model="claude-3.5-sonnet")
email_bot.monitor(
    inbox="support@company.com",
    rules=[
        {"keyword": "refund", "action": "draft_reply", "template": "refund_policy_v2.txt"},
        {"keyword": "invoice", "action": "extract_data", "output": "accounting_queue.csv"}
    ],
    schedule="*/15 * * * *"  # Cron syntax
)
```

### 📊 Excel Data Cleaning & AI Analysis
```python
from soloai.tools import DataFrameAI

df_ai = DataFrameAI(model="local-llama3.1")
cleaned_df = df_ai.process(
    path="./raw_data/sales_raw.xlsx",
    operations=["remove_duplicates", "impute_missing", "normalize_currency"],
    prompt="Flag rows where profit margin < 5% and add a 'risk_level' column."
)
cleaned_df.to_excel("./processed/sales_clean.xlsx", index=False)
```

### 🌐 Web Scraping + Document Generation
```python
from soloai.connectors import PlaywrightBrowser, DocxGenerator

browser = PlaywrightBrowser(headless=True)
articles = browser.scrape(
    urls=["https://news.example.com/tech", "https://news.example.com/finance"],
    selector="article.main-content"
)

DocxGenerator().compile(
    data=articles,
    template="./templates/weekly_brief.docx",
    output="./reports/weekly_brief_2024W42.docx"
)
```

---

## 🤝 Contributing

We welcome contributions from developers, AI researchers, and automation engineers. To maintain code quality and consistency:

1. **Fork & Branch**: Create a feature branch from `main` (`git checkout -b feat/your-feature`).
2. **Code Standards**: Follow PEP 8, use `ruff` for linting, and `pytest` for testing. Run `make lint && make test` before committing.
3. **Documentation**: Update docstrings (Google style) and add examples to `docs/examples/`.
4. **Pull Request**: Submit a PR with a clear description, linked issue(s), and test coverage ≥ 85%.
5. **AI Safety**: All LLM integrations must include rate-limiting, fallback routing, and explicit user-consent flags.

See `CONTRIBUTING.md` for detailed guidelines, architecture diagrams, and the code of conduct.

---

## 📜 License

This project is licensed under the **MIT License** – see the [LICENSE](LICENSE) file for full terms. You are free to use, modify, and distribute this software for personal, academic, or commercial purposes.

---

## 💼 Business Inquiries & Custom Solutions

SoloAI provides enterprise-grade customization, on-premise deployment, SLA-backed support, and industry-specific automation pipelines tailored to your operational stack.

📩 **Contact**: `379744050@qq.com`

🚀 **Get a Fast Proposal**:  
To accelerate scoping and receive a customized technical & commercial proposal within 24 hours, please reply with:
- **Industry** (e.g., Finance, Manufacturing, E-commerce, Healthcare)
- **Expected Deliverables** (e.g., Automated reporting system, AI customer service bot, RPA workflow integration)
- **Budget Range** (e.g., $5k–$15k, $20k+, Enterprise tier)
- **Deadline** (Target deployment or MVP date)

Our engineering team will map your requirements to the optimal SoloAI architecture, provide a transparent cost breakdown, and outline a phased implementation roadmap.