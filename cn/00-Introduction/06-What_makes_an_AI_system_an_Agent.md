# What makes an AI system an Agent?

In simple terms, an **AI agent** is a system designed to perceive its environment and take actions to achieve a specific goal. It's an evolution from a standard Large Language Model (LLM), enhanced with the abilities to plan, use tools, and interact with its surroundings. Think of an Agentic AI as a smart assistant that learns on the job. It follows a simple, five-step loop to get things done (see Fig.1):

> 简而言之，**AI 智能体**是为感知环境并采取行动以达成特定目标而设计的系统。它在标准大语言模型（LLM）之上演进，增加了规划、使用工具与与环境交互的能力。不妨把智能体化 AI 看作边干边学的智能助手；它遵循一个简单的五步循环完成任务（见图 1）：

1. **Get the Mission:** You give it a goal, like "organize my schedule."
2. **Scan the Scene:** It gathers all the necessary information—reading emails, checking calendars, and accessing contacts—to understand what's happening.
3. **Think It Through:** It devises a plan of action by considering the optimal approach to achieve the goal.
4. **Take Action:** It executes the plan by sending invitations, scheduling meetings, and updating your calendar.
5. **Learn and Get Better:** It observes successful outcomes and adapts accordingly. For example, if a meeting is rescheduled, the system learns from this event to enhance its future performance.

> 1. **获取任务：** 你给它一个目标，例如「整理我的日程」。
> 2. **扫描现场：** 收集必要信息——读邮件、查日历、访问联系人——以了解现状。
> 3. **思考对策：** 通过权衡最优路径来制定行动计划。
> 4. **采取行动：** 发送邀请、安排会议、更新日历等执行计划。
> 5. **学习改进：** 观察成功结果并相应调整。例如会议改期，系统从该事件学习以提升日后表现。

![Agentic AI Problem-Solving Process](../assets-new/Agentic_AI_Problem_Solving_Process.png)

Fig.1: Agentic AI functions as an intelligent assistant, continuously learning through experience. It operates via a straightforward five-step loop to accomplish tasks.

> 图 1：智能体化 AI 作为智能助手，通过经验持续学习；经由直接的五步循环完成任务。

Agents are becoming increasingly popular at a stunning pace. According to recent studies, a majority of large IT companies are actively using these agents, and a fifth of them just started within the past year. The financial markets are also taking notice. By the end of 2024, AI agent startups had raised more than $2 billion, and the market was valued at $5.2 billion. It's expected to explode to nearly $200 billion in value by 2034\. In short, all signs point to AI agents playing a massive role in our future economy.

> 智能体正以惊人速度普及。近期研究表明，大多数大型 IT 公司在积极使用智能体，其中约五分之一在过去一年内才起步。金融市场亦在关注：截至 2024 年底，AI 智能体初创公司已融资逾 20 亿美元，市场规模约 52 亿美元；预计到 2034 年将暴增至近 2000 亿美元。简言之，种种迹象表明智能体将在未来经济中扮演重要角色。

In just two years, the AI paradigm has shifted dramatically, moving from simple automation to sophisticated, autonomous systems (see Fig. 2). Initially, workflows relied on basic prompts and triggers to process data with LLMs. This evolved with Retrieval-Augmented Generation (RAG), which enhanced reliability by grounding models on factual information. We then saw the development of individual AI Agents capable of using various tools.  Today, we are entering the era of Agentic AI, where a team of specialized agents works in concert to achieve complex goals, marking a significant leap in AI's collaborative power.

> 短短两年间，AI 范式剧烈转变：从简单自动化走向复杂自主系统（见图 2）。最初工作流依赖基本提示与触发器，用 LLM 处理数据；随后出现检索增强生成（RAG），通过将模型锚定在事实信息上提升可靠性；再发展到能使用多种工具的独立 AI 智能体。今天我们正进入智能体化 AI 时代：多支专业化智能体协同达成复杂目标，标志着 AI 协作能力的显著跃升。

![Transitioning from LLMs to RAG, then to Agentic RAG, and finally to Agentic AI](../assets-new/Transitioning_from_LLMs_to_RAG_to_Agentic_RAG_to_Agentic_AI.png)

Fig 2.: Transitioning from LLMs to RAG, then to Agentic RAG, and finally to Agentic AI.

> 图 2：从 LLM 到 RAG，再到智能体化 RAG，直至智能体化 AI 的演进。

The intent of this book is to discuss the design patterns of how  specialized agents can work in concert and collaborate to achieve  complex goals, and you will see one paradigm of collaboration and interaction in each chapter.

> 本书旨在讨论专业化智能体如何协同合作以达成复杂目标的设计模式；每一章你都会看到一种协作与交互范式。

Before doing that, let's examine examples that span the range of agent complexity (see Fig. 3).

> 在此之前，先看贯穿智能体复杂度谱系的示例（见图 3）。

## Level 0: The Core Reasoning Engine

While an LLM is not an agent in itself, it can serve as the reasoning core of a basic agentic system. In a 'Level 0' configuration, the LLM operates without tools, memory, or environment interaction, responding solely based on its pretrained knowledge. Its strength lies in leveraging its extensive training data to explain established concepts. The trade-off for this powerful internal reasoning is a complete lack of current-event awareness. For instance, it would be unable to name the 2025 Oscar winner for "Best Picture" if that information is outside its pre-trained knowledge.

> LLM 本身不是智能体，但可作为基础智能体化系统的推理核心。在「0 级」配置下，LLM 无工具、无记忆、不与环境交互，仅基于预训练知识回应。其优势在于利用海量训练数据解释既有概念；代价是完全没有对时事的感知——例如若预训练知识未覆盖，它无法说出 2025 年奥斯卡「最佳影片」得主。

## Level 1: The Connected Problem-Solver

At this level, the LLM becomes a functional agent by connecting to and utilizing external tools. Its problem-solving is no longer limited to its pre-trained knowledge. Instead, it can execute a sequence of actions to gather and process information from sources like the internet (via search) or databases (via Retrieval Augmented Generation, or RAG). For detailed information, refer to Chapter 14\.

> 在此层级，LLM 通过连接并使用外部工具成为功能性智能体；解题不再限于预训练知识，而可执行一系列行动，从互联网（搜索）或数据库（检索增强生成，RAG）等来源收集与处理信息。详见第 14 章。

For instance, to find new TV shows, the agent recognizes the need for current information, uses a search tool to find it, and then synthesizes the results. Crucially, it can also use specialized tools for higher accuracy, such as calling a financial API to get the live stock price for AAPL. This ability to interact with the outside world across multiple steps is the core capability of a Level 1 agent.

> 例如寻找新剧时，智能体识别需要最新信息，用搜索工具检索并综合结果。它也能调用专用工具以提高准确度，例如调用金融 API 获取 AAPL 实时股价。跨多步与外部世界交互的能力，是 1 级智能体的核心能力。

## Level 2: The Strategic Problem-Solver

At this level, an agent's capabilities expand significantly, encompassing strategic planning, proactive assistance, and self-improvement, with prompt engineering and context engineering as core enabling skills.

> 在此层级，智能体能力显著扩展，涵盖战略规划、主动协助与自我改进；提示工程与上下文工程是核心使能技能。

First, the agent moves beyond single-tool use to tackle complex, multi-part problems through strategic problem-solving. As it executes a sequence of actions, it actively performs context engineering: the strategic process of selecting, packaging, and managing the most relevant information for each step. For example, to find a coffee shop between two locations, it first uses a mapping tool. It then engineers this output, curating a short, focused context—perhaps just a list of street names—to feed into a local search tool, preventing cognitive overload and ensuring the second step is efficient and accurate. To achieve maximum accuracy from an AI, it must be given a short, focused, and powerful context. Context engineering is the discipline that accomplishes this by strategically selecting, packaging, and managing the most critical information from all available sources. It effectively curates the model's limited attention to prevent overload and ensure high-quality, efficient performance on any given task. For detailed information, refer to the Appendix A\.

> 首先，智能体超越单工具使用，通过战略解题处理复杂多部分问题。执行一系列行动时，它主动进行上下文工程：为每一步选择、打包并管理最相关信息。例如要在两地之间找咖啡馆，先用地图工具，再对输出做工程化处理，整理成短而聚焦的上下文（或许只是一串街名）喂给本地搜索工具，避免认知过载并保证第二步高效准确。要从 AI 获得最高准确度，必须给予短、聚焦且有力的上下文；上下文工程正是从所有可用来源中策略性选取、打包并管理最关键信息的学科，实质是在模型有限注意力下策展，以防过载并保证任务上的高质量与高效率。详见附录 A。

This level leads to proactive and continuous operation. A travel assistant linked to your email demonstrates this by engineering the context from a verbose flight confirmation email; it selects only the key details (flight numbers, dates, locations) to package for subsequent tool calls to your calendar and a weather API.

> 这一层级带来主动、持续运行。与邮箱联动的旅行助手即是一例：从冗长的航班确认邮件中做上下文工程，只抽取关键细节（航班号、日期、地点）打包，供后续调用日历与天气 API。

In specialized fields like software engineering, the agent manages an entire workflow by applying this discipline. When assigned a bug report, it reads the report and accesses the codebase, then strategically engineers these large sources of information into a potent, focused context that allows it to efficiently write, test, and submit the correct code patch.

> 在软件工程等专业领域，智能体用同一套纪律管理完整工作流：接到缺陷报告后阅读报告与代码库，再将大量信息策略性工程化为强而聚焦的上下文，从而高效编写、测试并提交正确补丁。

Finally, the agent achieves self-improvement by refining its own context engineering processes. When it asks for feedback on how a prompt could have been improved, it is learning how to better curate its initial inputs. This allows it to automatically improve how it packages information for future tasks, creating a powerful, automated feedback loop that increases its accuracy and efficiency over time. For detailed information, refer to Chapter 17\.

> 最后，智能体通过精炼自身上下文工程流程实现自我改进：当它询问提示可如何改进时，正是在学习更好地策展初始输入，从而自动改进未来任务中的信息打包，形成强有力的自动化反馈闭环，随时间提升准确度与效率。详见第 17 章。

![Various Instances Demonstrating the Spectrum of Agent Complexity](../assets-new/Various_Instances_Demonstrating_the_Spectrum_of_Agent_Complexity.png)

Fig. 3: Various instances demonstrating the spectrum of agent complexity.

> 图 3：展示智能体复杂度谱系的若干实例。

## Level 3: The Rise of Collaborative Multi-Agent Systems

At Level 3, we see a significant paradigm shift in AI development, moving away from the pursuit of a single, all-powerful super-agent and towards the rise of sophisticated, collaborative multi-agent systems. In essence, this approach recognizes that complex challenges are often best solved not by a single generalist, but by a team of specialists working in concert. This model directly mirrors the structure of a human organization, where different departments are assigned specific roles and collaborate to tackle multi-faceted objectives. The collective strength of such a system lies in this division of labor and the synergy created through coordinated effort. For detailed information, refer to Chapter 7\.

> 在 3 级，AI 开发出现显著范式转移：从追求单一全能超级智能体，转向复杂协作式多智能体系统。本质上，它承认复杂问题往往最好由专家团队协作解决，而非单个通才。该模型直接映射人类组织：不同部门分工协作应对多目标。系统集体力量来自分工与协调产生的协同。详见第 7 章。

To bring this concept to life, consider the intricate workflow of launching a new product. Rather than one agent attempting to handle every aspect, a "Project Manager" agent could serve as the central coordinator. This manager would orchestrate the entire process by delegating tasks to other specialized agents: a "Market Research" agent to gather consumer data, a "Product Design" agent to develop concepts, and a "Marketing" agent to craft promotional materials. The key to their success would be the seamless communication and information sharing between them, ensuring all individual efforts align to achieve the collective goal.

> 以发布新产品的复杂工作流为例：不必由一个智能体包办一切，可由「项目经理」智能体作为中心协调者，将任务委派给其他专精智能体：「市场研究」收集消费者数据、「产品设计」开发概念、「营销」撰写推广材料。成功的关键在于彼此无缝沟通与信息共享，使个体努力对齐集体目标。

While this vision of autonomous, team-based automation is already being developed, it's important to acknowledge the current hurdles. The effectiveness of  such multi-agent systems is presently constrained by the reasoning limitations of LLMs they are using. Furthermore, their ability to genuinely learn from one another and improve as a cohesive unit is still in its early stages. Overcoming these technological bottlenecks is the critical next step, and doing so will unlock the profound promise of this level: the ability to automate entire business workflows from start to finish.

> 尽管这种自主团队式自动化的愿景已在开发中，也需正视当前障碍：此类多智能体系统的效能仍受所用 LLM 推理能力限制；彼此真正学习并作为整体共同进步的能力尚处早期。突破这些技术瓶颈是下一步关键，也将释放本层级的深远前景：端到端自动化整个业务流程。

## The Future of Agents: Top 5 Hypotheses

AI agent development is progressing at an unprecedented pace across domains such as software automation, scientific research, and customer service among others. While current systems are impressive, they are just the beginning. The next wave of innovation will likely focus on making agents more reliable, collaborative, and deeply integrated into our lives. Here are five leading hypotheses for what's next (see Fig. 4).

> AI 智能体开发在软件自动化、科学研究、客户服务等领域以前所未有的速度推进。现有系统虽已令人印象深刻，却只是开端。下一波创新可能聚焦让智能体更可靠、更具协作性、更深地融入生活。以下是关于下一步的五大领先假设（见图 4）。

### Hypothesis 1: The Emergence of the Generalist Agent

The first hypothesis is that AI agents will evolve from narrow specialists into true generalists capable of managing complex, ambiguous, and long-term goals with high reliability. For instance, you could give an agent a simple prompt like, "Plan my company's offsite retreat for 30 people in Lisbon next quarter." The agent would then manage the entire project for weeks, handling everything from budget approvals and flight negotiations to venue selection and creating a detailed itinerary from employee feedback, all while providing regular updates. Achieving this level of autonomy will require fundamental breakthroughs in AI reasoning, memory, and near-perfect reliability. An alternative, yet not mutually exclusive, approach is the rise of Small Language Models (SLMs). This "Lego-like" concept involves composing systems from small, specialized expert agents rather than scaling up a single monolithic model. This method promises systems that are cheaper, faster to debug, and easier to deploy. Ultimately, the development of large generalist models and the composition of smaller specialized ones are both plausible paths forward, and they could even complement each other.

> 假设一：AI 智能体将从狭窄专才演化为能高可靠地管理复杂、模糊、长期目标的真正通才。例如你可提示：「为 30 人规划下季度在里斯本的公司团建。」智能体可数周管理整个项目，从预算审批、机票谈判到场地选择与根据员工反馈制定详细行程，并持续汇报。实现这种自主需要在推理、记忆与近乎完美可靠性上的根本突破。另一路径（且不互斥）是小语言模型（SLM）兴起：用「乐高式」小专精智能体组合系统，而非扩展单一单体模型，有望更便宜、更易调试、更易部署。大通才模型与小专精组合都是可行路径，亦可互补。

### Hypothesis 2: Deep Personalization and Proactive Goal Discovery

The second hypothesis posits that agents will become deeply personalised and proactive partners. We are witnessing the emergence of a new class of agent: the proactive partner. By learning from your unique patterns and goals, these systems are beginning to shift from just following orders to anticipating your needs. AI systems operate as agents when they move beyond simply responding to chats or instructions. They initiate and execute tasks on behalf of the user, actively collaborating in the process.  This moves beyond simple task execution into the realm of proactive goal discovery.

> 假设二：智能体将成为深度个性化、主动的伙伴。我们正见证「主动伙伴」这一新类别：通过学习你的独特模式与目标，系统从仅服从指令转向预判需求。当 AI 超越仅响应聊天或指令、代表用户发起并执行任务、在过程中主动协作时，即作为智能体运行；这超越简单任务执行，进入主动发现目标的领域。

For instance, if you're exploring sustainable energy, the agent might identify your latent goal and proactively support it by suggesting courses or summarizing research. While these systems are still developing, their trajectory is clear. They will become increasingly proactive, learning to take initiative on your behalf when highly confident that the action will be helpful. Ultimately, the agent becomes an indispensable ally, helping you discover and achieve ambitions you have yet to fully articulate.

> 例如你探索可持续能源时，智能体可能识别潜在目标并主动建议课程或综述研究。这些系统仍在发展，但轨迹清晰：将越来越主动，在高度确信行动有益时代表你采取主动。最终智能体成为不可或缺的盟友，帮助你发现并实现尚未完全言明的志向。

![Five Hypotheses about the Future of Agents](../assets-new/Five_Hypotheses_about_the_Future_of_Agents.png)

Fig. 4: Five hypotheses about the future of agents

> 图 4：关于智能体未来的五大假设

### Hypothesis 3: Embodiment and Physical World Interaction

This hypothesis foresees agents breaking free from their purely digital confines to operate in the physical world. By integrating agentic AI with robotics, we will see the rise of "embodied agents." Instead of just booking a handyman, you might ask your home agent to fix a leaky tap. The agent would use its vision sensors to perceive the problem, access a library of plumbing knowledge to formulate a plan, and then control its robotic manipulators with precision to perform the repair. This would represent a monumental step, bridging the gap between digital intelligence and physical action, and transforming everything from manufacturing and logistics to elder care and home maintenance.

> 假设三：智能体将突破纯数字边界，在物理世界运作。将智能体化 AI 与机器人结合，将出现「具身智能体」。你或可请家庭智能体修理漏水龙头，而不只是预约工匠：它用视觉感知问题、查阅管道知识库制定计划，再精确控制机械臂完成维修。这将是弥合数字智能与物理行动鸿沟的重要一步，深刻影响制造、物流、养老与居家维护等。

### Hypothesis 4: The Agent-Driven Economy

The fourth hypothesis is that highly autonomous agents will become active participants in the economy, creating new markets and business models. We could see agents acting as independent economic entities, tasked with maximising a specific outcome, such as profit. An entrepreneur could launch an agent to run an entire e-commerce business. The agent would identify trending products by analysing social media, generate marketing copy and visuals, manage supply chain logistics by interacting with other automated systems, and dynamically adjust pricing based on real-time demand. This shift would create a new, hyper-efficient "agent economy" operating at a speed and scale impossible for humans to manage directly.

> 假设四：高度自主的智能体将成为经济中的积极参与者，催生新市场与商业模式。智能体可作为独立经济实体被指派最大化某类结果（如利润）。创业者可启动智能体运营整家电商：分析社交媒体找爆款、生成营销文案与视觉、与其他自动化系统交互管理供应链物流、依实时需求动态调价。这将形成一种人类难以直接驾驭速度与规模的超高效「智能体经济」。

### Hypothesis 5:  The Goal-Driven, Metamorphic Multi-Agent System

This hypothesis posits the emergence of intelligent systems that operate not from explicit programming, but from a declared goal. The user simply states the desired outcome, and the system autonomously figures out how to achieve it. This marks a fundamental shift towards metamorphic multi-agent systems capable of true self-improvement at both the individual and collective levels.

> 假设五：将出现并非由显式编程、而是由声明目标驱动的智能系统。用户只陈述期望结果，系统自主找出实现路径。这标志着向可变形多智能体系统的根本转变，个体与集体层面均可真正自我改进。

This system would be a dynamic entity, not a single agent. It would have the ability to analyze its own performance and modify the topology of its multi-agent workforce, creating, duplicating, or removing agents as needed to form the most effective team for the task at hand. This evolution happens at multiple levels:

> 该系统是动态整体，而非单一智能体：能分析自身表现并修改多智能体队伍的拓扑，按需创建、复制或移除智能体以组成当下任务最有效的团队。演化发生在多个层级：

- Architectural Modification: At the deepest level, individual agents can rewrite their own source code and re-architect their internal structures for higher efficiency, as in the original hypothesis.  
- Instructional Modification: At a higher level, the system continuously performs automatic prompt engineering and context engineering. It refines the instructions and information given to each agent, ensuring they are operating with optimal guidance without any human intervention.

> - **架构修改：** 在最深层，单个智能体可重写自身源码并重构内部结构以提高效率（如原始假设所述）。  
> - **指令修改：** 在更高层，系统持续进行自动提示工程与上下文工程，精炼赋予各智能体的指令与信息，使其在无人工干预下获得最优指导。

For instance, an entrepreneur would simply declare the intent: "Launch a successful e-commerce business selling artisanal coffee." The system, without further programming, would spring into action. It might initially spawn a "Market Research" agent and a "Branding" agent. Based on the initial findings, it could decide to remove the branding agent and spawn three new specialized agents: a "Logo Design" agent, a "Webstore Platform" agent, and a "Supply Chain" agent. It would constantly tune their internal prompts for better performance. If the webstore agent becomes a bottleneck, the system might duplicate it into three parallel agents to work on different parts of the site, effectively re-architecting its own structure on the fly to best achieve the declared goal.

> 例如创业者只声明意图：「成功启动销售手工咖啡的电商业务。」系统无需进一步编程即可启动：可能先产生「市场研究」与「品牌」智能体；根据初步结果，或移除品牌智能体并新建「Logo 设计」「网店平台」「供应链」三支专精智能体；持续调优内部提示。若网店智能体成瓶颈，可复制为三台并行处理站点不同部分，实质即时重构自身结构以最好地达成声明目标。

## Conclusion

In essence, an AI agent represents a significant leap from traditional models, functioning as an autonomous system that perceives, plans, and acts to achieve specific goals. The evolution of this technology is advancing from single, tool-using agents to complex, collaborative multi-agent systems that tackle multifaceted objectives. Future hypotheses predict the emergence of generalist, personalized, and even physically embodied agents that will become active participants in the economy. This ongoing development signals a major paradigm shift towards self-improving, goal-driven systems poised to automate entire workflows and fundamentally redefine our relationship with technology.

> 总之，AI 智能体相对传统模型是一次重大跃迁：作为自主系统感知、规划并行动以达成目标。技术正从单智能体、工具使用走向协作式多智能体系统以应对多面目标。未来假设预见通才、深度个性化乃至具身智能体将参与经济。这一持续演进标志着向自我改进、目标驱动系统的重大范式转移，有望自动化整条工作流并重新定义我们与技术的关系。

## References

1. Cloudera, Inc. (April 2025), 96% of enterprises are increasing their use of AI agents.[https://www.cloudera.com/about/news-and-blogs/press-releases/2025-04-16-96-percent-of-enterprises-are-expanding-use-of-ai-agents-according-to-latest-data-from-cloudera.html](https://www.cloudera.com/about/news-and-blogs/press-releases/2025-04-16-96-percent-of-enterprises-are-expanding-use-of-ai-agents-according-to-latest-data-from-cloudera.html)
2. Autonomous generative AI agents: [https://www.deloitte.com/us/en/insights/industry/technology/technology-media-and-telecom-predictions/2025/autonomous-generative-ai-agents-still-under-development.html](https://www.deloitte.com/us/en/insights/industry/technology/technology-media-and-telecom-predictions/2025/autonomous-generative-ai-agents-still-under-development.html)
3. Market.us. Global Agentic AI Market Size, Trends and Forecast 2025–2034. [https://market.us/report/agentic-ai-market/](https://market.us/report/agentic-ai-market/)

