# Chapter 13: Human-in-the-Loop

The Human-in-the-Loop (HITL) pattern represents a pivotal strategy in the development and deployment of Agents. It deliberately interweaves the unique strengths of human cognition—such as judgment, creativity, and nuanced understanding—with the computational power and efficiency of AI. This strategic integration is not merely an option but often a necessity, especially as AI systems become increasingly embedded in critical decision-making processes.

> 「人在回路中」（Human-in-the-Loop，HITL）模式是智能体开发与部署中的关键策略。它有意将人类认知的独特优势——如判断、创造力与细致理解——与 AI 的计算能力与效率交织在一起。这种战略整合往往不仅是可选项，更是必需，尤其当 AI 系统越来越多地嵌入关键决策流程时。

The core principle of HITL is to ensure that AI operates within ethical boundaries, adheres to safety protocols, and achieves its objectives with optimal effectiveness. These concerns are particularly acute in domains characterized by complexity, ambiguity, or significant risk, where the implications of AI errors or misinterpretations can be substantial. In such scenarios, full autonomy—where AI systems function independently without any human intervention—may prove to be imprudent. HITL acknowledges this reality and emphasizes that even with rapidly advancing AI technologies, human oversight, strategic input, and collaborative interactions remain indispensable.

> HITL 的核心原则是确保 AI 在伦理边界内运行、遵守安全协议，并以最优效果达成目标。在复杂、模糊或高风险领域，AI 错误或误解的后果可能严重，这些关切尤为尖锐。在此类情境下，完全自主（AI 在无任何人工干预下独立运作）可能并不明智。HITL 承认这一现实，并强调：即便 AI 技术飞速进步，人类监督、战略投入与协作互动仍不可或缺。

The HITL approach fundamentally revolves around the idea of synergy between artificial and human intelligence. Rather than viewing AI as a replacement for human workers, HITL positions AI as a tool that augments and enhances human capabilities. This augmentation can take various forms, from automating routine tasks to providing data-driven insights that inform human decisions. The end goal is to create a collaborative ecosystem where both humans and AI Agents can leverage their distinct strengths to achieve outcomes that neither could accomplish alone.

> HITL 方法从根本上围绕人机智能协同的理念。它不是把 AI 视为替代人力，而是将 AI 定位为增强与扩展人类能力的工具。这种增强形式多样：从自动化例行任务，到提供数据驱动的洞见以支撑人类决策。最终目标是构建协作生态，使人类与 AI 智能体各自发挥所长，达成单方无法单独完成的结果。

In practice, HITL can be implemented in diverse ways. One common approach involves humans acting as validators or reviewers, examining AI outputs to ensure accuracy and identify potential errors. Another implementation involves humans actively guiding AI behavior, providing feedback or making corrections in real-time. In more complex setups, humans may collaborate with AI as partners, jointly solving problems or making decisions through interactive dialog or shared interfaces. Regardless of the specific implementation, the HITL pattern underscores the importance of maintaining human control and oversight, ensuring that AI systems remain aligned with human ethics, values, goals, and societal expectations.

> 在实践中，HITL 可有多种落地方式。常见做法包括人类作为校验者或审核者检查 AI 输出以确保准确并发现潜在错误；或由人类主动引导 AI 行为，实时提供反馈或纠正。在更复杂的设置中，人类可与 AI 作为伙伴协作，通过交互式对话或共享界面共同解决问题或做决策。无论具体形式如何，HITL 模式都强调保持人类控制与监督的重要性，使 AI 系统与人类伦理、价值观、目标及社会期望保持一致。

## Human-in-the-Loop Pattern Overview

The Human-in-the-Loop (HITL) pattern integrates artificial intelligence with human input to enhance Agent capabilities. This approach acknowledges that optimal AI performance frequently requires a combination of automated processing and human insight, especially in scenarios with high complexity or ethical considerations. Rather than replacing human input, HITL aims to augment human abilities by ensuring that critical judgments and decisions are informed by human understanding.

> HITL 模式将人工智能与人类输入结合，以增强智能体能力。它承认：最佳 AI 表现常常需要自动化处理与人类洞见相结合，尤其在高度复杂或涉及伦理的情境中。HITL 并非取代人类输入，而是通过确保关键判断与决策有人类理解参与，来增强人类能力。

HITL encompasses several key aspects: Human Oversight, which involves monitoring AI agent performance and output (e.g., via log reviews or real-time dashboards) to ensure adherence to guidelines and prevent undesirable outcomes. Intervention and Correction occurs when an AI agent encounters errors or ambiguous scenarios and may request human intervention; human operators can rectify errors, supply missing data, or guide the agent, which also informs future agent improvements. Human Feedback for Learning is collected and used to refine AI models, prominently in methodologies like reinforcement learning with human feedback, where human preferences directly influence the agent's learning trajectory. Decision Augmentation is where an AI agent provides analyses and recommendations to a human, who then makes the final decision, enhancing human decision-making through AI-generated insights rather than full autonomy. Human-Agent Collaboration is a cooperative interaction where humans and AI agents contribute their respective strengths; routine data processing may be handled by the agent, while creative problem-solving or complex negotiations are managed by the human. Finally, Escalation Policies are established protocols that dictate when and how an agent should escalate tasks to human operators, preventing errors in situations beyond the agent's capability.

> HITL 涵盖若干关键方面：**人类监督**，即监测智能体表现与输出（如通过日志审查或实时仪表板），以确保符合规范并防止不良结果。**干预与纠正**发生在智能体遇到错误或模糊情形并可能请求人工介入时；人类操作员可纠正错误、补充缺失数据或引导智能体，这也会促进智能体后续改进。**用于学习的人类反馈**被收集并用于改进 AI 模型，在「人类反馈强化学习」等方法中尤为突出，人类偏好直接影响智能体的学习轨迹。**决策增强**指智能体向人类提供分析与建议，由人类做最终决定，通过 AI 洞见增强人类决策而非完全自主。**人机协作**是人与智能体各展所长的合作互动：例行数据处理可由智能体承担，创造性问题解决或复杂谈判则由人类主导。最后，**升级策略**是规定智能体何时、如何将任务升级给人类操作员的既定规程，以防在超出智能体能力的情境中出错。

Implementing HITL patterns enables the use of Agents in sensitive sectors where full autonomy is not feasible or permitted. It also provides a mechanism for ongoing improvement through feedback loops. For example, in finance, the final approval of a large corporate loan requires a human loan officer to assess qualitative factors like leadership character. Similarly, in the legal field, core principles of justice and accountability demand that a human judge retain final authority over critical decisions like sentencing, which involve complex moral reasoning.

> 落实 HITL 模式使智能体可用于完全自主不可行或不被允许的敏感行业，并通过反馈闭环提供持续改进机制。例如在金融领域，大额企业贷款的最终批准需要人类信贷员评估领导力品格等定性因素。在法律领域，正义与问责的核心原则要求人类法官对量刑等涉及复杂道德推理的关键决定保留最终权威。

**Caveats:** Despite its benefits, the HITL pattern has significant caveats, chief among them being a lack of scalability. While human oversight provides high accuracy, operators cannot manage millions of tasks, creating a fundamental trade-off that often requires a hybrid approach combining automation for scale and HITL for accuracy. Furthermore, the effectiveness of this pattern is heavily dependent on the expertise of the human operators; for example, while an AI can generate software code, only a skilled developer can accurately identify subtle errors and provide the correct guidance to fix them. This need for expertise also applies when using HITL to generate training data, as human annotators may require special training to learn how to correct an AI in a way that produces high-quality data. Lastly, implementing HITL raises significant privacy concerns, as sensitive information must often be rigorously anonymized before it can be exposed to a human operator, adding another layer of process complexity.

> **注意：** 尽管有益处，HITL 模式也有明显局限，最主要的是缺乏可扩展性：人类监督虽能带来高准确率，操作员却无法处理数以百万计的任务，由此形成根本权衡，往往需要「自动化扩规模 + HITL 保精度」的混合方案。此外，该模式成效高度依赖人类操作员的专业度；例如 AI 能生成代码，但只有熟练开发者才能准确识别细微错误并给出正确修复指导。用 HITL 生成训练数据时同样需要专业能力，标注人员可能需要专门培训，以学会如何纠正 AI 才能产出高质量数据。最后，落实 HITL 会带来显著的隐私关切：敏感信息在暴露给人类操作员前往往必须严格匿名化，从而增加流程复杂度。

## Practical Applications & Use Cases

The Human-in-the-Loop pattern is vital across a wide range of industries and applications, particularly where accuracy, safety, ethics, or nuanced understanding are paramount.

> HITL 模式在广泛行业与应用中至关重要，尤其在准确性、安全、伦理或细致理解至上的场景。

* **Content Moderation:** AI agents can rapidly filter vast amounts of online content for violations (e.g., hate speech, spam). However, ambiguous cases or borderline content are escalated to human moderators for review and final decision, ensuring nuanced judgment and adherence to complex policies.  
* **Autonomous Driving:** While self-driving cars handle most driving tasks autonomously, they are designed to hand over control to a human driver in complex, unpredictable, or dangerous situations that the AI cannot confidently navigate (e.g., extreme weather, unusual road conditions).  
* **Financial Fraud Detection:** AI systems can flag suspicious transactions based on patterns. However, high-risk or ambiguous alerts are often sent to human analysts who investigate further, contact customers, and make the final determination on whether a transaction is fraudulent.  
* **Legal Document Review:** AI can quickly scan and categorize thousands of legal documents to identify relevant clauses or evidence. Human legal professionals then review the AI's findings for accuracy, context, and legal implications, especially for critical cases.  
* **Customer Support (Complex Queries):** A chatbot might handle routine customer inquiries. If the user's problem is too complex, emotionally charged, or requires empathy that the AI cannot provide, the conversation is seamlessly handed over to a human support agent.  
* **Data Labeling and Annotation:** AI models often require large datasets of labeled data for training. Humans are put in the loop to accurately label images, text, or audio, providing the ground truth that the AI learns from. This is a continuous process as models evolve.  
* **Generative AI Refinement:** When an LLM generates creative content (e.g., marketing copy, design ideas), human editors or designers review and refine the output, ensuring it meets brand guidelines, resonates with the target audience, and maintains quality.  
* **Autonomous Networks:** AI systems are capable of analyzing alerts and forecasting network issues and traffic anomalies by leveraging key performance indicators (KPIs) and identified patterns. Nevertheless, crucial decisions—such as addressing high-risk alerts—are frequently escalated to human analysts. These analysts conduct further investigation and make the ultimate determination regarding the approval of network changes.

> * **内容审核：** AI 智能体可快速筛除大量违规在线内容（如仇恨言论、垃圾信息）；但模糊或边界案例会升级给人类审核员做终审，以保证细致判断并符合复杂政策。  
> * **自动驾驶：** 自动驾驶车辆虽能自主处理大部分驾驶任务，但在 AI 无法有把握应对的复杂、不可预测或危险情境（如极端天气、异常路况）下，设计上会将控制权交还人类驾驶员。  
> * **金融欺诈检测：** AI 可基于模式标记可疑交易；但高风险或模糊告警常交人类分析师进一步调查、联系客户，并对是否欺诈做最终决定。  
> * **法律文档审查：** AI 可快速扫描、归类大量法律文件以定位相关条款或证据；人类法律专业人士再审核 AI 结论的准确性、语境与法律影响，尤其在关键案件中。  
> * **客户支持（复杂咨询）：** 聊天机器人可处理常规咨询；若用户问题过于复杂、情绪激烈或需要 AI 难以提供的共情，对话会无缝转交人类客服。  
> * **数据标注：** 训练 AI 常需大量标注数据；人类进入回路以准确标注图像、文本或音频，提供 AI 学习的 ground truth；随模型演进这一过程持续进行。  
> * **生成式 AI 润色：** 当 LLM 生成创意内容（如营销文案、设计构思）时，人类编辑或设计师审核并打磨输出，确保符合品牌规范、契合受众并保持质量。  
> * **自治网络：** AI 可利用 KPI 与已识别模式分析告警、预测网络问题与流量异常；尽管如此，关键决策——如处理高风险告警——仍常升级给人类分析师；由他们进一步调查并对是否批准网络变更做最终决定。

This pattern exemplifies a practical method for AI implementation. It harnesses AI for enhanced scalability and efficiency, while maintaining human oversight to ensure quality, safety, and ethical compliance.

> 该模式体现了 AI 落地的一种务实方法：利用 AI 提升规模与效率，同时保留人类监督以确保质量、安全与伦理合规。

"Human-on-the-loop" is a variation of this pattern where human experts define the overarching policy, and the AI then handles immediate actions to ensure compliance. Let's consider two examples:

> 「人在回路上方」（human-on-the-loop）是该模式的一种变体：人类专家定义总体策略，AI 再执行即时动作以确保合规。下面看两个例子：

* **Automated financial trading system**: In this scenario, a human financial expert sets the overarching investment strategy and rules. For instance, the human might define the policy as: "Maintain a portfolio of 70% tech stocks and 30% bonds, do not invest more than 5% in any single company, and automatically sell any stock that falls 10% below its purchase price." The AI then monitors the stock market in real-time, executing trades instantly when these predefined conditions are met. The AI is handling the immediate, high-speed actions based on the slower, more strategic policy set by the human operator.  
* **Modern call center**:  In this setup, a human manager establishes high-level policies for customer interactions. For instance, the manager might set rules such as "any call mentioning 'service outage' should be immediately routed to a technical support specialist," or "if a customer's tone of voice indicates high frustration, the system should offer to connect them directly to a human agent." The AI system then handles the initial customer interactions, listening to and interpreting their needs in real-time. It autonomously executes the manager's policies by instantly routing the calls or offering escalations without needing human intervention for each individual case. This allows the AI to manage the high volume of immediate actions according to the slower, strategic guidance provided by the human operator.

> * **自动化金融交易系统：** 人类金融专家设定总体投资策略与规则。例如策略可为：「组合保持 70% 科技股与 30% 债券；单一公司持仓不超过 5%；任何股票跌破买入价 10% 即自动卖出。」AI 实时监控股市，在满足预设条件时即时执行交易；AI 依据人类操作员较慢、更具战略性的策略设定来处理即时、高速的动作。  
> * **现代呼叫中心：** 人类管理者为客户互动制定高层策略。例如规则可为：「任何提到『服务中断』的来电立即转技术专家」，或「若客户语气显示高度沮丧，系统应提供直接转人工的选项。」AI 系统处理初始客户互动，实时倾听并理解需求；按管理者策略自动即时路由或提供升级，无需对每一通电话都人工介入；从而使 AI 能按人类操作员较慢的战略指引，管理大量即时动作。

## Hands-On Code Example

To demonstrate the Human-in-the-Loop pattern, an ADK agent can identify scenarios requiring human review and initiate an escalation process . This allows for human intervention in situations where the agent's autonomous decision-making capabilities are limited or when complex judgments are required. This is not an isolated feature; other popular frameworks have adopted similar capabilities. LangChain, for instance, also provides tools to implement these types of interactions.

> 为演示 HITL 模式，ADK 智能体可识别需要人工复核的情形并启动升级流程，从而在智能体自主决策能力有限或需要复杂判断时允许人工介入。这并非孤立能力；其他主流框架也有类似能力，例如 LangChain 也提供工具实现此类交互。

```python
from typing import Optional

from google.adk.agents import Agent
from google.adk.tools.tool_context import ToolContext
from google.adk.callbacks import CallbackContext
from google.adk.models.llm import LlmRequest
from google.genai import types


# Placeholder for tools (replace with actual implementations if needed)
def troubleshoot_issue(issue: str) -> dict:
    return {"status": "success", "report": f"Troubleshooting steps for {issue}."}


def create_ticket(issue_type: str, details: str) -> dict:
    return {"status": "success", "ticket_id": "TICKET123"}


def escalate_to_human(issue_type: str) -> dict:
    # This would typically transfer to a human queue in a real system
    return {"status": "success", "message": f"Escalated {issue_type} to a human specialist."}


technical_support_agent = Agent(
    name="technical_support_specialist",
    model="gemini-2.0-flash-exp",
    instruction="""
    You are a technical support specialist for our electronics company.
    FIRST, check if the user has a support history in state["customer_info"]["support_history"].
    If they do, reference this history in your responses.

    For technical issues:
    1. Use the troubleshoot_issue tool to analyze the problem.
    2. Guide the user through basic troubleshooting steps.
    3. If the issue persists, use create_ticket to log the issue.

    For complex issues beyond basic troubleshooting:
    1. Use escalate_to_human to transfer to a human specialist.

    Maintain a professional but empathetic tone. Acknowledge the frustration technical issues can cause,
    while providing clear steps toward resolution.
    """,
    tools=[troubleshoot_issue, create_ticket, escalate_to_human],
)


def personalization_callback(
    callback_context: CallbackContext, llm_request: LlmRequest
) -> Optional[LlmRequest]:
    """Adds personalization information to the LLM request."""
    # Get customer info from state
    customer_info = callback_context.state.get("customer_info")
    if customer_info:
        customer_name = customer_info.get("name", "valued customer")
        customer_tier = customer_info.get("tier", "standard")
        recent_purchases = customer_info.get("recent_purchases", [])

        personalization_note = (
            f"\nIMPORTANT PERSONALIZATION:\n"
            f"Customer Name: {customer_name}\n"
            f"Customer Tier: {customer_tier}\n"
        )
        if recent_purchases:
            personalization_note += f"Recent Purchases: {', '.join(recent_purchases)}\n"

        if llm_request.contents:
            # Add as a system message before the first content
            system_content = types.Content(
                role="system",
                parts=[types.Part(text=personalization_note)],
            )
            llm_request.contents.insert(0, system_content)

    return None  # Return None to continue with the modified request
```

This code offers a blueprint for creating a technical support agent using Google's ADK, designed around a HITL framework. The agent acts as an intelligent first line of support, configured with specific instructions and equipped with tools like `troubleshoot_issue`, `create_ticket`, and `escalate_to_human` to manage a complete support workflow. The escalation tool is a core part of the HITL design, ensuring complex or sensitive cases are passed to human specialists.

> 该代码提供了使用 Google ADK 构建技术支持智能体的蓝图，围绕 HITL 框架设计。智能体作为智能一线支持，配有明确指令以及 `troubleshoot_issue`、`create_ticket`、`escalate_to_human` 等工具以管理完整支持工作流。升级工具是 HITL 设计的核心，确保复杂或敏感案例交给人类专家。

A key feature of this architecture is its capacity for deep personalization, achieved through a dedicated callback function. Before contacting the LLM, this function dynamically retrieves customer-specific data—such as their name, tier, and purchase history—from the agent's state. This context is then injected into the prompt as a system message, enabling the agent to provide highly tailored and informed responses that reference the user's history. By combining a structured workflow with essential human oversight and dynamic personalization, this code serves as a practical example of how the ADK facilitates the development of sophisticated and robust AI support solutions.

> 该架构的一大特点是可通过专用回调实现深度个性化：在调用 LLM 之前，函数从智能体状态中动态读取客户专属数据（如姓名、等级、购买历史），再以系统消息形式注入提示，使智能体能提供高度贴合且能引用用户历史的回应。将结构化工作流、必要的人类监督与动态个性化相结合，展示了 ADK 如何助力构建精密、稳健的 AI 支持方案。

## At Glance

**What:** AI systems, including advanced LLMs, often struggle with tasks that require nuanced judgment, ethical reasoning, or a deep understanding of complex, ambiguous contexts. Deploying fully autonomous AI in high-stakes environments carries significant risks, as errors can lead to severe safety, financial, or ethical consequences. These systems lack the inherent creativity and common-sense reasoning that humans possess. Consequently, relying solely on automation in critical decision-making processes is often imprudent and can undermine the system's overall effectiveness and trustworthiness.

> **是什么：** 包括先进 LLM 在内的 AI 系统，常在需要细致判断、伦理推理或对复杂模糊语境深入理解的任务上吃力。在高风险环境中部署完全自主的 AI 风险显著，错误可能导致严重安全、财务或伦理后果。这些系统缺乏人类固有的创造力与常识推理。因此，在关键决策流程中仅依赖自动化往往不明智，并可能损害系统整体效能与可信度。

**Why:** The Human-in-the-Loop (HITL) pattern provides a standardized solution by strategically integrating human oversight into AI workflows. This agentic approach creates a symbiotic partnership where AI handles computational heavy-lifting and data processing, while humans provide critical validation, feedback, and intervention. By doing so, HITL ensures that AI actions align with human values and safety protocols. This collaborative framework not only mitigates the risks of full automation but also enhances the system's capabilities through continuous learning from human input. Ultimately, this leads to more robust, accurate, and ethical outcomes that neither human nor AI could achieve alone.

> **为什么：** HITL 模式通过将人类监督战略性地嵌入 AI 工作流，提供标准化方案。这种智能体化路径形成共生伙伴关系：AI 承担计算密集型与数据处理任务，人类提供关键校验、反馈与干预。由此 HITL 确保 AI 行为与人类价值观及安全规程一致。该协作框架不仅缓解完全自动化的风险，还通过持续向人类学习增强系统能力，最终带来更鲁棒、准确且符合伦理的结果，这是人或 AI 单独难以达成的。

**Rule of Thumb:** Use this pattern when deploying AI in domains where errors have significant safety, ethical, or financial consequences, such as in healthcare, finance, or autonomous systems. It is essential for tasks involving ambiguity and nuance that LLMs cannot reliably handle, like content moderation or complex customer support escalations. Employ HITL when the goal is to continuously improve an AI model with high-quality, human-labeled data or to refine generative AI outputs to meet specific quality standards.

> **经验法则：** 当在错误可能带来重大安全、伦理或财务后果的领域部署 AI（如医疗、金融或自主系统）时使用该模式。对 LLM 难以可靠处理的模糊与细微任务（如内容审核或复杂客服升级）尤为必要。若以高质量人工标注数据持续改进模型，或要将生成式 AI 输出打磨到特定质量标准，应采用 HITL。

**Visual Summary:**

> **可视化摘要：**

![Human in the Loop Design Pattern](../assets-new/Human_in_the_Loop_Design_Pattern.png)

Fig.1: Human in the loop design pattern

> 图 1：人在回路设计模式

## Key Takeaways

Key takeaways include:

> 要点包括：

* Human-in-the-Loop (HITL) integrates human intelligence and judgment into AI workflows.  
* It's crucial for safety, ethics, and effectiveness in complex or high-stakes scenarios.  
* Key aspects include human oversight, intervention, feedback for learning, and decision augmentation.  
* Escalation policies are essential for agents to know when to hand off to a human.  
* HITL allows for responsible AI deployment and continuous improvement.  
* The primary drawbacks of Human-in-the-Loop are its inherent lack of scalability, creating a trade-off between accuracy and volume, and its dependence on highly skilled domain experts for effective intervention.
* Its implementation presents operational challenges, including the need to train human operators for data generation and to address privacy concerns by anonymizing sensitive information.

> * HITL 将人类智能与判断融入 AI 工作流。  
> * 在复杂或高风险场景中，它对安全、伦理与有效性至关重要。  
> * 关键方面包括人类监督、干预、用于学习的反馈与决策增强。  
> * 升级策略对智能体知晓何时交棒给人类必不可少。  
> * HITL 支持负责任的 AI 部署与持续改进。  
> * HITL 的主要缺点是固有的可扩展性不足，在准确率与处理量之间形成权衡，且有效干预依赖高技能领域专家。  
> * 其实施还带来运营挑战，包括需培训人类操作员参与数据生成，以及通过匿名化敏感信息应对隐私关切。

## Conclusion

This chapter explored the vital Human-in-the-Loop (HITL) pattern, emphasizing its role in creating robust, safe, and ethical AI systems. We discussed how integrating human oversight, intervention, and feedback into agent workflows can significantly enhance their performance and trustworthiness, especially in complex and sensitive domains. The practical applications demonstrated HITL's widespread utility, from content moderation and medical diagnosis to autonomous driving and customer support. The conceptual code example provided a glimpse into how ADK can facilitate these human-agent interactions through escalation mechanisms. As AI capabilities continue to advance, HITL remains a cornerstone for responsible AI development, ensuring that human values and expertise remain central to intelligent system design.

> 本章探讨至关重要的 HITL 模式，强调其在构建鲁棒、安全且符合伦理的 AI 系统中的作用。我们讨论了将人类监督、干预与反馈嵌入智能体工作流如何显著提升其表现与可信度，尤其在复杂、敏感领域。应用场景展示了 HITL 的广泛用途，从内容审核、医学诊断到自动驾驶与客户支持。概念性代码示例简要说明 ADK 如何通过升级机制促进人机交互。随着 AI 能力持续进步，HITL 仍是负责任 AI 开发的基石，确保人类价值观与专业知识始终是智能系统设计的核心。

## References

> 参考文献：以下条目保留英文与原始链接，不作逐条翻译。

1. A Survey of Human-in-the-loop for Machine Learning, Xingjiao Wu, Luwei Xiao, Yixuan Sun, Junhang Zhang, Tianlong Ma, Liang He, [https://arxiv.org/abs/2108.00941](https://arxiv.org/abs/2108.00941)
