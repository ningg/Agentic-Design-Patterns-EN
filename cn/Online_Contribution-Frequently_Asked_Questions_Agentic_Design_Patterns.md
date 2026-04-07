# **Frequently Asked Questions: Agentic Design Patterns**

> **常见问题：智能体设计模式**

## 1. What is an "agentic design pattern"?

> ## 1. 什么是「智能体设计模式」？

An agentic design pattern is a reusable, high-level solution to a common problem encountered when building intelligent, autonomous systems (agents). These patterns provide a structured framework for designing agent behaviors, much like software design patterns do for traditional programming. They help developers build more robust, predictable, and effective AI agents.

> 智能体设计模式是在构建智能、自主系统（智能体）时，针对常见问题可复用的高层解决方案。这些模式为设计智能体行为提供结构化框架，作用类似传统编程中的软件设计模式，帮助开发者构建更稳健、可预期、更有效的 AI 智能体。

## 2. What is the main goal of this guide?

> ## 2. 本指南的主要目标是什么？

The guide aims to provide a practical, hands-on introduction to designing and building agentic systems. It moves beyond theoretical discussions to offer concrete architectural blueprints that developers can use to create agents capable of complex, goal-oriented behavior in a reliable way.

> 本指南旨在以实践、动手的方式介绍如何设计与构建智能体系统。它超越纯理论讨论，提供具体的架构蓝图，供开发者用来可靠地创建能够完成复杂、目标导向行为的智能体。

## 3. Who is the intended audience for this guide?

> ## 3. 本指南面向哪些读者？

This guide is written for AI developers, software engineers, and system architects who are building applications with large language models (LLMs) and other AI components. It is for those who want to move from simple prompt-response interactions to creating sophisticated, autonomous agents.

> 本指南面向使用大语言模型（LLM）及其他 AI 组件构建应用的 AI 开发者、软件工程师与系统架构师，也适合希望从简单「提示—回复」交互迈向构建复杂、自主智能体的读者。

## 4. What are some of the key agentic patterns discussed?

> ## 4. 文中讨论了哪些关键智能体模式？

Based on the table of contents, the guide covers several key patterns, including:

> 根据目录，本指南涵盖若干关键模式，包括：

- **Reflection:** The ability of an agent to critique its own actions and outputs to improve performance.  
> - **反思（Reflection）：** 智能体能够审视自身行为与输出以改进表现的能力。
- **Planning:** The process of breaking down a complex goal into smaller, manageable steps or tasks.  
> - **规划（Planning）：** 将复杂目标拆解为更小、可执行的步骤或任务的过程。
- **Tool Use:** The pattern of an agent utilizing external tools (like code interpreters, search engines, or other APIs) to acquire information or perform actions it cannot do on its own.  
> - **工具使用（Tool Use）：** 智能体利用外部工具（如代码解释器、搜索引擎或其他 API）获取信息或执行其自身无法完成的动作的模式。
- **Multi-Agent Collaboration:** The architecture for having multiple specialized agents work together to solve a problem, often involving a "leader" or "orchestrator" agent.  
> - **多智能体协作（Multi-Agent Collaboration）：** 多个专业智能体协同解决问题的架构，通常包含「负责人」或「编排」智能体。
- **Human-in-the-Loop:** The integration of human oversight and intervention, allowing for feedback, correction, and approval of an agent's actions.  
> - **人在回路（Human-in-the-Loop）：** 融入人类监督与干预，以便对智能体的行为进行反馈、纠正与批准。

## 5. Why is "planning" an important pattern

> ## 5. 为什么「规划」是重要的模式？

Planning is crucial because it allows an agent to tackle complex, multi-step tasks that cannot be solved with a single action. By creating a plan, the agent can maintain a coherent strategy, track its progress, and handle errors or unexpected obstacles in a structured manner. This prevents the agent from getting "stuck" or deviating from the user's ultimate goal.

> 规划至关重要，因为它使智能体能够处理无法靠单一动作完成的复杂、多步骤任务。通过制定计划，智能体可以保持连贯策略、跟踪进度，并以结构化方式应对错误或意外障碍，从而避免「卡住」或偏离用户的最终目标。

## 6. What is the difference between a "tool" and a "skill" for an agent

> ## 6. 对智能体而言，「工具」与「技能」有何不同？

While the terms are often used interchangeably, a "tool" generally refers to an external resource the agent can call upon (e.g., a weather API, a calculator). A "skill" is a more integrated capability that the agent has learned, often combining tool use with internal reasoning to perform a specific function (e.g., the skill of "booking a flight" might involve using calendar and airline APIs).

> 二者常被混用，但「工具」一般指智能体可调用的外部资源（如天气 API、计算器）。「技能」则是更整合的能力，通常结合工具使用与内部推理以完成特定功能（例如「预订航班」可能涉及日历与航司 API）。

## 7. How does the "Reflection" pattern improve an agent's performance

> ## 7. 「反思」模式如何提升智能体表现？

Reflection acts as a form of self-correction. After generating a response or completing a task, the agent can be prompted to review its work, check for errors, assess its quality against certain criteria, or consider alternative approaches. This iterative refinement process helps the agent produce more accurate, relevant, and high-quality results.

> 反思是一种自我纠正。在生成回复或完成任务后，可提示智能体复查工作、检查错误、按标准评估质量或考虑其他做法。这种迭代精炼有助于产出更准确、相关且高质量的结果。

## 8. What is the core idea of the Reflection pattern

> ## 8. 反思模式的核心思想是什么？

The Reflection pattern gives an agent the ability to step back and critique its own work. Instead of producing a final output in one go, the agent generates a draft and then "reflects" on it, identifying flaws, missing information, or areas for improvement. This self-correction process is key to enhancing the quality and accuracy of its responses.

> 反思模式让智能体能够退后一步、审视自身工作。它不是一次性给出终稿，而是先产生草稿再对其「反思」，找出缺陷、缺失信息或可改进之处。这一自我纠正过程是提升回复质量与准确性的关键。

## 9. Why is simple "prompt chaining" not enough for high-quality output?**

> ## 9. 为什么简单的「提示链」不足以得到高质量输出？**

Simple prompt chaining (where the output of one prompt becomes the input for the next) is often too basic. The model might just rephrase its previous output without genuinely improving it. A true Reflection pattern requires a more structured critique, prompting the agent to analyze its work against specific standards, check for logical errors, or verify facts.

> 简单提示链（上一段提示的输出作为下一段输入）往往过于粗糙。模型可能只是改写先前输出而并未真正改进。真正的反思模式需要更结构化的批判，引导智能体按具体标准分析工作、检查逻辑错误或核实事实。

## 10. What are the two main types of reflection mentioned in this chapter?**

> ## 10. 本章提到的两类主要反思是什么？**

The chapter discusses two primary forms of reflection:

> 本章讨论两种主要形式的反思：

- **"Check your work" Reflection:** This is a basic form where the agent is simply asked to review and fix its previous output. It's a good starting point for catching simple errors.  
> - **「检查你的工作」式反思：** 基础形式，要求智能体复查并修正先前输出，适合作为发现简单错误的起点。
- **"Internal Critic" Reflection:** This is a more advanced form where a separate, "critic" agent (or a dedicated prompt) is used to evaluate the output of the "worker" agent. This critic can be given specific criteria to look for, leading to more rigorous and targeted improvements.  
> - **「内部批评者」式反思：** 更高级的形式，由独立的「批评者」智能体（或专用提示）评估「工作者」智能体的输出；可为批评者设定具体评判标准，从而带来更严格、更有针对性的改进。

## 11. How does reflection help in reducing "hallucinations"?

> ## 11. 反思如何帮助减少「幻觉」？

By prompting an agent to review its work, especially by comparing its statements against a known source or by checking its own reasoning steps, the Reflection pattern can significantly reduce the likelihood of hallucinations (making up facts). The agent is forced to be more grounded in the provided context and less likely to generate unsupported information.

> 通过提示智能体复查工作——尤其是将陈述与已知来源对照或检查自身推理步骤——反思模式可显著降低编造事实（幻觉）的概率，促使智能体更扎根于给定上下文，减少无依据信息。

## 12. Can the Reflection pattern be applied more than once?

> ## 12. 反思模式可以多次应用吗？

Yes, reflection can be an iterative process. An agent can be made to reflect on its work multiple times, with each loop refining the output further. This is particularly useful for complex tasks where the first or second attempt may still contain subtle errors or could be substantially improved.

> 可以，反思可以是迭代过程。可让智能体多次反思，每一轮进一步精炼输出；这对复杂任务尤其有用，因为第一、二次尝试仍可能有细微错误或仍有较大改进空间。

## 13. What is the Planning pattern in the context of AI agents?

> ## 13. 在 AI 智能体语境下，规划模式是什么？

The Planning pattern involves enabling an agent to break down a complex, high-level goal into a sequence of smaller, actionable steps. Instead of trying to solve a big problem at once, the agent first creates a "plan" and then executes each step in the plan, which is a much more reliable approach.

> 规划模式指让智能体将复杂的高层目标分解为一系列更小、可执行的步骤。不是一次性解决大问题，而是先制定「计划」再逐步执行，这种方式可靠得多。

## 14. Why is planning necessary for complex tasks?

> ## 14. 为什么复杂任务需要规划？

LLMs can struggle with tasks that require multiple steps or dependencies. Without a plan, an agent might lose track of the overall objective, miss crucial steps, or fail to handle the output of one step as the input for the next. A plan provides a clear roadmap, ensuring all requirements of the original request are met in a logical order.

> LLM 在多步骤或有依赖的任务上容易吃力。没有计划，智能体可能迷失总体目标、遗漏关键步骤，或无法把一步的输出正确作为下一步的输入。计划提供清晰路线图，确保按逻辑顺序满足原始请求的全部要求。

## 15. What is a common way to implement the Planning pattern?

> ## 15. 实现规划模式的常见做法是什么？

A common implementation is to have the agent first generate a list of steps in a structured format (like a JSON array or a numbered list). The system can then iterate through this list, executing each step one by one and feeding the result back to the agent to inform the next action.

> 常见实现是先让智能体以结构化格式（如 JSON 数组或编号列表）生成步骤清单；系统再逐项执行，并把结果回传给智能体以指导下一步动作。

## 16. How does the agent handle errors or changes during execution?

> ## 16. 执行过程中智能体如何处理错误或变化？

A robust planning pattern allows for dynamic adjustments. If a step fails or the situation changes, the agent can be prompted to "re-plan" from the current state. It can analyze the error, modify the remaining steps, or even add new ones to overcome the obstacle.

> 稳健的规划模式允许动态调整。若某步失败或情况变化，可提示智能体从当前状态「重新规划」：分析错误、修改后续步骤，甚至增加新步骤以克服障碍。

## 17. Does the user see the plan?

> ## 17. 用户会看到计划吗？

This is a design choice. In many cases, showing the plan to the user first for approval is a great practice. This aligns with the "Human-in-the-Loop" pattern, giving the user transparency and control over the agent's proposed actions before they are executed.

> 这是设计选择。许多情况下，先向用户展示计划并征得同意是良好实践，与「人在回路」一致，在执行前给用户透明度与对拟议行为的控制权。

## 18. What does the "Tool Use" pattern entail?

> ## 18. 「工具使用」模式包含什么？

The Tool Use pattern allows an agent to extend its capabilities by interacting with external software or APIs. Since an LLM's knowledge is static and it can't perform real-world actions on its own, tools give it access to live information (e.g., Google Search), proprietary data (e.g., a company's database), or the ability to perform actions (e.g., send an email, book a meeting).

> 工具使用模式让智能体通过与外部软件或 API 交互来扩展能力。LLM 的知识是静态的且无法独自完成现实世界动作，工具使其能访问实时信息（如 Google 搜索）、专有数据（如公司数据库）或执行动作（如发邮件、订会议）。

## 19. How does an agent decide which tool to use?

> ## 19. 智能体如何决定使用哪个工具？

The agent is typically given a list of available tools along with descriptions of what each tool does and what parameters it requires. When faced with a request it can't handle with its internal knowledge, the agent's reasoning ability allows it to select the most appropriate tool from the list to accomplish the task.

> 通常会给智能体可用工具列表，并说明各工具用途与所需参数。当请求无法仅靠内部知识处理时，智能体的推理能力使其能从列表中选择最合适的工具完成任务。

## 20. What is the "ReAct" (Reason and Act) framework mentioned in this context?

> ## 20. 此处提到的「ReAct」（推理与行动）框架是什么？

ReAct is a popular framework that integrates reasoning and acting. The agent follows a loop of **Thought** (reasoning about what it needs to do), **Action** (deciding which tool to use and with what inputs), and **Observation** (seeing the result from the tool). This loop continues until it has gathered enough information to fulfill the user's request.

> ReAct 是融合推理与行动的常用框架。智能体循环进行：**思考**（推理需要做什么）、**行动**（决定使用哪个工具及输入）、**观察**（查看工具返回结果），直到收集足够信息以满足用户请求。

## 21. What are some challenges in implementing tool use?

> ## 21. 实现工具使用有哪些挑战？

Key challenges include:

> 主要挑战包括：

- **Error Handling:** Tools can fail, return unexpected data, or time out. The agent needs to be able to recognize these errors and decide whether to try again, use a different tool, or ask the user for help.  
> - **错误处理：** 工具可能失败、返回异常数据或超时。智能体需能识别这些错误，并决定重试、换工具或向用户求助。
- **Security:** Giving an agent access to tools, especially those that perform actions, has security implications. It's crucial to have safeguards, permissions, and often human approval for sensitive operations.  
> - **安全：** 让智能体访问工具（尤其是可执行动作的工具）涉及安全影响，必须有防护、权限，敏感操作常需人工批准。
- **Prompting:** The agent must be prompted effectively to generate correctly formatted tool calls (e.g., the right function name and parameters).  
> - **提示工程：** 必须有效提示智能体生成格式正确的工具调用（如正确的函数名与参数）。

## 22. What is the Human-in-the-Loop (HITL) pattern?

> ## 22. 什么是人在回路（HITL）模式？

HITL is a pattern that integrates human oversight and interaction into the agent's workflow. Instead of being fully autonomous, the agent pauses at critical junctures to ask for human feedback, approval, clarification, or direction.

> HITL 将人类监督与互动融入智能体工作流。智能体并非完全自主，而是在关键节点暂停，征求人类反馈、批准、澄清或指示。

## 23. Why is HITL important for agentic systems?

> ## 23. 为什么 HITL 对智能体系统很重要？

It's crucial for several reasons:

> 原因包括：

- **Safety and Control:** For high-stakes tasks (e.g., financial transactions, sending official communications), HITL ensures a human verifies the agent's proposed actions before they are executed.  
> - **安全与控制：** 对高风险任务（如金融交易、发送正式通信），HITL 确保在执行前由人类核实智能体的拟议动作。
- **Improving Quality:** Humans can provide corrections or nuanced feedback that the agent can use to improve its performance, especially in subjective or ambiguous tasks.  
> - **提升质量：** 人类可提供纠正或细致反馈，供智能体改进表现，尤其在主观或模糊任务中。
- **Building Trust:** Users are more likely to trust and adopt an AI system that they can guide and supervise.  
> - **建立信任：** 用户更可能信任并采用其能够引导与监督的 AI 系统。

## 24. At what points in a workflow should you include a human?

> ## 24. 工作流中应在哪些环节纳入人类？

Common points for human intervention include:

> 常见的人类介入点包括：

- **Plan Approval:** Before executing a multi-step plan.  
> - **计划批准：** 在执行多步计划之前。
- **Tool Use Confirmation:** Before using a tool that has real-world consequences or costs money.  
> - **工具使用确认：** 在使用有现实世界后果或产生费用的工具之前。
- **Ambiguity Resolution:** When the agent is unsure how to proceed or needs more information from the user.  
> - **消歧：** 当智能体不确定如何推进或需要用户提供更多信息时。
- **Final Output Review:** Before delivering the final result to the end-user or system.  
> - **终稿审阅：** 在向最终用户或系统交付最终结果之前。

## 25. Isn't constant human intervention inefficient?

> ## 25. 持续人工介入难道不低效吗？

It can be, which is why the key is to find the right balance. HITL should be implemented at critical checkpoints, not for every single action. The goal is to build a collaborative partnership between the human and the agent, where the agent handles the bulk of the work and the human provides strategic guidance.

> 可能会，因此关键在于把握平衡。HITL 应设在关键检查点，而非每一步动作。目标是建立人与智能体的协作伙伴关系：智能体承担大部分工作，人类提供战略指引。

## 26. What is the Multi-Agent Collaboration pattern?

> ## 26. 什么是多智能体协作模式？

This pattern involves creating a system composed of multiple specialized agents that work together to achieve a common goal. Instead of one "generalist" agent trying to do everything, you create a team of "specialist" agents, each with a specific role or expertise.

> 该模式由多个专业智能体协同实现共同目标。不是让一个「通才」智能体包办一切，而是组建「专家」团队，各担特定角色或专长。

## 27. What are the benefits of a multi-agent system?

> ## 27. 多智能体系统有什么好处？

- **Modularity and Specialization:** Each agent can be fine-tuned and prompted for its specific task (e.g., a "researcher" agent, a "writer" agent, a "code" agent), leading to higher quality results.  
> - **模块化与专业化：** 每个智能体可针对其任务微调与提示（如「研究」「写作」「代码」智能体），从而得到更高质量结果。
- **Reduced Complexity:** Breaking a complex workflow down into specialized roles makes the overall system easier to design, debug, and maintain.  
> - **降低复杂度：** 将复杂工作流拆成专业角色，使整体系统更易设计、调试与维护。
- **Simulated Brainstorming:** Different agents can offer different perspectives on a problem, leading to more creative and robust solutions, similar to how a human team works.  
> - **模拟头脑风暴：** 不同智能体可从不同角度看待问题，产生更有创意、更稳健的解法，类似人类团队协作。

## 28. What is a common architecture for multi-agent systems?

> ## 28. 多智能体系统的常见架构是什么？

A common architecture involves an **Orchestrator Agent** (sometimes called a "manager" or "conductor"). The orchestrator understands the overall goal, breaks it down, and delegates sub-tasks to the appropriate specialist agents. It then collects the results from the specialists and synthesizes them into a final output.

> 常见架构包含**编排智能体（Orchestrator Agent）**（有时称「经理」或「指挥」）。编排者理解总体目标、进行分解，并将子任务委派给合适的专家智能体，再汇总专家结果并合成为最终输出。

## How do the agents communicate with each other?

> ## 智能体之间如何通信？

Communication is often managed by the orchestrator. For example, the orchestrator might pass the output of the "researcher" agent to the "writer" agent as context. A shared "scratchpad" or message bus where agents can post their findings is another common communication method.

> 通信常由编排者管理。例如，编排者可将「研究」智能体的输出作为上下文传给「写作」智能体。共享「草稿本」或消息总线供智能体发布发现，也是常见通信方式。

## Why is evaluating an agent more difficult than evaluating a traditional software program?

> ## 为什么评估智能体比评估传统软件更难？

Traditional software has deterministic outputs (the same input always produces the same output). Agents, especially those using LLMs, are non-deterministic and their performance can be subjective. Evaluating them requires assessing the *quality* and *relevance* of their output, not just whether it's technically "correct."

> 传统软件输出是确定性的（相同输入总得到相同输出）。使用 LLM 的智能体往往非确定性，表现也可能带主观性。评估需判断输出的*质量*与*相关性*，而非仅看技术上是否「正确」。

## What are some common methods for evaluating agent performance?

> ## 评估智能体表现的常用方法有哪些？

The guide suggests a few methods:

> 本指南提出若干方法：

- **Outcome-based Evaluation:** Did the agent successfully achieve the final goal? For example, if the task was "book a flight," was a flight actually booked correctly? This is the most important measure.  
> - **结果导向评估：** 智能体是否成功达成最终目标？例如任务是「订机票」，是否确实正确订到？这是最重要的衡量。
- **Process-based Evaluation:** Was the agent's *process* efficient and logical? Did it use the right tools? Did it follow a sensible plan? This helps debug why an agent might be failing.  
> - **过程导向评估：** *过程*是否高效、合乎逻辑？是否用了对的工具？是否遵循合理计划？有助于调试失败原因。
- **Human Evaluation:** Having humans score the agent's performance on a scale (e.g., 1-5) based on criteria like helpfulness, accuracy, and coherence. This is crucial for user-facing applications.  
> - **人工评估：** 由人类按有用性、准确性、连贯性等标准打分（如 1–5），对面向用户的应用尤为关键。

## What is an "agent trajectory"?

> ## 什么是「智能体轨迹（agent trajectory）」？

An agent trajectory is the complete log of an agent's steps while performing a task. It includes all its thoughts, actions (tool calls), and observations. Analyzing these trajectories is a key part of debugging and understanding agent behavior.

> 智能体轨迹是执行任务时各步骤的完整日志，包含所有思考、动作（工具调用）与观察。分析轨迹是调试与理解智能体行为的关键部分。

## How can you create reliable tests for a non-deterministic system?

> ## 如何为非确定性系统编写可靠测试？

While you can't guarantee the exact wording of an agent's output, you can create tests that check for key elements. For example, you can write a test that verifies if the agent's final response *contains* specific information or if it successfully called a certain tool with the right parameters. This is often done using mock tools in a dedicated testing environment.

> 虽无法保证智能体输出的逐字一致，但可以编写检查关键要素的测试。例如验证最终回复是否*包含*特定信息，或是否以正确参数成功调用某工具；常在专用测试环境中用模拟（mock）工具实现。

## How is prompting an agent different from a simple ChatGPT prompt?

> ## 给智能体写提示与简单 ChatGPT 提示有何不同？

Prompting an agent involves creating a detailed "system prompt" or constitution that acts as its operating instructions. This goes beyond a single user query; it defines the agent's role, its available tools, the patterns it should follow (like ReAct or Planning), its constraints, and its personality.

> 对智能体提示意味着编写详细的「系统提示」或宪章式说明作为运行指令。这超越单次用户查询，需定义角色、可用工具、应遵循的模式（如 ReAct 或规划）、约束与个性。

## What are the key components of a good system prompt for an agent?

> ## 好的智能体系统提示应包含哪些要素？

A strong system prompt typically includes:

> 强健的系统提示通常包括：

- **Role and Goal:** Clearly define who the agent is and what its primary purpose is.  
> - **角色与目标：** 明确智能体是谁、首要目的为何。
- **Tool Definitions:** A list of available tools, their descriptions, and how to use them (e.g., in a specific function-calling format).  
> - **工具定义：** 可用工具列表、说明及用法（如特定函数调用格式）。
- **Constraints and Rules:** Explicit instructions on what the agent *should not* do (e.g., "Do not use tools without approval," "Do not provide financial advice").  
> - **约束与规则：** 明确*不应*做什么（如「未经批准不得使用工具」「不得提供理财建议」）。
- **Process Instructions:** Guidance on which patterns to use. For example, "First, create a plan. Then, execute the plan step-by-step."  
> - **流程说明：** 指导使用哪些模式，例如「先制定计划，再逐步执行」。
- **Example Trajectories:** Providing a few examples of successful "thought-action-observation" loops can significantly improve the agent's reliability.  
> - **示例轨迹：** 提供若干成功的「思考—行动—观察」循环示例，可显著提升可靠性。

## What is "prompt leakage"?

> ## 什么是「提示泄漏（prompt leakage）」？

Prompt leakage occurs when parts of the system prompt (like tool definitions or internal instructions) are inadvertently revealed in the agent's final response to the user. This can be confusing for the user and expose underlying implementation details. Techniques like using separate prompts for reasoning and for generating the final answer can help prevent this.

> 提示泄漏指系统提示的部分（如工具定义或内部指令）无意中出现在给用户的最终回复中，会令用户困惑并暴露实现细节。将推理与生成最终答案拆成不同提示等技术有助于防范。

## What are some future trends in agentic systems?

> ## 智能体系统有哪些未来趋势？

The guide points towards a future with:

> 本指南指向的未来包括：

- **More Autonomous Agents:** Agents that require less human intervention and can learn and adapt on their own.  
> - **更自主的智能体：** 更少人工干预、能自主学习与适应。
- **Highly Specialized Agents:** An ecosystem of agents that can be hired or subscribed to for specific tasks (e.g., a travel agent, a research agent).  
> - **高度专业化智能体：** 可雇佣或订阅以完成特定任务（如旅行、研究）的智能体生态。
- **Better Tools and Platforms:** The development of more sophisticated frameworks and platforms that make it easier to build, test, and deploy robust multi-agent systems.  
> - **更好的工具与平台：** 更成熟的框架与平台，使构建、测试与部署稳健的多智能体系统更容易。