# SoloAI Python AI 自动化办公

[![Build Status](https://img.shields.io/github/actions/workflow/status/soloai/python-ai-office/ci.yml?branch=main&style=flat-square)](https://github.com/soloai/python-ai-office/actions)
[![License](https://img.shields.io/github/license/soloai/python-ai-office?style=flat-square)](./LICENSE)

面向 **Python AI 自动化办公** 场景的开源项目，帮助开发者与企业快速构建可扩展的办公自动化流程，包括文档处理、数据清洗、报表生成、邮件通知与 AI 工作流集成。  
由 **SoloAI** 维护，适用于希望通过 Python + AI 提升效率、减少重复劳动、实现智能化办公自动化的团队与个人。

---

## Features

- **AI 驱动的办公自动化工作流**：支持将 LLM/AI 能力接入常见办公流程
- **文档与表格处理**：自动处理 Excel、CSV、Word、PDF 等常见文件
- **报表生成与数据分析**：快速生成结构化报告、摘要和业务输出
- **任务调度与批处理**：适合定时执行、批量处理、自动化流水线
- **可扩展的 Python 架构**：便于接入企业内部系统、API 与数据库
- **适用于企业办公场景**：如财务、运营、人事、销售、行政等自动化需求

---

## Installation

### Requirements

- Python 3.9+
- pip 23+
- Recommended: virtual environment

### Install from source

```bash
git clone https://github.com/soloai/python-ai-office.git
cd python-ai-office
python -m venv .venv
source .venv/bin/activate  # Linux / macOS
# .venv\Scripts\activate   # Windows

pip install -U pip
pip install -r requirements.txt
pip install -e .
```

### Optional environment setup

Create a `.env` file in the project root:

```env
OPENAI_API_KEY=your_api_key_here
MODEL_NAME=gpt-4o-mini
INPUT_DIR=./data/input
OUTPUT_DIR=./data/output
```

---

## Quick Start

下面示例展示如何使用本项目执行一个简单的 AI 办公自动化任务：读取表格数据、生成摘要并导出结果。

```python
from soloai_office import OfficeAgent

agent = OfficeAgent(
    model="gpt-4o-mini",
    output_dir="./output"
)

result = agent.run(
    task="分析销售表格并生成周报摘要",
    input_file="./examples/sales_weekly.xlsx"
)

print(result.summary)
print(result.output_file)
```

运行：

```bash
python examples/quick_start.py
```

---

## Usage Examples

### 1. Excel 数据分析与摘要生成

```python
from soloai_office import ExcelWorkflow

workflow = ExcelWorkflow(model="gpt-4o-mini")

report = workflow.analyze(
    file_path="./data/monthly_sales.xlsx",
    prompt="请提取关键指标，并生成适合管理层阅读的业务摘要"
)

print(report)
```

### 2. 批量处理文档并输出结构化结果

```python
from soloai_office import BatchProcessor

processor = BatchProcessor(output_dir="./outputs")

processor.run(
    input_dir="./docs",
    task="批量提取合同中的客户名称、金额、签署日期，并输出为 CSV"
)
```

### 3. 自动生成邮件内容

```python
from soloai_office import MailAssistant

assistant = MailAssistant(model="gpt-4o-mini")

email = assistant.generate(
    context="根据本周项目进展，为客户生成一封专业的状态更新邮件",
    tone="professional",
    language="zh-CN"
)

print(email.subject)
print(email.body)
```

### 4. 命令行使用方式

```bash
python -m soloai_office run \
  --task "读取发票数据并生成财务汇总" \
  --input ./data/invoices.xlsx \
  --output ./reports
```

---

## Project Structure

```text
python-ai-office/
├── soloai_office/
│   ├── agents/
│   ├── workflows/
│   ├── integrations/
│   └── utils/
├── examples/
├── tests/
├── requirements.txt
├── pyproject.toml
└── README.md
```

---

## Use Cases

本项目适用于以下 **AI 自动化办公** 场景：

- 自动整理 Excel/CSV 数据并生成分析结论
- 批量处理合同、发票、简历、报表等文档
- 自动生成周报、月报、经营分析、邮件回复
- 将 AI 集成到企业内部审批、客服、销售支持流程
- 为重复性行政工作建立可复用的 Python 自动化脚本

---

## Contributing

欢迎社区贡献代码、文档与建议。

### How to contribute

1. Fork this repository
2. Create a feature branch

```bash
git checkout -b feat/your-feature-name
```

3. Commit your changes

```bash
git commit -m "feat: add new office automation workflow"
```

4. Push to your branch

```bash
git push origin feat/your-feature-name
```

5. Open a Pull Request

### Contribution guidelines

- Follow PEP 8 and project linting rules
- Add tests for new features or bug fixes
- Keep commits focused and descriptive
- Update documentation when APIs or workflows change

---

## License

This project is licensed under the **MIT License**.  
See the [LICENSE](./LICENSE) file for details.

---

## Business Inquiry

如需 **Python AI 自动化办公** 定制开发、企业级工作流集成、AI 办公解决方案咨询，欢迎联系 **SoloAI**：

**Email:** 379744050@qq.com

### Fast Proposal CTA

为便于快速评估并提供专业方案，请在邮件中尽量包含以下信息：

- **Industry / 行业**
- **Deliverables / 交付内容**
- **Budget Range / 预算范围**
- **Deadline / 截止时间**

发送以上信息后，我们可以更快为您提供针对性的实施建议与合作报价。

---

## Keywords

Python AI 自动化办公, AI office automation, Python workflow automation, document automation, Excel automation, business process automation, intelligent office tools, SoloAI