# SoloAI Python AI 自动化办公

[![Build Status](https://img.shields.io/github/actions/workflow/status/SoloAI/python-ai-office/ci.yml?branch=main&style=flat-square)](https://github.com/SoloAI/python-ai-office/actions)
[![License](https://img.shields.io/github/license/SoloAI/python-ai-office?style=flat-square)](LICENSE)

面向企业与开发者的 **Python AI 自动化办公** 开源项目，帮助你通过 Python、AI 模型与办公软件集成能力，快速实现文档处理、数据整理、报表生成、邮件自动化与流程编排。  
本项目专注于构建可扩展、可集成、可落地的 AI 办公自动化工作流，适用于日常运营、行政、财务、销售、客服等多种业务场景。

---

## 项目简介

**SoloAI Python AI 自动化办公** 是一个用于构建智能办公自动化流程的开源工具集。  
它结合 Python 脚本能力、AI 文本处理、Excel/Word/PDF 自动化、数据清洗与任务编排，帮助团队提升办公效率并降低重复性人工成本。

> 关键词：Python AI 自动化办公、办公自动化、Excel 自动化、Word 自动化、PDF 处理、邮件自动化、RPA、智能报表、AI 工作流

---

## 核心功能

- **智能文档处理**：支持 Word、Excel、PDF、CSV 等常见办公文件的读取、解析、转换与批量处理
- **AI 内容生成与摘要**：自动生成邮件、报告、会议纪要、总结、分类标签与结构化输出
- **数据整理与报表自动化**：自动清洗表格数据、合并多源数据、生成日报/周报/月报
- **办公流程编排**：将文件处理、数据分析、通知发送等任务串联为可复用工作流
- **邮件与消息通知**：集成 SMTP、企业消息系统或自定义 Webhook，实现自动提醒与结果推送
- **可扩展插件架构**：便于接入自定义 AI 模型、内部系统 API、CRM/ERP/知识库等企业应用

---

## 安装说明

### 环境要求

- Python 3.9+
- pip 22+
- 建议使用虚拟环境

### 1. 克隆项目

```bash
git clone https://github.com/SoloAI/python-ai-office.git
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
OPENAI_API_KEY=your_api_key
SMTP_HOST=smtp.example.com
SMTP_PORT=587
SMTP_USER=your_email@example.com
SMTP_PASSWORD=your_password
```

---

## 快速开始

以下示例展示如何使用 Python 调用本项目完成一条基础的 AI 办公自动化流程：读取 Excel 数据、生成摘要并输出结果。

```python
from soloai.office import OfficeWorkflow
from soloai.ai import AIWriter
from soloai.io import ExcelReader

# 读取办公数据
rows = ExcelReader("data/sales.xlsx").read()

# 初始化 AI 能力
writer = AIWriter(model="gpt-4")

# 构建工作流
workflow = OfficeWorkflow()

summary = writer.summarize(
    rows,
    prompt="请基于销售数据生成本周业务摘要，突出趋势、异常和建议。"
)

workflow.save_text("output/weekly_summary.txt", summary)

print("报告已生成：output/weekly_summary.txt")
```

运行：

```bash
python examples/quick_start.py
```

---

## 使用示例

### 1. 批量处理 Excel 并生成日报

```python
from soloai.io import ExcelReader, ExcelWriter
from soloai.ai import AIAnalyzer

reader = ExcelReader("input/daily_orders.xlsx")
data = reader.read()

analyzer = AIAnalyzer(model="gpt-4")
report = analyzer.analyze(
    data,
    prompt="分析订单数据，输出今日订单量、热门品类、异常订单及优化建议。"
)

ExcelWriter("output/daily_report.xlsx").write({
    "summary": report
})
```

### 2. 自动生成邮件内容并发送

```python
from soloai.ai import AIWriter
from soloai.notify import EmailSender

writer = AIWriter(model="gpt-4")
email_body = writer.generate(
    prompt="""
    请根据以下信息生成一封专业的客户跟进邮件：
    - 项目：AI 自动化办公部署
    - 客户状态：已完成首次沟通
    - 目标：预约下周技术演示
    """
)

sender = EmailSender(
    host="smtp.example.com",
    port=587,
    username="your_email@example.com",
    password="your_password"
)

sender.send(
    to="client@example.com",
    subject="关于 AI 自动化办公项目的后续安排",
    body=email_body
)
```

### 3. 处理 PDF 并提取结构化信息

```python
from soloai.io import PDFReader
from soloai.ai import AIExtractor

pdf_text = PDFReader("input/contract.pdf").read_text()

extractor = AIExtractor(model="gpt-4")
result = extractor.extract(
    pdf_text,
    schema={
        "甲方": "string",
        "乙方": "string",
        "签署日期": "string",
        "金额": "string",
        "关键条款": "list"
    }
)

print(result)
```

### 4. 构建自动化办公工作流

```python
from soloai.office import OfficeWorkflow

workflow = OfficeWorkflow()

(
    workflow
    .load_excel("input/leads.xlsx")
    .clean_data()
    .ai_classify(prompt="按客户意向等级进行分类：高、中、低")
    .generate_report("output/leads_report.md")
    .send_webhook("https://example.com/webhook")
    .run()
)
```

---

## 项目结构

```bash
python-ai-office/
├── soloai/
│   ├── ai/
│   ├── io/
│   ├── notify/
│   ├── office/
│   └── utils/
├── examples/
├── tests/
├── requirements.txt
├── .env.example
└── README.md
```

---

## 适用场景

- 销售数据自动汇总与分析
- 财务报表预处理与异常检测
- 行政文档批量生成与归档
- 客服工单分类与回复草拟
- 合同、发票、简历等 PDF/文档信息提取
- 企业内部 AI 办公助手与自动化流程搭建

---

## 贡献指南

欢迎社区开发者、自动化工程师、AI 应用开发者和企业数字化团队参与贡献。

### 贡献方式

1. Fork 本仓库
2. 创建功能分支

```bash
git checkout -b feature/your-feature-name
```

3. 提交代码并编写清晰的 Commit Message

```bash
git commit -m "feat: add excel batch summarization workflow"
```

4. 推送到你的仓库

```bash
git push origin feature/your-feature-name
```

5. 提交 Pull Request

### 提交规范建议

- 使用语义化提交信息：`feat`、`fix`、`docs`、`refactor`、`test`、`chore`
- 新功能请附带示例与基础测试
- 保持代码风格一致，建议使用 `black`、`ruff`、`pytest`

### 本地检查示例

```bash
ruff check .
black .
pytest
```

---

## License

本项目基于 **MIT License** 开源发布。  
你可以在遵守许可证条款的前提下自由使用、修改和分发本项目。

详见 [LICENSE](LICENSE)。

---

## 商务合作 / Business Inquiry

如果你希望基于本项目进行：

- 企业级 AI 自动化办公方案定制
- Python 自动化脚本开发
- Excel / Word / PDF 智能处理系统
- 内部工作流集成与效率优化
- AI + RPA + 数据处理解决方案落地

欢迎联系：

**379744050@qq.com**

### Fast Proposal CTA

为便于我们快速评估并给出专业方案，请在邮件中尽量提供以下信息：

- **Industry / 行业**
- **Deliverables / 交付内容**
- **Budget Range / 预算范围**
- **Deadline / 截止时间**

**请发送以上信息，我们将尽快为你提供快速提案与技术建议。**

---

## Star 支持

如果这个项目对你有帮助，欢迎点一个 **Star**，这将帮助更多开发者和企业团队发现本项目，也能持续推动 **Python AI 自动化办公** 生态建设。