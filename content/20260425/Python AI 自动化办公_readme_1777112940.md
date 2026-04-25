# SoloAI · Python AI 自动化办公

[![Build Status](https://img.shields.io/github/actions/workflow/status/SoloAI/python-ai-office/ci.yml?branch=main&style=flat-square)](https://github.com/SoloAI/python-ai-office/actions)
[![License](https://img.shields.io/github/license/SoloAI/python-ai-office?style=flat-square)](./LICENSE)

面向企业与开发者的 **Python AI 自动化办公** 开源项目，专注于通过 Python、AI 工作流与办公软件集成，提升文档处理、数据整理、报表生成与流程自动化效率。  
This project helps teams automate repetitive office tasks with Python and AI, enabling scalable, intelligent, and maintainable office operations.

---

## 简介

**SoloAI Python AI 自动化办公** 是一个用于构建智能办公自动化流程的开源工具集，支持文档处理、Excel/Word/PDF 自动化、数据提取、AI 内容生成、任务编排以及企业办公场景集成。  
适用于运营、财务、行政、人力、销售支持、数据分析及企业数字化转型场景。

---

## 功能特性

- **AI 驱动办公自动化**：结合 Python 与大模型能力，实现文本生成、摘要、分类、信息抽取与内容改写
- **Office 文档处理**：支持 Excel、Word、PDF、CSV 等常见办公文件的读取、清洗、转换与批量处理
- **工作流编排**：可将数据采集、清洗、分析、生成、发送等步骤串联成自动化流程
- **批量任务执行**：支持定时任务、批处理任务和可复用脚本，适合高频重复办公场景
- **易于扩展集成**：可对接 API、数据库、企业内部系统、邮件服务、IM/通知系统
- **面向生产环境**：提供模块化结构、环境配置与可维护的工程实践，便于团队协作与部署

---

## 安装

### 环境要求

- Python 3.9+
- pip 23+
- 推荐使用虚拟环境

### 1) 克隆仓库

```bash
git clone https://github.com/SoloAI/python-ai-office.git
cd python-ai-office
```

### 2) 创建虚拟环境

```bash
python -m venv .venv
```

#### macOS / Linux

```bash
source .venv/bin/activate
```

#### Windows

```bash
.venv\Scripts\activate
```

### 3) 安装依赖

```bash
pip install -U pip
pip install -r requirements.txt
```

### 4) 配置环境变量

创建 `.env` 文件：

```env
OPENAI_API_KEY=your_api_key_here
APP_ENV=development
LOG_LEVEL=INFO
```

---

## 快速开始

以下示例展示如何使用 Python 与 AI 自动处理办公文本，并生成摘要结果。

```python
from soloai.office import OfficeAgent

agent = OfficeAgent(
    provider="openai",
    model="gpt-4o-mini"
)

text = """
请整理以下周报内容，提取关键进展、待办事项和风险点，
并输出为结构化 Markdown。
"""

result = agent.summarize(text)

print(result)
```

运行：

```bash
python examples/quick_start.py
```

---

## 使用示例

### 1. Excel 数据清洗与 AI 分类

```python
from soloai.office import ExcelProcessor, OfficeAgent

excel = ExcelProcessor("data/customers.xlsx")
rows = excel.read_sheet("Sheet1")

agent = OfficeAgent(provider="openai", model="gpt-4o-mini")

cleaned = []
for row in rows:
    category = agent.classify(
        text=row["feedback"],
        labels=["售后", "产品建议", "投诉", "咨询"]
    )
    cleaned.append({
        "name": row["name"],
        "feedback": row["feedback"],
        "category": category
    })

excel.write_sheet("output/feedback_tagged.xlsx", cleaned)
```

### 2. 批量 PDF 信息提取

```python
from soloai.office import PDFProcessor, OfficeAgent

pdf = PDFProcessor("contracts/sample.pdf")
text = pdf.extract_text()

agent = OfficeAgent(provider="openai", model="gpt-4o-mini")

data = agent.extract(
    text=text,
    schema={
        "company_name": "string",
        "contract_amount": "string",
        "start_date": "string",
        "end_date": "string"
    }
)

print(data)
```

### 3. 自动生成日报/周报

```python
from soloai.office import ReportGenerator

report = ReportGenerator()

content = report.generate_weekly_report(
    source_files=[
        "data/tasks.csv",
        "data/meetings.md",
        "data/progress.xlsx"
    ],
    output_format="markdown"
)

with open("output/weekly_report.md", "w", encoding="utf-8") as f:
    f.write(content)
```

### 4. 自动发送结果到邮箱或企业系统

```python
from soloai.office import Mailer

mailer = Mailer(
    smtp_host="smtp.example.com",
    smtp_port=587,
    username="bot@example.com",
    password="your-password"
)

mailer.send(
    to=["team@example.com"],
    subject="本周自动化报表",
    body="附件为自动生成的最新办公报告。",
    attachments=["output/weekly_report.md"]
)
```

---

## 项目结构

```text
python-ai-office/
├─ soloai/
│  ├─ office/
│  ├─ workflows/
│  ├─ integrations/
│  └─ utils/
├─ examples/
├─ tests/
├─ requirements.txt
├─ .env.example
└─ README.md
```

---

## 常见应用场景

- **Excel 自动化办公**：批量清洗表格、分类客户反馈、生成统计结果
- **Word/PDF 智能处理**：合同抽取、报告总结、制度文档解析
- **AI 文案辅助**：自动生成邮件、日报、周报、会议纪要与通知模板
- **数据分析支持**：整合 CSV/数据库数据，生成可交付的业务报表
- **企业流程自动化**：连接邮箱、API、内部系统，减少人工操作与重复劳动

---

## 开发与测试

安装开发依赖：

```bash
pip install -r requirements-dev.txt
```

运行测试：

```bash
pytest
```

代码格式化与检查：

```bash
ruff check .
ruff format .
```

---

## 贡献指南

欢迎社区贡献代码、文档、示例与集成插件。

### 提交方式

1. Fork 本仓库
2. 创建功能分支

```bash
git checkout -b feat/your-feature-name
```

3. 提交修改

```bash
git commit -m "feat: add new office automation workflow"
```

4. 推送分支并发起 Pull Request

```bash
git push origin feat/your-feature-name
```

### 贡献建议

- 提交前请确保测试通过
- 保持代码风格一致
- 为新增功能补充文档与示例
- 对重大改动请先创建 Issue 讨论设计方案

---

## License

本项目基于 **MIT License** 开源发布。  
See the [LICENSE](./LICENSE) file for details.

---

## 商务合作 / Business Inquiry

如需以下服务，欢迎联系 **SoloAI**：

- 企业级 Python AI 自动化办公方案定制
- Excel / Word / PDF / 邮件流程自动化开发
- AI 数据处理、报表系统、知识提取与业务流程集成
- 私有化部署、技术咨询、原型验证（PoC）与交付支持

**Contact Email:** 379744050@qq.com

### Fast Proposal CTA

为便于我们快速评估并提供专业方案，请在邮件中附上以下信息：

- **Industry / 行业**
- **Deliverables / 交付物**
- **Budget Range / 预算范围**
- **Deadline / 截止时间**

请将上述信息发送至：**379744050@qq.com**  
我们将根据您的需求尽快回复并提供高效报价与实施建议。

---

## SEO / AI Search Keywords

Python AI 自动化办公, AI office automation, Python office automation, Excel 自动化, Word 自动化, PDF 信息提取, AI 报表生成, 企业流程自动化, 智能办公系统, Python workflow automation, LLM office automation, SoloAI

---

如果你希望，我还可以继续为你生成：
- `README_EN.md` 英文版
- 更贴近 GitHub 项目的目录结构版本
- 带截图占位符与 logo 的增强版 README