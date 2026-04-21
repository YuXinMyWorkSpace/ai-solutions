```markdown
# SoloAI Python AI 自动化办公
[![Build Status](https://img.shields.io/github/actions/workflow/status/SoloAI/python-ai-office/ci.yml?branch=main)](https://github.com/SoloAI/python-ai-office/actions)
[![License](https://img.shields.io/github/license/SoloAI/python-ai-office)](./LICENSE)

一个面向开发者与企业场景的 **Python AI 自动化办公** 开源项目，专注于通过 AI + Python 工作流提升文档处理、数据整理、表格分析、邮件生成与日常办公自动化效率。  
该项目帮助团队快速构建可扩展、可集成、可部署的智能办公自动化解决方案，适用于 OA、RPA、知识处理和业务流程自动化场景。

---

## 概述

**SoloAI Python AI 自动化办公** 是一个结合 Python 脚本能力、AI 模型调用能力与办公文件处理能力的自动化框架。  
它支持对常见办公任务进行智能化编排，例如 Excel/CSV 数据清洗、Word/PDF 信息提取、邮件内容生成、批量报告创建以及基于自然语言的办公流程自动化。

> 适用关键词：**Python AI 自动化办公、AI Office Automation、智能办公自动化、Python 办公自动化、AI 文档处理、Excel 自动化、PDF 解析、邮件自动生成**

---

## 核心特性

- **多类型办公文件自动处理**  
  支持 Excel、CSV、Word、PDF、TXT 等文档的读取、清洗、转换与内容提取。

- **AI 驱动的文本生成与摘要**  
  可基于大语言模型生成邮件、周报、会议纪要、通知公告和业务文案。

- **表格分析与数据自动化**  
  自动完成数据汇总、分类统计、异常检测、报表生成与可视化输出。

- **可编排工作流引擎**  
  通过 Python 配置任务流，将“读取文件 → 分析内容 → 生成结果 → 导出报告”串联为自动化办公流程。

- **易于集成与扩展**  
  支持接入 OpenAI 兼容接口、本地模型服务、企业内部 API 与自定义插件。

- **面向生产环境设计**  
  提供模块化结构、日志记录、环境变量配置与 CI 友好的工程实践，便于部署到本地或服务器环境。

---

## 安装

### 环境要求

- Python 3.9+
- pip 23+
- 建议使用虚拟环境

### 1. 克隆仓库

```bash
git clone https://github.com/SoloAI/python-ai-office.git
cd python-ai-office
```

### 2. 创建虚拟环境

```bash
python -m venv .venv
source .venv/bin/activate
```

Windows:

```powershell
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
```

---

## 快速开始

下面示例展示了如何使用 SoloAI 对一份 Excel 文件进行读取、分析，并生成摘要报告。

```python
from soloai.office import OfficeAgent

agent = OfficeAgent(
    model="gpt-4o-mini",
    task="分析销售报表并输出摘要"
)

result = agent.run(
    input_file="data/sales_report.xlsx",
    output_file="output/summary.md"
)

print(result)
```

运行方式：

```bash
python examples/quickstart.py
```

---

## 使用示例

### 1. 自动生成邮件内容

根据客户信息和业务场景自动生成邮件草稿：

```python
from soloai.office import MailAgent

agent = MailAgent(model="gpt-4o-mini")

email = agent.generate(
    subject="产品续费提醒",
    context={
        "customer_name": "ACME Corp",
        "renewal_date": "2025-09-01",
        "plan": "Enterprise",
        "language": "zh-CN"
    }
)

print(email)
```

---

### 2. Excel 数据分析与报告输出

对表格进行自动汇总并导出 Markdown 报告：

```python
from soloai.office import ExcelAnalyzer

analyzer = ExcelAnalyzer(model="gpt-4o-mini")

report = analyzer.analyze(
    file_path="data/finance.xlsx",
    sheet_name="Q2",
    output_format="markdown"
)

print(report)
```

---

### 3. PDF 文档提取与总结

从 PDF 合同或报告中提取关键信息并生成摘要：

```python
from soloai.office import DocumentAgent

agent = DocumentAgent(model="gpt-4o-mini")

summary = agent.summarize(
    file_path="docs/contract.pdf",
    prompt="提取合同关键条款、风险点和付款节点"
)

print(summary)
```

---

### 4. 批量办公任务自动化

批量处理指定目录中的文件，并统一输出结果：

```python
from soloai.office import WorkflowRunner

runner = WorkflowRunner(model="gpt-4o-mini")

runner.run_batch(
    input_dir="input/",
    output_dir="output/",
    workflow="summarize_and_export"
)
```

---

## 项目结构

```text
python-ai-office/
├── soloai/
│   ├── office/
│   │   ├── agents/
│   │   ├── parsers/
│   │   ├── workflows/
│   │   └── utils/
├── examples/
├── tests/
├── requirements.txt
├── .env.example
└── README.md
```

---

## 配置说明

项目通过环境变量管理模型配置与运行参数：

| 变量名 | 说明 | 示例 |
|---|---|---|
| `OPENAI_API_KEY` | AI 模型服务密钥 | `sk-***` |
| `OPENAI_BASE_URL` | OpenAI 兼容接口地址 | `https://api.openai.com/v1` |
| `MODEL_NAME` | 默认模型名称 | `gpt-4o-mini` |
| `LOG_LEVEL` | 日志级别 | `INFO` |

---

## 开发与贡献

我们欢迎社区贡献代码、提交 Issue 和改进建议。

### 贡献流程

1. Fork 本项目
2. 创建功能分支

```bash
git checkout -b feat/your-feature-name
```

3. 提交修改

```bash
git commit -m "feat: add new office automation workflow"
```

4. 推送分支并提交 Pull Request

```bash
git push origin feat/your-feature-name
```

### 开发建议

- 遵循 **PEP 8** 编码规范
- 为新增功能补充测试用例
- 保持模块低耦合、可复用
- 更新相关文档与示例代码

### 本地测试

```bash
pytest
```

### 代码质量检查

```bash
ruff check .
black .
```

---

## 路线图

- [ ] 支持更多办公文档格式
- [ ] 集成企业微信 / 钉钉 / 邮件通知
- [ ] 增加可视化工作流配置
- [ ] 支持本地大模型推理
- [ ] 增强 RAG 知识库办公场景

---

## 许可证

本项目基于 **MIT License** 开源，详情请参阅 [LICENSE](./LICENSE)。

---

## 致谢

本项目由 **SoloAI** 维护，致力于推动 **Python AI 自动化办公**、**智能工作流自动化** 与 **企业 AI 应用开发** 的开源实践。

如果你正在寻找一个适用于文档智能处理、数据分析自动化、AI 生成办公内容和业务流程自动化的 Python 项目，欢迎 Star、Fork 与参与贡献。
```