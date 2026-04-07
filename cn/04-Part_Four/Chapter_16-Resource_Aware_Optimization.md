# Chapter 16: Resource-Aware Optimization

> 第十六章：资源感知优化

Resource-Aware Optimization enables intelligent agents to dynamically monitor and manage computational, temporal, and financial resources during operation. This differs from simple planning, which primarily focuses on action sequencing. Resource-Aware Optimization requires agents to make decisions regarding action execution to achieve goals within specified resource budgets or to optimize efficiency. This involves choosing between more accurate but expensive models and faster, lower-cost ones, or deciding whether to allocate additional compute for a more refined response versus returning a quicker, less detailed answer.

> 资源感知优化使智能体在运行中动态监控并管理计算、时间与财务资源。这与主要关注动作排序的简单规划不同：资源感知优化要求智能体就动作执行做决策，以在既定资源预算内达成目标或提升效率——例如在更准确但昂贵的模型与更快、更廉价模型之间取舍，或在投入更多算力以得到更精细答复与更快返回较简略答案之间取舍。

For example, consider an agent tasked with analyzing a large dataset for a financial analyst. If the analyst needs a preliminary report immediately, the agent might use a faster, more affordable model to quickly summarize key trends. However, if the analyst requires a highly accurate forecast for a critical investment decision and has a larger budget and more time, the agent would allocate more resources to utilize a powerful, slower, but more precise predictive model. A key strategy in this category is the fallback mechanism, which acts as a safeguard when a preferred model is unavailable due to being overloaded or throttled. To ensure graceful degradation, the system automatically switches to a default or more affordable model, maintaining service continuity instead of failing completely.

> 例如，某智能体需为金融分析师分析大型数据集：若分析师要立即得到初步报告，智能体可能用更快、更经济的模型快速总结关键趋势；若分析师为关键投资决策需要高精度预测且有更大预算与时间，智能体则会分配更多资源使用更强大、更慢但更精确的预测模型。该类策略中的关键是回退机制：当首选模型因过载或限流不可用时作为保险；为做到优雅降级，系统自动切换到默认或更经济的模型，维持服务连续性而非彻底失败。

## Practical Applications & Use Cases

> ## 实际应用与用例

Practical use cases include:

> 实际用例包括：

* **Cost-Optimized LLM Usage:** An agent deciding whether to use a large, expensive LLM for complex tasks or a smaller, more affordable one for simpler queries, based on a budget constraint.  
* **Latency-Sensitive Operations:** In real-time systems, an agent chooses a faster but potentially less comprehensive reasoning path to ensure a timely response.  
* **Energy Efficiency:** For agents deployed on edge devices or with limited power, optimizing their processing to conserve battery life.  
* **Fallback for service reliability:**  An agent automatically switches to a backup model when the primary choice is unavailable, ensuring service continuity and graceful degradation.  
* **Data Usage Management:** An agent opting for summarized data retrieval instead of full dataset downloads to save bandwidth or storage.  
* **Adaptive Task Allocation:** In multi-agent systems, agents self-assign tasks based on their current computational load or available time.

> * **成本优化的 LLM 使用：** 智能体在预算约束下决定复杂任务用大型昂贵 LLM，简单查询用更小更经济的模型。  
> * **延迟敏感操作：** 在实时系统中选择更快但可能不够全面的推理路径以保证及时响应。  
> * **能效：** 在边缘设备或供电受限场景优化处理以延长电池续航。  
> * **服务可靠性的回退：** 主模型不可用时自动切换备用模型，保证连续性与优雅降级。  
> * **数据用量管理：** 以摘要检索替代全量下载以节省带宽或存储。  
> * **自适应任务分配：** 多智能体系统中按当前算力负载或可用时间自行认领任务。

## Hands-On Code Example

> ## 动手代码示例

An intelligent system for answering user questions can assess the difficulty of each question. For simple queries, it utilizes a cost-effective language model such as Gemini Flash. For complex inquiries, a more powerful, but expensive, language model (like Gemini Pro) is considered. The decision to use the more powerful model also depends on resource availability, specifically budget and time constraints. This system dynamically selects appropriate models.

> 面向问答的智能系统可评估每道题难度：简单查询用 Gemini Flash 等经济型模型；复杂问题则考虑更强大但更昂贵的模型（如 Gemini Pro）。是否启用更强模型还取决于资源可用性，尤其是预算与时间约束；系统据此动态选型。

For example, consider a travel planner built with a hierarchical agent. The high-level planning, which involves understanding a user's complex request, breaking it down into a multi-step itinerary, and making logical decisions, would be managed by a sophisticated and more powerful LLM like Gemini Pro. This is the "planner" agent that requires a deep understanding of context and the ability to reason.

> 例如分层智能体构建的旅行规划器：理解用户复杂需求、拆解为多步行程并做逻辑决策的高层规划，由更强大、更复杂的 LLM（如 Gemini Pro）承担——即需要深度语境理解与推理能力的「规划」智能体。

However, once the plan is established, the individual tasks within that plan, such as looking up flight prices, checking hotel availability, or finding restaurant reviews, are essentially simple, repetitive web queries. These "tool function calls" can be executed by a faster and more affordable model like Gemini Flash. It is easier to visualize why the affordable model can be used for these straightforward web searches, while the intricate planning phase requires the greater intelligence of the more advanced model to ensure a coherent and logical travel plan.

> 计划确定后，计划内的单项任务（查机票、看酒店空房、找餐厅评价等）本质上是简单、重复的网页查询；这些「工具函数调用」可由 Gemini Flash 等更快更经济的模型执行。直观上，简单检索可用经济模型，而复杂规划阶段需要更强模型以保证行程连贯、逻辑自洽。

Google's ADK supports this approach through its multi-agent architecture, which allows for modular and scalable applications. Different agents can handle specialized tasks. Model flexibility enables the direct use of various Gemini models, including both Gemini Pro and Gemini Flash, or integration of other models through LiteLLM. The ADK's orchestration capabilities support dynamic, LLM-driven routing for adaptive behavior. Built-in evaluation features allow systematic assessment of agent performance, which can be used for system refinement (see the Chapter on Evaluation and Monitoring).

> 谷歌 ADK 通过多智能体架构支持该思路，便于模块化与可扩展应用；不同智能体承担专精任务。模型灵活性允许直接使用多种 Gemini（含 Pro 与 Flash），或通过 LiteLLM 接入其他模型。ADK 编排支持由 LLM 驱动的动态路由以实现自适应；内置评估能力可系统衡量智能体表现并用于系统改进（参见评估与监控相关章节）。

Next, two agents with identical setup but utilizing different models and costs will be defined.

> 下面定义配置相同但模型与成本不同的两个智能体。

```python
# Conceptual Python-like structure, not runnable code
from google.adk.agents import Agent
# from google.adk.models.lite_llm import LiteLlm  # If using models not directly supported by ADK's default Agent

# Agent using the more expensive Gemini Pro 2.5
gemini_pro_agent = Agent(
    name="GeminiProAgent",
    model="gemini-2.5-pro",  # Placeholder for actual model name if different
    description="A highly capable agent for complex queries.",
    instruction="You are an expert assistant for complex problem-solving.",
)

# Agent using the less expensive Gemini Flash 2.5
gemini_flash_agent = Agent(
    name="GeminiFlashAgent",
    model="gemini-2.5-flash",  # Placeholder for actual model name if different
    description="A fast and efficient agent for simple queries.",
    instruction="You are a quick assistant for straightforward questions.",
)
```

A Router Agent can direct queries based on simple metrics like query length, where shorter queries go to less expensive models and longer queries to more capable models. However, a more sophisticated Router Agent can utilize either  LLM or ML models to analyze query nuances and complexity. This LLM router can determine which downstream language model is most suitable. For example, a query requesting a factual recall is routed to a flash model, while a complex query requiring deep analysis is routed to a pro model.

> 路由智能体可按简单指标（如查询长度）分流：短查询走经济模型，长查询走更强模型。更复杂的路由器可用 LLM 或 ML 模型分析查询细微差别与复杂度；例如事实回忆类查询走 Flash，需深度分析的复杂查询走 Pro。

Optimization techniques can further enhance the LLM router's effectiveness. Prompt tuning involves crafting prompts to guide the router LLM for better routing decisions. Fine-tuning the LLM router on a dataset of queries and their optimal model choices improves its accuracy and efficiency. This dynamic routing capability balances response quality with cost-effectiveness.

> 优化技术可进一步提升路由器效果：提示调优通过精心编写提示引导路由 LLM；在「查询—最优模型」数据集上微调路由 LLM 可提升准确性与效率。动态路由在响应质量与成本效益间取得平衡。

```python
# Conceptual Python-like structure, not runnable code
import asyncio
from typing import AsyncGenerator

from google.adk.agents import Agent, BaseAgent
from google.adk.events import Event
from google.adk.agents.invocation_context import InvocationContext


class QueryRouterAgent(BaseAgent):
    name: str = "QueryRouter"
    description: str = "Routes user queries to the appropriate LLM agent based on complexity."

    async def _run_async_impl(self, context: InvocationContext) -> AsyncGenerator[Event, None]:
        user_query = context.current_message.text  # Assuming text input
        query_length = len(user_query.split())  # Simple metric: number of words

        if query_length < 20:  # Example threshold for simplicity vs. complexity
            print(f"Routing to Gemini Flash Agent for short query (length: {query_length})")
            # In a real ADK setup, you would 'transfer_to_agent' or directly invoke
            # For demonstration, we'll simulate a call and yield its response
            response = await gemini_flash_agent.run_async(context.current_message)
            yield Event(author=self.name, content=f"Flash Agent processed: {response}")
        else:
            print(f"Routing to Gemini Pro Agent for long query (length: {query_length})")
            response = await gemini_pro_agent.run_async(context.current_message)
            yield Event(author=self.name, content=f"Pro Agent processed: {response}")
```

The Critique Agent evaluates responses from language models, providing feedback that serves several functions. For self-correction, it identifies errors or inconsistencies, prompting the answering agent to refine its output for improved quality. It also systematically assesses responses for performance monitoring, tracking metrics like accuracy and relevance, which are used for optimization.

> 批评（Critique）智能体评估语言模型的回答，其反馈可用于：自我纠正——发现错误或不一致，促使回答智能体改进输出；系统评估——为性能监控跟踪准确率、相关性等指标以支持优化。

Additionally, its feedback can signal reinforcement learning or fine-tuning; consistent identification of inadequate Flash model responses, for instance, can refine the router agent's logic. While not directly managing the budget, the Critique Agent contributes to indirect budget management by identifying suboptimal routing choices, such as directing simple queries to a Pro model or complex queries to a Flash model, which leads to poor results. This informs adjustments that improve resource allocation and cost savings.

> 此外，反馈还可用于强化学习或微调；例如持续发现 Flash 回答不足可改进路由逻辑。虽不直接管预算，但通过识别次优路由（简单题走 Pro、复杂题走 Flash 导致效果差），可间接改善资源分配与节省成本。

The Critique Agent can be configured to review either only the generated text from the answering agent or both the original query and the generated text, enabling a comprehensive evaluation of the response's alignment with the initial question.

> 可配置批评智能体仅审回答文本，或同时审原始问题与生成文本，以全面评估与初始问题的一致性。

```python
CRITIC_SYSTEM_PROMPT = """
You are the **Critic Agent**, serving as the quality assurance arm of our collaborative research assistant system. Your primary function is to **meticulously review and challenge** information from the Researcher Agent, guaranteeing **accuracy, completeness, and unbiased presentation**. Your duties encompass: * **Assessing research findings** for factual correctness, thoroughness, and potential leanings. * **Identifying any missing data** or inconsistencies in reasoning. * **Raising critical questions** that could refine or expand the current understanding. * **Offering constructive suggestions** for enhancement or exploring different angles. * **Validating that the final output is comprehensive** and balanced. All criticism must be constructive. Your goal is to fortify the research, not invalidate it. Structure your feedback clearly, drawing attention to specific points for revision. Your overarching aim is to ensure the final research product meets the highest possible quality standards. 
"""
```

The Critic Agent operates based on a predefined system prompt that outlines its role, responsibilities, and feedback approach. A well-designed prompt for this agent must clearly establish its function as an evaluator. It should specify the areas for critical focus and emphasize providing constructive feedback rather than mere dismissal. The prompt should also encourage the identification of both strengths and weaknesses, and it must guide the agent on how to structure and present its feedback.

> 批评智能体依据预定义系统提示运作，说明角色、职责与反馈方式。良好提示须明确其评估者身份、批判焦点，并强调建设性反馈而非一味否定；还应鼓励识别优缺点，并指导如何组织与呈现反馈。

## Hands-On Code with OpenAI

> ## OpenAI 动手代码

This system uses a resource-aware optimization strategy to handle user queries efficiently. It first classifies each query into one of three categories to determine the most appropriate and cost-effective processing pathway. This approach avoids wasting computational resources on simple requests while ensuring complex queries get the necessary attention. The three categories are:

> 该系统采用资源感知优化策略高效处理用户查询：先将每条查询分为三类，以选择最合适且成本效益最高的处理路径——避免在简单请求上浪费算力，同时保证复杂查询得到足够关注。三类为：

* simple: For straightforward questions that can be answered directly without complex reasoning or external data.  
* reasoning: For queries that require logical deduction or multi-step thought processes, which are routed to more powerful models.  
* `internetsearch`: For questions needing current information, which automatically triggers a Google Search to provide an up-to-date answer.

> * simple：可直接回答、无需复杂推理或外部数据的直白问题。  
> * reasoning：需要逻辑推演或多步思考的查询，路由到更强模型。  
> * `internetsearch`：需要最新信息的问题，自动触发 Google 搜索以提供时效答案。

The code is under the MIT license and available on Github: ([https://github.com/mahtabsyed/21-Agentic-Patterns/blob/main/16ResourceAwareOptLLMReflectionv2.ipynb](https://github.com/mahtabsyed/21-Agentic-Patterns/blob/main/16_Resource_Aware_Opt_LLM_Reflection_v2.ipynb))

> 代码以 MIT 许可发布，见 GitHub：（[https://github.com/mahtabsyed/21-Agentic-Patterns/blob/main/16ResourceAwareOptLLMReflectionv2.ipynb](https://github.com/mahtabsyed/21-Agentic-Patterns/blob/main/16_Resource_Aware_Opt_LLM_Reflection_v2.ipynb)）

```python
# MIT License
# Copyright (c) 2025 Mahtab Syed
# https://www.linkedin.com/in/mahtabsyed/

import os
import json
import requests
from dotenv import load_dotenv
from openai import OpenAI


# Load environment variables
load_dotenv()

OPENAI_API_KEY = os.getenv("OPENAI_API_KEY")
GOOGLE_CUSTOM_SEARCH_API_KEY = os.getenv("GOOGLE_CUSTOM_SEARCH_API_KEY")
GOOGLE_CSE_ID = os.getenv("GOOGLE_CSE_ID")

if not OPENAI_API_KEY or not GOOGLE_CUSTOM_SEARCH_API_KEY or not GOOGLE_CSE_ID:
    raise ValueError(
        "Please set OPENAI_API_KEY, GOOGLE_CUSTOM_SEARCH_API_KEY, and GOOGLE_CSE_ID in your .env file."
    )

client = OpenAI(api_key=OPENAI_API_KEY)


# --- Step 1: Classify the Prompt ---
def classify_prompt(prompt: str) -> dict:
    system_message = {
        "role": "system",
        "content": (
            "You are a classifier that analyzes user prompts and returns one of three categories ONLY:\n\n"
            "- simple\n"
            "- reasoning\n"
            "- internet_search\n\n"
            "Rules:\n"
            "- Use 'simple' for direct factual questions that need no reasoning or current events.\n"
            "- Use 'reasoning' for logic, math, or multi-step inference questions.\n"
            "- Use 'internet_search' if the prompt refers to current events, recent data, or things not in your training data.\n\n"
            "Respond ONLY with JSON like:\n"
            '{ "classification": "simple" }'
        ),
    }
    user_message = {"role": "user", "content": prompt}

    response = client.chat.completions.create(
        model="gpt-4o",
        messages=[system_message, user_message],
        temperature=1,
    )
    reply = response.choices[0].message.content
    return json.loads(reply)


# --- Step 2: Google Search ---
def google_search(query: str, num_results: int = 1) -> list:
    url = "https://www.googleapis.com/customsearch/v1"
    params = {
        "key": GOOGLE_CUSTOM_SEARCH_API_KEY,
        "cx": GOOGLE_CSE_ID,
        "q": query,
        "num": num_results,
    }
    try:
        response = requests.get(url, params=params)
        response.raise_for_status()
        results = response.json()
        if "items" in results and results["items"]:
            return [
                {
                    "title": item.get("title"),
                    "snippet": item.get("snippet"),
                    "link": item.get("link"),
                }
                for item in results["items"]
            ]
        else:
            return []
    except requests.exceptions.RequestException as e:
        return {"error": str(e)}


# --- Step 3: Generate Response ---
def generate_response(prompt: str, classification: str, search_results=None) -> tuple[str, str]:
    if classification == "simple":
        model = "gpt-4o-mini"
        full_prompt = prompt

    elif classification == "reasoning":
        model = "o4-mini"
        full_prompt = prompt

    elif classification == "internet_search":
        model = "gpt-4o"
        # Convert each search result dict to a readable string
        if search_results:
            search_context = "\n".join(
                [
                    f"Title: {item.get('title')}\nSnippet: {item.get('snippet')}\nLink: {item.get('link')}"
                    for item in search_results
                ]
            )
        else:
            search_context = "No search results found."
        full_prompt = (
            "Use the following web results to answer the user query: "
            f"{search_context}\nQuery: {prompt}"
        )
    else:
        # Fallback
        model = "gpt-4o"
        full_prompt = prompt

    response = client.chat.completions.create(
        model=model,
        messages=[{"role": "user", "content": full_prompt}],
        temperature=1,
    )
    return response.choices[0].message.content, model


# --- Step 4: Combined Router ---
def handle_prompt(prompt: str) -> dict:
    classification_result = classify_prompt(prompt)
    classification = classification_result["classification"]

    search_results = None
    if classification == "internet_search":
        search_results = google_search(prompt)

    answer, model = generate_response(prompt, classification, search_results)
    return {"classification": classification, "response": answer, "model": model}


if __name__ == "__main__":
    test_prompt = "What is the capital of Australia?"
    # test_prompt = "Explain the impact of quantum computing on cryptography."
    # test_prompt = "When does the Australian Open 2026 start, give me full date?"

    result = handle_prompt(test_prompt)

    print("🔍 Classification:", result["classification"])
    print("🧠 Model Used:", result["model"])
    print("🧠 Response:\n", result["response"])
```

This Python code implements a prompt routing system to answer user questions. It begins by loading necessary API keys from a .env file for OpenAI and Google Custom Search. The core functionality lies in classifying the user's prompt into three categories: simple, reasoning, or internet search. A dedicated function utilizes an OpenAI model for this classification step. If the prompt requires current information, a Google search is performed using the Google Custom Search API. Another function then generates the final response, selecting an appropriate OpenAI model based on the classification. For internet search queries, the search results are provided as context to the model. The main `handleprompt` function orchestrates this workflow, calling the classification and search (if needed) functions before generating the response. It returns the classification, the model used, and the generated answer. This system efficiently directs different types of queries to optimized methods for a better response.

> 该 Python 实现基于提示路由回答用户问题：从 `.env` 加载 OpenAI 与 Google 自定义搜索的密钥；核心是将用户提示分为 simple、reasoning、internet_search 三类，由专用函数调用 OpenAI 完成分类；若需最新信息则调用 Google 自定义搜索；再按分类选择合适 OpenAI 生成最终答复，搜索类查询将结果作为上下文。主流程 `handle_prompt`（原文误写为 handleprompt）编排分类、（如需要的）搜索与生成，返回分类、所用模型与答案，从而把不同类型查询导向更优路径。

# Hands-On Code Example (OpenRouter)

> # 动手代码示例（OpenRouter）

OpenRouter offers a unified interface to hundreds of AI models via a single API endpoint. It provides automated failover and cost-optimization, with easy integration through your preferred SDK or framework.

> OpenRouter 通过单一 API 端点统一对接数百种 AI 模型，提供自动故障转移与成本优化，并可通过常用 SDK 或框架轻松集成。

```python
import json
import requests

response = requests.post(
    url="https://openrouter.ai/api/v1/chat/completions",
    headers={
        "Authorization": "Bearer <OPENROUTER_API_KEY>",
        "HTTP-Referer": "<YOUR_SITE_URL>",  # Optional. Site URL for rankings on openrouter.ai.
        "X-Title": "<YOUR_SITE_NAME>",      # Optional. Site title for rankings on openrouter.ai.
    },
    data=json.dumps({
        "model": "openai/gpt-4o",  # Optional
        "messages": [
            {
                "role": "user",
                "content": "What is the meaning of life?"
            }
        ]
    }),
)
```

This code snippet uses the requests library to interact with the OpenRouter API. It sends a POST request to the chat completion endpoint with a user message. The request includes authorization headers with an API key and optional site information. The goal is to get a response from a specified language model, in this case, "openai/gpt-4o".

> 该片段用 `requests` 调用 OpenRouter API：向聊天补全端点发送 POST，附带用户消息、含 API 密钥的鉴权头及可选站点信息，以从指定模型（此处为 `openai/gpt-4o`）获得响应。

Openrouter offers two distinct methodologies for routing and determining the computational model used to process a given request.

> OpenRouter 提供两种不同的路由与算力模型选择方式。

* **Automated Model Selection:** This function routes a request to an optimized model chosen from a curated set of available models. The selection is predicated on the specific content of the user's prompt. The identifier of the model that ultimately processes the request is returned in the response's metadata.

> * **自动模型选择：** 根据用户提示内容，从精选模型集中选择优化后的模型处理请求；最终处理请求的模型标识会在响应元数据中返回。

```json
{  
    "model": "openrouter/auto",  
    ... // Other params 
}
```

* **Sequential Model Fallback:** This mechanism provides operational redundancy by allowing users to specify a hierarchical list of models. The system will first attempt to process the request with the primary model designated in the sequence. Should this primary model fail to respond due to any number of error conditions—such as service unavailability, rate-limiting, or content filtering—the system will automatically re-route the request to the next specified model in the sequence. This process continues until a model in the list successfully executes the request or the list is exhausted. The final cost of the operation and the model identifier returned in the response will correspond to the model that successfully completed the computation.

> * **顺序模型回退：** 用户可指定分层模型列表以提供运行冗余：系统先尝试序列中的主模型；若因服务不可用、限流、内容过滤等失败，则自动依次尝试下一模型，直至成功或列表用尽；最终费用与响应中的模型标识对应实际完成计算的模型。

```json
{  
    "models": ["anthropic/claude-3.5-sonnet", "gryphe/mythomax-l2-13b"],  
    ... // Other params }
```

OpenRouter offers a detailed leaderboard ( [https://openrouter.ai/rankings](https://openrouter.ai/rankings)) which ranks available AI models based on their cumulative token production. It also offers latest models from different providers (ChatGPT, Gemini, Claude) (see Fig. 1)

> OpenRouter 提供详细排行榜（[https://openrouter.ai/rankings](https://openrouter.ai/rankings)），按累计 token 产出等对模型排序，并提供来自不同厂商（ChatGPT、Gemini、Claude 等）的最新模型（见图 1）。

![OpenRouter Web site](../assets-new/OpenRouter_Web_Site.png) 

Fig. 1: OpenRouter Web site ([https://openrouter.ai/](https://openrouter.ai/))

> 图 1：OpenRouter 网站（[https://openrouter.ai/](https://openrouter.ai/)）

## Beyond Dynamic Model Switching: A Spectrum of Agent Resource Optimizations

> ## 超越动态换模：智能体资源优化谱系

Resource-aware optimization is paramount in developing intelligent agent systems that operate efficiently and effectively within real-world constraints. Let's see a number of additional techniques:

> 在现实约束下高效、有效地运行智能体系统，资源感知优化至关重要。下面列举更多技术：

**Dynamic Model Switching** is a critical technique involving the strategic selection of large language models  based on the intricacies of the task at hand and the available computational resources. When faced with simple queries, a lightweight, cost-effective LLM can be deployed, whereas complex, multifaceted problems necessitate the utilization of more sophisticated and resource-intensive models.

> **动态模型切换：** 根据任务复杂度与可用算力策略性选择 LLM；简单查询部署轻量经济模型，复杂多面问题则需更强、更耗资源的模型。

**Adaptive Tool Use & Selection** ensures agents can intelligently choose from a suite of tools, selecting the most appropriate and efficient one for each specific sub-task, with careful consideration given to factors like API usage costs, latency, and execution time. This dynamic tool selection enhances overall system efficiency by optimizing the use of external APIs and services.

> **自适应工具使用与选择：** 使智能体能从工具集中为每个子任务选择最合适、最高效的工具，综合考虑 API 成本、延迟与执行时间，从而优化对外部 API 与服务的使用。

**Contextual Pruning & Summarization** plays a vital role in managing the amount of information processed by agents, strategically minimizing the prompt token count and reducing inference costs by intelligently summarizing and selectively retaining only the most relevant information from the interaction history, preventing unnecessary computational overhead.

> **上下文剪枝与摘要：** 通过智能摘要与选择性保留交互历史中最相关信息，策略性降低提示 token 与推理成本，避免不必要算力开销。

**Proactive Resource Prediction** involves anticipating resource demands by forecasting future workloads and system requirements, which allows for proactive allocation and management of resources, ensuring system responsiveness and preventing bottlenecks.

> **主动资源预测：** 通过预测未来负载与系统需求预判资源需求，主动分配与管理资源，保持响应并缓解瓶颈。

**Cost-Sensitive Exploration** in multi-agent systems extends optimization considerations to encompass communication costs alongside traditional computational costs, influencing the strategies employed by agents to collaborate and share information, aiming to minimize the overall resource expenditure.

> **成本敏感探索（多智能体）：** 将通信成本与传统计算成本一并纳入优化，影响协作与信息共享策略，以降低总体资源消耗。

**Energy-Efficient Deployment** is specifically tailored for environments with stringent resource constraints, aiming to minimize the energy footprint of intelligent agent systems, extending operational time and reducing overall running costs.

> **能效部署：** 面向严苛资源约束环境，降低智能体系统能耗，延长运行时间并降低总体运行成本。

**Parallelization & Distributed Computing Awareness** leverages distributed resources to enhance the processing power and throughput of agents, distributing computational workloads across multiple machines or processors to achieve greater efficiency and faster task completion.

> **并行与分布式意识：** 利用分布式资源提升吞吐，将计算负载分散到多机或多核以提高效率、加快任务完成。

**Learned Resource Allocation Policies** introduce a learning mechanism, enabling agents to adapt and optimize their resource allocation strategies over time based on feedback and performance metrics, improving efficiency through continuous refinement.

> **学习的资源分配策略：** 引入学习机制，依据反馈与性能指标随时间调整资源分配策略，通过持续改进提升效率。

**Graceful Degradation and Fallback Mechanisms** ensure that intelligent agent systems can continue to function, albeit perhaps at a reduced capacity, even when resource constraints are severe, gracefully degrading performance and falling back to alternative strategies to maintain operation and provide essential functionality.

> **优雅降级与回退机制：** 在资源严重受限时仍能（可能以降容方式）继续运行，通过降级与备选策略维持基本功能。

## At a Glance

> ## 速览

**What:** Resource-Aware Optimization addresses the challenge of managing the consumption of computational, temporal, and financial resources in intelligent systems. LLM-based applications can be expensive and slow, and selecting the best model or tool for every task is often inefficient. This creates a fundamental trade-off between the quality of a system's output and the resources required to produce it. Without a dynamic management strategy, systems cannot adapt to varying task complexities or operate within budgetary and performance constraints.

> **是什么：** 资源感知优化解决智能系统中计算、时间与财务资源消耗的管理难题。基于 LLM 的应用可能昂贵且缓慢，为每项任务都选「最好」的模型或工具往往低效，从而在输出质量与所需资源之间形成根本权衡。没有动态管理策略，系统难以适应不同任务复杂度或在预算与性能约束内运行。

**Why:** The standardized solution is to build an agentic system that intelligently monitors and allocates resources based on the task at hand. This pattern typically employs a "Router Agent" to first classify the complexity of an incoming request. The request is then forwarded to the most suitable LLM or tool—a fast, inexpensive model for simple queries, and a more powerful one for complex reasoning. A "Critique Agent" can further refine the process by evaluating the quality of the response, providing feedback to improve the routing logic over time. This dynamic, multi-agent approach ensures the system operates efficiently, balancing response quality with cost-effectiveness.

> **为什么：** 标准化做法是构建能按任务智能监控与分配资源的智能体系统。该模式通常用「路由智能体」先对请求复杂度分类，再转发到最合适的 LLM 或工具——简单查询用快而经济的模型，复杂推理用更强模型。「批评智能体」可进一步评估回答质量并反馈以改进路由逻辑。这种动态多智能体方法在响应质量与成本效益间取得平衡。

**Rule of Thumb:** Use this pattern when operating under strict financial budgets for API calls or computational power, building latency-sensitive applications where quick response times are critical, deploying agents on resource-constrained hardware such as edge devices with limited battery life, programmatically balancing the trade-off between response quality and operational cost, and managing complex, multi-step workflows where different tasks have varying resource requirements.

> **经验法则：** 在 API 或算力预算严格、延迟敏感、边缘等电池受限硬件部署、需在程序上平衡质量与运营成本，或管理各子任务资源需求不同的复杂多步工作流时，宜采用本模式。

**Visual Summary:**

> **图示摘要：**

![Resource-Aware Optimization Design Pattern](../assets-new/Resource_Aware_Optimization_Design_Pattern.png)

Fig. 2: Resource-Aware Optimization Design Pattern

> 图 2：资源感知优化设计模式

## Key Takeaways

> ## 要点

* Resource-Aware Optimization is Essential: Intelligent agents can manage computational, temporal, and financial resources dynamically. Decisions regarding model usage and execution paths are made based on real-time constraints and objectives.  
* Multi-Agent Architecture for Scalability: Google's ADK provides a multi-agent framework, enabling modular design. Different agents (answering, routing, critique) handle specific tasks.  
* Dynamic, LLM-Driven Routing: A Router Agent directs queries to language models (Gemini Flash for simple, Gemini Pro for complex) based on query complexity and budget. This optimizes cost and performance.  
* Critique Agent Functionality: A dedicated Critique Agent provides feedback for self-correction, performance monitoring, and refining routing logic, enhancing system effectiveness.  
* Optimization Through Feedback and Flexibility: Evaluation capabilities for critique and model integration flexibility contribute to adaptive and self-improving system behavior.  
* Additional Resource-Aware Optimizations: Other methods include Adaptive Tool Use & Selection, Contextual Pruning & Summarization, Proactive Resource Prediction, Cost-Sensitive Exploration in Multi-Agent Systems, Energy-Efficient Deployment, Parallelization & Distributed Computing Awareness, Learned Resource Allocation Policies, Graceful Degradation and Fallback Mechanisms, and Prioritization of Critical Tasks.

> * 资源感知优化至关重要：智能体可动态管理计算、时间与财务资源，按实时约束与目标决定模型与执行路径。  
> * 可扩展的多智能体架构：谷歌 ADK 提供多智能体框架，模块化设计；不同智能体（回答、路由、批评）各司其职。  
> * 由 LLM 驱动的动态路由：路由智能体按查询复杂度与预算将查询导向 Gemini Flash（简单）或 Gemini Pro（复杂）等，优化成本与性能。  
> * 批评智能体功能：专用批评智能体提供自我纠正、性能监控与路由逻辑改进的反馈，提升系统效果。  
> * 通过反馈与灵活性优化：批评相关的评估能力与模型集成灵活性有助于自适应与自我改进。  
> * 其他资源感知优化：还包括自适应工具选择与使用、上下文剪枝与摘要、主动资源预测、多智能体中的成本敏感探索、能效部署、并行与分布式意识、学习的资源分配策略、优雅降级与回退，以及关键任务优先级等。

## Conclusions

> ## 结论

Resource-aware optimization is essential for the development of intelligent agents, enabling efficient operation within real-world constraints. By managing computational, temporal, and financial resources, agents can achieve optimal performance and cost-effectiveness. Techniques such as dynamic model switching, adaptive tool use, and contextual pruning are crucial for attaining these efficiencies. Advanced strategies, including learned resource allocation policies and graceful degradation, enhance an agent's adaptability and resilience under varying conditions. Integrating these optimization principles into agent design is fundamental for building scalable, robust, and sustainable AI systems.

> 资源感知优化对开发智能体至关重要，使其能在现实约束下高效运行。通过管理计算、时间与财务资源，智能体可在性能与成本效益间取得较优平衡。动态换模、自适应工具使用与上下文剪枝等技术是实现这些效率的关键；学习的资源分配策略与优雅降级等高级策略则增强在不同条件下的适应性与韧性。将这些优化原则融入智能体设计，是构建可扩展、稳健且可持续 AI 系统的基础。

## References

1. Google's Agent Development Kit (ADK): [https://google.github.io/adk-docs/](https://google.github.io/adk-docs/)
2. Gemini Flash 2.5 & Gemini 2.5 Pro:  [https://aistudio.google.com/](https://aistudio.google.com/)
3. OpenRouter: [https://openrouter.ai/docs/quickstart](https://openrouter.ai/docs/quickstart)
