---
title: "Prompt Engineering + 数据清洗 + 实战：用高质量输入打造可靠 AI 工作流"
date: 2026-04-26
tags: [Prompt Engineering, 数据清洗, LLM, Python, AI实战]
description: "深入解析 Prompt Engineering 与数据清洗的结合实践，涵盖核心概念、Python 代码示例、实施步骤、最佳实践与常见陷阱。"
---

# Prompt Engineering + 数据清洗 + 实战：用高质量输入打造可靠 AI 工作流

## 1. 引言：为什么这件事如此重要

在大模型应用快速落地的今天，很多团队把注意力集中在“选哪个模型”“上下文窗口有多大”“推理速度够不够快”这些问题上，却常常忽视了两个对效果影响极大的基础环节：**Prompt Engineering（提示工程）**与**数据清洗**。

如果把大模型系统看作一个生产线，那么模型本身更像是“高性能引擎”，而 Prompt 是控制引擎的方向盘，数据清洗则是进入引擎前的燃料过滤系统。方向盘打不好，模型会偏航；燃料不纯净，再强的引擎也会出现噪声、误判、幻觉，甚至直接输出不可用结果。

尤其在企业级场景中，这个问题更加突出。无论是客服问答、内容生成、文档抽取、舆情分析，还是知识库问答、数据标注、结构化信息提取，实际输入数据几乎都不是“理想状态”：

- 文本中夹杂 HTML、特殊符号、乱码
- 字段命名不统一
- 存在重复、缺失、异常值
- 同一语义的表达方式高度分散
- 用户输入噪声极大，口语化严重

这意味着：**Prompt 再优秀，如果喂给模型的是脏数据，最终效果依然不稳定；反过来，数据再干净，如果缺乏清晰、可约束、可复用的 Prompt 设计，模型结果同样难以落地。**

因此，真正可用的 AI 应用，不是单纯比拼模型参数，而是要建立一条完整链路：

> 数据清洗 → 输入标准化 → Prompt 设计 → 模型调用 → 输出校验 → 结果迭代

本文将从实战视角出发，系统介绍 Prompt Engineering 与数据清洗如何协同工作，并通过 Python 示例演示如何搭建一个面向真实业务的数据预处理与提示生成流程，帮助你构建更稳定、更可维护、更具可扩展性的 LLM 工作流。

---

## 2. 核心概念

### 2.1 什么是 Prompt Engineering

Prompt Engineering 指的是围绕大模型输入提示进行设计、组织、约束和优化的过程，目标是让模型更稳定地输出符合预期的结果。

它并不只是“会提问”，更像是一种**面向语言模型的人机接口设计**。优秀的 Prompt 通常包含以下要素：

- **任务定义清晰**：告诉模型要做什么
- **上下文充分**：提供必要背景信息
- **输出格式明确**：例如 JSON、Markdown、表格等
- **约束条件完整**：限制长度、语气、字段范围、错误处理方式
- **示例驱动**：通过 few-shot 示例降低歧义

例如，下面两个 Prompt 的效果通常会有明显差异：

**低质量 Prompt：**

```text
帮我总结这段用户评论。
```

**高质量 Prompt：**

```text
你是一名电商运营分析师。
请根据输入的用户评论，完成以下任务：
1. 提取评论主题
2. 判断情绪：正面 / 中性 / 负面
3. 提取是否提到物流、价格、质量、客服
4. 使用 JSON 输出

输出格式：
{
  "theme": "",
  "sentiment": "",
  "mentions": {
    "logistics": false,
    "price": false,
    "quality": false,
    "service": false
  }
}
```

本质上，Prompt Engineering 的价值在于**减少模型的自由解释空间**，提升结果的一致性与可解析性。

### 2.2 什么是数据清洗

数据清洗（Data Cleaning）是指对原始数据进行检测、纠正、转换和标准化的过程，以提高数据质量，便于分析、建模或供下游系统使用。

在大模型场景中，数据清洗的意义尤为重要，因为 LLM 对输入非常敏感。常见清洗任务包括：

- 去除 HTML 标签、脚本、样式信息
- 删除多余空白符、换行符、制表符
- 统一大小写、标点、时间格式
- 去重与重复文本压缩
- 修复乱码或非法字符
- 缺失值填充或剔除
- 字段映射与标签规范化
- 敏感信息脱敏

例如，原始评论数据可能长这样：

```text
<div>物流真的慢！！！   三天了还没到，客服也不回。。。</div>
```

清洗后更适合模型处理：

```text
物流真的慢！三天了还没到，客服也不回复。
```

### 2.3 Prompt 与数据清洗的关系

很多人把 Prompt Engineering 看成“模型层”的工作，把数据清洗看成“数据层”的工作，实际上两者高度耦合。

可以这样理解：

- **数据清洗决定输入质量下限**
- **Prompt Engineering 决定输出效果上限**

如果输入文本中存在大量无意义噪声，Prompt 必须花更多篇幅“容错”；而如果数据经过标准化处理，Prompt 可以更聚焦业务目标。

因此，成熟实践往往不是先写 Prompt，而是先回答三个问题：

1. 我的原始数据长什么样？
2. 哪些噪声会影响模型判断？
3. 我希望模型输出什么结构，反向需要怎样的清洗与字段整理？

这是一种**以输出为导向设计输入**的工程思路。

---

## 3. 分步实现：从脏数据到可用 AI 工作流

下面以“电商用户评论分析”为例，构建一个完整流程。目标是让模型对评论进行结构化分析，输出主题、情绪和关键词标签。

### 第一步：明确任务目标

不要一上来就调用模型，先把任务拆清楚。

我们要实现的目标是：

- 输入：原始用户评论文本
- 输出：结构化分析结果
- 字段包括：
  - 评论主题
  - 情绪分类
  - 是否提及物流、价格、质量、客服

这里有一个关键原则：**先定义输出 Schema，再设计 Prompt 和清洗规则。**

例如输出 Schema：

```json
{
  "theme": "物流慢",
  "sentiment": "负面",
  "mentions": {
    "logistics": true,
    "price": false,
    "quality": false,
    "service": true
  }
}
```

### 第二步：分析原始数据问题

假设我们拿到的评论数据来自多个渠道，常见问题可能有：

- HTML 标签残留
- Emoji、特殊字符过多
- 重复评论
- 空评论、超短评论
- 大量口语、错别字、缩写
- 中英文标点混用

这些问题会影响模型判断，尤其是结构化抽取任务。

### 第三步：设计清洗策略

清洗并不是“越狠越好”，而是要围绕任务目标做最小充分处理。比如评论情绪分析中，感叹号、重复词、语气词有时是有价值的，不应盲目删除。

建议采用以下策略：

#### 1）基础清洗

- 去 HTML 标签
- 去多余空白
- 统一标点
- 清理控制字符

#### 2）业务清洗

- 去除空评论
- 合并重复评论
- 过滤过短无意义文本，例如“嗯”“好”“。”

#### 3）安全清洗

- 手机号、邮箱等敏感信息脱敏
- 避免把用户隐私直接送入模型

### 第四步：将清洗后的数据映射到 Prompt 模板

Prompt 最好模板化，而不是每次手写。模板化的好处包括：

- 便于批量处理
- 便于版本管理
- 便于 A/B 测试
- 便于统一输出格式

一个好的模板通常包含：

- 角色设定
- 任务描述
- 输出格式
- 约束条件
- 输入数据占位符

### 第五步：输出校验与失败重试

生产环境里，不能假设模型每次都返回完美 JSON。因此需要：

- 校验返回格式
- 检查字段是否缺失
- 对异常结果重试或回退
- 必要时做二次解析

这一步非常关键，也是很多“Demo 能跑、线上不稳”的根本原因。

---

## 4. 代码示例

下面用 Python 实现一个简化版流程：原始评论清洗 → Prompt 构造 → 模拟调用模型 → 结果校验。

### 4.1 准备示例数据

```python
raw_reviews = [
    "<div>物流真的慢！！！   三天了还没到，客服也不回。。。</div>",
    "包装不错，质量也可以，下次还会买！",
    "  ",
    "价格有点贵，不过东西还行",
    "客服态度很好，但是发货速度一般",
    "物流真的慢！！！   三天了还没到，客服也不回。。。"
]
```

### 4.2 数据清洗函数

```python
import re
import html
from typing import List


def remove_html_tags(text: str) -> str:
    return re.sub(r'<[^>]+>', '', text)


def normalize_punctuation(text: str) -> str:
    replacements = {
        '。。。': '。',
        '！！！！！': '！',
        '!!!': '！',
        '..': '。'
    }
    for old, new in replacements.items():
        text = text.replace(old, new)
    return text


def remove_extra_whitespace(text: str) -> str:
    return re.sub(r'\s+', ' ', text).strip()


def mask_sensitive_info(text: str) -> str:
    # 脱敏手机号
    text = re.sub(r'1[3-9]\d{9}', '[PHONE]', text)
    # 脱敏邮箱
    text = re.sub(r'[\w\.-]+@[\w\.-]+', '[EMAIL]', text)
    return text


def clean_text(text: str) -> str:
    text = html.unescape(text)
    text = remove_html_tags(text)
    text = mask_sensitive_info(text)
    text = normalize_punctuation(text)
    text = remove_extra_whitespace(text)
    return text


def is_meaningful(text: str, min_len: int = 4) -> bool:
    return bool(text) and len(text) >= min_len


def clean_reviews(reviews: List[str]) -> List[str]:
    cleaned = []
    seen = set()

    for review in reviews:
        text = clean_text(review)
        if not is_meaningful(text):
            continue
        if text in seen:
            continue
        seen.add(text)
        cleaned.append(text)

    return cleaned


cleaned_reviews = clean_reviews(raw_reviews)
print(cleaned_reviews)
```

输出示例：

```python
[
    '物流真的慢！ 三天了还没到，客服也不回。',
    '包装不错，质量也可以，下次还会买！',
    '价格有点贵，不过东西还行',
    '客服态度很好，但是发货速度一般'
]
```

### 4.3 构造 Prompt 模板

```python
def build_prompt(review: str) -> str:
    return f"""
你是一名电商评论分析助手。
请根据输入评论完成结构化分析。

任务要求：
1. 提取评论主题
2. 判断情绪，只能输出：正面 / 中性 / 负面
3. 判断是否提及以下维度：物流、价格、质量、客服
4. 仅输出 JSON，不要输出解释

输出格式：
{{
  "theme": "",
  "sentiment": "",
  "mentions": {{
    "logistics": false,
    "price": false,
    "quality": false,
    "service": false
  }}
}}

输入评论：
{review}
""".strip()
```

### 4.4 模拟模型调用

实际项目中你会调用具体的 LLM API。这里为了聚焦流程，先写一个模拟函数。

```python
import json


def mock_llm_response(review: str) -> str:
    if "物流" in review or "发货" in review:
        return json.dumps({
            "theme": "物流服务",
            "sentiment": "负面" if "慢" in review or "一般" in review else "中性",
            "mentions": {
                "logistics": True,
                "price": False,
                "quality": False,
                "service": "客服" in review
            }
        }, ensure_ascii=False)

    if "价格" in review:
        return json.dumps({
            "theme": "价格",
            "sentiment": "中性",
            "mentions": {
                "logistics": False,
                "price": True,
                "quality": False,
                "service": False
            }
        }, ensure_ascii=False)

    return json.dumps({
        "theme": "商品体验",
        "sentiment": "正面",
        "mentions": {
            "logistics": False,
            "price": False,
            "quality": "质量" in review,
            "service": False
        }
    }, ensure_ascii=False)
```

### 4.5 结果校验

```python
def validate_result(result: dict) -> bool:
    required_keys = {"theme", "sentiment", "mentions"}
    mention_keys = {"logistics", "price", "quality", "service"}

    if not required_keys.issubset(result.keys()):
        return False

    if result["sentiment"] not in {"正面", "中性", "负面"}:
        return False

    if not isinstance(result["mentions"], dict):
        return False

    if not mention_keys.issubset(result["mentions"].keys()):
        return False

    return True


def analyze_reviews(reviews: List[str]) -> List[dict]:
    results = []

    for review in reviews:
        prompt = build_prompt(review)
        print("Prompt:\n", prompt, "\n")

        raw_output = mock_llm_response(review)
        parsed = json.loads(raw_output)

        if validate_result(parsed):
            results.append({
                "review": review,
                "analysis": parsed
            })
        else:
            results.append({
                "review": review,
                "analysis": None,
                "error": "Invalid model output"
            })

    return results


final_results = analyze_reviews(cleaned_reviews)
print(json.dumps(final_results, ensure_ascii=False, indent=2))
```

### 4.6 如果接入真实 LLM API，应注意什么

如果你接入 OpenAI、Azure OpenAI 或其他模型服务，可以保留相同的清洗与模板化流程，只替换模型调用层。

一个更接近真实项目的调用结构可能是：

```python
def call_llm(client, prompt: str) -> str:
    response = client.responses.create(
        model="gpt-4.1",
        input=prompt
    )
    return response.output_text
```

然后再配合 `json.loads()` 和校验逻辑进行结果解析。生产环境建议增加：

- 超时控制
- 重试机制
- 日志记录
- Prompt 版本号
- 输出异常样本回流

---

## 5. 最佳实践与常见陷阱

### 5.1 最佳实践一：先定义输出，再反推输入

这是最容易被忽略的一点。很多团队先收集数据、写 Prompt、调用模型，最后才发现输出无法解析、字段不完整、结果无法入库。

更合理的做法是：

1. 先定义输出 JSON Schema
2. 明确哪些字段必须稳定返回
3. 再设计 Prompt
4. 最后反推需要怎样的数据清洗

这会显著提升整体可维护性。

### 5.2 最佳实践二：清洗要服务于任务，而不是追求“绝对干净”

数据清洗不是把文本变得越短越整洁越好，而是保留对任务有价值的信息。

例如情绪分析中：

- “太慢了！！！” 中的重复感叹号可能强化负面情绪
- “还行吧” 是典型中性表达
- “客服不回” 是明确服务问题

如果一刀切把这些语气特征清掉，模型效果反而会下降。

### 5.3 最佳实践三：模板化 Prompt，避免散落在业务代码中

不要把 Prompt 写死在多个函数、脚本或服务里。建议：

- 建立 Prompt 模板目录
- 为模板添加版本号
- 记录适用场景
- 用变量注入上下文
- 对模板做回归测试

这样当你优化 Prompt 时，才能明确知道哪些线上行为受到影响。

### 5.4 最佳实践四：输出必须可验证

一个能“看起来像对”的模型结果，不等于一个能进入生产系统的结果。特别是在结构化场景中，输出必须具备：

- 固定字段
- 固定枚举值
- 类型正确
- 缺失可识别
- 异常可回退

因此，**JSON 校验不是锦上添花，而是必需品。**

### 5.5 常见陷阱一：把 Prompt 当魔法

很多人遇到结果不好时，第一反应是继续堆 Prompt 技巧，例如加更多角色设定、更多限制语、更多示例。但如果问题根源在数据噪声、字段不一致或样本分布异常，Prompt 调整的收益会非常有限。

要记住：

> Prompt 解决的是“表达与约束问题”，数据清洗解决的是“输入质量问题”。

两者不能互相替代。

### 5.6 常见陷阱二：忽略数据分层

不同来源的数据往往质量差异巨大。比如：

- App 评论更口语化
- 工单文本更长、更正式
- 社媒评论噪声更多

如果你对所有数据采用同一套清洗规则和同一个 Prompt，很可能效果不稳定。更合理的方法是做数据分层：

- 按渠道分层
- 按文本长度分层
- 按语言或地区分层
- 按任务类型分层

然后为不同分层定制清洗与 Prompt 策略。

### 5.7 常见陷阱三：没有建立反馈闭环

Prompt Engineering 不是一次性工作，数据清洗也不是。生产环境里，应该持续收集：

- 模型错误样本
- 解析失败样本
- 用户纠正结果
- 高价值边界案例

基于这些反馈，你可以不断优化：

- 清洗规则
- Prompt 模板
- Few-shot 示例
- 输出校验逻辑

真正成熟的系统，都是在反馈闭环中演进出来的。

---

## 6. 结论

Prompt Engineering 与数据清洗，表面上看是两个不同方向：一个偏模型交互，一个偏数据治理；但在实际 AI 应用建设中，它们本质上共同服务于同一个目标：**让模型接收到更清晰、更稳定、更可控的输入，并产出更可靠、更结构化、更可落地的结果。**

如果只关注模型能力而忽略输入质量，系统会变得脆弱；如果只做数据清洗而缺乏良好的 Prompt 设计，模型价值又难以充分释放。真正有效的实践路径是把两者串成一个完整工程链路：

> 明确业务目标 → 定义输出结构 → 清洗与标准化输入 → 设计 Prompt 模板 → 调用模型 → 校验输出 → 持续优化

对开发者和技术团队而言，这种方法带来的不仅是“效果更好”，更重要的是：

- 系统更稳定
- 调试更高效
- 输出更易集成
- 迭代更可控
- 成本更可预测

如果你正准备把大模型接入真实业务，不妨从最基础但最关键的两件事开始：**认真清洗数据，认真设计 Prompt。** 这往往比盲目追逐更新的模型版本，更能决定你的项目能否真正跑通实战。
