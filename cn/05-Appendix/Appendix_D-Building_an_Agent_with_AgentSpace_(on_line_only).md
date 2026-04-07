# Appendix D - Building an Agent with AgentSpace

> **附录 D：使用 AgentSpace 构建智能体**

## Overview

> ## 概述

AgentSpace is a platform designed to facilitate an "agent-driven enterprise" by integrating artificial intelligence into daily workflows. At its core, it provides a unified search capability across an organization's entire digital footprint, including documents, emails, and databases. This system utilizes advanced AI models, like Google's Gemini, to comprehend and synthesize information from these varied sources.

> AgentSpace 是一个平台，旨在通过将人工智能融入日常工作流，推动「智能体驱动型企业」。其核心能力之一，是在组织全部数字足迹（文档、邮件、数据库等）上提供统一搜索。系统采用 Google Gemini 等先进模型，理解并综合来自这些异构来源的信息。

The platform enables the creation and deployment of specialized AI "agents" that can perform complex tasks and automate processes. These agents are not merely chatbots; they can reason, plan, and execute multi-step actions autonomously. For instance, an agent could research a topic, compile a report with citations, and even generate an audio summary.

> 该平台支持创建与部署可执行复杂任务、自动化流程的专业化 AI「智能体」。它们不只是聊天机器人，还能推理、规划并自主执行多步动作。例如，智能体可以调研主题、整理带引用的报告，甚至生成音频摘要。

To achieve this, AgentSpace constructs an enterprise knowledge graph, mapping the relationships between people, documents, and data. This allows the AI to understand context and deliver more relevant and personalized results. The platform also includes a no-code interface called Agent Designer for creating custom agents without requiring deep technical expertise.

> 为此，AgentSpace 构建企业知识图谱，映射人员、文档与数据之间的关系，使 AI 能理解上下文并返回更相关、更个性化的结果。平台还提供名为 Agent Designer 的无代码界面，可在无需深厚技术背景的情况下创建自定义智能体。

Furthermore, AgentSpace supports a multi-agent system where different AI agents can communicate and collaborate through an open protocol known as the Agent2Agent (A2A) Protocol. This interoperability allows for more complex and orchestrated workflows. Security is a foundational component, with features like role-based access controls and data encryption to protect sensitive enterprise information. Ultimately, AgentSpace aims to enhance productivity and decision-making by embedding intelligent, autonomous systems directly into an organization's operational fabric.

> 此外，AgentSpace 支持多智能体系统，不同 AI 智能体可通过名为 Agent2Agent（A2A）的开放协议通信与协作，互操作性带来更复杂、可编排的工作流。安全是基础能力，包含基于角色的访问控制与数据加密等，以保护敏感企业信息。最终目标是：将智能、自主系统直接嵌入组织运营肌理，提升生产力与决策质量。

## How to build an Agent with AgentSpace UI

> ## 如何通过 AgentSpace 界面构建智能体

Figure 1 illustrates how to access AgentSpace by selecting AI Applications from the Google Cloud Console.

> 图 1 说明如何通过 Google 云控制台选择 AI Applications 进入 AgentSpace。

![GCP: Access AgentSpace](../assets-new/GCP_Access_AgentSpace.png)

Fig. 1:  How to use Google Cloud Console to access AgentSpace

> 图 1：如何使用 Google Cloud Console 访问 AgentSpace

Your agent can be connected to various services, including Calendar, Google Mail, Workaday, Jira, Outlook, and Service Now (see Fig. 2).

> 智能体可连接多种服务，包括 Calendar、Google Mail、Workaday、Jira、Outlook、Service Now 等（见图 2）。

![GCP: Integrate with diverse services](../assets-new/GCP_Integrate_with_diverse_services.png)

Fig. 2: Integrate with diverse services, including Google and third-party platforms.

> 图 2：与多种服务集成，包括 Google 与第三方平台。

The Agent can then utilize its own prompt, chosen from a gallery of pre-made prompts provided by Google, as illustrated in Fig. 3\.

> 随后智能体可使用自有提示，从 Google 提供的预制提示库中选择，如图 3 所示。

![GCP: Googles Gallery of Pre-Assembled Prompts](../assets-new/GCP_Googles_Gallery_of_Pre_Assembled_Prompts.png)

Fig.3: Google's Gallery of Pre-assembled  prompts

> 图 3：Google 的预制提示库

In alternative you can create your own prompt as in Fig.4, which will be then used by your agent  

> 也可以如图 4 自行创建提示，供智能体使用。

![GCP: Customizing the Agent's Prompt](../assets-new/GCP_Customizing_the_Agents_Prompt.png)

Fig.4: Customizing the Agent's Prompt

> 图 4：自定义智能体的提示

AgentSpace offers a number of advanced features such as integration with datastores to store your own data, integration with Google Knowledge Graph or with your private Knowledge Graph, Web interface for exposing your agent to the Web, and Analytics to monitor usage, and more (see Fig. 5\)

> AgentSpace 还提供多项高级能力，例如与数据存储集成以存放自有数据、与 Google 知识图谱或私有知识图谱集成、用于将智能体暴露到 Web 的 Web 界面、用于监控使用情况的 Analytics 等（见图 5）。

![GCP: AgentSpace Advanced Capabilities](../assets-new/GCP_AgentSpace_Advanced_Capabilities.png)

Fig. 5: AgentSpace advanced capabilities

> 图 5：AgentSpace 高级能力

Upon completion, the AgentSpace chat interface (Fig. 6\) will be accessible.

> 完成后即可使用 AgentSpace 聊天界面（图 6）。

![GCP: AgentSpace User Interface for initiating a chat with your Agent](../assets-new/GCP_AgentSpace_User_Interface_for_initiating_a_chat_with_your_Agent.png)

Fig. 6: The AgentSpace User Interface for initiating a chat with your Agent.

> 图 6：用于与智能体发起聊天的 AgentSpace 用户界面

## Conclusion

> ## 结语

In conclusion, AgentSpace provides a functional framework for developing and deploying AI agents within an organization's existing digital infrastructure. The system's architecture links complex backend processes, such as autonomous reasoning and enterprise knowledge graph mapping, to a graphical user interface for agent construction. Through this interface, users can configure agents by integrating various data services and defining their operational parameters via prompts, resulting in customized, context-aware automated systems.

> 总之，AgentSpace 为在组织既有数字基础设施中开发与部署 AI 智能体提供了可用框架。系统架构将自主推理、企业知识图谱映射等复杂后端过程，与用于构建智能体的图形用户界面连接起来。用户可通过该界面集成各类数据服务并以提示定义运行参数，从而得到定制化、上下文感知的自动化系统。

This approach abstracts the underlying technical complexity, enabling the construction of specialized multi-agent systems without requiring deep programming expertise. The primary objective is to embed automated analytical and operational capabilities directly into workflows, thereby increasing process efficiency and enhancing data-driven analysis. For practical instruction, hands-on learning modules are available, such as the "Build a Gen AI Agent with Agentspace" lab on Google Cloud Skills Boost, which provides a structured environment for skill acquisition.

> 该方式抽象了底层技术复杂度，使无需深厚编程能力也能构建专业化多智能体系统。首要目标是将自动化分析与运营能力直接嵌入工作流，从而提高流程效率并加强数据驱动分析。实践学习方面，Google Cloud Skills Boost 上提供动手实验模块，例如「使用 Agentspace 构建生成式 AI 智能体」实验，可在结构化环境中习得技能。

## References

1. Create a no-code agent with Agent Designer, [https://cloud.google.com/agentspace/agentspace-enterprise/docs/agent-designer](https://cloud.google.com/agentspace/agentspace-enterprise/docs/agent-designer)
2. Google Cloud Skills Boost, [https://www.cloudskillsboost.google/](https://www.cloudskillsboost.google/)
