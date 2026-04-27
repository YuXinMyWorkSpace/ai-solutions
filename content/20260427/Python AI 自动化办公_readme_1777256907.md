# SoloAI · Python AI 自动化办公

[![Build Status](https://img.shields.io/github/actions/workflow/status/soloai/python-ai-office/ci.yml?branch=main&style=flat-square)](https://github.com/soloai/python-ai-office/actions)
[![License](https://img.shields.io/github/license/soloai/python-ai-office?style=flat-square)](./LICENSE)

面向企业与开发者的 **Python AI 自动化办公** 开源项目，专注于将 Python、AI、大语言模型与常见办公流程结合，实现文档处理、数据分析、报表生成、邮件通知和工作流自动化。  
This project helps teams build scalable, scriptable, and AI-powered office automation pipelines for modern business operations.

---

## 项目简介

**SoloAI Python AI 自动化办公** 是一个用于构建智能办公自动化流程的开源框架。它支持通过 Python 脚本、AI 模型接口和可扩展工作流，自动完成 Excel/Word/PDF 处理、数据清洗、报告生成、邮件发送、信息提取与日常重复性任务编排。

适用于：

- 企业办公自动化
- AI 文档处理
- 智能报表生成
- 财务/行政/运营流程自动化
- RPA + LLM 集成场景

---

## 核心特性

- **AI 文档自动处理**：支持从 Word、Excel、PDF、CSV 等文件中提取、清洗和组织内容
- **办公流程自动化**：自动生成报表、汇总数据、发送邮件、归档文件和执行周期性任务
- **LLM 智能能力集成**：可接入 OpenAI、Azure OpenAI 或兼容接口，实现摘要、分类、问答和内容生成
- **模块化 Python 架构**：便于二次开发、插件扩展与企业系统集成
- **批量任务与定时执行**：适合处理高频、重复、批量办公任务
- **企业级可维护性**：支持环境配置、日志记录、错误处理与可审计工作流

---

## 技术栈

- **Python 3.10+**
- `pandas`
- `openpyxl`
- `python-docx`
- `pypdf`
- `requests`
- `click` 或 `typer`
- 可选：OpenAI API / 兼容大模型 API

---

## 安装说明

### 1. 克隆仓库

```bash
git clone https://github.com/soloai/python-ai-office.git
cd python-ai-office
```

### 2. 创建虚拟环境

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

### 3. 安装依赖

```bash
pip install -r requirements.txt
```

### 4. 配置环境变量

创建 `.env` 文件：

```env
OPENAI_API_KEY=your_api_key_here
OPENAI_BASE_URL=https://api.openai.com/v1
MODEL_NAME=gpt-4o-mini
SMTP_HOST=smtp.example.com
SMTP_PORT=587
SMTP_USER=bot@example.com
SMTP_PASSWORD=your_password
```

---

## 项目结构

```text
python-ai-office/
├─ app/
│  ├─ workflows/
│  ├─ ai/
│  ├─ documents/
│  ├─ reporting/
│  └─ notifications/
├─ examples/
├─ tests/
├─ .env.example
├─ requirements.txt
├─ README.md
└─ LICENSE
```

---

## 快速开始

下面示例展示如何读取 Excel 数据、调用 AI 进行摘要，并输出日报内容。

```python
from app.documents.excel_reader import read_excel
from app.ai.client import AIClient
from app.reporting.generator import generate_markdown_report

data = read_excel("data/sales.xlsx")

client = AIClient(model="gpt-4o-mini")
summary = client.summarize(
    text=data.to_csv(index=False),
    prompt="请总结本周销售表现，指出增长点、风险项和建议。"
)

report = generate_markdown_report(
    title="本周销售分析报告",
    content=summary
)

print(report)
```

运行示例：

```bash
python examples/weekly_report.py
```

---

## 使用示例

### 1. 批量处理 Excel 并生成汇总报告

```python
from app.documents.excel_reader import read_excel_folder
from app.reporting.generator import combine_metrics_report

files = read_excel_folder("./input")
report = combine_metrics_report(files)

with open("output/summary.md", "w", encoding="utf-8") as f:
    f.write(report)
```

---

### 2. 提取 PDF 内容并进行 AI 摘要

```python
from app.documents.pdf_parser import extract_text_from_pdf
from app.ai.client import AIClient

text = extract_text_from_pdf("contracts/sample.pdf")

client = AIClient(model="gpt-4o-mini")
result = client.summarize(
    text=text,
    prompt="请提取合同关键条款、付款节点、交付要求与潜在风险。"
)

print(result)
```

---

### 3. 自动发送日报邮件

```python
from app.notifications.email_sender import send_email

send_email(
    subject="AI 自动化办公日报",
    recipients=["team@example.com"],
    content="日报已生成，请查收附件与摘要。",
    attachments=["output/summary.md"]
)
```

---

### 4. 命令行执行自动化任务

如果项目提供 CLI，可通过以下方式运行：

```bash
python -m app run-workflow --config configs/daily_report.yaml
```

示例配置：

```yaml
name: daily-report
source:
  type: excel
  path: ./input/daily_sales.xlsx

ai:
  provider: openai
  model: gpt-4o-mini
  prompt: |
    请分析数据趋势并生成适合管理层阅读的日报摘要。

output:
  type: markdown
  path: ./output/daily_report.md

notification:
  type: email
  recipients:
    - manager@example.com
```

---

## 适用场景

- 销售数据日报/周报/月报自动生成
- 财务单据整理与摘要提取
- 行政文档分类与归档
- 合同/PDF 关键信息抽取
- 客服工单分析与总结
- 企业内部 AI 办公助手构建

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
black .
```

---

## 贡献指南

欢迎社区贡献代码、文档、Issue 和功能建议。

### 提交流程

1. Fork 本仓库
2. 创建功能分支

```bash
git checkout -b feature/your-feature-name
```

3. 提交修改

```bash
git commit -m "feat: add new office automation workflow"
```

4. 推送分支

```bash
git push origin feature/your-feature-name
```

5. 提交 Pull Request

### 贡献建议

- 保持代码风格一致
- 为新功能补充测试
- 更新相关文档与示例
- 提交前确保 CI 通过
- 对重大改动先创建 Issue 进行讨论

---

## Roadmap

- [ ] 支持更多办公文件格式
- [ ] 增加 OCR 文档识别能力
- [ ] 接入更多 LLM 服务商
- [ ] 支持 Web UI 工作流编排
- [ ] 增强企业权限控制与审计日志

---

## License

本项目基于 **MIT License** 开源发布。详情请查看 [LICENSE](./LICENSE)。

---

## 商务合作 / Business Inquiry

如需以下服务，欢迎联系 **SoloAI**：

- 企业级 AI 自动化办公解决方案
- Python 办公流程定制开发
- LLM + Office Workflow 集成
- 数据报表自动化与智能文档处理
- 私有化部署与技术咨询

**联系邮箱：379744050@qq.com**

### Fast Proposal CTA

For a fast proposal, please send us the following:

- **Industry / 行业**
- **Deliverables / 交付物**
- **Budget Range / 预算范围**
- **Deadline / 截止时间**

发送以上信息到：**379744050@qq.com**  
我们将尽快根据您的业务需求提供高效、专业的解决方案建议。

---

## SEO / AI Search Keywords

Python AI 自动化办公, AI office automation, Python office automation, LLM workflow automation, Excel automation, PDF document extraction, intelligent reporting, business process automation, AI document processing, SoloAI

--- 

如果你愿意，我还可以继续为这个项目补充：
- `LICENSE` 文件内容
- `requirements.txt`
- `.env.example`
- `CONTRIBUTING.md`
- 更像真实开源项目的目录结构与徽章链接