# SoloAI · Python AI 自动化办公

[![Build Status](https://img.shields.io/github/actions/workflow/status/SoloAI/python-ai-office/ci.yml?branch=main&style=flat-square)](https://github.com/SoloAI/python-ai-office/actions)
[![License](https://img.shields.io/github/license/SoloAI/python-ai-office?style=flat-square)](./LICENSE)

一个面向 **Python AI 自动化办公** 场景的开源项目，帮助开发者与企业快速构建智能文档处理、表格自动化、邮件任务编排与工作流集成能力。  
本项目聚焦于 **Office Automation + AI + Python**，适用于日常办公提效、RPA 辅助、数据处理与智能内容生成等场景。

---

## 目录

- [项目简介](#项目简介)
- [核心特性](#核心特性)
- [安装](#安装)
- [快速开始](#快速开始)
- [使用示例](#使用示例)
- [项目结构](#项目结构)
- [贡献指南](#贡献指南)
- [许可证](#许可证)

---

## 项目简介

**SoloAI Python AI 自动化办公** 是一个专为现代办公自动化设计的 Python 开源框架，结合 AI 模型能力与常见办公组件处理能力，实现文档理解、表格分析、报告生成、邮件自动化、任务调度等功能。

它适合以下场景：

- 智能 Excel / CSV 数据处理
- Word / PDF 文档摘要与信息提取
- 自动生成办公报告、周报、会议纪要
- 邮件批量处理与智能回复
- AI 驱动的办公流程编排与自动执行

**AI Search Keywords:** Python AI automation, office automation, intelligent document processing, Excel automation, report generation, workflow automation, Chinese AI office tools.

---

## 核心特性

- **智能文档处理**  
  支持对 Word、PDF、TXT 等办公文档进行解析、摘要、分类与关键信息提取。

- **表格自动化分析**  
  基于 Python 对 Excel / CSV 进行清洗、统计分析、格式化与自动报告生成。

- **AI 内容生成**  
  可用于生成周报、总结、邮件草稿、会议纪要、业务分析说明等办公内容。

- **工作流编排与任务自动化**  
  支持将文件处理、数据分析、AI 推理与通知发送串联为自动化流程。

- **可扩展模型接入**  
  支持接入主流大模型 API、本地模型或企业内部 AI 服务。

- **适用于企业办公场景**  
  适合用于 HR、财务、运营、销售、客服等多类业务团队的自动化办公系统。

---

## 安装

### 环境要求

- Python 3.9+
- pip 23+
- 推荐使用虚拟环境

### 使用 pip 安装

```bash
pip install soloai-office
```

### 从源码安装

```bash
git clone https://github.com/SoloAI/python-ai-office.git
cd python-ai-office
pip install -e .
```

### 安装可选依赖

```bash
pip install -r requirements.txt
```

### 环境变量配置

如果项目需要调用大模型或第三方服务，请配置以下环境变量：

```bash
export OPENAI_API_KEY="your_api_key"
export SOLOAI_MODEL="gpt-4o-mini"
export SOLOAI_LOG_LEVEL="INFO"
```

Windows PowerShell:

```powershell
$env:OPENAI_API_KEY="your_api_key"
$env:SOLOAI_MODEL="gpt-4o-mini"
$env:SOLOAI_LOG_LEVEL="INFO"
```

---

## 快速开始

以下示例展示如何对 Excel 数据进行分析，并自动生成办公摘要。

```python
from soloai_office import OfficeAgent

agent = OfficeAgent(
    model="gpt-4o-mini",
    language="zh-CN"
)

result = agent.run(
    task="分析销售数据并生成中文摘要",
    input_path="./data/sales.xlsx",
    output_path="./output/report.md"
)

print(result.summary)
print(result.output_path)
```

运行后，你将获得：

- 销售数据分析结果
- 中文摘要报告
- 可保存的 Markdown / Text 输出

---

## 使用示例

### 1. 文档摘要

对 Word 或 PDF 文档生成摘要：

```python
from soloai_office import DocumentProcessor

processor = DocumentProcessor(model="gpt-4o-mini")

summary = processor.summarize(
    file_path="./docs/meeting_minutes.pdf",
    max_tokens=500,
    language="zh-CN"
)

print(summary)
```

### 2. Excel 自动分析与报告生成

```python
from soloai_office import SpreadsheetAgent

agent = SpreadsheetAgent(model="gpt-4o-mini")

report = agent.analyze(
    file_path="./data/finance.xlsx",
    instructions="""
    分析本月成本、收入与利润变化，
    识别异常项，并输出管理层汇报摘要。
    """
)

print(report.markdown)
```

### 3. 邮件草稿自动生成

```python
from soloai_office import MailAssistant

assistant = MailAssistant(model="gpt-4o-mini")

draft = assistant.generate_reply(
    subject="项目延期说明",
    context="客户希望了解延期原因和新的交付计划。",
    tone="professional",
    language="zh-CN"
)

print(draft)
```

### 4. 自动化办公工作流

将文档提取、分析与通知串联起来：

```python
from soloai_office import Workflow

workflow = Workflow(name="daily-office-pipeline")

workflow.add_step("extract", {
    "type": "document.extract",
    "input": "./inbox/daily_report.pdf"
})

workflow.add_step("analyze", {
    "type": "ai.analyze",
    "prompt": "提取关键指标并输出给管理层的简要摘要"
})

workflow.add_step("notify", {
    "type": "email.send",
    "to": "manager@example.com"
})

result = workflow.run()
print(result.status)
```

---

## 项目结构

```text
python-ai-office/
├── docs/
├── examples/
├── soloai_office/
│   ├── agents/
│   ├── workflows/
│   ├── integrations/
│   └── utils/
├── tests/
├── requirements.txt
├── pyproject.toml
└── README.md
```

---

## 贡献指南

欢迎社区贡献代码、文档、Issue 与功能建议。

### 如何贡献

1. Fork 本仓库
2. 创建功能分支

```bash
git checkout -b feat/your-feature-name
```

3. 提交代码并附带清晰的 commit message

```bash
git commit -m "feat: add document summarization pipeline"
```

4. 推送分支并发起 Pull Request

```bash
git push origin feat/your-feature-name
```

### 开发建议

- 遵循 **PEP 8** 编码规范
- 为新增功能补充单元测试
- 更新相关文档与示例
- 保持 API 命名清晰、一致、可扩展

### 问题反馈

如果你发现 Bug 或有功能建议，请通过 [Issues](https://github.com/SoloAI/python-ai-office/issues) 提交：

- 问题描述
- 复现步骤
- 运行环境
- 日志信息或截图

---

## 许可证

本项目基于 **MIT License** 开源发布。详情请参阅 [LICENSE](./LICENSE)。

---

## 致谢

由 **SoloAI** 维护与发布。  
如果这个项目对你的团队或个人工作流有帮助，欢迎点亮 Star 支持项目发展。