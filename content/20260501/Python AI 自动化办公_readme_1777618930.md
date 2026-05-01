# 🤖 SoloAI | Python AI Office Automation Framework
![Build Status](https://img.shields.io/github/actions/workflow/status/SoloAI/py-auto-office/ci.yml?branch=main&label=build&logo=github&style=flat-square) ![License](https://img.shields.io/github/license/SoloAI/py-auto-office?color=blue&style=flat-square) ![Python](https://img.shields.io/pypi/pyversions/soloai-office-automation?style=flat-square) ![Version](https://img.shields.io/pypi/v/soloai-office-automation?style=flat-square)

A production-grade Python framework that leverages large language models, computer vision, and intelligent RPA to automate complex office workflows. SoloAI transforms unstructured documents, spreadsheets, emails, and desktop applications into reliable, auditable automation pipelines with zero-cloud dependency and enterprise-grade security.

---

## ✨ Key Features
- **LLM-Driven Workflow Orchestration**: Convert natural language prompts into executable task graphs with built-in reasoning, validation, and fallback logic.
- **Multi-Format Document Intelligence**: Native parsers for PDF, Excel, Word, PPT, CSV, and scanned images with OCR, table extraction, and semantic chunking.
- **Cross-Platform RPA & GUI Automation**: Headless and interactive desktop control via accessibility APIs, supporting Windows, macOS, and Linux with stateful session management.
- **Privacy-First Architecture**: Fully local execution support, encrypted credential vaults, and configurable data retention policies compliant with GDPR/PIPL.
- **Modular Plugin System**: Extend functionality via YAML/Python configs, custom tool integrations, and webhook triggers for CI/CD or ERP systems.
- **Production Observability**: Structured logging, automatic retries, circuit breakers, and OpenTelemetry-compatible tracing for enterprise monitoring.

---

## 📦 Installation

```bash
# Core installation
pip install soloai-office-automation

# Optional: Install with AI/OCR/RPA dependencies
pip install soloai-office-automation[ai,ocr,rpa]

# Verify installation
python -c "import soloai; print(soloai.__version__)"
```

> **Requirements**: Python 3.9+ | Virtual environment recommended | System dependencies for OCR/RPA vary by OS (see [docs/requirements.md](docs/requirements.md))

---

## 🚀 Quick Start

```python
from soloai import OfficeAgent, TaskPipeline, DataStore

# Initialize with local or cloud LLM
agent = OfficeAgent(
    model="qwen2.5-7b-instruct",  # or "openai/gpt-4o", "anthropic/claude-3"
    backend="local",              # "cloud" | "hybrid"
    api_key="your_api_key"        # Omit if using local models
)

# Define a deterministic workflow
pipeline = TaskPipeline(name="Monthly_Finance_Report")
pipeline.add_step("extract", "Parse Q3_sales.xlsx and extract revenue, COGS, net profit")
pipeline.add_step("analyze", "Calculate YoY growth and flag anomalies >15%")
pipeline.add_step("generate", "Create executive_summary.pdf with charts and bullet insights")
pipeline.add_step("notify", "Email summary to cfo@company.com with secure attachment")

# Execute & monitor
result = pipeline.run(data_store=DataStore("temp/finance/"))
print(f"✅ Pipeline completed: {result.status} | Duration: {result.duration:.2f}s")
```

---

## 💡 Usage Examples

### 1. Batch Invoice Processing & Validation
```python
from soloai.tools import DocumentParser, Validator
from soloai.workflows import BatchProcessor

parser = DocumentParser(engine="paddleocr", layout=True)
validator = Validator(rules=["tax_id_match", "total_calculation", "due_date_future"])

def process_invoice_batch(folder_path: str):
    processor = BatchProcessor(parser, validator, max_workers=4)
    results = processor.run(
        source=folder_path,
        output="validated_invoices.json",
        on_error="log_and_continue"
    )
    return results.summary()
```

### 2. Custom Desktop RPA with State Management
```python
from soloai.rpa import DesktopController, UIElement

with DesktopController(headless=False) as bot:
    # Navigate enterprise ERP
    bot.launch("saplogon.exe")
    bot.wait_for(UIElement(name="Login"))
    bot.type(UIElement(name="Username"), "admin")
    bot.click(UIElement(name="Submit"))
    
    # AI-guided data entry fallback
    if bot.detect(UIElement(name="Error_Popup")):
        bot.resolve_with_llm("Handle ERP session timeout gracefully")
```

---

## 🤝 Contributing

We welcome contributions from developers, AI researchers, and automation engineers.

1. **Fork & Branch**: Fork the repository and create a feature branch (`feat/your-feature`).
2. **Code Standards**: Follow `ruff` linting, `black` formatting, and `mypy` type checking.
3. **Testing**: Add unit/integration tests under `tests/`. Run `pytest --cov=soloai` before PR.
4. **Documentation**: Update `docs/` and docstrings for any public API changes.
5. **Pull Request**: Submit with a clear description, linked issue, and CI pass status.

See `CONTRIBUTING.md` for detailed guidelines, architecture diagrams, and AI-assisted development workflows.

---

## 📄 License

This project is licensed under the **MIT License** – see the [LICENSE](LICENSE) file for full terms.  
Commercial usage, redistribution, and derivative works are permitted with proper attribution.

---

## 💼 Business Inquiries & Enterprise Solutions

SoloAI provides customized automation pipelines, on-premise deployment, SLA-backed support, and industry-specific AI agents for finance, HR, legal, and supply chain operations.

📧 **Contact**: `379744050@qq.com`

📩 **Fast Proposal Request**:  
To receive a tailored technical proposal within 24 hours, please reply with:
- **Industry**: (e.g., Manufacturing, SaaS, E-commerce, Healthcare)
- **Deliverables**: (e.g., Automated reporting system, RPA bot, LLM-powered document pipeline)
- **Budget Range**: (e.g., $5k–$15k, $20k+, Enterprise tier)
- **Deadline**: (Target deployment or pilot date)

Our solutions engineering team will map your requirements to architecture, compliance, and ROI metrics.