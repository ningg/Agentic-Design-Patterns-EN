# Chapter 12: Exception Handling and Recovery

For AI agents to operate reliably in diverse real-world environments, they must be able to manage unforeseen situations, errors, and malfunctions. Just as humans adapt to unexpected obstacles, intelligent agents need robust systems to detect problems, initiate recovery procedures, or at least ensure controlled failure. This essential requirement forms the basis of the Exception Handling and Recovery pattern.

> 要使 AI 智能体在多样的真实环境中可靠运行，它们必须能够应对意外情况、错误与故障。正如人类会适应突发障碍，智能体也需要稳健的机制来发现问题、启动恢复流程，或至少保证受控失败。这一基本要求构成了「异常处理与恢复」模式的基础。

This pattern focuses on developing exceptionally durable and resilient agents that can maintain uninterrupted functionality and operational integrity despite various difficulties and anomalies. It emphasizes the importance of both proactive preparation and reactive strategies to ensure continuous operation, even when facing challenges. This adaptability is critical for agents to function successfully in complex and unpredictable settings, ultimately boosting their overall effectiveness and trustworthiness.

> 该模式侧重于培养极其耐久、有韧性的智能体，使其在各类困难与异常下仍能维持不间断的功能与运行完整性。它强调主动准备与被动应对并重，以确保持续运行，即便面临挑战。这种适应性对智能体在复杂、不可预测环境中成功运作至关重要，并最终提升其整体效能与可信度。

The capacity to handle unexpected events ensures these AI systems are not only intelligent but also stable and reliable, which fosters greater confidence in their deployment and performance. Integrating comprehensive monitoring and diagnostic tools further strengthens an agent's ability to quickly identify and address issues, preventing potential disruptions and ensuring smoother operation in evolving conditions. These advanced systems are crucial for maintaining the integrity and efficiency of AI operations, reinforcing their ability to manage complexity and unpredictability.

> 处理意外事件的能力使这些 AI 系统不仅智能，而且稳定、可靠，从而增强人们对其部署与表现的信心。整合全面的监控与诊断工具，还能强化智能体快速识别与处理问题、预防潜在中断、并在变化条件下更顺畅运行的能力。这些先进系统对于维持 AI 运作的完整性与效率至关重要，并巩固其驾驭复杂性与不确定性的能力。

This pattern may sometimes be used with reflection. For example, if an initial attempt fails and raises an exception, a reflective process can analyze the failure and reattempt the task with a refined approach, such as an improved prompt, to resolve the error.

> 该模式有时可与反思结合使用。例如，若初次尝试失败并抛出异常，反思过程可以分析失败原因，并以改进后的方式（如优化后的提示）重新尝试任务，以消除错误。

## Exception Handling and Recovery Pattern Overview

The Exception Handling and Recovery pattern addresses the need for AI agents to manage operational failures. This pattern involves anticipating potential issues, such as tool errors or service unavailability, and developing strategies to mitigate them. These strategies may include error logging, retries, fallbacks, graceful degradation, and notifications. Additionally, the pattern emphasizes recovery mechanisms like state rollback, diagnosis, self-correction, and escalation, to restore agents to stable operation. Implementing this pattern enhances the reliability and robustness of AI agents, allowing them to function in unpredictable environments. Examples of practical applications include chatbots managing database errors, trading bots handling financial errors, and smart home agents addressing device malfunctions. The pattern ensures that agents can continue to operate effectively despite encountering complexities and failures.

> 「异常处理与恢复」模式回应的是：AI 智能体需要管理运行故障。该模式包含预见潜在问题（如工具错误或服务不可用），并制定缓解策略。这些策略可包括错误日志、重试、回退、优雅降级与通知。此外，该模式强调恢复机制，如状态回滚、诊断、自我纠正与升级，以使智能体恢复稳定运行。落实该模式可提升 AI 智能体的可靠性与鲁棒性，使其能在不可预测环境中工作。实际应用包括：聊天机器人处理数据库错误、交易机器人处理金融错误、智能家居智能体处理设备故障等。该模式确保智能体在遭遇复杂性与故障时仍能持续有效运行。

Key Components of Exception Handling and Recovery for AI agents

> AI 智能体异常处理与恢复的关键组成部分

Fig.1: Key components of exception handling and recovery for AI agents

> 图 1：AI 智能体异常处理与恢复的关键组成部分

**Error Detection:** This involves meticulously identifying operational issues as they arise. This could manifest as invalid or malformed tool outputs, specific API errors such as 404 (Not Found) or 500 (Internal Server Error) codes, unusually long response times from services or APIs, or incoherent and nonsensical responses that deviate from expected formats. Additionally, monitoring by other agents or specialized monitoring systems might be implemented for more proactive anomaly detection, enabling the system to catch potential issues before they escalate.

> **错误检测：** 指在问题出现时细致识别运行异常。可能表现为无效或格式错误的工具输出、特定 API 错误（如 404「未找到」或 500「内部服务器错误」）、服务或 API 响应时间异常偏长，或与预期格式不符的混乱、无意义回复。此外，还可由其他智能体或专用监控系统进行监测，以更主动地发现异常，从而在问题恶化前将其捕获。

**Error Handling**: Once an error is detected, a carefully thought-out response plan is essential. This includes recording error details meticulously in logs for later debugging and analysis (logging). Retrying the action or request, sometimes with slightly adjusted parameters, may be a viable strategy, especially for transient errors (retries). Utilizing alternative strategies or methods (fallbacks) can ensure that some functionality is maintained. Where complete recovery is not immediately possible, the agent can maintain partial functionality to provide at least some value (graceful degradation). Finally, alerting human operators or other agents might be crucial for situations that require human intervention or collaboration (notification).

> **错误处理：** 一旦检测到错误，必须有周密应对方案。包括将错误详情详尽记入日志以供后续调试与分析（日志记录）。对操作或请求进行重试，有时配合微调参数，对瞬时错误尤为可行（重试）。采用替代策略或方法（回退）可维持部分能力。若无法立即完全恢复，智能体可保留部分功能以至少提供一定价值（优雅降级）。最后，在需要人工介入或协作的情形下，向人类操作员或其他智能体发出告警可能至关重要（通知）。

**Recovery:** This stage is about restoring the agent or system to a stable and operational state after an error. It could involve reversing recent changes or transactions to undo the effects of the error (state rollback). A thorough investigation into the cause of the error is vital for preventing recurrence. Adjusting the agent's plan, logic, or parameters through a self-correction mechanism or replanning process may be needed to avoid the same error in the future. In complex or severe cases, delegating the issue to a human operator or a higher-level system (escalation) might be the best course of action.

> **恢复：** 该阶段旨在错误之后将智能体或系统恢复到稳定、可运行状态。可能包括撤销近期变更或事务以抵消错误影响（状态回滚）。深入调查错误原因对防止复发至关重要。可能需通过自我纠正机制或重新规划流程来调整智能体的计划、逻辑或参数，以避免重蹈覆辙。在复杂或严重情况下，将问题交由人类操作员或更高级系统处理（升级）可能是最佳选择。

Implementation of this robust exception handling and recovery pattern can transform AI agents from fragile and unreliable systems into robust, dependable components capable of operating effectively and resiliently in challenging and highly unpredictable environments. This ensures that the agents maintain functionality, minimize downtime, and provide a seamless and reliable experience even when faced with unexpected issues.

> 落实这一稳健的异常处理与恢复模式，可将 AI 智能体从脆弱、不可靠的系统转变为能够在充满挑战、高度不可预测的环境中有效、有弹性地运行的可靠组件。这有助于智能体保持功能、缩短停机时间，并在遭遇意外问题时仍提供流畅、可靠的体验。

## Practical Applications & Use Cases

Exception Handling and Recovery is critical for any agent deployed in a real-world scenario where perfect conditions cannot be guaranteed.

> 对任何部署于无法保证理想条件的真实场景中的智能体而言，异常处理与恢复都至关重要。

- **Customer Service Chatbots:** If a chatbot tries to access a customer database and the database is temporarily down, it shouldn't crash. Instead, it should detect the API error, inform the user about the temporary issue, perhaps suggest trying again later, or escalate the query to a human agent.  
- **Automated Financial Trading:** A trading bot attempting to execute a trade might encounter an "insufficient funds" error or a "market closed" error. It needs to handle these exceptions by logging the error, not repeatedly trying the same invalid trade, and potentially notifying the user or adjusting its strategy.  
- **Smart Home Automation:** An agent controlling smart lights might fail to turn on a light due to a network issue or a device malfunction. It should detect this failure, perhaps retry, and if still unsuccessful, notify the user that the light could not be turned on and suggest manual intervention.  
- **Data Processing Agents:** An agent tasked with processing a batch of documents might encounter a corrupted file. It should skip the corrupted file, log the error, continue processing other files, and report the skipped files at the end rather than halting the entire process.  
- **Web Scraping Agents:** When a web scraping agent encounters a CAPTCHA, a changed website structure, or a server error (e.g., 404 Not Found, 503 Service Unavailable), it needs to handle these gracefully. This could involve pausing, using a proxy, or reporting the specific URL that failed.  
- **Robotics and Manufacturing:** A robotic arm performing an assembly task might fail to pick up a component due to misalignment. It needs to detect this failure (e.g., via sensor feedback), attempt to readjust, retry the pickup, and if persistent, alert a human operator or switch to a different component.

> - **客服聊天机器人：** 若聊天机器人访问客户数据库时数据库暂时不可用，不应崩溃；而应检测 API 错误，告知用户暂时性问题，可建议稍后再试，或将查询升级给人工坐席。  
> - **自动化金融交易：** 执行交易的交易机器人可能遇到「资金不足」或「市场已闭市」等错误；需通过记录错误、避免对同一无效交易反复重试、并可能通知用户或调整策略来处理这些异常。  
> - **智能家居自动化：** 控制智能灯的智能体可能因网络或设备故障无法开灯；应检测失败，可重试；若仍失败，应通知用户无法开灯并建议人工处理。  
> - **数据处理智能体：** 批量处理文档时可能遇到损坏文件；应跳过该文件、记录错误、继续处理其余文件，并在最后报告被跳过的文件，而非中止整个流程。  
> - **网页抓取智能体：** 遇到验证码、网站结构变更或服务器错误（如 404、503）时，应妥善处理：可暂停、使用代理，或报告失败的具体 URL。  
> - **机器人与制造：** 机械臂因对位失败可能无法拾取零件；需检测失败（如通过传感器反馈）、尝试重新对位并重试拾取；若持续失败，应告警人工操作员或改用其他零件。

In short, this pattern is fundamental for building agents that are not only intelligent but also reliable, resilient, and user-friendly in the face of real-world complexities.

> 简言之，该模式是构建不仅智能，而且在真实世界复杂性面前仍可靠、有韧性且易用的智能体的基础。

## Hands-On Code Example (ADK)

Exception handling and recovery are vital for system robustness and reliability. Consider, for instance, an agent's response to a failed tool call. Such failures can stem from incorrect tool input or issues with an external service that the tool depends on.

> 异常处理与恢复对系统鲁棒性与可靠性至关重要。例如，考虑智能体在工具调用失败时的应对：失败可能源于工具输入错误，或工具所依赖的外部服务出现问题。

```python
from google.adk.agents import Agent, SequentialAgent


# Agent 1: Tries the primary tool. Its focus is narrow and clear.
primary_handler = Agent(
    name="primary_handler",
    model="gemini-2.0-flash-exp",
    instruction="""
    Your job is to get precise location information. Use the get_precise_location_info
    tool with the user's provided address.
    """,
    tools=[get_precise_location_info],
)

# Agent 2: Acts as the fallback handler, checking state to decide its action.
fallback_handler = Agent(
    name="fallback_handler",
    model="gemini-2.0-flash-exp",
    instruction="""
    Check if the primary location lookup failed by looking at state["primary_location_failed"].
    - If it is True, extract the city from the user's original query and use the get_general_area_info tool.
    - If it is False, do nothing.
    """,
    tools=[get_general_area_info],
)

# Agent 3: Presents the final result from the state.
response_agent = Agent(
    name="response_agent",
    model="gemini-2.0-flash-exp",
    instruction="""
    Review the location information stored in state["location_result"]. Present this information
    clearly and concisely to the user. If state["location_result"] does not exist or is empty,
    apologize that you could not retrieve the location.
    """,
    tools=[],  # This agent only reasons over the final state.
)

# The SequentialAgent ensures the handlers run in a guaranteed order.
robust_location_agent = SequentialAgent(
    name="robust_location_agent",
    sub_agents=[primary_handler, fallback_handler, response_agent],
)
```

This code defines a robust location retrieval system using a ADK's SequentialAgent with three sub-agents. The `primary_handler` is the first agent, attempting to get precise location information using the `get_precise_location_info` tool. The `fallback_handler` acts as a backup, checking if the primary lookup failed by inspecting a state variable. If the primary lookup failed, the fallback agent extracts the city from the user's query and uses the `get_general_area_info` tool. The `response_agent` is the final agent in the sequence. It reviews the location information stored in the state. This agent is designed to present the final result to the user. If no location information was found, it apologizes. The SequentialAgent ensures that these three agents execute in a predefined order. This structure allows for a layered approach to location information retrieval.

> 上述代码使用 ADK 的 `SequentialAgent` 与三个子智能体，定义了一个稳健的位置检索系统。`primary_handler` 作为第一个智能体，尝试用 `get_precise_location_info` 工具获取精确位置信息。`fallback_handler` 作为备份，通过检查状态变量判断主查询是否失败；若失败，则从用户查询中提取城市并使用 `get_general_area_info` 工具。`response_agent` 是序列中的最后一个智能体，负责审阅状态中存储的位置信息并向用户呈现最终结果；若未找到位置信息则致歉。`SequentialAgent` 保证三者按预定顺序执行，从而形成分层的地址信息检索方式。

## At a Glance

**What:** AI agents operating in real-world environments inevitably encounter unforeseen situations, errors, and system malfunctions. These disruptions can range from tool failures and network issues to invalid data, threatening the agent's ability to complete its tasks. Without a structured way to manage these problems, agents can be fragile, unreliable, and prone to complete failure when faced with unexpected hurdles. This unreliability makes it difficult to deploy them in critical or complex applications where consistent performance is essential.

> **是什么：** 在真实环境中运行的 AI 智能体不可避免地会遇到意外情况、错误与系统故障。干扰可能来自工具失败、网络问题或无效数据等，威胁智能体完成任务的能力。若没有结构化方式管理这些问题，智能体可能脆弱、不可靠，并在意外障碍面前全盘崩溃。这种不可靠性使其难以部署于需要稳定表现的关键或复杂应用。

**Why**: The Exception Handling and Recovery pattern provides a standardized solution for building robust and resilient AI agents. It equips them with the agentic capability to anticipate, manage, and recover from operational failures. The pattern involves proactive error detection, such as monitoring tool outputs and API responses, and reactive handling strategies like logging for diagnostics, retrying transient failures, or using fallback mechanisms. For more severe issues, it defines recovery protocols, including reverting to a stable state, self-correction by adjusting its plan, or escalating the problem to a human operator. This systematic approach ensures agents can maintain operational integrity, learn from failures, and function dependably in unpredictable settings.

> **为什么：** 「异常处理与恢复」模式为构建鲁棒、有韧性的 AI 智能体提供了标准化方案，赋予其预见、管理与从运行故障中恢复的智能体能力。该模式包含主动错误检测（如监测工具输出与 API 响应），以及被动处理策略（如诊断日志、对瞬时失败重试或使用回退机制）。对更严重问题，还定义恢复规程：回到稳定状态、通过调整计划自我纠正，或将问题升级给人类操作员。这一系统化路径有助于智能体维持运行完整性、从失败中学习，并在不可预测环境中可靠运作。

**Rule of Thumb:** Use this pattern for any AI agent deployed in a dynamic, real-world environment where system failures, tool errors, network issues, or unpredictable inputs are possible and operational reliability is a key requirement.

> **经验法则：** 当 AI 智能体部署于动态、真实环境，且可能出现系统故障、工具错误、网络问题或不可预测输入，而运行可靠性是关键要求时，应采用该模式。

**Visual Summary:**

> **可视化摘要：**

Exception Handling Pattern

> 异常处理模式

Fig.2: Exception handling pattern

> 图 2：异常处理模式

## Key Takeaways

Essential points to remember:

> 需要记住的要点：

- Exception Handling and Recovery is essential for building robust and reliable Agents.  
- This pattern involves detecting errors, handling them gracefully, and implementing strategies to recover.  
- Error detection can involve validating tool outputs, checking API error codes, and using timeouts.  
- Handling strategies include logging, retries, fallbacks, graceful degradation, and notifications.  
- Recovery focuses on restoring stable operation through diagnosis, self-correction, or escalation.  
- This pattern ensures agents can operate effectively even in unpredictable real-world environments.

> - 异常处理与恢复对于构建鲁棒、可靠的智能体必不可少。  
> - 该模式包括检测错误、妥善处理并实施恢复策略。  
> - 错误检测可包括校验工具输出、检查 API 错误码与使用超时。  
> - 处理策略包括日志、重试、回退、优雅降级与通知。  
> - 恢复侧重于通过诊断、自我纠正或升级恢复稳定运行。  
> - 该模式确保智能体即便在不可预测的真实环境中也能有效工作。

## Conclusion

This chapter explores the Exception Handling and Recovery pattern, which is essential for developing robust and dependable AI agents. This pattern addresses how AI agents can identify and manage unexpected issues, implement appropriate responses, and recover to a stable operational state. The chapter discusses various aspects of this pattern, including the detection of errors, the handling of these errors through mechanisms such as logging, retries, and fallbacks, and the strategies used to restore the agent or system to proper function. Practical applications of the Exception Handling and Recovery pattern are illustrated across several domains to demonstrate its relevance in handling real-world complexities and potential failures. These applications show how equipping AI agents with exception handling capabilities contributes to their reliability and adaptability in dynamic environments.

> 本章探讨「异常处理与恢复」模式，该模式对开发鲁棒、可依赖的 AI 智能体至关重要。本章说明智能体如何识别与管理意外问题、采取适当响应并恢复到稳定运行状态；涵盖错误检测、通过日志、重试与回退等机制处理错误，以及将智能体或系统恢复至正常功能的策略。文中在多个领域举例说明该模式在处理真实世界复杂性与潜在故障方面的相关性，展示为智能体配备异常处理能力如何提升其在动态环境中的可靠性与适应性。

## References

> 参考文献：以下条目保留英文与原始链接，不作逐条翻译。

1. McConnell, S. (2004). *Code Complete (2nd ed.)*. Microsoft Press.
2. Shi, Y., Pei, H., Feng, L., Zhang, Y., & Yao, D. (2024). *Towards Fault Tolerance in Multi-Agent Reinforcement Learning*. arXiv preprint arXiv:2412.00534.
3. O'Neill, V. (2022). *Improving Fault Tolerance and Reliability of Heterogeneous Multi-Agent IoT Systems Using Intelligence Transfer*. Electronics, 11(17), 2724.
