# Chapter 3: Parallelization

> 第三章：并行化（Parallelization）

## Parallelization Pattern Overview

> ## 并行化模式概览

In the previous chapters, we've explored Prompt Chaining for sequential workflows and Routing for dynamic decision-making and transitions between different paths. While these patterns are essential, many complex agentic tasks involve multiple sub-tasks that can be executed *simultaneously* rather than one after another. This is where the **Parallelization** pattern becomes crucial.

> 前几章我们探讨了用于顺序工作流的提示链，以及用于动态决策与路径切换的路由。这些模式都很重要，但许多复杂智能体任务包含多个可*同时*执行而非一个接一个的子任务，此时**并行化**模式至关重要。

Parallelization involves executing multiple components, such as LLM calls, tool usages, or even entire sub-agents, concurrently (see Fig.1). Instead of waiting for one step to complete before starting the next, parallel execution allows independent tasks to run at the same time, significantly reducing the overall execution time for tasks that can be broken down into independent parts.

> 并行化指并发执行多个组件，如 LLM 调用、工具使用乃至整个子智能体（见图 1）。不必等一步完成再开始下一步；独立任务可同时运行，从而显著缩短可拆分为独立部分的任务的总耗时。

Consider an agent designed to research a topic and summarize its findings. A sequential approach might:

> 考虑一个研究主题并总结发现的智能体。顺序做法可能是：

1. Search for Source A.  
2. Summarize Source A.  
3. Search for Source B.  
4. Summarize Source B.  
5. Synthesize a final answer from summaries A and B.

> 1. 检索来源 A。  
> 2. 总结来源 A。  
> 3. 检索来源 B。  
> 4. 总结来源 B。  
> 5. 从摘要 A 与 B 综合出最终答案。

A parallel approach could instead:

> 并行做法可以是：

1. Search for Source A *and* Search for Source B simultaneously.  
2. Once both searches are complete, Summarize Source A *and* Summarize Source B simultaneously.  
3. Synthesize a final answer from summaries A and B (this step is typically sequential, waiting for the parallel steps to finish).

> 1. *同时*检索来源 A 与来源 B。  
> 2. 两次检索均完成后，*同时*总结来源 A 与来源 B。  
> 3. 从摘要 A 与 B 综合最终答案（该步通常为顺序的，需等待并行步骤结束）。

The core idea is to identify parts of the workflow that do not depend on the output of other parts and execute them in parallel. This is particularly effective when dealing with external services (like APIs or databases) that have latency, as you can issue multiple requests concurrently.

> 核心思想是找出工作流中不依赖其他部分输出的环节并并行执行。对外部服务（如 API、数据库）等有延迟的场景尤其有效，因为可并发发出多个请求。

Implementing parallelization often requires frameworks that support asynchronous execution or multi-threading/multi-processing. Modern agentic frameworks are designed with asynchronous operations in mind, allowing you to easily define steps that can run in parallel.

> 实现并行化通常需要支持异步执行或多线程/多进程的框架。现代智能体框架在设计时考虑了异步操作，便于定义可并行运行的步骤。

![Parallelization with Sub-Agents](../assets-new/Parallelization_with_Sub_Agents.png)

Fig.1. Example of parallelization with sub-agents

> 图 1. 子智能体并行化示例

Frameworks like LangChain, LangGraph, and Google ADK provide mechanisms for parallel execution. In LangChain Expression Language (LCEL), you can achieve parallel execution by combining runnable objects using operators like | (for sequential) and by structuring your chains or graphs to have branches that execute concurrently. LangGraph, with its graph structure, allows you to define multiple nodes that can be executed from a single state transition, effectively enabling parallel branches in the workflow. Google ADK provides robust, native mechanisms to facilitate and manage the parallel execution of agents, significantly enhancing the efficiency and scalability of complex, multi-agent systems. This inherent capability within the ADK framework allows developers to design and implement solutions where multiple agents can operate concurrently, rather than sequentially.

> LangChain、LangGraph 与 Google ADK 等框架提供并行执行机制。在 LangChain 表达式语言（LCEL）中，可用 `|`（顺序）等运算符组合可运行对象，并构造具有并发分支的链或图以实现并行。LangGraph 借助图结构，允许从单次状态转移启动多个节点，从而在工作流中形成并行分支。Google ADK 提供稳健的原生机制以促进与管理智能体的并行执行，显著提升复杂多智能体系统的效率与可扩展性；开发者可据此设计多智能体并发而非顺序运行的方案。

The Parallelization pattern is vital for improving the efficiency and responsiveness of agentic systems, especially when dealing with tasks that involve multiple independent lookups, computations, or interactions with external services. It's a key technique for optimizing the performance of complex agent workflows.

> 并行化模式对提升智能体系统的效率与响应性至关重要，尤其当任务包含多次独立查询、计算或与外部服务交互时；它是优化复杂智能体工作流性能的关键技术。

## Practical Applications & Use Cases

> ## 实际应用与用例

Parallelization is a powerful pattern for optimizing agent performance across various applications:

> 并行化是在多种应用中优化智能体表现的有力模式：

### 1. Information Gathering and Research

> ### 1. 信息收集与研究

Collecting information from multiple sources simultaneously is a classic use case.

> 同时从多源收集信息是经典用例。

* **Use Case:** An agent researching a company.  
  * **Parallel Tasks:** Search news articles, pull stock data, check social media mentions, and query a company database, all at the same time.  
  * **Benefit:** Gathers a comprehensive view much faster than sequential lookups.

> * **用例：** 研究某公司的智能体。  
>   * **并行任务：** 同时搜索新闻、拉取股价数据、查看社交媒体提及、查询公司数据库。  
>   * **收益：** 比顺序查询更快获得全面视图。

### 2. Data Processing and Analysis

> ### 2. 数据处理与分析

Applying different analysis techniques or processing different data segments concurrently.

> 并发应用不同分析技术或处理不同数据片段。

* **Use Case:** An agent analyzing customer feedback.  
  * **Parallel Tasks:** Run sentiment analysis, extract keywords, categorize feedback, and identify urgent issues simultaneously across a batch of feedback entries.  
  * **Benefit:** Provides a multi-faceted analysis quickly.

> * **用例：** 分析客户反馈的智能体。  
>   * **并行任务：** 在一批反馈条目上同时运行情感分析、关键词抽取、分类与紧急问题识别。  
>   * **收益：** 快速得到多维度分析。

### 3. Multi-API or Tool Interaction

> ### 3. 多 API 或工具交互

Calling multiple independent APIs or tools to gather different types of information or perform different actions.

> 调用多个彼此独立的 API 或工具以收集不同信息或执行不同动作。

* **Use Case:** A travel planning agent.  
  * **Parallel Tasks:** Check flight prices, search for hotel availability, look up local events, and find restaurant recommendations concurrently.  
  * **Benefit:** Presents a complete travel plan faster.

> * **用例：** 旅行规划智能体。  
>   * **并行任务：** 同时查机票、搜酒店空房、查当地活动、找餐厅推荐。  
>   * **收益：** 更快呈现完整行程方案。

### 4. Content Generation with Multiple Components

> ### 4. 多组件内容生成

Generating different parts of a complex piece of content in parallel.

> 并行生成复杂内容的多个部分。

* **Use Case:** An agent creating a marketing email.  
  * **Parallel Tasks:** Generate a subject line, draft the email body, find a relevant image, and create a call-to-action button text simultaneously.  
  * **Benefit:** Assembles the final email more efficiently.

> * **用例：** 撰写营销邮件的智能体。  
>   * **并行任务：** 同时生成主题行、正文草稿、相关配图与行动号召按钮文案。  
>   * **收益：** 更高效组装最终邮件。

### 5. Validation and Verification

> ### 5. 校验与验证

Performing multiple independent checks or validations concurrently.

> 并发执行多项独立检查或验证。

* **Use Case:** An agent verifying user input.  
  * **Parallel Tasks:** Check email format, validate phone number, verify address against a database, and check for profanity simultaneously.  
  * **Benefit:** Provides faster feedback on input validity.

> * **用例：** 校验用户输入的智能体。  
>   * **并行任务：** 同时检查邮箱格式、验证电话、对照数据库校验地址、检测不当用语。  
>   * **收益：** 更快反馈输入是否有效。

### 6. Multi-Modal Processing

> ### 6. 多模态处理

Processing different modalities (text, image, audio) of the same input concurrently.

> 对同一输入的不同模态（文本、图像、音频）并发处理。

* **Use Case:** An agent analyzing a social media post with text and an image.  
  * **Parallel Tasks:** Analyze the text for sentiment and keywords *and* analyze the image for objects and scene description simultaneously.  
  * **Benefit:** Integrates insights from different modalities more quickly.

> * **用例：** 分析含文字与图片的帖子的智能体。  
>   * **并行任务：** *同时*对文本做情感与关键词分析，*并对图像做物体与场景描述分析。  
>   * **收益：** 更快整合不同模态的洞见。

### 7. A/B Testing or Multiple Options Generation

> ### 7. A/B 测试或多方案生成

Generating multiple variations of a response or output in parallel to select the best one.

> 并行生成多种回复或输出变体以供择优。

* **Use Case:** An agent generating different creative text options.  
  * **Parallel Tasks:** Generate three different headlines for an article simultaneously using slightly different prompts or models.  
  * **Benefit:** Allows for quick comparison and selection of the best option.

> * **用例：** 生成多种创意文案选项的智能体。  
>   * **并行任务：** 用略有不同的提示或模型同时为文章生成三个标题。  
>   * **收益：** 便于快速比较并选出最佳方案。

Parallelization is a fundamental optimization technique in agentic design, allowing developers to build more performant and responsive applications by leveraging concurrent execution for independent tasks.

> 并行化是智能体设计中的基础优化技术：通过对独立任务利用并发执行，开发者可构建更高性能、更灵敏的应用。

## Hands-On Code Example (LangChain)

> ## 动手代码示例（LangChain）

Parallel execution within the LangChain framework is facilitated by the LangChain Expression Language (LCEL). The primary method involves structuring multiple runnable components within a dictionary or list construct. When this collection is passed as input to a subsequent component in the chain, the LCEL runtime executes the contained runnables concurrently.

> LangChain 框架内的并行执行由 LangChain 表达式语言（LCEL）促成：主要做法是把多个可运行组件组织在字典或列表结构中；当该集合作为链中后续组件的输入传入时，LCEL 运行时并发执行其中各可运行对象。

In the context of LangGraph, this principle is applied to the graph's topology. Parallel workflows are defined by architecting the graph such that multiple nodes, lacking direct sequential dependencies, can be initiated from a single common node. These parallel pathways execute independently before their results can be aggregated at a subsequent convergence point in the graph.

> 在 LangGraph 中，该原则体现在图拓扑上：通过构图使多个无直接顺序依赖的节点可从同一公共节点启动，这些并行路径独立执行，随后在图中某汇合点聚合结果。

The following implementation demonstrates a parallel processing workflow constructed with the LangChain framework. This workflow is designed to execute two independent operations concurrently in response to a single user query. These parallel processes are instantiated as distinct chains or functions, and their respective outputs are subsequently aggregated into a unified result.

> 下列实现演示用 LangChain 构建的并行处理工作流：针对单一用户查询并发执行两个独立操作；这些并行过程实例化为不同链或函数，其输出随后聚合为统一结果。

The prerequisites for this implementation include the installation of the requisite Python packages, such as langchain, langchain-community, and a model provider library like langchain-openai. Furthermore, a valid API key for the chosen language model must be configured in the local environment for authentication.

> 前置条件包括安装所需 Python 包（如 langchain、langchain-community、langchain-openai 等模型提供商库），并在本地环境配置所选语言模型的有效 API 密钥以完成认证。

```python
import os
import asyncio
from typing import Optional

from langchain_openai import ChatOpenAI
from langchain_core.prompts import ChatPromptTemplate
from langchain_core.output_parsers import StrOutputParser
from langchain_core.runnables import Runnable, RunnableParallel, RunnablePassthrough


# --- Configuration ---
# Ensure your API key environment variable is set (e.g., OPENAI_API_KEY)
try:
    llm: Optional[ChatOpenAI] = ChatOpenAI(model="gpt-4o-mini", temperature=0.7)
except Exception as e:
    print(f"Error initializing language model: {e}")
    llm = None


# --- Define Independent Chains ---
# These three chains represent distinct tasks that can be executed in parallel.
summarize_chain: Runnable = (
    ChatPromptTemplate.from_messages([
        ("system", "Summarize the following topic concisely:"),
        ("user", "{topic}"),
    ])
    | llm
    | StrOutputParser()
)

questions_chain: Runnable = (
    ChatPromptTemplate.from_messages([
        ("system", "Generate three interesting questions about the following topic:"),
        ("user", "{topic}"),
    ])
    | llm
    | StrOutputParser()
)

terms_chain: Runnable = (
    ChatPromptTemplate.from_messages([
        ("system", "Identify 5-10 key terms from the following topic, separated by commas:"),
        ("user", "{topic}"),
    ])
    | llm
    | StrOutputParser()
)


# --- Build the Parallel + Synthesis Chain ---
# 1. Define the block of tasks to run in parallel. The results of these,
#    along with the original topic, will be fed into the next step.
map_chain = RunnableParallel(
    {
        "summary": summarize_chain,
        "questions": questions_chain,
        "key_terms": terms_chain,
        "topic": RunnablePassthrough(),  # Pass the original topic through
    }
)

# 2. Define the final synthesis prompt which will combine the parallel results.
synthesis_prompt = ChatPromptTemplate.from_messages([
    (
        "system",
        """Based on the following information:
        Summary: {summary}
        Related Questions: {questions}
        Key Terms: {key_terms}
        Synthesize a comprehensive answer."""
    ),
    ("user", "Original topic: {topic}"),
])

# 3. Construct the full chain by piping the parallel results directly
#    into the synthesis prompt, followed by the LLM and output parser.
full_parallel_chain = map_chain | synthesis_prompt | llm | StrOutputParser()


# --- Run the Chain ---
async def run_parallel_example(topic: str) -> None:
    """
    Asynchronously invokes the parallel processing chain with a specific topic
    and prints the synthesized result.

    Args:
        topic: The input topic to be processed by the LangChain chains.
    """
    if not llm:
        print("LLM not initialized. Cannot run example.")
        return

    print(f"\n--- Running Parallel LangChain Example for Topic: '{topic}' ---")
    try:
        # The input to `ainvoke` is the single 'topic' string,
        # then passed to each runnable in the `map_chain`.
        response = await full_parallel_chain.ainvoke(topic)
        print("\n--- Final Response ---")
        print(response)
    except Exception as e:
        print(f"\nAn error occurred during chain execution: {e}")


if __name__ == "__main__":
    test_topic = "The history of space exploration"
    # In Python 3.7+, asyncio.run is the standard way to run an async function.
    asyncio.run(run_parallel_example(test_topic))
```

The provided Python code implements a LangChain application designed for processing a given topic efficiently by leveraging parallel execution. Note that asyncio provides concurrency, not parallelism. It achieves this on a single thread by using an event loop that intelligently switches between tasks when one is idle (e.g., waiting for a network request). This creates the effect of multiple tasks progressing at once, but the code itself is still being executed by only one thread, constrained by Python's Global Interpreter Lock (GIL).

> 所提供的 Python 代码实现了一个 LangChain 应用，通过并行执行高效处理给定主题。注意：`asyncio` 提供的是并发而非并行：在单线程上用事件循环在某任务空闲（如等待网络请求）时在任务间切换，造成多任务同时推进的观感，但代码仍主要由单线程执行，受 Python 全局解释器锁（GIL）约束。

The code begins by importing essential modules from `langchain_openai` and `langchain_core`, including components for language models, prompts, output parsing, and runnable structures. The code attempts to initialize a ChatOpenAI instance, specifically using the "gpt-4o-mini" model, with a specified temperature for controlling creativity. A try-except block is used for robustness during the language model initialization. Three independent LangChain "chains" are then defined, each designed to perform a distinct task on the input topic. The first chain is for summarizing the topic concisely, using a system message and a user message containing the topic placeholder. The second chain is configured to generate three interesting questions related to the topic. The third chain is set up to identify between 5 and 10 key terms from the input topic, requesting them to be comma-separated. Each of these independent chains consists of a ChatPromptTemplate tailored to its specific task, followed by the initialized language model and a StrOutputParser to format the output as a string.

> 代码从 `langchain_openai` 与 `langchain_core` 导入语言模型、提示、输出解析与可运行结构等组件；尝试初始化 `ChatOpenAI`（具体为 `gpt-4o-mini`）并设温度；用 try-except 增强初始化稳健性。随后定义三条独立 LangChain「链」：第一条简洁总结主题；第二条生成三个相关问题；第三条识别 5–10 个关键词并以逗号分隔。各链由针对任务的 `ChatPromptTemplate`、已初始化模型与 `StrOutputParser` 组成。

A RunnableParallel block is then constructed to bundle these three chains, allowing them to execute simultaneously. This parallel runnable also includes a RunnablePassthrough to ensure the original input topic is available for subsequent steps. A separate ChatPromptTemplate is defined for the final synthesis step, taking the summary, questions, key terms, and the original topic as input to generate a comprehensive answer. The full end-to-end processing chain, named `full_parallel_chain`, is created by sequencing the `map_chain` (the parallel block) into the synthesis prompt, followed by the language model and the output parser. An asynchronous function `run_parallel_example` is provided to demonstrate how to invoke this `full_parallel_chain`. This function takes the topic as input and uses invoke to run the asynchronous chain. Finally, the standard Python `if __name__ \== "__main__":` block shows how to execute the `run_parallel_example` with a sample topic, in this case, "The history of space exploration", using asyncio.run to manage the asynchronous execution.

> 继而用 `RunnableParallel` 打包三条链以同时执行；并行块含 `RunnablePassthrough` 以保留原始主题。另设最终综合步骤的 `ChatPromptTemplate`，输入摘要、问题、关键词与原始主题以生成全面回答。端到端链 `full_parallel_chain` 将 `map_chain` 接到综合提示，再接语言模型与输出解析器。异步函数 `run_parallel_example` 演示如何调用该链。标准 `if __name__ == "__main__":` 块以样例主题「The history of space exploration」通过 `asyncio.run` 运行异步执行。

In essence, this code sets up a workflow where multiple LLM calls (for summarizing, questions, and terms) happen at the same time for a given topic, and their results are then combined by a final LLM call. This showcases the core idea of parallelization in an agentic workflow using LangChain.

> 本质上，该代码建立的工作流对给定主题同时发起多次 LLM 调用（总结、问题、术语），再由最终一次 LLM 调用合并结果，展示 LangChain 智能体工作流中并行化的核心思想。

## Hands-On Code Example (Google ADK)

> ## 动手代码示例（Google ADK）

Okay, let's now turn our attention to a concrete example illustrating these concepts within the Google ADK framework. We'll examine how the ADK primitives, such as ParallelAgent and SequentialAgent, can be applied to build an agent flow that leverages concurrent execution for improved efficiency.

> 下面看 Google ADK 框架中的具体示例，考察 `ParallelAgent`、`SequentialAgent` 等原语如何用于构建利用并发执行以提升效率的智能体流。

```python
from google.adk.agents import LlmAgent, ParallelAgent, SequentialAgent
from google.adk.tools import google_search

GEMINI_MODEL = "gemini-2.0-flash"


# --- 1. Define Researcher Sub-Agents (to run in parallel) ---

# Researcher 1: Renewable Energy
researcher_agent_1 = LlmAgent(
    name="RenewableEnergyResearcher",
    model=GEMINI_MODEL,
    instruction="""You are an AI Research Assistant specializing in energy. Research the latest advancements in 'renewable energy sources'. Use the Google Search tool provided. Summarize your key findings concisely (1-2 sentences). Output *only* the summary. """,
    description="Researches renewable energy sources.",
    tools=[google_search],
    # Store result in state for the merger agent
    output_key="renewable_energy_result",
)

# Researcher 2: Electric Vehicles
researcher_agent_2 = LlmAgent(
    name="EVResearcher",
    model=GEMINI_MODEL,
    instruction="""You are an AI Research Assistant specializing in transportation. Research the latest developments in 'electric vehicle technology'. Use the Google Search tool provided. Summarize your key findings concisely (1-2 sentences). Output *only* the summary. """,
    description="Researches electric vehicle technology.",
    tools=[google_search],
    # Store result in state for the merger agent
    output_key="ev_technology_result",
)

# Researcher 3: Carbon Capture
researcher_agent_3 = LlmAgent(
    name="CarbonCaptureResearcher",
    model=GEMINI_MODEL,
    instruction="""You are an AI Research Assistant specializing in climate solutions. Research the current state of 'carbon capture methods'. Use the Google Search tool provided. Summarize your key findings concisely (1-2 sentences). Output *only* the summary. """,
    description="Researches carbon capture methods.",
    tools=[google_search],
    # Store result in state for the merger agent
    output_key="carbon_capture_result",
)


# --- 2. Create the ParallelAgent (Runs researchers concurrently) ---
# This agent orchestrates the concurrent execution of the researchers.
# It finishes once all researchers have completed and stored their results in state.
parallel_research_agent = ParallelAgent(
    name="ParallelWebResearchAgent",
    sub_agents=[researcher_agent_1, researcher_agent_2, researcher_agent_3],
    description="Runs multiple research agents in parallel to gather information.",
)


# --- 3. Define the Merger Agent (Runs after the parallel agents) ---
# This agent takes the results stored in the session state by the parallel agents
# and synthesizes them into a single, structured response with attributions.
merger_agent = LlmAgent(
    name="SynthesisAgent",
    model=GEMINI_MODEL,  # Or potentially a more powerful model if needed for synthesis
    instruction="""You are an AI Assistant responsible for combining research findings into a structured report. Your primary task is to synthesize the following research summaries, clearly attributing findings to their source areas. Structure your response using headings for each topic. Ensure the report is coherent and integrates the key points smoothly.

**Crucially:** Your entire response MUST be grounded *exclusively* on the information provided in the 'Input Summaries' below. Do NOT add any external knowledge, facts, or details not present in these specific summaries.

**Input Summaries:**
*   **Renewable Energy:**
    {renewable_energy_result}
*   **Electric Vehicles:**
    {ev_technology_result}
*   **Carbon Capture:**
    {carbon_capture_result}

**Output Format:**
## Summary of Recent Sustainable Technology Advancements

### Renewable Energy Findings (Based on RenewableEnergyResearcher's findings)
[Synthesize and elaborate *only* on the renewable energy input summary provided above.]

### Electric Vehicle Findings (Based on EVResearcher's findings)
[Synthesize and elaborate *only* on the EV input summary provided above.]

### Carbon Capture Findings (Based on CarbonCaptureResearcher's findings)
[Synthesize and elaborate *only* on the carbon capture input summary provided above.]

### Overall Conclusion
[Provide a brief (1-2 sentence) concluding statement that connects *only* the findings presented above.]

Output *only* the structured report following this format. Do not include introductory or concluding phrases outside this structure, and strictly adhere to using only the provided input summary content.
""",
    description="Combines research findings from parallel agents into a structured, cited report, strictly grounded on provided inputs.",
    # No tools needed for merging
    # No output_key needed here, as its direct response is the final output of the sequence
)


# --- 4. Create the SequentialAgent (Orchestrates the overall flow) ---
# This is the main agent that will be run. It first executes the ParallelAgent
# to populate the state, and then executes the MergerAgent to produce the final output.
sequential_pipeline_agent = SequentialAgent(
    name="ResearchAndSynthesisPipeline",
    # Run parallel research first, then merge
    sub_agents=[parallel_research_agent, merger_agent],
    description="Coordinates parallel research and synthesizes the results.",
)

root_agent = sequential_pipeline_agent
```

This code defines a multi-agent system used to research and synthesize information on sustainable technology advancements. It sets up three LlmAgent instances to act as specialized researchers. `ResearcherAgent_1` focuses on renewable energy sources, `ResearcherAgent_2` researches electric vehicle technology, and `ResearcherAgent_3` investigates carbon capture methods. Each researcher agent is configured to use a `GEMINI_MODEL` and the `google_search` tool. They are instructed to summarize their findings concisely (1-2 sentences) and store these summaries in the session state using `output_key`.

> 该代码定义用于研究并综合可持续技术进展信息的多智能体系统：三个 `LlmAgent` 作为专用研究员——`ResearcherAgent_1` 关注可再生能源，`ResearcherAgent_2` 研究电动车技术，`ResearcherAgent_3` 调查碳捕集方法。各研究员配置 `GEMINI_MODEL` 与 `google_search`，被要求用 1–2 句简洁总结，并通过 `output_key` 写入会话状态。

A ParallelAgent named ParallelWebResearchAgent is then created to run these three researcher agents concurrently. This allows the research to be conducted in parallel, potentially saving time. The ParallelAgent completes its execution once all its sub-agents (the researchers) have finished and populated the state.

> 随后创建名为 ParallelWebResearchAgent 的 `ParallelAgent`，并发运行三名研究员，可节省时间；当所有子智能体完成并写入状态后，`ParallelAgent` 结束执行。

Next, a MergerAgent (also an LlmAgent) is defined to synthesize the research results. This agent takes the summaries stored in the session state by the parallel researchers as input. Its instruction emphasizes that the output must be strictly based only on the provided input summaries, prohibiting the addition of external knowledge. The MergerAgent is designed to structure the combined findings into a report with headings for each topic and a brief overall conclusion.

> 接着定义 MergerAgent（亦为 `LlmAgent`）以综合研究结果：输入为并行研究员写入会话状态的摘要；指令强调输出必须严格仅基于所给摘要，禁止加入外部知识；设计为按主题标题与简短总结构成报告。

Finally, a SequentialAgent named ResearchAndSynthesisPipeline is created to orchestrate the entire workflow. As the primary controller, this main agent first executes the ParallelAgent to perform the research. Once the ParallelAgent is complete, the SequentialAgent then executes the MergerAgent to synthesize the collected information. The `sequential_pipeline_agent` is set as the `root_agent`, representing the entry point for running this multi-agent system. The overall process is designed to efficiently gather information from multiple sources in parallel and then combine it into a single, structured report.

> 最后创建名为 ResearchAndSynthesisPipeline 的 `SequentialAgent` 编排全流程：主控先执行 `ParallelAgent` 做研究，完成后执行 `MergerAgent` 综合信息。`sequential_pipeline_agent` 设为 `root_agent` 作为入口。整体设计旨在并行从多源高效收集信息，再合并为单一结构化报告。

## At a Glance

> ## 速览

**What:** Many agentic workflows involve multiple sub-tasks that must be completed to achieve a final goal. A purely sequential execution, where each task waits for the previous one to finish, is often inefficient and slow. This latency becomes a significant bottleneck when tasks depend on external I/O operations, such as calling different APIs or querying multiple databases. Without a mechanism for concurrent execution, the total processing time is the sum of all individual task durations, hindering the system's overall performance and responsiveness.

> **是什么：** 许多智能体工作流包含为达成最终目标必须完成的多个子任务。纯顺序执行（每项等上一项结束）往往低效缓慢；当任务依赖外部 I/O（如调用不同 API、查询多库）时，延迟会成为显著瓶颈。若无并发机制，总耗时为各任务耗时之和，拖累整体性能与响应性。

**Why:** The Parallelization pattern provides a standardized solution by enabling the simultaneous execution of independent tasks. It works by identifying components of a workflow, like tool usages or LLM calls, that do not rely on each other's immediate outputs. Agentic frameworks like LangChain and the Google ADK provide built-in constructs to define and manage these concurrent operations. For instance, a main process can invoke several sub-tasks that run in parallel and wait for all of them to complete before proceeding to the next step. By running these independent tasks at the same time rather than one after another, this pattern drastically reduces the total execution time.

> **为什么：** 并行化模式通过同时执行独立任务提供标准解法：识别工作流中彼此不立即依赖输出的环节（如工具使用或 LLM 调用）。LangChain、Google ADK 等框架提供内建构造以定义与管理并发。例如主进程可并行启动若干子任务，待全部完成后再进入下一步。独立任务同时而非依次运行，可大幅缩短总执行时间。

**Rule of thumb:** Use this pattern when a workflow contains multiple independent operations that can run simultaneously, such as fetching data from several APIs, processing different chunks of data, or generating multiple pieces of content for later synthesis.

> **经验法则：** 当工作流含多个可同时运行的独立操作时采用本模式，例如从多个 API 取数、处理不同数据块，或为后续综合并发生成多段内容。

**Visual summary:**

> **图示摘要：**

![Parallelization Design Pattern](../assets-new/Parallelization_Design_Pattern.png)

Fig.2: Parallelization design pattern

> 图 2：并行化设计模式

## Key Takeaways

> ## 要点

Here are the key takeaways:

> 要点如下：

* Parallelization is a pattern for executing independent tasks concurrently to improve efficiency.  
* It is particularly useful when tasks involve waiting for external resources, such as API calls.  
* The adoption of a concurrent or parallel architecture introduces substantial complexity and cost, impacting key development phases such as design, debugging, and system logging.  
* Frameworks like LangChain and Google ADK provide built-in support for defining and managing parallel execution.  
* In LangChain Expression Language (LCEL), RunnableParallel is a key construct for running multiple runnables side-by-side.  
* Google ADK can facilitate parallel execution through LLM-Driven Delegation, where a Coordinator agent's LLM identifies independent sub-tasks and triggers their concurrent handling by specialized sub-agents.  
* Parallelization helps reduce overall latency and makes agentic systems more responsive for complex tasks.

> * 并行化是并发执行独立任务以提升效率的模式。  
> * 任务需等待外部资源（如 API）时尤其有用。  
> * 采用并发/并行架构会引入显著复杂度与成本，影响设计、调试与系统日志等阶段。  
> * LangChain 与 Google ADK 等框架提供定义与管理并行执行的内建支持。  
> * 在 LCEL 中，`RunnableParallel` 是并排运行多个可运行对象的关键构造。  
> * Google ADK 可通过 LLM 驱动委托实现并行：协调智能体的 LLM 识别独立子任务并触发专用子智能体并发处理。  
> * 并行化有助于降低整体延迟，使复杂任务下的智能体系统更灵敏。

## Conclusion

> ## 结语

The parallelization pattern is a method for optimizing computational workflows by concurrently executing independent sub-tasks. This approach reduces overall latency, particularly in complex operations that involve multiple model inferences or calls to external services.

> 并行化模式通过并发执行独立子任务优化计算工作流，降低整体延迟，尤其在含多次模型推理或外部服务调用的复杂操作中。

Frameworks provide distinct mechanisms for implementing this pattern. In LangChain, constructs like RunnableParallel are used to explicitly define and execute multiple processing chains simultaneously. In contrast, frameworks like the Google Agent Developer Kit (ADK) can achieve parallelization through multi-agent delegation, where a primary coordinator model assigns different sub-tasks to specialized agents that can operate concurrently.

> 各框架提供不同实现机制：LangChain 用 `RunnableParallel` 等显式定义并同时执行多条处理链；Google Agent Developer Kit（ADK）等则可通过多智能体委托实现并行——主协调模型将不同子任务分给可并发运行的专用智能体。

By integrating parallel processing with sequential (chaining) and conditional (routing) control flows, it becomes possible to construct sophisticated, high-performance computational systems capable of efficiently managing diverse and complex tasks.

> 将并行处理与顺序（链式）及条件（路由）控制流结合，可构建能高效管理多样复杂任务的高性能计算系统。

## References

> 下列为英文参考资料链接（条目保持原文）。

Here are some resources for further reading on the Parallelization pattern and related concepts:

1. LangChain Expression Language (LCEL) Documentation (Parallelism): [https://python.langchain.com/docs/concepts/lcel/](https://python.langchain.com/docs/concepts/lcel/)
2. Google Agent Developer Kit (ADK) Documentation (Multi-Agent Systems): [https://google.github.io/adk-docs/agents/multi-agents/](https://google.github.io/adk-docs/agents/multi-agents/)  
3. Python `asyncio` Documentation: [https://docs.python.org/3/library/asyncio.html](https://docs.python.org/3/library/asyncio.html)
