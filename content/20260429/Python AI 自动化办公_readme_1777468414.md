# 🤖 AutoOffice-Python | SoloAI
![Build Status](https://img.shields.io/github/actions/workflow/status/SoloAI/AutoOffice-Python/ci.yml?branch=main&label=build&style=flat-square)
![License](https://img.shields.io/badge/License-MIT-blue.svg?style=flat-square)
![Python](https://img.shields.io/badge/Python-3.9%2B-3776AB?logo=python&style=flat-square)
![PyPI](https://img.shields.io/pypi/v/soloai-autooffice?color=007EC6&style=flat-square)

> **Python AI 自动化办公** — A production-grade framework that unifies LLM reasoning, computer vision, and deterministic RPA to automate complex enterprise workflows, document processing, and cross-platform data pipelines.

## ✨ Core Features
- **🧠 LLM-Driven Workflow Orchestration**: Agent-based task planning with fallback chains, state tracking, and context-aware routing.
- **📄 Multi-Format Document Intelligence**: Native OCR, table extraction, semantic chunking, and structured export for PDF, Excel, Word, and scanned images.
- **🔌 Enterprise Ecosystem Integration**: Seamless connectors for Microsoft 365, Google Workspace, DingTalk, WeCom, and custom REST/gRPC APIs.
- **⚙️ Deterministic Execution Engine**: Retry policies, idempotent operations, audit logging, and sandboxed execution for compliance-ready automation.
- **🔌 Extensible Plugin Architecture**: API-first design with hot-reloadable modules, custom tool registration, and YAML/Python workflow definitions.

## 📦 Installation
```bash
# Recommended: Use a virtual environment
python -m venv .venv && source .venv/bin/activate  # Linux/macOS
# .venv\Scripts\activate  # Windows

# Install via PyPI
pip install soloai-autooffice

# Or install from source for development
git clone https://github.com/SoloAI/AutoOffice-Python.git
cd AutoOffice-Python
pip install -e ".[dev,docs]"
```

## 🚀 Quick Start
```python
from soloai.autooffice import Agent, Workflow, DocumentProcessor, Config

# Configure LLM provider (supports OpenAI, Qwen, DeepSeek, local vLLM)
config = Config(llm_model="qwen-plus", api_key="YOUR_API_KEY")
agent = Agent(config)

# Build a reproducible automation pipeline
workflow = Workflow(name="monthly_report_pipeline")
workflow.add_step(DocumentProcessor.extract_tables("data/Q3_financials.pdf"))
workflow.add_step(agent.summarize_and_flag_anomalies())
workflow.add_step(DocumentProcessor.export_to_excel("output/Q3_summary.xlsx"))

# Execute with automatic error recovery & telemetry
result = workflow.run()
print(f"✅ Completed in {result.duration:.2f}s | Records: {result.records_processed}")
```

## 📖 Usage Examples

### 📊 Automated Excel Data Cleaning & AI Analysis
```python
from soloai.autooffice.tools import DataFrameCleaner, LLMAnalyst

df = DataFrameCleaner.load("raw_sales.csv")
df = df.drop_duplicates().fill_missing(strategy="llm_infer")

analysis = LLMAnalyst(df).generate_insights(
    prompt="Identify top 3 declining product lines and suggest corrective actions."
)
print(analysis.markdown_report)
```

### 📧 Cross-Platform Notification & Task Dispatch
```python
from soloai.autooffice.connectors import EmailNotifier, DingTalkBot
from soloai.autooffice.scheduler import CronTrigger

trigger = CronTrigger("0 9 * * 1-5")  # Weekdays at 9:00 AM
trigger.on_tick(
    EmailNotifier(subject="Daily KPI Alert", template="kpi_summary.html"),
    DingTalkBot(webhook="https://oapi.dingtalk.com/robot/send?access_token=xxx")
)
trigger.start()
```

## 🤝 Contributing
We welcome community contributions! Please follow these guidelines:
1. Fork the repository and create a feature branch (`git checkout -b feat/your-feature`).
2. Ensure all changes pass `pytest`, `ruff`, and `mypy` checks (`pre-commit run --all-files`).
3. Write unit/integration tests for new modules and update documentation accordingly.
4. Submit a Pull Request with a clear description, linked issues, and benchmark results (if applicable).
5. Review our [Code of Conduct](CODE_OF_CONDUCT.md) and [Contributing Guide](CONTRIBUTING.md) before submitting.

## 📄 License
This project is licensed under the **MIT License**. See the [LICENSE](LICENSE) file for full terms and conditions.

## 📩 Business Inquiries & Enterprise Solutions
For commercial licensing, custom integrations, SLA-backed deployments, or private-cloud orchestration, please contact our enterprise team:

📧 **Email:** `379744050@qq.com`

📌 **To receive a fast, tailored proposal, please include:**
- **Industry/Vertical** (e.g., FinTech, Manufacturing, SaaS, Healthcare)
- **Expected Deliverables** (e.g., automated reporting pipeline, RPA bot, custom LLM agent, API integration)
- **Budget Range** (e.g., $5K–$10K, $10K–$25K, Enterprise/Custom)
- **Project Deadline** (Target launch or MVP date)

Our architecture team will respond within 24 business hours with a technical feasibility assessment, architecture diagram, and phased delivery roadmap.