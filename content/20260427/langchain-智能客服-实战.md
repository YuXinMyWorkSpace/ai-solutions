---
title: "LangChain + 智能客服实战：从知识库问答到可落地的企业级客服系统"
date: 2026-04-27
tags: [LangChain, 智能客服, 大语言模型, RAG, Python]
description: "深入讲解如何用 LangChain 构建智能客服系统，涵盖 RAG、会话记忆、工具调用、订单查询、代码实战与企业级最佳实践。"
---

# LangChain + 智能客服实战：从知识库问答到可落地的企业级客服系统

## 1. 引言：为什么这件事值得认真做

过去几年里，企业客服系统经历了明显的演进：从固定规则的 FAQ 机器人，到基于意图识别的对话系统，再到今天由大语言模型驱动的智能客服。对于很多团队来说，真正的挑战并不是“能不能接入一个模型”，而是“如何把模型变成一个稳定、可维护、可衡量的客服产品”。

这正是 **LangChain** 发挥价值的地方。

LangChain 并不是一个“让模型更聪明”的魔法工具，而是一套用于编排大模型应用的工程化框架。它帮助开发者把提示词、检索、记忆、工具调用、工作流和观测能力组织起来，最终构建出可交付的业务系统。对于智能客服场景而言，这种能力尤其关键，因为客服天然具备以下特点：

- **强知识依赖**：回答必须基于企业文档、产品手册、工单经验、售后政策。
- **高准确性要求**：客服错误回复可能带来投诉、退款甚至合规风险。
- **多轮对话复杂**：用户表达不完整、上下文跳跃、情绪化输入都很常见。
- **需要系统集成**：客服往往需要查询订单、库存、物流、账户状态等内部系统。
- **要可监控、可迭代**：上线后必须知道它答得怎么样、错在哪里、如何优化。

如果仅靠一个基础聊天接口，很快会遇到典型问题：

- 模型“编答案”，出现幻觉；
- 不知道企业内部政策，回答与实际流程不一致；
- 多轮对话记不住上下文；
- 用户问“我的订单为什么还没发货”，机器人无法连接业务系统；
- 回答风格不统一，品牌体验差；
- 无法定位是提示词问题、检索问题，还是模型本身的问题。

因此，**智能客服的核心不是聊天，而是“基于企业知识与业务流程的可信对话”**。LangChain 非常适合承担这个中间层角色：它把模型、向量数据库、检索逻辑、记忆机制、工具调用和链路观测串联起来，让客服系统真正具备生产可用性。

本文将围绕“LangChain + 智能客服 + 实战”展开，带你从核心概念到完整实现，一步步搭建一个可运行的客服原型：

- 使用企业知识库实现 **RAG（检索增强生成）**；
- 使用 **会话记忆** 支持多轮上下文；
- 使用 **工具调用** 查询订单状态；
- 设计适合客服场景的提示词与兜底策略；
- 讨论常见踩坑点与上线建议。

如果你正在构建企业问答机器人、售后助手、工单辅助系统，或者希望把大模型能力真正落到客服业务中，这篇文章会是一份偏工程实践的指南。

---

## 2. 核心概念

在开始写代码之前，我们先统一几个关键概念。理解这些概念，能够帮助你更清楚地设计客服系统，而不是把所有问题都丢给模型。

### 2.1 LangChain 是什么

LangChain 是一个面向 LLM 应用开发的框架，它提供了一系列组件，用于组织复杂的 AI 工作流，例如：

- **Prompt Templates**：管理提示词模板；
- **Models**：接入 OpenAI、Anthropic、Ollama 等模型；
- **Chains / Runnables**：组织调用流程；
- **Retrievers**：从知识库检索相关内容；
- **Memory**：保留对话上下文；
- **Tools / Agents**：调用外部函数或系统；
- **Tracing / Observability**：追踪链路，便于排查问题。

对于智能客服，LangChain 更像一个“AI 应用后端框架”。

### 2.2 智能客服的典型架构

一个现代智能客服系统通常包含四层：

1. **用户交互层**：Web Chat、小程序、App、企业微信、WhatsApp 等；
2. **对话编排层**：意图识别、提示词控制、记忆、工具调用；
3. **知识与业务层**：知识库、订单系统、CRM、物流系统、工单平台；
4. **治理与运营层**：日志、评估、反馈、人工接管、敏感词与合规控制。

本文重点讨论中间两层，也就是 LangChain 能直接赋能的部分。

### 2.3 RAG：客服系统的基础能力

RAG（Retrieval-Augmented Generation，检索增强生成）是智能客服落地的关键。

它的核心思想很简单：

1. 用户提问；
2. 系统从企业知识库中检索相关文档片段；
3. 把这些片段连同问题一起交给模型；
4. 模型基于检索结果生成答案。

这样做的好处是：

- 降低幻觉；
- 让回答基于企业真实资料；
- 便于更新知识，不必频繁微调模型；
- 可以追溯“答案依据来自哪篇文档”。

### 2.4 Memory：多轮对话为什么重要

客服对话几乎不可能只靠单轮完成。用户常常会连续提问：

> 用户：我买的耳机怎么还没发货？  
> 客服：请提供订单号。  
> 用户：A20240101。  
> 客服：正在为您查询。  
> 用户：如果今天发不了可以退款吗？

最后一句里，用户没有重复“耳机”与“订单号”，但客服系统必须理解上下文。这就需要 **Memory** 或者你自行管理会话状态。

需要注意的是，记忆并不是“把所有聊天记录都丢给模型”。在实际系统中，需要控制：

- 保留多少轮历史；
- 是否需要摘要；
- 哪些信息结构化存储，如订单号、手机号、问题类型；
- 如何避免上下文过长导致成本和延迟上升。

### 2.5 Tools：客服不只是回答，还要“办事”

高质量客服不仅回答“是什么”，还要处理“帮我查一下”“帮我提交一个工单”“帮我看看物流”。

这就需要让模型调用外部工具，例如：

- 查询订单状态；
- 获取物流详情；
- 检查账户余额；
- 创建售后工单；
- 升级人工客服。

在 LangChain 中，这类能力通常通过 **Tool** 来实现。模型先判断是否需要调用工具，再根据返回结果组织自然语言回复。

### 2.6 Guardrails：为什么客服必须有边界

很多人做原型时容易忽略一个问题：客服场景非常需要边界控制。比如：

- 对未知问题不要瞎答；
- 对退款、赔付、时效等敏感表述必须严格；
- 涉及隐私信息时要校验身份；
- 涉及医疗、金融、法律建议时要限制回答范围。

所以，智能客服系统必须具备：

- 明确的系统提示词；
- 不确定时的兜底话术；
- 工具调用前的参数校验；
- 无法处理时转人工。

---

## 3. 分步实现：从 0 搭建一个智能客服原型

下面我们用一个典型场景来实现：**电商售后客服机器人**。

目标能力包括：

1. 回答知识库问题，如退货规则、发票政策、保修期限；
2. 支持多轮对话；
3. 查询订单状态；
4. 对不确定问题进行安全兜底。

### 3.1 项目依赖安装

我们以 Python 为例，使用较新的 LangChain 组件。

```bash
pip install langchain langchain-openai langchain-community faiss-cpu tiktoken pypdf
```

如果你使用其他模型供应商，也可以替换相应的集成包。

### 3.2 准备知识库文档

假设我们有以下文档：

- `refund_policy.txt`：退换货政策
- `shipping_policy.txt`：物流与发货说明
- `warranty_policy.txt`：保修条款

这些文档可以是 txt、pdf、html，甚至来自数据库或内部 CMS。

### 3.3 文档切分与向量化

客服知识库不能直接整篇丢给模型，通常需要切分成小块，再向量化存储到向量数据库中。这样用户提问时才能快速召回相关片段。

关键点包括：

- **chunk size** 不宜过大，否则检索不精确；
- **chunk overlap** 可以保留上下文连续性；
- 为每个文档块附加 metadata，如来源、文档类型、更新时间。

### 3.4 构建 Retriever

Retriever 的职责是：给定用户问题，返回最相关的文档片段。

常见策略：

- Top-K 相似度检索；
- MMR（最大边际相关性）减少重复；
- 混合检索（关键词 + 向量）；
- 按 metadata 过滤，比如只查“售后政策”类文档。

在客服场景里，Retriever 的质量往往比提示词更影响最终效果。

### 3.5 设计客服提示词

系统提示词建议明确约束：

- 你的角色是某品牌客服助手；
- 优先使用知识库内容回答；
- 不知道时明确说明，不要编造；
- 回答简洁、礼貌；
- 涉及订单、账户类问题，提示用户提供必要信息；
- 需要调用工具时先调用工具再回答。

一个好的客服提示词，不只是让模型“会说话”，更重要的是让它“知道什么时候不要乱说”。

### 3.6 添加会话记忆

对于简单场景，可以保留最近几轮消息；对于复杂场景，建议采用“滑动窗口 + 摘要”的方式。

另外，很多关键信息最好结构化保存，而不是只依赖自然语言上下文，例如：

- 当前订单号；
- 当前意图（退款、发货、保修）；
- 是否已身份校验；
- 是否已转人工。

### 3.7 接入工具：查询订单状态

对于“我的订单什么时候发货”这类问题，仅靠知识库不够，必须访问业务系统。

在原型中，我们可以先用一个模拟函数表示订单查询接口。真实项目里，这里通常会接 CRM、ERP、OMS 或电商中台 API。

### 3.8 增加兜底与人工转接

客服系统上线后，最重要的不是“100% 全能”，而是“在不会的时候也别出错”。

建议设置以下兜底逻辑：

- 检索结果置信度低时，不直接给结论；
- 订单不存在或接口异常时，使用标准化错误提示；
- 涉及投诉、情绪激烈、连续失败时，推荐转人工；
- 对高风险问题使用固定模板回答。

---

## 4. 代码示例

下面给出一个简化但完整的 Python 示例，演示如何用 LangChain 构建智能客服原型。

### 4.1 构建知识库

```python
import os
from langchain_community.document_loaders import TextLoader
from langchain_text_splitters import RecursiveCharacterTextSplitter
from langchain_openai import OpenAIEmbeddings
from langchain_community.vectorstores import FAISS

OPENAI_API_KEY = os.getenv("OPENAI_API_KEY")

# 1. 加载文档
files = [
    "docs/refund_policy.txt",
    "docs/shipping_policy.txt",
    "docs/warranty_policy.txt"
]

documents = []
for file in files:
    loader = TextLoader(file, encoding="utf-8")
    documents.extend(loader.load())

# 2. 切分文档
splitter = RecursiveCharacterTextSplitter(
    chunk_size=500,
    chunk_overlap=80
)
chunks = splitter.split_documents(documents)

# 3. 生成向量并存储
embeddings = OpenAIEmbeddings(model="text-embedding-3-small")
vectorstore = FAISS.from_documents(chunks, embeddings)

# 4. 构建检索器
retriever = vectorstore.as_retriever(search_kwargs={"k": 4})
```

### 4.2 定义订单查询工具

```python
from langchain.tools import tool

MOCK_ORDERS = {
    "A20240101": {
        "status": "待发货",
        "estimated_ship_time": "2024-01-03 18:00",
        "carrier": None,
        "tracking_no": None
    },
    "B20240102": {
        "status": "已发货",
        "estimated_ship_time": "2024-01-02 10:30",
        "carrier": "顺丰速运",
        "tracking_no": "SF1234567890"
    }
}

@tool
def query_order_status(order_id: str) -> str:
    """根据订单号查询订单状态。输入必须是订单号字符串。"""
    order = MOCK_ORDERS.get(order_id)
    if not order:
        return f"未查询到订单 {order_id}，请核对订单号是否正确。"

    return (
        f"订单号：{order_id}\n"
        f"状态：{order['status']}\n"
        f"预计发货时间：{order['estimated_ship_time']}\n"
        f"物流公司：{order['carrier'] or '暂无'}\n"
        f"运单号：{order['tracking_no'] or '暂无'}"
    )
```

### 4.3 构建带检索的客服链路

```python
from langchain_openai import ChatOpenAI
from langchain.prompts import ChatPromptTemplate
from langchain.chains.combine_documents import create_stuff_documents_chain
from langchain.chains import create_retrieval_chain

llm = ChatOpenAI(
    model="gpt-4o-mini",
    temperature=0
)

prompt = ChatPromptTemplate.from_messages([
    (
        "system",
        """
你是某电商品牌的智能客服助手，请严格遵守以下规则：
1. 优先依据提供的知识库内容回答。
2. 如果知识库中没有明确答案，请直接说明“我暂时无法确认”，不要编造。
3. 回答要简洁、专业、礼貌。
4. 涉及退款、保修、发票、物流时，优先引用政策内容。
5. 如果用户提供订单号并询问订单状态，应提示使用订单查询工具。

知识库内容：
{context}
"""
    ),
    ("human", "用户问题：{input}")
])

doc_chain = create_stuff_documents_chain(llm, prompt)
retrieval_chain = create_retrieval_chain(retriever, doc_chain)
```

### 4.4 处理普通知识问答

```python
def answer_with_knowledge(user_query: str):
    result = retrieval_chain.invoke({"input": user_query})
    return result["answer"]

print(answer_with_knowledge("你们的耳机支持7天无理由退货吗？"))
```

### 4.5 加入简单的工具路由逻辑

为了便于理解，这里先不用完整 Agent，而是使用一个简单路由：如果用户提到“订单号”或符合订单号模式，就调用工具；否则走知识库问答。

```python
import re

ORDER_ID_PATTERN = r"[A-Z]\d{8}"

def customer_service_reply(user_query: str) -> str:
    match = re.search(ORDER_ID_PATTERN, user_query)

    if "订单" in user_query and match:
        order_id = match.group(0)
        tool_result = query_order_status.invoke(order_id)
        return f"已为您查询到订单信息：\n{tool_result}"

    return answer_with_knowledge(user_query)

print(customer_service_reply("我的订单 A20240101 为什么还没发货？"))
print(customer_service_reply("发票可以补开吗？"))
```

### 4.6 加入多轮会话记忆

在新版 LangChain 生态中，你可以自行维护消息列表。下面是一个轻量示例：

```python
from langchain_core.messages import HumanMessage, AIMessage, SystemMessage

chat_history = [
    SystemMessage(content="你是某电商品牌的智能客服助手。")
]

def chat_with_memory(user_query: str) -> str:
    global chat_history

    # 这里只做演示：真实项目中建议限制历史长度
    messages = chat_history + [HumanMessage(content=user_query)]
    response = llm.invoke(messages)

    chat_history.append(HumanMessage(content=user_query))
    chat_history.append(AIMessage(content=response.content))
    return response.content

print(chat_with_memory("我买的耳机一直没发货"))
print(chat_with_memory("如果今天发不了，可以退款吗？"))
```

不过在真实客服系统中，更推荐把“记忆”与“RAG / 工具调用”一起编排，而不是单独聊天。你可以在服务端维护一个 `session_id`，并把以下信息结构化存储到 Redis 或数据库中：

- 最近 5~10 轮对话；
- 用户当前订单号；
- 当前问题标签；
- 是否已命中转人工条件。

### 4.7 一个更贴近生产的统一处理函数

```python
def smart_customer_service(user_query: str, session: dict) -> str:
    # 1. 优先识别订单号
    match = re.search(ORDER_ID_PATTERN, user_query)
    if match:
        session["order_id"] = match.group(0)

    # 2. 如果是订单相关问题且已有订单号，则查工具
    if "订单" in user_query or "发货" in user_query or "物流" in user_query:
        if session.get("order_id"):
            result = query_order_status.invoke(session["order_id"])
            return f"这是您订单的最新状态：\n{result}\n\n如您需要，我也可以继续为您说明退款或催发货规则。"
        else:
            return "为了帮您查询订单状态，请提供订单号。"

    # 3. 其他问题走知识库问答
    answer = answer_with_knowledge(user_query)

    # 4. 简单兜底
    if "暂时无法确认" in answer or len(answer.strip()) < 8:
        return "抱歉，这个问题我暂时无法准确判断。建议您联系人工客服，我们会进一步为您处理。"

    return answer

session = {}
print(smart_customer_service("我的订单还没发货", session))
print(smart_customer_service("订单号是 A20240101", session))
print(smart_customer_service("那如果明天还不发可以退款吗？", session))
```

这个版本已经具备了一个基础客服机器人的核心能力：

- 有知识库；
- 能检索；
- 能查询订单；
- 能维护简单会话状态；
- 有一定兜底逻辑。

在生产环境中，你可以进一步封装成 FastAPI 服务，对接前端聊天窗口。

---

## 5. 最佳实践与常见陷阱

真正把智能客服做上线，难点往往不在“代码跑通”，而在“系统稳定可靠”。下面是一些非常关键的实践建议。

### 5.1 不要把所有问题都交给大模型

很多客服问题其实可以走更简单、更确定的路径：

- 查询订单：调用 API；
- 查询物流：调用 API；
- 判断是否满足退款条件：规则 + 知识库；
- 用户身份校验：业务系统处理。

大模型适合做的是：

- 理解自然语言；
- 组织答案；
- 多轮上下文衔接；
- 在知识中做语义匹配。

换句话说，**模型负责理解与表达，业务系统负责事实与执行**。

### 5.2 检索质量决定回答上限

很多人发现“模型答得不准”，实际根因不在模型，而在检索。

常见问题包括：

- 文档切分太粗，导致关键信息被淹没；
- chunk 太碎，语义不完整；
- 文档版本混乱，旧政策被召回；
- 相似度检索缺乏 metadata 过滤；
- FAQ 与长文档混在一起，影响召回质量。

建议做法：

- 为不同知识类型分库或加标签；
- 保留文档更新时间与版本号；
- 对高频问题建立标准 FAQ；
- 用真实用户问题评测检索效果。

### 5.3 设计“拒答”机制，而不是追求全答

客服机器人最危险的情况，不是“答不上来”，而是“答错了还很自信”。

建议你显式设计拒答机制：

- 没有检索到足够相关内容时拒答；
- 敏感业务问题使用固定模板；
- 超出权限范围时提示人工协助；
- 给出答案时附带来源依据。

### 5.4 工具调用要做参数校验

当模型开始调用订单、账户、支付相关工具时，必须谨慎：

- 订单号格式校验；
- 用户身份是否已验证；
- 工具返回异常时不要把技术报错直接暴露给用户；
- 涉及修改动作时要有二次确认。

例如“帮我取消订单”绝不能只因为模型理解了这句话就直接执行。必须增加安全流程。

### 5.5 控制上下文长度与成本

长对话历史、多个知识片段、复杂提示词都会增加 Token 消耗，进而带来成本和延迟问题。

建议：

- 只保留必要历史；
- 定期摘要旧对话；
- 控制检索返回文档数；
- 对高频简单问题走缓存；
- 为不同问题选择不同大小的模型。

比如：

- FAQ 问答用小模型；
- 复杂投诉总结用更强模型；
- 订单查询优先规则引擎 + 工具。

### 5.6 人工转接不是失败，而是系统能力的一部分

很多团队把“转人工”看成机器人不够聪明，但在企业客服里，人工转接是必需能力。建议设定明确条件：

- 连续两次未命中有效答案；
- 用户情绪激烈；
- 涉及赔偿、投诉升级；
- 需要人工审批；
- 高价值客户的专属服务。

优秀的客服机器人不是永远不转人工，而是能在正确时机把问题交给正确的人。

### 5.7 做评估与可观测性

没有评估，就没有优化方向。至少要监控以下指标：

- 首次解决率；
- 人工转接率；
- 检索命中率；
- 用户满意度；
- 幻觉率；
- 工具调用成功率；
- 平均响应时间。

如果条件允许，建议接入链路追踪工具，记录每次对话的：

- 用户问题；
- 检索结果；
- 提示词；
- 工具调用参数与返回；
- 最终回答。

这会极大提升排障和迭代效率。

---

## 6. 结语

LangChain 之所以适合智能客服，并不是因为它让大模型“变得万能”，而是因为它提供了一套把模型能力工程化、产品化的方式。对于企业客服来说，真正重要的从来不是炫技，而是：

- 回答是否基于真实知识；
- 是否能接入业务系统处理实际问题；
- 多轮对话是否稳定；
- 错误时能否安全兜底；
- 上线后是否可监控、可优化。

通过本文的实战示例，我们构建了一个基础但完整的客服原型：

- 用 LangChain 组织对话流程；
- 用 RAG 连接企业知识库；
- 用 Tool 查询订单信息；
- 用会话状态支持多轮交互；
- 用兜底策略控制风险。

如果你准备把它进一步投入生产，下一步可以考虑：

1. 接入真实的向量数据库，如 Milvus、pgvector、Weaviate；
2. 用 FastAPI / Django 封装 API 服务；
3. 引入 Redis 保存会话状态；
4. 构建人工转接与工单系统联动；
5. 建立离线评测集和线上监控面板；
6. 针对客服场景做更细粒度的意图路由。

智能客服已经不再只是“自动回复工具”，而是在逐渐变成企业服务体验的核心入口。LangChain 提供了一个非常实用的起点，帮助团队从 Demo 走向真正可落地的应用。

如果你正在做相关项目，我的建议是：**先做一个小而可控的垂直场景，优先把知识可信、流程闭环、风险可控做好，再逐步扩展能力边界。** 这通常比一开始追求“全能客服”更现实，也更容易成功。

---

## 商务咨询 / 代做服务

如果你想把本文方案真正落地到业务里，可以直接联系 SoloAI：

- 邮箱：379744050@qq.com
- 适合需求：知识库/RAG、数据清洗、Agent 自动化、内容增长、技术方案落地
- 响应时效：24 小时内回复

### 内容服务报价
- Article Pack：$99 / 10篇技术文章
- Strategy Pack：$199 / AIO策略+SEO资产
- Growth Pack：$499 / 月度内容增长包

### 支付方式
- 中国区：支付宝, 微信支付
- 海外：PayPal, USDT (TRC20)

### 咨询时建议附带
- 你的行业/项目类型
- 目标交付物
- 预算范围
- 截止时间
