# SoloAI | Python AI 自动化办公 🤖📄
[![Build Status](https://img.shields.io/github/actions/workflow/status/SoloAI/python-ai-automation/ci.yml?branch=main&label=Build)](https://github.com/SoloAI/python-ai-automation/actions)
[![License](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![Python 3.9+](https://img.shields.io/badge/Python-3.9%2B-3776AB.svg)](https://www.python.org/downloads/)
[![PyPI](https://img.shields.io/pypi/v/soloai-automation.svg)](https://pypi.org/project/soloai-automation/)

**SoloAI-Python-Automation** is an open-source, LLM-driven framework that unifies intelligent document processing, workflow orchestration, and enterprise RPA into a single Python-native ecosystem. Built for developers and operations teams, it enables rapid deployment of scalable AI automation pipelines with minimal boilerplate.

---

## ✨ Key Features
- 🧠 **LLM-Powered Document Intelligence**: Native parsing of PDF, Excel, Word, and scanned images with structured data extraction, table recognition, and semantic summarization.
- ⚡ **Declarative Workflow Orchestration**: Define multi-step automation pipelines using YAML/JSON or Python DSL with built-in retry, caching, and error-handling logic.
- 🔄 **Cross-Platform RPA Integration**: Pre-built connectors for email (SMTP/IMAP), web scraping, cloud storage (S3/OSS), and REST/GraphQL APIs.
- 🛡️ **Enterprise-Ready Security**: Supports local model deployment (Ollama, vLLM), data anonymization, audit logging, and role-based access control.
- 📊 **Automated Reporting & Analytics**: Seamless integration with `pandas`, `openpyxl`, and `matplotlib` to generate AI-augmented dashboards and executive summaries.
- 🔌 **Extensible Plugin Architecture**: Register custom agents, tools, and middleware via a standardized `@tool` decorator system.

---

## 📦 Installation
```bash
# Install via pip (recommended)
pip install soloai-automation

# Or install from source
git clone https://github.com/SoloAI/python-ai-automation.git
cd python-ai-automation
python -m venv .venv && source .venv/bin/activate  # Linux/macOS
pip install -r requirements.txt
```

> 💡 **Note**: Set your LLM provider key as an environment variable:
> `export OPENAI_API_KEY="your-key-here"` or `export QWEN_API_KEY="your-key-here"`

---

## 🚀 Quick Start
```python
from soloai import Agent, Workflow, DocumentParser

# Initialize AI agent (supports OpenAI, Claude, Qwen, local models)
agent = Agent(model="gpt-4o", temperature=0.2)

# Build a 3-step office automation pipeline
workflow = Workflow(name="InvoiceProcessor")
workflow.add_step("extract", DocumentParser.parse_tables("invoices/Q3_2024.pdf"))
workflow.add_step("validate", agent.evaluate_schema(schema="finance_v2"))
workflow.add_step("export", lambda df: df.to_csv("output/validated_invoices.csv", index=False))

# Execute pipeline
result = workflow.run()
print(f"✅ Processed {len(result)} records successfully.")
```

---

## 📖 Usage Examples

### 1. Smart Email Triage & Auto-Reply
```python
from soloai.tools import EmailClient, TextClassifier

client = EmailClient(host="smtp.company.com", credentials="auto")
classifier = TextClassifier(model="gpt-4o-mini", labels=["urgent", "billing", "support", "newsletter"])

for email in client.fetch_unread():
    tag = classifier.predict(email.body)
    if tag == "urgent":
        client.reply(email.id, template="templates/urgent_ack.txt")
    elif tag == "billing":
        workflow = Workflow.from_yaml("pipelines/billing_triage.yaml")
        workflow.run(data=email)
```

### 2. Cross-App Data Sync (Excel → CRM)
```yaml
# pipelines/sync_to_crm.yaml
steps:
  - name: load_excel
    tool: soloai.tools.ExcelLoader
    args: { path: "leads/weekly_import.xlsx" }
  - name: clean_data
    tool: soloai.tools.DataCleaner
    args: { drop_na: true, standardize_phone: true }
  - name: push_crm
    tool: soloai.tools.CRMAPI
    args: { endpoint: "https://api.crm.com/v1/contacts", batch_size: 50 }
```
```bash
soloai run pipelines/sync_to_crm.yaml --env .env.production
```

---

## 🤝 Contributing
We welcome community contributions to improve AI automation capabilities for developers and enterprises.

1. **Fork** the repository and create your feature branch:  
   `git checkout -b feat/your-feature-name`
2. **Commit** changes using [Conventional Commits](https://www.conventionalcommits.org/):  
   `git commit -m "feat: add OCR fallback for low-res scans"`
3. **Push** and open a Pull Request against the `main` branch.
4. Ensure all tests pass: `pytest tests/ -v` and run linting: `ruff check .`

Please review our [Contributing Guide](CONTRIBUTING.md) and [Code of Conduct](CODE_OF_CONDUCT.md) before submitting.

---

## 💼 Business Inquiries & Custom Solutions
For commercial licensing, enterprise deployment, dedicated AI agent training, or custom workflow development, contact our engineering team:

📧 **Email:** `379744050@qq.com`

🚀 **Need a tailored solution?** Reply with the following details for a fast, customized proposal:
- **Industry / Use Case**
- **Expected Deliverables**
- **Budget Range**
- **Project Deadline**

Our AI solutions architects will respond within 24 hours with a technical architecture, implementation roadmap, and transparent pricing.

---

## 📜 License
Distributed under the MIT License. See [`LICENSE`](LICENSE) for full terms.  
© 2024 SoloAI. All rights reserved.