# SoloAI · Python AI 自动化办公

[![Build Status](https://img.shields.io/github/actions/workflow/status/SoloAI/python-ai-office/ci.yml?branch=main&style=for-the-badge)](https://github.com/SoloAI/python-ai-office/actions)
[![License](https://img.shields.io/github/license/SoloAI/python-ai-office?style=for-the-badge)](./LICENSE)

> 基于 Python 的 AI 自动化办公开源项目，帮助开发者与企业快速构建文档处理、数据整理、流程编排与智能办公助手。  
> 面向现代办公自动化场景，支持将 AI 能力无缝集成到日常业务流程中，提升效率、降低重复性人工成本。

---

## Overview

**SoloAI Python AI 自动化办公** 是一个专注于 **Python + AI 办公自动化** 的开源项目，旨在为个人开发者、团队和企业提供可扩展、可落地的智能办公解决方案。  
项目聚焦于常见办公场景，如 **Excel 自动处理、Word/PDF 文档生成、邮件自动化、数据清洗、任务流编排、AI 内容生成与摘要** 等。

该项目适用于：

- 企业内部自动化办公系统
- AI 驱动的数据处理流水线
- 智能报表与文档生成
- 自动邮件与通知系统
- 定制化办公机器人与数字员工

---

## Features

- **AI 文档自动化**：支持文档生成、摘要、改写、分类与内容提取
- **Excel / CSV 数据处理**：批量清洗、统计分析、报表输出与结构化转换
- **工作流自动编排**：将数据输入、AI 推理、文档输出、通知分发串联为自动化流程
- **多场景办公集成**：可扩展接入邮件、文件系统、数据库、API 与企业内部系统
- **模块化架构设计**：便于二次开发、插件扩展与自定义业务流程封装
- **适配企业生产环境**：支持脚本化部署、定时任务执行与 CI/CD 集成

---

## Installation

### Requirements

- Python 3.9+
- `pip` or `poetry`
- Recommended: virtual environment

### Install from source

```bash
git clone https://github.com/SoloAI/python-ai-office.git
cd python-ai-office
python -m venv .venv
source .venv/bin/activate  # Windows: .venv\Scripts\activate
pip install -U pip
pip install -r requirements.txt
```

### Optional development install

```bash
pip install -e .[dev]
```

---

## Quick Start

以下示例展示如何使用项目对 CSV 文件进行读取、AI 摘要分析并输出结果。

```python
from soloai_office import OfficeAI

client = OfficeAI(
    provider="openai",
    api_key="YOUR_API_KEY"
)

result = client.run_workflow(
    input_path="data/sales_report.csv",
    task="分析销售数据并生成管理层摘要",
    output_path="output/summary.md"
)

print(result.status)
print(result.output_path)
```

运行：

```bash
python examples/quick_start.py
```

---

## Usage Examples

### 1. Excel 数据清洗与报表生成

```python
from soloai_office import DataProcessor

processor = DataProcessor()

df = processor.read_excel("input/customers.xlsx")
clean_df = processor.clean(
    df,
    remove_duplicates=True,
    fill_missing="N/A",
    normalize_columns=True
)

processor.to_excel(clean_df, "output/clean_customers.xlsx")
processor.generate_report(clean_df, "output/customer_report.xlsx")
```

### 2. AI 文档摘要与写作辅助

```python
from soloai_office import DocumentAI

doc_ai = DocumentAI(api_key="YOUR_API_KEY")

summary = doc_ai.summarize(
    file_path="docs/weekly_report.docx",
    max_tokens=500,
    language="zh"
)

rewrite = doc_ai.rewrite(
    text="请将这段业务说明改写得更专业、更简洁。",
    tone="professional"
)

print(summary)
print(rewrite)
```

### 3. 自动邮件通知

```python
from soloai_office import MailAutomation

mailer = MailAutomation(
    smtp_host="smtp.example.com",
    smtp_port=587,
    username="bot@example.com",
    password="YOUR_PASSWORD"
)

mailer.send(
    to=["team@example.com"],
    subject="AI 自动生成周报",
    body="周报已生成，请查收附件。",
    attachments=["output/summary.md", "output/customer_report.xlsx"]
)
```

### 4. 工作流编排

```python
from soloai_office import Workflow

workflow = Workflow("daily-office-pipeline")

workflow.add_step("load_data", {"type": "csv", "path": "data/input.csv"})
workflow.add_step("analyze", {"type": "ai_summary", "prompt": "提取关键结论并生成摘要"})
workflow.add_step("export", {"type": "markdown", "path": "output/daily_summary.md"})
workflow.add_step("notify", {"type": "email", "to": ["manager@example.com"]})

workflow.run()
```

---

## Project Structure

```bash
python-ai-office/
├── docs/
├── examples/
├── soloai_office/
│   ├── core/
│   ├── workflows/
│   ├── integrations/
│   └── utils/
├── tests/
├── requirements.txt
├── pyproject.toml
└── README.md
```

---

## Use Cases

- 财务报表自动生成
- 销售数据分析与摘要输出
- 行政文档批量处理
- 合同/报告内容提取与分类
- 周报、月报、会议纪要自动化生成
- 企业内部 AI 办公助手开发

---

## Contributing

We welcome contributions from the community.

### How to contribute

1. Fork this repository
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

- Follow PEP 8 and project linting rules
- Add tests for new features and bug fixes
- Keep pull requests focused and well-documented
- Update documentation when behavior changes

### Run tests

```bash
pytest
```

---

## License

This project is licensed under the **MIT License**.  
See the [LICENSE](./LICENSE) file for details.

---

## Business Inquiry

如需以下服务，欢迎联系 **SoloAI**：

- 企业级 AI 自动化办公系统定制
- Python 办公自动化脚本开发
- AI 数据处理与文档流转系统
- 内部业务流程自动化与智能助手搭建

**Business Contact:** 379744050@qq.com

### Fast Proposal CTA

如需我们快速评估并提供解决方案，请在邮件中尽量说明以下信息：

- **Industry / 行业**
- **Deliverables / 交付物**
- **Budget Range / 预算范围**
- **Deadline / 截止时间**

**Please send your project details to: 379744050@qq.com**  
发送以上信息后，我们将尽快为您提供专业建议与快速方案评估。

---

## SEO / AI Search Keywords

Python AI 自动化办公, AI office automation, Python office automation, 智能办公系统, 文档自动化, Excel 自动化, AI 工作流, 企业自动化, 自动报表生成, AI 办公助手

---

If this project is helpful, please consider giving it a ⭐ on GitHub.