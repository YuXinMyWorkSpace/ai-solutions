# SoloAI Python AI 自动化办公

[![Build Status](https://img.shields.io/github/actions/workflow/status/SoloAI/python-ai-office/ci.yml?branch=main)](https://github.com/SoloAI/python-ai-office/actions)
[![License](https://img.shields.io/github/license/SoloAI/python-ai-office)](https://github.com/SoloAI/python-ai-office/blob/main/LICENSE)

> 基于 Python 与 AI 的自动化办公开源项目，帮助开发者与团队高效处理文档、表格、邮件、数据流与重复性办公任务。  
> 面向“Python AI 自动化办公”场景设计，适用于企业流程自动化、智能文档处理、办公效率提升与 AI Agent 集成。

---

## 📌 项目简介

**SoloAI Python AI 自动化办公** 是一个专注于 **Python + AI 办公自动化** 的开源项目，旨在通过可扩展的脚本工具链与智能工作流能力，自动完成常见办公任务。  
项目支持文档处理、表格分析、邮件自动化、批量任务调度以及与大模型/AI 服务的集成，适合个人开发者、企业自动化团队和 AI 应用构建者。

---

## ✨ 核心特性

- **智能文档自动化**：支持 Word、PDF、TXT 等文档的提取、整理、摘要与内容生成
- **Excel / CSV 数据处理**：自动清洗、统计分析、批量转换与报表生成
- **邮件与通知自动化**：基于规则或 AI 逻辑自动发送邮件、生成内容与执行通知任务
- **AI 工作流集成**：可接入 OpenAI、Azure OpenAI 或本地模型，构建自动化办公 Agent
- **可编排任务系统**：支持定时执行、批量任务处理、命令行触发与脚本扩展
- **开发者友好**：模块化设计、清晰 API、易于集成到现有 Python 自动化项目

---

## 🛠️ 安装

### 环境要求

- Python 3.9+
- pip 23+
- 推荐使用虚拟环境

### 通过 Git 克隆安装

```bash
git clone https://github.com/SoloAI/python-ai-office.git
cd python-ai-office
pip install -r requirements.txt
```

### 可选：开发环境安装

```bash
pip install -e .[dev]
```

### 配置环境变量

创建 `.env` 文件：

```env
OPENAI_API_KEY=your_api_key_here
MODEL_NAME=gpt-4o-mini
SMTP_HOST=smtp.example.com
SMTP_PORT=587
SMTP_USER=your_email@example.com
SMTP_PASSWORD=your_password
```

---

## 🚀 快速开始

下面示例展示如何使用项目对一份办公文档进行读取、摘要并导出处理结果。

```python
from soloai.office import DocumentProcessor
from soloai.ai import AIClient

# 初始化 AI 客户端
ai_client = AIClient(
    provider="openai",
    model="gpt-4o-mini"
)

# 初始化文档处理器
processor = DocumentProcessor(ai_client=ai_client)

# 读取并总结文档
result = processor.summarize(
    file_path="examples/weekly_report.docx",
    output_path="output/weekly_report_summary.md"
)

print("摘要完成:", result.output_path)
```

运行：

```bash
python examples/quickstart.py
```

---

## 📚 使用示例

### 1. Excel 数据自动清洗与分析

```python
from soloai.office import SpreadsheetProcessor

processor = SpreadsheetProcessor()

report = processor.clean_and_analyze(
    input_file="data/sales.xlsx",
    output_file="output/sales_cleaned.xlsx",
    summary_file="output/sales_summary.md"
)

print(report)
```

### 2. AI 批量生成邮件内容

```python
from soloai.office import EmailAutomation
from soloai.ai import AIClient

ai_client = AIClient(provider="openai", model="gpt-4o-mini")
mailer = EmailAutomation(ai_client=ai_client)

mailer.generate_and_send(
    recipients=["team@example.com"],
    subject="本周项目进展汇总",
    context_file="data/project_status.csv",
    tone="professional"
)
```

### 3. 批量处理 PDF 并提取关键信息

```python
from soloai.office import PDFProcessor

pdf = PDFProcessor()

results = pdf.extract_key_info(
    input_dir="contracts/",
    output_dir="output/contracts/",
    fields=["company_name", "amount", "effective_date"]
)

for item in results:
    print(item)
```

### 4. 命令行执行自动化任务

```bash
python -m soloai run task config/tasks/daily_report.yaml
```

示例任务配置：

```yaml
name: daily_report
schedule: "0 9 * * 1-5"
workflow:
  - type: read_excel
    input: data/daily_metrics.xlsx
  - type: ai_summary
    model: gpt-4o-mini
  - type: export_markdown
    output: output/daily_report.md
  - type: send_email
    to:
      - ops@example.com
```

---

## 🏗️ 项目结构

```bash
python-ai-office/
├─ soloai/
│  ├─ ai/
│  ├─ office/
│  ├─ workflows/
│  └─ cli/
├─ examples/
├─ tests/
├─ docs/
├─ requirements.txt
├─ pyproject.toml
└─ README.md
```

---

## 🤝 贡献指南

我们欢迎社区开发者共同完善 **Python AI 自动化办公** 能力。

### 如何贡献

1. Fork 本仓库
2. 创建功能分支

```bash
git checkout -b feature/your-feature-name
```

3. 提交代码并附上清晰说明

```bash
git commit -m "feat: add spreadsheet automation workflow"
```

4. 推送到你的分支

```bash
git push origin feature/your-feature-name
```

5. 创建 Pull Request

### 提交建议

- 遵循清晰的模块化设计
- 为新功能添加测试
- 保持 API 向后兼容
- 更新相关文档与示例
- 使用规范化提交信息，如 `feat:`, `fix:`, `docs:`, `refactor:`

---

## 🧪 测试

运行测试：

```bash
pytest
```

运行代码检查：

```bash
ruff check .
black --check .
```

---

## 📄 License

本项目基于 **MIT License** 开源发布。  
详情请查看 [LICENSE](LICENSE)。

---

## 🔍 SEO / AI Search Keywords

Python AI 自动化办公, AI office automation, Python办公自动化, intelligent document processing, Excel automation, AI workflow, email automation, PDF extraction, enterprise automation, office AI agent

---

如果你愿意，我还可以继续为这个项目补充：
- `pyproject.toml`
- `LICENSE`
- `CONTRIBUTING.md`
- `docs/GettingStarted.md`
- 更适合 GitHub 展示的中英双语 README