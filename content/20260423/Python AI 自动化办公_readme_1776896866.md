# Python AI 自动化办公

[![Build Status](https://img.shields.io/github/actions/workflow/status/SoloAI/python-ai-office/ci.yml?branch=main)](https://github.com/SoloAI/python-ai-office/actions)
[![License](https://img.shields.io/github/license/SoloAI/python-ai-office)](./LICENSE)

面向 **Python AI 自动化办公** 场景的开源工具集，帮助开发者与企业快速构建文档处理、数据整理、流程自动化与 AI 助手能力。  
本项目聚焦 **办公自动化（Office Automation）+ 人工智能（AI）+ Python 工作流**，适用于报表生成、表格处理、邮件自动化、文档分析与任务编排。

---

## Features

- **智能文档处理**：支持对 Word、Excel、PDF、CSV 等办公文件进行解析、提取与结构化处理
- **AI 驱动工作流**：结合大语言模型实现文本摘要、内容生成、分类、信息提取与问答
- **办公流程自动化**：自动完成报表整理、邮件通知、文件归档、批量重命名与定时任务
- **可扩展 Python API**：模块化设计，便于集成到现有 Python 自动化办公项目与企业内部系统
- **多场景脚本化支持**：适用于财务、人事、运营、行政等日常办公自动化场景
- **CLI + SDK 双模式**：既可通过命令行快速执行，也可在 Python 项目中灵活调用

---

## Installation

### Requirements

- Python 3.9+
- pip 23+
- Optional: OpenAI-compatible API key or local LLM service

### Install from PyPI

```bash
pip install python-ai-office
```

### Install from source

```bash
git clone https://github.com/SoloAI/python-ai-office.git
cd python-ai-office
pip install -e .
```

### Optional dependencies

```bash
pip install "python-ai-office[excel,pdf,llm]"
```

### Environment variables

创建 `.env` 文件：

```env
OPENAI_API_KEY=your_api_key
OPENAI_BASE_URL=https://api.openai.com/v1
MODEL_NAME=gpt-4o-mini
```

---

## Quick Start

以下示例展示如何使用 Python 进行 AI 自动化办公：读取 Excel 数据、生成摘要，并输出结果。

```python
from ai_office import OfficeAgent

agent = OfficeAgent(
    model="gpt-4o-mini",
    temperature=0.2
)

result = agent.run(
    task="请分析本月销售表，生成一段管理层摘要，并指出异常数据。",
    input_file="data/sales.xlsx",
    output_format="markdown"
)

print(result.content)
```

### CLI 快速体验

```bash
ai-office run \
  --task "总结 invoices 文件夹中的 PDF 发票，并生成费用汇总表" \
  --input ./invoices \
  --output ./reports/summary.xlsx
```

---

## Usage Examples

### 1. Excel 数据分析与报表生成

```python
from ai_office import ExcelProcessor, ReportGenerator

processor = ExcelProcessor("data/finance.xlsx")
df = processor.read(sheet_name="Q1")

report = ReportGenerator().generate(
    data=df,
    prompt="分析季度财务数据，输出关键指标、趋势和风险提示"
)

print(report)
```

### 2. 批量文档摘要

```python
from ai_office import DocumentPipeline

pipeline = DocumentPipeline(model="gpt-4o-mini")

summaries = pipeline.summarize_folder(
    folder_path="./docs",
    file_types=["pdf", "docx"],
    language="zh"
)

for item in summaries:
    print(item["filename"], item["summary"])
```

### 3. 邮件自动化发送

```python
from ai_office import MailAutomation

mailer = MailAutomation(
    smtp_host="smtp.example.com",
    smtp_port=587,
    username="bot@example.com",
    password="your_password"
)

mailer.send(
    to=["team@example.com"],
    subject="每日报表",
    body="您好，附件为今日自动生成的业务报表。",
    attachments=["./reports/daily-report.xlsx"]
)
```

### 4. 自定义自动化工作流

```python
from ai_office import Workflow

workflow = Workflow("daily-office-job")

workflow.step("load_excel", input_path="./data/tasks.xlsx")
workflow.step("analyze", prompt="提取待办事项并按优先级分类")
workflow.step("generate_doc", template="./templates/daily-report.docx")
workflow.step("send_email", recipients=["ops@example.com"])

workflow.run()
```

---

## Project Structure

```text
python-ai-office/
├── ai_office/
│   ├── agents/
│   ├── processors/
│   ├── workflows/
│   ├── integrations/
│   └── cli/
├── examples/
├── tests/
├── docs/
└── README.md
```

---

## Use Cases

- **AI 办公助手**：自动总结会议纪要、生成日报/周报、提取行动项
- **Excel 自动化处理**：批量清洗数据、统计分析、生成图表与报告
- **合同/发票处理**：OCR 提取信息、字段结构化、自动归档
- **邮件与通知系统**：自动发送审批提醒、业务汇报、运营通知
- **企业知识处理**：文档检索、知识问答、FAQ 自动生成

---

## Contributing

欢迎社区开发者参与贡献，共同打造更强大的 Python AI 自动化办公平台。

### How to contribute

1. Fork 本仓库
2. 创建特性分支

```bash
git checkout -b feat/your-feature
```

3. 提交修改

```bash
git commit -m "feat: add new office automation module"
```

4. 推送到远程分支

```bash
git push origin feat/your-feature
```

5. 提交 Pull Request

### Development setup

```bash
git clone https://github.com/SoloAI/python-ai-office.git
cd python-ai-office
python -m venv .venv
source .venv/bin/activate  # Windows: .venv\Scripts\activate
pip install -e ".[dev]"
pre-commit install
pytest
```

### Contribution guidelines

- 遵循 **PEP 8** 和项目既有代码风格
- 为新功能补充测试与文档
- 提交信息建议遵循 **Conventional Commits**
- 对重大变更请先提交 Issue 讨论设计方案

---

## License

本项目基于 **MIT License** 开源发布。详情请参阅 [LICENSE](./LICENSE)。

---

## Keywords

**Python AI 自动化办公**, **office automation**, **AI workflow**, **Excel automation**, **document AI**, **办公自动化**, **Python 办公脚本**, **LLM automation**, **企业自动化**, **智能文档处理**

---

如果你希望，我还可以继续为你生成：
- `README_EN.md` 英文版
- 更适合实际开源仓库的项目目录与徽章链接
- 配套的 `pyproject.toml`、`LICENSE`、`CONTRIBUTING.md` 模板