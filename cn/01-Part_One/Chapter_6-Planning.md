# Chapter 6: Planning

Intelligent behavior often involves more than just reacting to the immediate input. It requires foresight, breaking down complex tasks into smaller, manageable steps, and strategizing how to achieve a desired outcome. This is where the Planning pattern comes into play. At its core, planning is the ability for an agent or a system of agents to formulate a sequence of actions to move from an initial state towards a goal state.

> 智能行为往往不只是对即时输入做出反应；它需要前瞻、把复杂任务拆成更小可管理的步骤，并谋划如何达成期望结果。这就是规划（Planning）模式发挥作用之处。其核心是：智能体或多智能体系统能够制定一系列行动，从初始状态走向目标状态。

## Planning Pattern Overview

In the context of AI, it's helpful to think of a planning agent as a specialist to whom you delegate a complex goal. When you ask it to "organize a team offsite," you are defining the what—the objective and its constraints—but not the how. The agent's core task is to autonomously chart a course to that goal. It must first understand the initial state (e.g., budget, number of participants, desired dates) and the goal state (a successfully booked offsite), and then discover the optimal sequence of actions to connect them. The plan is not known in advance; it is created in response to the request.

> 在 AI 语境下，不妨把规划智能体看作你委以复杂目标的专家。当你让它「组织一次团队外出活动时」，你定义的是做什么——目标与约束——而非怎么做。智能体的核心任务是自主规划通往该目标的路线。它必须先理解初始状态（如预算、人数、意向日期）与目标状态（成功订好活动），再发现连接二者的最优行动序列。计划并非预先已知，而是应请求而生成。

A hallmark of this process is adaptability. An initial plan is merely a starting point, not a rigid script. The agent's real power is its ability to incorporate new information and steer the project around obstacles. For instance, if the preferred venue becomes unavailable or a chosen caterer is fully booked, a capable agent doesn't simply fail. It adapts. It registers the new constraint, re-evaluates its options, and formulates a new plan, perhaps by suggesting alternative venues or dates.

> 这一过程的特点是适应性。初始计划只是起点，不是僵死剧本。智能体的真正力量在于吸收新信息并绕过障碍推进项目。例如首选场地不可用或所选餐饮已满，有能力的智能体不会简单失败，而是适应：记录新约束、重估选项、制定新计划，或许建议换场地或改日期。

However, it is crucial to recognize the trade-off between flexibility and predictability. Dynamic planning is a specific tool, not a universal solution. When a problem's solution is already well-understood and repeatable, constraining the agent to a predetermined, fixed workflow is more effective. This approach limits the agent's autonomy to reduce uncertainty and the risk of unpredictable behavior, guaranteeing a reliable and consistent outcome. Therefore, the decision to use a planning agent versus a simple task-execution agent hinges on a single question: does the "how" need to be discovered, or is it already known?

> 然而必须认清灵活性与可预测性之间的权衡。动态规划是特定工具，并非万能解。当问题的解法已充分理解且可重复时，把智能体约束在预定、固定的工作流中往往更有效：限制自主性以降低不确定性与行为失控风险，保证可靠一致的结果。因此，选用规划智能体还是简单任务执行智能体，取决于一个问题：「怎么做」还需要被发现，还是已经知道？

## Practical Applications & Use Cases

The Planning pattern is a core computational process in autonomous systems, enabling an agent to synthesize a sequence of actions to achieve a specified goal, particularly within dynamic or complex environments. This process transforms a high-level objective into a structured plan composed of discrete, executable steps.

> 规划模式是自主系统中的核心计算过程，使智能体能够综合出一系列行动以达成指定目标，尤其在动态或复杂环境中。它将高层目标转化为由离散、可执行步骤构成的结构化计划。

In domains such as procedural task automation, planning is used to orchestrate complex workflows. For example, a business process like onboarding a new employee can be decomposed into a directed sequence of sub-tasks, such as creating system accounts, assigning training modules, and coordinating with different departments. The agent generates a plan to execute these steps in a logical order, invoking necessary tools or interacting with various systems to manage dependencies.

> 在程序性任务自动化等领域，规划用于编排复杂工作流。例如新员工入职可分解为有向子任务序列：创建系统账号、分配培训模块、与各部门协调等。智能体生成计划按逻辑顺序执行这些步骤，调用必要工具或与各系统交互以管理依赖。

Within robotics and autonomous navigation, planning is fundamental for state-space traversal. A system, whether a physical robot or a virtual entity, must generate a path or sequence of actions to transition from an initial state to a goal state. This involves optimizing for metrics such as time or energy consumption while adhering to environmental constraints, like avoiding obstacles or following traffic regulations.

> 在机器人与自主导航中，规划是状态空间遍历的基础。无论物理机器人还是虚拟实体，都必须生成路径或行动序列，从初始状态过渡到目标状态；这涉及在时间或能耗等指标上优化，同时遵守环境约束，如避障或遵守交通规则。

This pattern is also critical for structured information synthesis. When tasked with generating a complex output like a research report, an agent can formulate a plan that includes distinct phases for information gathering, data summarization, content structuring, and iterative refinement. Similarly, in customer support scenarios involving multi-step problem resolution, an agent can create and follow a systematic plan for diagnosis, solution implementation, and escalation.

> 该模式对结构化信息综合也至关重要。生成研究报告等复杂产出时，智能体可制定计划，分阶段完成信息收集、数据摘要、内容结构与迭代打磨。同理，在多步问题解决的客服场景中，智能体可创建并遵循系统化的诊断、方案实施与升级计划。

In essence, the Planning pattern allows an agent to move beyond simple, reactive actions to goal-oriented behavior. It provides the logical framework necessary to solve problems that require a coherent sequence of interdependent operations.

> 本质上，规划模式使智能体超越简单反应式行动，走向目标导向行为；它为需要连贯、相互依赖操作序列的问题提供必要的逻辑框架。

## Hands-on code (Crew AI)

The following section will demonstrate an implementation of the Planner pattern using the Crew AI framework. This pattern involves an agent that first formulates a multi-step plan to address a complex query and then executes that plan sequentially.

> 以下演示如何用 Crew AI 框架实现规划者（Planner）模式：智能体先针对复杂查询制定多步计划，再按顺序执行。

```python
import os
from dotenv import load_dotenv
from crewai import Agent, Task, Crew, Process
from langchain_openai import ChatOpenAI


# Load environment variables from .env file for security
load_dotenv()


# 1. Explicitly define the language model for clarity
llm = ChatOpenAI(model="gpt-4-turbo")


# 2. Define a clear and focused agent
planner_writer_agent = Agent(
    role='Article Planner and Writer',
    goal='Plan and then write a concise, engaging summary on a specified topic.',
    backstory=(
        'You are an expert technical writer and content strategist. '
        'Your strength lies in creating a clear, actionable plan before writing, '
        'ensuring the final summary is both informative and easy to digest.'
    ),
    verbose=True,
    allow_delegation=False,
    llm=llm,  # Assign the specific LLM to the agent
)


# 3. Define a task with a more structured and specific expected output
topic = "The importance of Reinforcement Learning in AI"

high_level_task = Task(
    description=(
        f"1. Create a bullet-point plan for a summary on the topic: '{topic}'.\n"
        f"2. Write the summary based on your plan, keeping it around 200 words."
    ),
    expected_output=(
        "A final report containing two distinct sections:\n\n"
        "### Plan\n"
        "- A bulleted list outlining the main points of the summary.\n\n"
        "### Summary\n"
        "- A concise and well-structured summary of the topic."
    ),
    agent=planner_writer_agent,
)


# Create the crew with a clear process
crew = Crew(
    agents=[planner_writer_agent],
    tasks=[high_level_task],
    process=Process.sequential,
)


# Execute the task
print("## Running the planning and writing task ##")
result = crew.kickoff()

print("\n\n---\n## Task Result ##\n---")
print(result)
```

This code uses the CrewAI library to create an AI agent that plans and writes a summary on a given topic. It starts by importing necessary libraries, including Crew.ai and `langchain_openai`, and loading environment variables from a .env file. A ChatOpenAI language model is explicitly defined for use with the agent. An Agent named `planner_writer_agent` is created with a specific role and goal: to plan and then write a concise summary. The agent's backstory emphasizes its expertise in planning and technical writing. A Task is defined with a clear description to first create a plan and then write a summary on the topic "The importance of Reinforcement Learning in AI", with a specific format for the expected output. A Crew is assembled with the agent and task, set to process them sequentially. Finally, the crew.kickoff() method is called to execute the defined task and the result is printed.

> 该代码用 CrewAI 库创建会规划并撰写给定主题摘要的 AI 智能体。先导入 Crew.ai、`langchain_openai` 等库，并从 .env 加载环境变量；显式定义 ChatOpenAI 供智能体使用。创建 `planner_writer_agent`，角色与目标是先规划再写简明摘要，背景故事强调规划与技术写作专长。任务描述要求先列计划再就「The importance of Reinforcement Learning in AI」写约 200 词摘要，并对期望输出格式有明确要求。用该智能体与任务组装 Crew，处理流程为顺序执行；最后调用 `crew.kickoff()` 执行任务并打印结果。

## Google DeepResearch

Google Gemini DeepResearch (see Fig.1)  is an agent-based system designed for autonomous information retrieval and synthesis. It functions through a multi-step agentic pipeline that dynamically and iteratively queries Google Search to systematically explore complex topics. The system is engineered to process a large corpus of web-based sources, evaluate the collected data for relevance and knowledge gaps, and perform subsequent searches to address them. The final output consolidates the vetted information into a structured, multi-page summary with citations to the original sources.

> Google Gemini DeepResearch（见图 1）是面向自主信息检索与综合的智能体系统，经由多步智能体流水线动态、迭代地查询 Google 搜索以系统探索复杂主题。系统设计为处理大量网页来源，评估所收集数据的相关性与知识缺口并继续搜索补缺；最终把经核实的信息整合为带引用的结构化多页摘要。

Expanding on this, the system's operation is not a single query-response event but a managed, long-running process. It begins by deconstructing a user's prompt into a multi-point research plan (see Fig. 1), which is then presented to the user for review and modification. This allows for a collaborative shaping of the research trajectory before execution. Once the plan is approved, the agentic pipeline initiates its iterative search-and-analysis loop. This involves more than just executing a series of predefined searches; the agent dynamically formulates and refines its queries based on the information it gathers, actively identifying knowledge gaps, corroborating data points, and resolving discrepancies.

> 进一步说，其运行不是单次问答，而是受控的长期过程：先将用户提示拆解为多点研究计划（见图 1）并交用户审阅修改，从而在执行前协作塑造研究路径。计划获批后，智能体流水线启动迭代搜索—分析循环——不仅是执行预设搜索序列，还会根据已获信息动态制定与细化查询，主动发现缺口、交叉验证数据并消解矛盾。

![Google Deep Research agent generating an execution plan for using Google Search as a tool](../assets-new/Google_Deep_Research_Agent_Generating_an_execution_plan_for_using_Google_Search_as_a_Tool.png)

Fig. 1: Google Deep Research agent generating an execution plan for using Google Search as a tool.

> 图 1：Google Deep Research 智能体生成使用 Google 搜索作为工具的执行计划。

A key architectural component is the system's ability to manage this process asynchronously. This design ensures that the investigation, which can involve analyzing hundreds of sources, is resilient to single-point failures and allows the user to disengage and be notified upon completion. The system can also integrate user-provided documents, combining information from private sources with its web-based research. The final output is not merely a concatenated list of findings but a structured, multi-page report. During the synthesis phase, the model performs a critical evaluation of the collected information, identifying major themes and organizing the content into a coherent narrative with logical sections. The report is designed to be interactive, often including features like an audio overview, charts, and links to the original cited sources, allowing for verification and further exploration by the user. In addition to the synthesized results, the model explicitly returns the full list of sources it searched and consulted (see Fig.2). These are presented as citations, providing complete transparency and direct access to the primary information. This entire process transforms a simple query into a comprehensive, synthesized body of knowledge.

> 关键架构能力之一是异步管理该过程：调查可能涉及数百个来源的分析，设计使其能抵御单点故障，并允许用户离开后在完成时收到通知。系统还可整合用户提供的文档，将私有来源与网页研究结合。最终产出不是简单拼接发现，而是结构化多页报告；综合阶段模型会批判性评估信息、提炼主题并组织成有逻辑的叙事与章节。报告常具交互性，如音频概览、图表与指向原始引文的链接，便于核实与深挖。除综合结果外，模型还会显式返回其搜索与查阅的完整来源列表（见图 2），以引用形式呈现，保证透明与对一手信息的直达。整个过程把简单查询转化为全面、综合的知识体。

![An example of Deep Research plan being executed, resulting in Google Search being used as a tool to search various web sources](../assets-new/Example_of_Deep_Research_Plan_Being_Executed_Resulting_in_Google_Search_being_used_as_a_Tool_to_Search_Various_Web_Sources.png)

Fig. 2: An example of Deep Research plan being executed, resulting in Google Search being used as a tool to search various web sources.

> 图 2：Deep Research 计划执行示例：将 Google 搜索作为工具检索各类网页来源。

By mitigating the substantial time and resource investment required for manual data acquisition and synthesis, Gemini DeepResearch provides a more structured and exhaustive method for information discovery. The system's value is particularly evident in complex, multi-faceted research tasks across various domains.

> 通过减轻手工采集与综合所需的大量时间与资源投入，Gemini DeepResearch 为信息发现提供更结构化、更穷尽的方法；在跨领域复杂、多面研究任务中价值尤为明显。

For instance, in competitive analysis, the agent can be directed to systematically gather and collate data on market trends, competitor product specifications, public sentiment from diverse online sources, and marketing strategies. This automated process replaces the laborious task of manually tracking multiple competitors, allowing analysts to focus on higher-order strategic interpretation rather than data collection (see Fig. 3).

> 例如竞争分析中，可引导智能体系统收集并整理市场趋势、竞品规格、多源舆情与营销策略等数据，替代手工跟踪多家对手的繁重工作，使分析者专注于更高阶的战略解读而非数据采集（见图 3）。

![Final output generated by the Google Deep Research agent, analyzing on our behalf sources obtained using Google Search as a tool](../assets-new/Final_Output_Generated_by_Google_Deep_Research_Agent_Analyzing_on_our_Behalf_Sources_Obtained_using_Google_Search_as_a_Tool.png)

Fig. 3: Final output generated by the Google Deep Research agent, analyzing on our behalf sources obtained using Google Search as a tool.

> 图 3：Google Deep Research 智能体生成的最终输出：代我们分析以 Google 搜索为工具获得的来源。

Similarly, in academic exploration, the system serves as a powerful tool for conducting extensive literature reviews. It can identify and summarize foundational papers, trace the development of concepts across numerous publications, and map out emerging research fronts within a specific field, thereby accelerating the initial and most time-consuming phase of academic inquiry.

> 同理，在学术探索中，该系统可有力支持大规模文献综述：识别与摘要奠基性论文、追踪概念在大量出版物中的演进、勾勒特定领域新兴研究前沿，从而加速学术探究最初也最耗时的阶段。

The efficiency of this approach stems from the automation of the iterative search-and-filter cycle, which is a core bottleneck in manual research. Comprehensiveness is achieved by the system's capacity to process a larger volume and variety of information sources than is typically feasible for a human researcher within a comparable timeframe. This broader scope of analysis helps to reduce the potential for selection bias and increases the likelihood of uncovering less obvious but potentially critical information, leading to a more robust and well-supported understanding of the subject matter.

> 效率来自自动化迭代搜索—筛选循环——这是手工研究的核心瓶颈。全面性则来自系统在可比时间窗内处理比人类研究者通常可行更大体量与更多样来源的能力；更广的分析范围有助于降低选择性偏差，并提高发现隐晦但关键信息的可能性，从而得到更稳健、证据更充分的主题理解。

## OpenAI Deep Research API

The OpenAI Deep Research API is a specialized tool designed to automate complex research tasks. It utilizes an advanced, agentic model that can independently reason, plan, and synthesize information from real-world sources. Unlike a simple Q\&A model, it takes a high-level query and autonomously breaks it down into sub-questions, performs web searches using its built-in tools, and delivers a structured, citation-rich final report. The API provides direct programmatic access to this entire process, using  at the time of writing models like o3-deep-research-2025-06-26 for high-quality synthesis and the faster o4-mini-deep-research-2025-06-26 for latency-sensitive application

> OpenAI Deep Research API 是用于自动化复杂研究任务的专用工具，采用能独立推理、规划并从真实世界来源综合信息的高级智能体模型。与简单问答模型不同，它接收高层查询后自主拆分子问题、用内置工具做网页搜索并交付结构化、富引用的最终报告。API 以编程方式暴露全流程；截至本文撰写，可使用如 o3-deep-research-2025-06-26 追求高质量综合，或 o4-mini-deep-research-2025-06-26 满足低延迟场景。

The Deep Research API is useful because it automates what would otherwise be hours of manual research, delivering professional-grade, data-driven reports suitable for informing business strategy, investment decisions, or policy recommendations. Its key benefits include:

> Deep Research API 的价值在于将原本需数小时的手工研究自动化，产出专业级、数据驱动的报告，适用于商业战略、投资决策或政策建议等。其主要优势包括：

* **Structured, Cited Output:** It produces well-organized reports with inline citations linked to source metadata, ensuring claims are verifiable and data-backed.  
* **Transparency:** Unlike the abstracted process in ChatGPT, the API exposes all intermediate steps, including the agent's reasoning, the specific web search queries it executed, and any code it ran. This allows for detailed debugging, analysis, and a deeper understanding of how the final answer was constructed.  
* **Extensibility:** It supports the Model Context Protocol (MCP), enabling developers to connect the agent to private knowledge bases and internal data sources, blending public web research with proprietary information.

> * **结构化与引用输出：** 生成条理清晰的报告，行内引用关联来源元数据，主张可核实、有数据支撑。  
> * **透明性：** 不同于 ChatGPT 中抽象的过程，API 暴露全部中间步骤，包括智能体推理、实际执行的网页搜索查询及所运行代码，便于调试、分析与理解最终答案如何构成。  
> * **可扩展性：** 支持模型上下文协议（MCP），开发者可把智能体接到私有知识库与内部数据源，将公开网页研究与专有信息结合。

To use the API, you send a request to the client.responses.create endpoint, specifying a model, an input prompt, and the tools the agent can use. The input typically includes a `system_message` that defines the agent's persona and desired output format, along with the `user_query`. You must also include the `web_search_preview` tool and can optionally add others like `code_interpreter` or custom MCP tools (see Chapter 10) for internal data.

> 使用时向 `client.responses.create` 端点发请求，指定模型、输入提示与智能体可用工具。输入通常含定义角色与期望输出格式的 `system_message` 以及 `user_query`；必须包含 `web_search_preview` 工具，并可选用 `code_interpreter` 或自定义 MCP 工具（见第 10 章）以访问内部数据。

```python
from openai import OpenAI


# Initialize the client with your API key
client = OpenAI(api_key="YOUR_OPENAI_API_KEY")


# Define the agent's role and the user's research question
system_message = """
You are a professional researcher preparing a structured, data-driven report.
Focus on data-rich insights, use reliable sources, and include inline citations.
"""

user_query = "Research the economic impact of semaglutide on global healthcare systems."


# Create the Deep Research API call
response = client.responses.create(
    model="o3-deep-research-2025-06-26",
    input=[
        {
            "role": "developer",
            "content": [{"type": "input_text", "text": system_message}],
        },
        {
            "role": "user",
            "content": [{"type": "input_text", "text": user_query}],
        },
    ],
    reasoning={"summary": "auto"},
    tools=[{"type": "web_search_preview"}],
)


# Access and print the final report from the response
final_report = response.output[-1].content[0].text
print(final_report)


# --- ACCESS INLINE CITATIONS AND METADATA ---
print("--- CITATIONS ---")
annotations = response.output[-1].content[0].annotations

if not annotations:
    print("No annotations found in the report.")
else:
    for i, citation in enumerate(annotations):
        # The text span the citation refers to
        cited_text = final_report[citation.start_index : citation.end_index]
        print(f"Citation {i + 1}:")
        print(f"  Cited Text: {cited_text}")
        print(f"  Title: {citation.title}")
        print(f"  URL: {citation.url}")
        print(f"  Location: chars {citation.start_index}–{citation.end_index}")

print("\n" + "=" * 50 + "\n")


# --- INSPECT INTERMEDIATE STEPS ---
print("--- INTERMEDIATE STEPS ---")

# 1. Reasoning Steps: Internal plans and summaries generated by the model.
try:
    reasoning_step = next(item for item in response.output if item.type == "reasoning")
    print("\n[Found a Reasoning Step]")
    for summary_part in reasoning_step.summary:
        print(f"  - {summary_part.text}")
except StopIteration:
    print("\nNo reasoning steps found.")

# 2. Web Search Calls: The exact search queries the agent executed.
try:
    search_step = next(item for item in response.output if item.type == "web_search_call")
    print("\n[Found a Web Search Call]")
    print(f"  Query Executed: '{search_step.action['query']}'")
    print(f"  Status: {search_step.status}")
except StopIteration:
    print("\nNo web search steps found.")

# 3. Code Execution: Any code run by the agent using the code interpreter.
try:
    code_step = next(item for item in response.output if item.type == "code_interpreter_call")
    print("\n[Found a Code Execution Step]")
    print("  Code Input:")
    print(f"  ```python\n{code_step.input}\n  ```")
    print("  Code Output:")
    print(f"  {code_step.output}")
except StopIteration:
    print("\nNo code execution steps found.")
```

This code snippet utilizes the OpenAI API to perform a "Deep Research" task. It starts by initializing the OpenAI client with your API key, which is crucial for authentication. Then, it defines the role of the AI agent as a professional researcher and sets the user's research question about the economic impact of semaglutide. The code constructs an API call to the o3-deep-research-2025-06-26 model, providing the defined system message and user query as input. It also requests an automatic summary of the reasoning and enables web search capabilities. After making the API call, it extracts and prints the final generated report.

> 该片段用 OpenAI API 执行「Deep Research」任务：先用 API 密钥初始化客户端以认证；将智能体角色设为专业研究者并设定关于司美格鲁肽对全球医疗体系经济影响的研究问题；向 o3-deep-research-2025-06-26 构造请求，传入系统消息与用户查询，并请求推理摘要摘要且启用网页搜索；调用后提取并打印最终报告。

Subsequently, it attempts to access and display inline citations and metadata from the report's annotations, including the cited text, title, URL, and location within the report. Finally, it inspects and prints details about the intermediate steps the model took, such as reasoning steps, web search calls (including the query executed), and any code execution steps if a code interpreter was used.

> 随后尝试从报告标注中读取并展示行内引用与元数据（被引文本、标题、URL、在报告中的位置）；最后检查并打印中间步骤详情，如推理步骤、网页搜索调用（含执行的查询）以及若使用代码解释器时的代码执行步骤。

## At a Glance

**What:** Complex problems often cannot be solved with a single action and require foresight to achieve a desired outcome. Without a structured approach, an agentic system struggles to handle multifaceted requests that involve multiple steps and dependencies. This makes it difficult to break down high-level objectives into a manageable series of smaller, executable tasks. Consequently, the system fails to strategize effectively, leading to incomplete or incorrect results when faced with intricate goals.

> **是什么：** 复杂问题往往无法靠单一行动解决，需要前瞻才能达成目标。缺乏结构化方法时，智能体系统难以处理含多步与依赖的多面请求，难以把高层目标拆成可管理的小任务序列，因而战略化不足，面对棘手目标时易产出不完整或错误结果。

**Why:** The Planning pattern offers a standardized solution by having an agentic system first create a coherent plan to address a goal. It involves decomposing a high-level objective into a sequence of smaller, actionable steps or sub-goals. This allows the system to manage complex workflows, orchestrate various tools, and handle dependencies in a logical order. LLMs are particularly well-suited for this, as they can generate plausible and effective plans based on their vast training data. This structured approach transforms a simple reactive agent into a strategic executor that can proactively work towards a complex objective and even adapt its plan if necessary.

> **为什么：** 规划模式提供标准化解法：先由智能体系统为目标制定连贯计划，将高层目标分解为更小可执行的步骤或子目标，从而管理复杂工作流、编排多种工具并按逻辑顺序处理依赖。LLM 尤其胜任——可基于海量训练数据生成合理有效的计划；该结构化路径把简单反应式智能体转变为能主动推进复杂目标、必要时还可调整计划的战略执行者。

**Rule of thumb:** Use this pattern when a user's request is too complex to be handled by a single action or tool. It is ideal for automating multi-step processes, such as generating a detailed research report, onboarding a new employee, or executing a competitive analysis. Apply the Planning pattern whenever a task requires a sequence of interdependent operations to reach a final, synthesized outcome.

> **经验法则：** 当用户请求复杂到无法由单一行动或工具完成时使用本模式；适用于自动化多步流程，如撰写详尽研究报告、新员工入职或竞争分析。凡任务需要相互依赖的操作序列以得到最终综合结果，即适用规划模式。

**Visual summary**  

![Planning Design Pattern](../assets-new/Planning_Design_Pattern.png)

Fig.4; Planning design pattern

> 图 4：规划设计模式。

## Key Takeaways

* Planning enables agents to break down complex goals into actionable, sequential steps.  
* It is essential for handling multi-step tasks, workflow automation, and navigating complex environments.  
* LLMs can perform planning by generating step-by-step approaches based on task descriptions.  
* Explicitly prompting or designing tasks to require planning steps encourages this behavior in agent frameworks.  
* Google Deep Research is an agent analyzing on our behalf sources obtained using Google Search as a tool. It reflects, plans, and executes

> * 规划使智能体能把复杂目标分解为可执行的顺序步骤。  
> * 对多步任务、工作流自动化与在复杂环境中导航至关重要。  
> * LLM 可根据任务描述生成逐步方案以执行规划。  
> * 在提示或任务设计中明确要求规划步骤，可在智能体框架中强化该行为。  
> * Google Deep Research 是以 Google 搜索为工具代我们分析来源的智能体；它会反思、规划并执行。

## Conclusion

In conclusion, the Planning pattern is a foundational component that elevates agentic systems from simple reactive responders to strategic, goal-oriented executors. Modern large language models provide the core capability for this, autonomously decomposing high-level objectives into coherent, actionable steps. This pattern scales from straightforward, sequential task execution, as demonstrated by the CrewAI agent creating and following a writing plan, to more complex and dynamic systems. The Google DeepResearch agent exemplifies this advanced application, creating iterative research plans that adapt and evolve based on continuous information gathering. Ultimately, planning provides the essential bridge between human intent and automated execution for complex problems. By structuring a problem-solving approach, this pattern enables agents to manage intricate workflows and deliver comprehensive, synthesized results.

> 总之，规划模式是基础构件，将智能体系统从简单反应式应答提升为战略化、目标导向的执行者。现代大语言模型提供自主将高层目标分解为连贯可行动步骤的核心能力。该模式可从 CrewAI 智能体制定并遵循写作计划这类直接的顺序执行，扩展到更复杂动态的系统；Google DeepResearch 智能体即高级范例——基于持续信息收集创建迭代研究计划并不断演进。归根结底，规划在复杂问题中连接人类意图与自动执行；通过结构化解题路径，使智能体能管理错综复杂的工作流并交付全面综合的结果。

## References

1. Google DeepResearch (Gemini Feature): [gemini.google.com](http://gemini.google.com)
2. OpenAI ,Introducing deep research  [https://openai.com/index/introducing-deep-research/](https://openai.com/index/introducing-deep-research/)
3. Perplexity, Introducing Perplexity Deep Research, [https://www.perplexity.ai/hub/blog/introducing-perplexity-deep-research](https://www.perplexity.ai/hub/blog/introducing-perplexity-deep-research)
