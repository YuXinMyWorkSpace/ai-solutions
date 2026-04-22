# SoloAI Python AI 自动化办公

[![Build Status](https://img.shields.io/github/actions/workflow/status/SoloAI/python-ai-office/ci.yml?branch=main&style=flat-square)](https://github.com/SoloAI/python-ai-office/actions)
[![License](https://img.shields.io/github/license/SoloAI/python-ai-office?style=flat-square)](./LICENSE)

面向 **Python AI 自动化办公** 场景的开源工具集，帮助开发者与企业通过 AI 能力自动化处理文档、表格、邮件、报告生成与日常办公流程。  
该项目聚焦于 **可扩展、可集成、可脚本化** 的办公自动化能力，适用于个人效率提升、企业流程自动化和 AI Agent 办公场景。

---

## ✨ Features

- **文档自动化处理**：支持 Word、PDF、Markdown、TXT 等文档的读取、解析、摘要与内容生成
- **Excel / 表格智能处理**：自动数据清洗、分析、汇总、报表生成与批量更新
- **AI 内容生成**：基于大模型进行邮件撰写、会议纪要整理、日报周报生成和知识提炼
- **办公流程自动化**：可串联文件处理、数据分析、通知发送等任务，构建自动化工作流
- **Python 优先设计**：提供清晰的 Python API，方便脚本集成、二次开发与企业系统接入
- **可扩展架构**：支持接入主流 LLM / API 服务，并适配本地化部署与多种办公场景

---

## 📦 Installation

### Requirements

- Python 3.9+
- pip 23+
- 推荐使用虚拟环境

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

如果你需要更完整的办公能力，可以安装扩展依赖：

```bash
pip install "soloai-office[excel,pdf,email,llm]"
```

---

## 🚀 Quick Start

下面示例展示如何使用 `SoloAI` 快速对办公文档进行分析并生成摘要。

```python
from soloai_office import OfficeAI

client = OfficeAI(
    api_key="YOUR_API_KEY",
    model="gpt-4o-mini"
)

result = client.summarize_document(
    file_path="docs/weekly_report.docx",
    prompt="请提取本周重点进展、风险项和下周计划，并输出为结构化要点。"
)

print(result.text)
```

---

## 🧠 Usage Examples

### 1. Excel 数据汇总与分析

```python
from soloai_office import OfficeAI

client = OfficeAI(api_key="YOUR_API_KEY")

analysis = client.analyze_spreadsheet(
    file_path="data/sales.xlsx",
    instructions="""
    分析销售数据的月度趋势、TOP 5 产品、
    异常波动，并生成管理层摘要。
    """
)

print(analysis.markdown)
```

### 2. 自动生成办公邮件

```python
from soloai_office import OfficeAI

client = OfficeAI(api_key="YOUR_API_KEY")

email = client.generate_email(
    subject="项目延期通知",
    context="""
    由于接口联调时间超出预期，项目将延期 3 个工作日。
    请保持专业、简洁，并给出新的交付时间。
    """,
    tone="professional",
    language="zh-CN"
)

print(email.body)
```

### 3. 批量处理 PDF 并输出摘要

```python
from soloai_office import OfficeAI

client = OfficeAI(api_key="YOUR_API_KEY")

batch_result = client.batch_process(
    input_dir="contracts/",
    task="summarize",
    output_dir="outputs/contracts_summary/"
)

print(batch_result.completed, batch_result.failed)
```

### 4. 构建自动化办公工作流

```python
from soloai_office import OfficeWorkflow

workflow = OfficeWorkflow(name="daily-office-automation")

workflow.add_step("load_excel", file_path="reports/daily.xlsx")
workflow.add_step("analyze_data", prompt="识别关键指标变化并生成摘要")
workflow.add_step("create_report", format="markdown")
workflow.add_step("send_email", to="team@example.com", subject="日报分析结果")

result = workflow.run()
print(result.status)
```

---

## 🛠️ Installation & Configuration

在使用 LLM 或云端服务前，请先配置环境变量：

```bash
export SOLOAI_API_KEY="your_api_key"
```

Windows PowerShell:

```powershell
$env:SOLOAI_API_KEY="your_api_key"
```

Python 中也可以直接读取：

```python
import os
from soloai_office import OfficeAI

client = OfficeAI(
    api_key=os.getenv("SOLOAI_API_KEY")
)
```

---

## 📁 Recommended Project Structure

```text
python-ai-office/
├── docs/
├── examples/
├── soloai_office/
├── tests/
├── README.md
├── pyproject.toml
└── LICENSE
```

---

## 🔧 Common Use Cases

- AI 自动化办公脚本开发
- 企业文档处理自动化
- Excel 数据分析与报告生成
- 智能邮件与通知生成
- AI Agent 办公助手集成
- Python 办公效率工具链构建

---

## 🤝 Contributing

欢迎社区开发者参与贡献，共同打造高质量的 **Python AI 自动化办公** 开源项目。

### How to contribute

1. Fork 本仓库
2. 创建功能分支

```bash
git checkout -b feat/your-feature-name
```

3. 提交修改

```bash
git commit -m "feat: add new office automation capability"
```

4. 推送到你的分支

```bash
git push origin feat/your-feature-name
```

5. 发起 Pull Request

### Development setup

```bash
git clone https://github.com/SoloAI/python-ai-office.git
cd python-ai-office
python -m venv .venv
source .venv/bin/activate  # Windows 请使用 .venv\Scripts\activate
pip install -e ".[dev]"
pytest
```

### Contribution guidelines

- 遵循清晰、可维护的 Python 编码风格
- 为新功能补充测试用例
- 更新相关文档与示例
- 提交信息建议遵循 Conventional Commits
- 对重大功能变更，请先提交 Issue 进行讨论

---

## 📜 License

本项目基于 **MIT License** 开源发布。  
你可以自由使用、修改和分发本项目，但请保留原始版权与许可声明。

详见 [LICENSE](./LICENSE)。

---

## 🔍 Keywords

Python AI 自动化办公, AI office automation, Python office automation, Excel automation, document AI, report generation, AI workflow automation, 智能办公, 自动化办公脚本, AI Agent 办公

--- 

如果你希望，我还可以继续为你生成：
1. **更像真实开源项目风格的 README**
2. **中英双语 README**
3. **带项目截图 / 架构图 / TOC 的增强版 README**