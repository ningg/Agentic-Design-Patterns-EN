# Chapter 15: Inter-Agent Communication (A2A)

> 第十五章：智能体间通信（A2A）

Individual AI agents often face limitations when tackling complex, multifaceted problems, even with advanced capabilities. To overcome this, Inter-Agent Communication (A2A) enables diverse AI agents, potentially built with different frameworks, to collaborate effectively. This collaboration involves seamless coordination, task delegation, and information exchange.

> 即便能力较强，单个 AI 智能体在应对复杂、多面问题时仍常遇瓶颈。为克服这一点，智能体间通信（A2A）使多种可能基于不同框架构建的智能体能够有效协作，包括顺畅的协调、任务委派与信息交换。

Google's A2A protocol is an open  standard designed to facilitate this universal communication. This chapter will explore A2A, its practical applications, and its implementation within the Google ADK.

> 谷歌的 A2A 协议是一项旨在促进这种通用通信的开放标准。本章将探讨 A2A、其实际应用以及在 Google ADK 中的实现。

## Inter-Agent Communication Pattern Overview

> ## 智能体间通信模式概览

The Agent2Agent (A2A) protocol is an open standard designed to enable communication and collaboration between different AI agent frameworks. It ensures interoperability, allowing AI agents developed with technologies like LangGraph, CrewAI, or Google ADK to work together regardless of their origin or framework differences.

> Agent2Agent（A2A）协议是一项开放标准，旨在使不同 AI 智能体框架之间能够通信与协作。它保证互操作性，使基于 LangGraph、CrewAI 或 Google ADK 等技术构建的智能体无论来源或框架差异如何都能协同工作。

A2A is supported by a range of technology companies and service providers, including Atlassian, Box, LangChain, MongoDB, Salesforce, SAP, and ServiceNow. Microsoft plans to integrate A2A into Azure AI Foundry and Copilot Studio, demonstrating its commitment to open protocols. Additionally, Auth0 and SAP are integrating A2A support into their platforms and agents.

> A2A 获得多家科技公司与服务商支持，包括 Atlassian、Box、LangChain、MongoDB、Salesforce、SAP 与 ServiceNow。微软计划将 A2A 集成到 Azure AI Foundry 与 Copilot Studio，体现其对开放协议的投入。此外，Auth0 与 SAP 也正将 A2A 支持集成到各自平台与智能体中。

As an open-source protocol, A2A welcomes community contributions to facilitate its evolution and widespread adoption.

> 作为开源协议，A2A 欢迎社区贡献，以促进其演进与广泛采用。

## Core Concepts of A2A

> ## A2A 的核心概念

The A2A protocol provides a structured approach for agent interactions, built upon several core concepts. A thorough grasp of these concepts is crucial for anyone developing or integrating with A2A-compliant systems. The foundational pillars of A2A include Core Actors, Agent Card, Agent Discovery, Communication and Tasks,  Interaction mechanisms, and Security, all of which will be reviewed in detail.

> A2A 协议为智能体交互提供结构化方法，建立在若干核心概念之上。开发与集成符合 A2A 的系统时，透彻理解这些概念至关重要。A2A 的支柱包括：核心参与者、智能体卡片（Agent Card）、智能体发现、通信与任务、交互机制与安全；下文将逐一详述。

**Core Actors:** A2A involves three main entities:

> **核心参与者：** A2A 涉及三类主要实体：

* User: Initiates requests for agent assistance.  
* A2A Client (Client Agent): An application or AI agent that acts on the user's behalf to request actions or information.  
* A2A Server (Remote Agent): An AI agent or system that provides an HTTP endpoint to process client requests and return results. The remote agent operates as an "opaque" system, meaning the client does not need to understand its internal operational details.

> * 用户：发起对智能体协助的请求。  
> * A2A 客户端（Client Agent）：代表用户请求操作或信息的应用或 AI 智能体。  
> * A2A 服务端（Remote Agent）：提供 HTTP 端点以处理客户端请求并返回结果的 AI 智能体或系统。远端智能体以「黑盒」方式运作，客户端无需了解其内部实现细节。

**Agent Card:** An agent's digital identity is defined by its Agent Card, usually a JSON file. This file contains key information for client interaction and automatic discovery, including the agent's identity, endpoint URL, and version. It also details supported capabilities like streaming or push notifications, specific skills, default input/output modes, and authentication requirements. Below is an example of an Agent Card for a WeatherBot.

> **智能体卡片（Agent Card）：** 智能体的数字身份由其 Agent Card 定义，通常为 JSON 文件。该文件包含客户端交互与自动发现所需的关键信息，如身份、端点 URL、版本；并说明所支持的能力（如流式输出或推送通知）、具体技能、默认输入/输出模式以及认证要求。下面是 WeatherBot 的 Agent Card 示例。

```json
{
    "name": "WeatherBot",
    "description": "Provides accurate weather forecasts and historical data.",
    "url": "http://weather-service.example.com/a2a",
    "version": "1.0.0",
    "capabilities": {
        "streaming": true,
        "pushNotifications": false,
        "stateTransitionHistory": true
    },
    "authentication": {
        "schemes": [
            "apiKey"
        ]
    },
    "defaultInputModes": [
        "text"
    ],
    "defaultOutputModes": [
        "text"
    ],
    "skills": [
        {
            "id": "get_current_weather",
            "name": "Get Current Weather",
            "description": "Retrieve real-time weather for any location.",
            "inputModes": [
                "text"
            ],
            "outputModes": [
                "text"
            ],
            "examples": [
                "What's the weather in Paris?",
                "Current conditions in Tokyo"
            ],
            "tags": [
                "weather",
                "current",
                "real-time"
            ]
        },
        {
            "id": "get_forecast",
            "name": "Get Forecast",
            "description": "Get 5-day weather predictions.",
            "inputModes": [
                "text"
            ],
            "outputModes": [
                "text"
            ],
            "examples": [
                "5-day forecast for New York",
                "Will it rain in London this weekend?"
            ],
            "tags": [
                "weather",
                "forecast",
                "prediction"
            ]
        }
    ]
}
```

**Agent discovery:** it allows clients to find Agent Cards, which describe the capabilities of available A2A Servers. Several strategies exist for this process:

> **智能体发现：** 使客户端能够找到描述可用 A2A 服务端能力的 Agent Card。常见策略包括：

* Well-Known URI: Agents host their Agent Card at a standardized path (e.g., /.well-known/agent.json). This approach offers broad, often automated, accessibility for public or domain-specific use.  
* Curated Registries**:** These provide a centralized catalog where Agent Cards are published and can be queried based on specific criteria. This is well-suited for enterprise environments needing centralized management and access control.  
* Direct Configuration**:** Agent Card information is embedded or privately shared. This method is appropriate for closely coupled or private systems where dynamic discovery isn't crucial.

> * 知名 URI（Well-Known URI）：智能体将 Agent Card 托管在标准化路径（如 `/.well-known/agent.json`），便于公开或域内场景的广泛、常可自动化的访问。  
> * **策展注册表（Curated Registries）：** 提供集中目录，发布 Agent Card 并可按条件查询，适合需要集中管理与访问控制的企业环境。  
> * **直接配置（Direct Configuration）：** 将 Agent Card 信息内嵌或私下共享，适用于紧耦合或私有系统、且动态发现不重要的场景。

Regardless of the chosen method, it is important to secure Agent Card endpoints. This can be achieved through access control, mutual TLS (mTLS), or network restrictions, especially if the card contains sensitive (though non-secret) information.

> 无论采用何种方式，都应保护 Agent Card 端点安全，可通过访问控制、双向 TLS（mTLS）或网络限制实现，尤其当卡片包含敏感（但非机密）信息时。

**Communications and Tasks:** In the A2A framework, communication is structured around asynchronous tasks, which represent the fundamental units of work for long-running processes. Each task is assigned a unique identifier and moves through a series of states—such as submitted, working, or completed—a design that supports parallel processing in complex operations. Communication between agents occurs through a Message.

> **通信与任务：** 在 A2A 框架中，通信围绕异步任务组织；任务是长时间运行过程的基本工作单元。每个任务有唯一标识，并在提交、进行中、完成等状态间迁移，该设计支持复杂操作中的并行处理。智能体间通过 Message 通信。

This communication  contains attributes, which are key-value metadata describing the message (like its priority or creation time), and one or more parts, which carry the actual content being delivered, such as plain text, files, or structured JSON data. The tangible outputs generated by an agent during a task are called artifacts. Like messages, artifacts are also composed of one or more parts and can be streamed incrementally as results become available. All communication within the A2A framework is conducted over HTTP(S) using the JSON-RPC 2.0 protocol for payloads. To maintain continuity across multiple interactions, a server-generated contextId is used to group related tasks and preserve context.

> 通信包含属性（描述消息的键值元数据，如优先级或创建时间）以及一个或多个部分（parts），承载实际内容，如纯文本、文件或结构化 JSON。任务执行过程中产生的具体输出称为工件（artifacts）；与消息类似，工件也由一个或多个部分组成，并可在结果逐步就绪时流式传输。A2A 框架内的通信均通过 HTTP(S) 进行，负载采用 JSON-RPC 2.0。为在多次交互间保持连续性，使用服务端生成的 `contextId` 对相关任务分组并保留上下文。

**Interaction Mechanisms**: Request/Response (Polling) Server-Sent Events (SSE). A2A provides multiple interaction methods to suit a variety of AI application needs, each with a distinct mechanism:

> **交互机制：** 请求/响应（轮询）、服务器推送事件（SSE）等。A2A 提供多种交互方式以适配不同 AI 应用需求，各自机制不同：

* Synchronous Request/Response: For quick, immediate operations. In this model, the client sends a request and actively waits for the server to process it and return a complete response in a single, synchronous exchange.  
* Asynchronous Polling: Suited for tasks that take longer to process. The client sends a request, and the server immediately acknowledges it with a "working" status and a task ID. The client is then free to perform other actions and can periodically poll the server by sending new requests to check the status of the task until it is marked as "completed" or "failed."  
* Streaming Updates (Server-Sent Events \- SSE): Ideal for receiving real-time, incremental results. This method establishes a persistent, one-way connection from the server to the client. It allows the remote agent to continuously push updates, such as status changes or partial results, without the client needing to make multiple requests.  
* Push Notifications (Webhooks): Designed for very long-running or resource-intensive tasks where maintaining a constant connection or frequent polling is inefficient. The client can register a webhook URL, and the server will send an asynchronous notification (a "push") to that URL when the task's status changes significantly (e.g., upon completion).

> * **同步请求/响应：** 用于快速、即时操作；客户端发送请求并等待服务端在一次同步交换中返回完整响应。  
> * **异步轮询：** 适合耗时较长的任务；服务端立即以「进行中」状态与任务 ID 确认，客户端可继续做其他事并周期性查询状态，直至「完成」或「失败」。  
> * **流式更新（SSE）：** 适合实时、增量结果；建立从服务端到客户端的持久单向连接，远端智能体可持续推送状态或部分结果，无需客户端反复请求。  
> * **推送通知（Webhooks）：** 适合极长或重资源任务；客户端注册 webhook URL，任务状态发生重大变化（如完成）时，服务端异步向该 URL 发送通知。

The Agent Card specifies whether an agent supports streaming or push notification capabilities. Furthermore, A2A is modality-agnostic, meaning it can facilitate these interaction patterns not just for text, but also for other data types like audio and video, enabling rich, multimodal AI applications. Both streaming and push notification capabilities are specified within the Agent Card.

> Agent Card 会标明是否支持流式或推送能力。此外，A2A 与模态无关，除文本外还可支持音频、视频等，从而支撑丰富的多模态应用；流式与推送能力均在 Agent Card 中声明。

```json
# Synchronous Request Example 
{
    "jsonrpc": "2.0",
    "id": "1",
    "method": "sendTask",
    "params": {
        "id": "task-001",
        "sessionId": "session-001",
        "message": {
            "role": "user",
            "parts": [
                {
                    "type": "text",
                    "text": "What is the exchange rate from USD to EUR?"
                }
            ]
        },
        "acceptedOutputModes": [
            "text/plain"
        ],
        "historyLength": 5
    }
}
```

The synchronous request uses the sendTask method, where the client asks for and expects a single, complete answer to its query. In contrast, the streaming request uses the sendTaskSubscribe method to establish a persistent connection, allowing the agent to send back multiple, incremental updates or partial results over time.

> 同步请求使用 `sendTask` 方法，客户端期望对查询得到单一完整答复。流式请求则使用 `sendTaskSubscribe` 建立持久连接，使智能体可随时间返回多条增量更新或部分结果。

```json
# Streaming Request Example 
{
    "jsonrpc": "2.0",
    "id": "2",
    "method": "sendTaskSubscribe",
    "params": {
        "id": "task-002",
        "sessionId": "session-001",
        "message": {
            "role": "user",
            "parts": [
                {
                    "type": "text",
                    "text": "What's the exchange rate for JPY to GBP today?"
                }
            ]
        },
        "acceptedOutputModes": [
            "text/plain"
        ],
        "historyLength": 5
    }
}
```

**Security:**  Inter-Agent Communication (A2A): Inter-Agent Communication (A2A) is a vital component of system architecture, enabling secure and seamless data exchange among agents. It ensures robustness and integrity through several built-in mechanisms.

> **安全：** 智能体间通信（A2A）是系统架构的关键组成部分，支持智能体间安全、无缝的数据交换，并通过多种内置机制保障稳健性与完整性。

Mutual Transport Layer Security (TLS): Encrypted and authenticated connections are established to prevent unauthorized access and data interception, ensuring secure communication.

> **双向传输层安全（mTLS）：** 建立加密且经认证的连接，防止未授权访问与窃听，保障通信安全。

Comprehensive Audit Logs: All inter-agent communications are meticulously recorded, detailing information flow, involved agents, and actions. This audit trail is crucial for accountability, troubleshooting, and security analysis.

> **全面审计日志：** 详尽记录智能体间通信的信息流、参与方与动作；该审计轨迹对问责、排障与安全分析至关重要。

Agent Card Declaration: Authentication requirements are explicitly declared in the Agent Card, a configuration artifact outlining the agent's identity, capabilities, and security policies. This centralizes and simplifies authentication management.

> **Agent Card 声明：** 认证要求在 Agent Card 中明确声明；该配置工件概括智能体身份、能力与安全策略，使认证管理集中且简化。

Credential Handling: Agents typically authenticate using secure credentials like OAuth 2.0 tokens or API keys, passed via HTTP headers. This method prevents credential exposure in URLs or message bodies, enhancing overall security.

> **凭据处理：** 智能体通常通过 HTTP 头传递 OAuth 2.0 令牌或 API 密钥等安全凭据，避免凭据出现在 URL 或消息体中，从而提升整体安全性。

## A2A vs. MCP

> ## A2A 与 MCP

A2A is a protocol that complements Anthropic's Model Context Protocol (MCP) (see Fig. 1). While MCP focuses on structuring context for agents and their interaction with external data and tools, A2A facilitates coordination and communication among agents, enabling task delegation and collaboration.

> A2A 与 Anthropic 的模型上下文协议（MCP）互补（见图 1）。MCP 侧重为智能体结构化上下文及其与外部数据、工具的交互；A2A 则促进智能体之间的协调与通信，支持任务委派与协作。

![Comparison A2A and MCP Protocols](../assets-new/Comparison_A2A_and_MCP_Protocols.png)

Fig.1: Comparison A2A and MCP Protocols

> 图 1：A2A 与 MCP 协议对比

The goal of A2A is to enhance efficiency, reduce integration costs, and foster innovation and interoperability in the development of complex, multi-agent AI systems. Therefore, a thorough understanding of A2A's core components and operational methods is essential for its effective design, implementation, and application in building collaborative and interoperable AI agent systems..

> A2A 的目标是提升效率、降低集成成本，并在复杂多智能体 AI 系统的开发中促进创新与互操作性。因此，深入理解其核心组件与运行方式，对于有效设计、实现与应用以构建协作且可互操作的智能体系统至关重要。

## Practical Applications & Use Cases

> ## 实际应用与用例

Inter-Agent Communication is indispensable for building sophisticated AI solutions across diverse domains, enabling modularity, scalability, and enhanced intelligence.

> 智能体间通信对于在广泛领域构建复杂 AI 解决方案不可或缺，可带来模块化、可扩展性与更强的智能。

* **Multi-Framework Collaboration:** A2A's primary use case is enabling independent AI agents, regardless of their underlying frameworks (e.g., ADK, LangChain, CrewAI), to communicate and collaborate. This is fundamental for building complex multi-agent systems where different agents specialize in different aspects of a problem.  
* **Automated Workflow Orchestration:** In enterprise settings, A2A can facilitate complex workflows by enabling agents to delegate and coordinate tasks. For instance, an agent might handle initial data collection, then delegate to another agent for analysis, and finally to a third for report generation, all communicating via the A2A protocol.  
* **Dynamic Information Retrieval:** Agents can communicate to retrieve and exchange real-time information. A primary agent might request live market data from a specialized "data fetching agent," which then uses external APIs to gather the information and send it back.

> * **多框架协作：** A2A 的首要用例是让独立智能体无论底层框架（如 ADK、LangChain、CrewAI）如何都能通信协作，这是构建复杂多智能体系统的基础。  
> * **自动化工作流编排：** 在企业场景中，A2A 可通过委派与协调任务支撑复杂工作流；例如先由一智能体采集数据，再委派分析，最后生成报告，全程经 A2A 通信。  
> * **动态信息检索：** 智能体可通信以获取并交换实时信息；主智能体可向专门的「数据获取智能体」请求行情，后者调用外部 API 收集并回传。

## Hands-On Code Example

> ## 动手代码示例

Let's examine the practical applications of the A2A protocol. The repository at [https://github.com/google-a2a/a2a-samples/tree/main/samples](https://github.com/google-a2a/a2a-samples/tree/main/samples) provides examples in Java, Go, and Python that illustrate how various agent frameworks, such as LangGraph, CrewAI, Azure AI Foundry, and AG2, can communicate using A2A. All code in this repository is released under the Apache 2.0 license. To further illustrate A2A's core concepts, we will review code excerpts focusing on setting up an A2A Server using an ADK-based agent with Google-authenticated tools. Looking at [https://github.com/google-a2a/a2a-samples/blob/main/samples/python/agents/birthday_planner_adk/calendar_agent/adk_agent.py](https://github.com/google-a2a/a2a-samples/blob/main/samples/python/agents/birthday_planner_adk/calendar_agent/adk_agent.py)

> 下面考察 A2A 协议的实际应用。仓库 [https://github.com/google-a2a/a2a-samples/tree/main/samples](https://github.com/google-a2a/a2a-samples/tree/main/samples) 提供 Java、Go、Python 示例，展示 LangGraph、CrewAI、Azure AI Foundry、AG2 等框架如何通过 A2A 通信；代码以 Apache 2.0 发布。为进一步说明 A2A 核心概念，我们将摘录基于 ADK、带谷歌认证工具搭建 A2A 服务端的代码，参见 [https://github.com/google-a2a/a2a-samples/blob/main/samples/python/agents/birthday_planner_adk/calendar_agent/adk_agent.py](https://github.com/google-a2a/a2a-samples/blob/main/samples/python/agents/birthday_planner_adk/calendar_agent/adk_agent.py)

```python
import datetime

from google.adk.agents import LlmAgent  # type: ignore[import-untyped]
from google.adk.tools.google_api_tool import CalendarToolset  # type: ignore[import-untyped]


async def create_agent(client_id: str, client_secret: str) -> LlmAgent:
    """Constructs the ADK agent."""
    toolset = CalendarToolset(client_id=client_id, client_secret=client_secret)
    return LlmAgent(
        model="gemini-2.0-flash-001",
        name="calendar_agent",
        description="An agent that can help manage a user's calendar",
        instruction=(
            f""" You are an agent that can help manage a user's calendar. Users will request information about the state of their calendar """
            f""" or to make changes to their calendar. Use the provided tools for interacting with the calendar API. """
            f""" If not specified, assume the calendar the user wants is the 'primary' calendar. """
            f""" When using the Calendar API tools, use well-formed RFC3339 timestamps. Today is {datetime.datetime.now()}. """
        ),
        tools=await toolset.get_tools(),
    )
```

This Python code defines an asynchronous function `create_agent` that constructs an ADK LlmAgent. It begins by initializing a `CalendarToolset` using the provided client credentials to access the Google Calendar API. Subsequently, an `LlmAgent` instance is created, configured with a specified Gemini model, a descriptive name, and instructions for managing a user's calendar. The agent is furnished with calendar tools from the `CalendarToolset`, enabling it to interact with the Calendar API and respond to user queries regarding calendar states or modifications. The agent's instructions dynamically incorporate the current date for temporal context. To illustrate how an agent is constructed, let's examine a key section from the `calendar_agent` found in the A2A samples on GitHub.

> 该 Python 代码定义异步函数 `create_agent`，用于构建 ADK `LlmAgent`。首先用客户端凭据初始化 `CalendarToolset` 以访问 Google 日历 API；随后创建 `LlmAgent`，配置指定 Gemini 模型、名称与日历管理说明，并从 `CalendarToolset` 挂载日历工具，使其能调用日历 API 并回答关于日历状态或修改的查询；说明中动态加入当前日期以提供时间上下文。为展示智能体如何构建，我们继续看 GitHub A2A 样例中 `calendar_agent` 的关键片段。

The code below shows how the agent is defined with its specific instructions and tools. Please note that only the code required to explain this functionality is shown; you can access the complete file here: [https://github.com/a2aproject/a2a-samples/blob/main/samples/python/agents/birthday_planner_adk/calendar_agent/__main__.py](https://github.com/a2aproject/a2a-samples/blob/main/samples/python/agents/birthday_planner_adk/calendar_agent/__main__.py)

> 下列代码展示如何用具体说明与工具定义智能体；为便于讲解仅摘录必要部分，完整文件见：[https://github.com/a2aproject/a2a-samples/blob/main/samples/python/agents/birthday_planner_adk/calendar_agent/__main__.py](https://github.com/a2aproject/a2a-samples/blob/main/samples/python/agents/birthday_planner_adk/calendar_agent/__main__.py)

```python
def main(host: str = "0.0.0.0", port: int = 8000):
    # Verify an API key is set.
    # Not required if using Vertex AI APIs.
    if os.getenv("GOOGLE_GENAI_USE_VERTEXAI") != "TRUE" and not os.getenv("GOOGLE_API_KEY"):
        raise ValueError(
            "GOOGLE_API_KEY environment variable not set and "
            "GOOGLE_GENAI_USE_VERTEXAI is not TRUE."
        )

    skill = AgentSkill(
        id="check_availability",
        name="Check Availability",
        description="Checks a user's availability for a time using their Google Calendar",
        tags=["calendar"],
        examples=["Am I free from 10am to 11am tomorrow?"],
    )

    agent_card = AgentCard(
        name="Calendar Agent",
        description="An agent that can manage a user's calendar",
        url=f"http://{host}:{port}/",
        version="1.0.0",
        defaultInputModes=["text"],
        defaultOutputModes=["text"],
        capabilities=AgentCapabilities(streaming=True),
        skills=[skill],
    )

    adk_agent = asyncio.run(
        create_agent(
            client_id=os.getenv("GOOGLE_CLIENT_ID"),
            client_secret=os.getenv("GOOGLE_CLIENT_SECRET"),
        )
    )

    runner = Runner(
        app_name=agent_card.name,
        agent=adk_agent,
        artifact_service=InMemoryArtifactService(),
        session_service=InMemorySessionService(),
        memory_service=InMemoryMemoryService(),
    )
    agent_executor = ADKAgentExecutor(runner, agent_card)

    async def handle_auth(request: Request) -> PlainTextResponse:
        await agent_executor.on_auth_callback(
            str(request.query_params.get("state")),
            str(request.url),
        )
        return PlainTextResponse("Authentication successful.")

    request_handler = DefaultRequestHandler(
        agent_executor=agent_executor,
        task_store=InMemoryTaskStore(),
    )

    a2a_app = A2AStarletteApplication(
        agent_card=agent_card,
        http_handler=request_handler,
    )
    routes = a2a_app.routes()
    routes.append(
        Route(
            path="/authenticate",
            methods=["GET"],
            endpoint=handle_auth,
        )
    )
    app = Starlette(routes=routes)

    uvicorn.run(app, host=host, port=port)


if __name__ == "__main__":
    main()
```

This Python code demonstrates setting up an A2A-compliant "Calendar Agent" for checking user availability using Google Calendar. It involves verifying API keys or Vertex AI configurations for authentication purposes. The agent's capabilities, including the "check_availability" skill, are defined within an AgentCard, which also specifies the agent's network address. Subsequently, an ADK agent is created, configured with in-memory services for managing artifacts, sessions, and memory. The code then initializes a Starlette web application, incorporates an authentication callback and the A2A protocol handler, and executes it using Uvicorn to expose the agent via HTTP.

> 该 Python 代码演示如何搭建符合 A2A 的「日历智能体」，用 Google 日历检查用户空闲时间；包括验证 API 密钥或 Vertex AI 配置以完成认证；在 `AgentCard` 中定义能力与 `check_availability` 技能并指定网络地址；随后创建 ADK 智能体并配置内存型工件、会话与记忆服务；再初始化 Starlette 应用，加入认证回调与 A2A 协议处理，并用 Uvicorn 通过 HTTP 暴露服务。

These examples illustrate the process of building an A2A-compliant agent, from defining its capabilities to running it as a web service. By utilizing Agent Cards and ADK, developers can create interoperable AI agents capable of integrating with tools like Google Calendar. This practical approach demonstrates the application of A2A in establishing a multi-agent ecosystem.

> 这些示例展示从定义能力到以 Web 服务运行的 A2A 智能体构建流程。借助 Agent Card 与 ADK，开发者可构建可与 Google 日历等工具集成的可互操作智能体，体现 A2A 在多智能体生态中的应用。

Further exploration of A2A is recommended through the code demonstration at [https://www.trickle.so/blog/how-to-build-google-a2a-project](https://www.trickle.so/blog/how-to-build-google-a2a-project). Resources available at this link include sample A2A clients and servers in Python and JavaScript, multi-agent web applications, command-line interfaces, and example implementations for various agent frameworks.

> 建议通过 [https://www.trickle.so/blog/how-to-build-google-a2a-project](https://www.trickle.so/blog/how-to-build-google-a2a-project) 的代码演示进一步探索 A2A；该链接提供 Python/JavaScript 的 A2A 客户端与服务端样例、多智能体 Web 应用、CLI 以及多种智能体框架的实现示例。

## At a Glance

> ## 速览

**What:** Individual AI agents, especially those built on different frameworks, often struggle with complex, multi-faceted problems on their own. The primary challenge is the lack of a common language or protocol that allows them to communicate and collaborate effectively. This isolation prevents the creation of sophisticated systems where multiple specialized agents can combine their unique skills to solve larger tasks. Without a standardized approach, integrating these disparate agents is costly, time-consuming, and hinders the development of more powerful, cohesive AI solutions.

> **是什么：** 单个 AI 智能体，尤其是基于不同框架构建时，往往难以独自应对复杂多面问题；主要挑战是缺乏通用语言或协议以实现有效通信与协作。这种隔离阻碍构建多专精智能体合力解决更大任务的复杂系统；没有标准化方法时，集成异构智能体成本高、耗时长，并制约更强大、内聚的 AI 方案发展。

**Why:** The Inter-Agent Communication (A2A) protocol provides an open, standardized solution for this problem. It is an HTTP-based protocol that enables interoperability, allowing distinct AI agents to coordinate, delegate tasks, and share information seamlessly, regardless of their underlying technology. A core component is the Agent Card, a digital identity file that describes an agent's capabilities, skills, and communication endpoints, facilitating discovery and interaction. A2A defines various interaction mechanisms, including synchronous and asynchronous communication, to support diverse use cases. By creating a universal standard for agent collaboration, A2A fosters a modular and scalable ecosystem for building complex, multi-agent Agentic systems.

> **为什么：** 智能体间通信（A2A）协议为此提供开放、标准化的方案。它是基于 HTTP 的协议，实现互操作性，使不同智能体无论底层技术如何都能协调、委派任务并无缝共享信息。核心是 Agent Card——描述能力、技能与通信端点的数字身份文件，便于发现与交互。A2A 定义同步与异步等多种交互机制以覆盖多样用例；通过统一协作标准，促进构建复杂多智能体智能系统的模块化、可扩展生态。

**Rule of Thumb:** Use this pattern when you need to orchestrate collaboration between two or more AI agents, especially if they are built using different frameworks (e.g., Google ADK, LangGraph, CrewAI). It is ideal for building complex, modular applications where specialized agents handle specific parts of a workflow, such as delegating data analysis to one agent and report generation to another. This pattern is also essential when an agent needs to dynamically discover and consume the capabilities of other agents to complete a task.

> **经验法则：** 当需要编排两个及以上 AI 智能体的协作，尤其它们基于不同框架（如 Google ADK、LangGraph、CrewAI）时，宜采用本模式。适合构建复杂模块化应用：专精智能体负责工作流片段，例如将数据分析委派给一智能体、报告生成委派给另一智能体。当某智能体需动态发现并调用其他智能体能力以完成任务时，本模式也必不可少。

**Visual Summary:**

> **图示摘要：**

![A2A Inter-Agent Communication Pattern](../assets-new/A2A_Inter-Agent_Communication_Pattern.png)

Fig.2: A2A inter-agent communication pattern

> 图 2：A2A 智能体间通信模式

## Key Takeaways

> ## 要点

Key Takeaways:

> 要点：

* The Google A2A protocol is an open, HTTP-based standard that facilitates communication and collaboration between AI agents built with different frameworks.  
* An AgentCard serves as a digital identifier for an agent, allowing for automatic discovery and understanding of its capabilities by other agents.  
* A2A offers both synchronous request-response interactions (using `tasks/send`) and streaming updates (using `tasks/sendSubscribe`) to accommodate varying communication needs.  
* The protocol supports multi-turn conversations, including an `input-required` state, which allows agents to request additional information and maintain context during interactions.  
* A2A encourages a modular architecture where specialized agents can operate independently on different ports, enabling system scalability and distribution.  
* Tools such as Trickle AI aid in visualizing and tracking A2A communications, which helps developers monitor, debug, and optimize multi-agent systems.  
* While A2A is a high-level protocol for managing tasks and workflows between different agents, the Model Context Protocol (MCP) provides a standardized interface for LLMs to interface with external resources

> * 谷歌 A2A 协议是开放的、基于 HTTP 的标准，促进不同框架构建的 AI 智能体之间的通信与协作。  
> * AgentCard 作为智能体的数字标识，使其他智能体能自动发现并理解其能力。  
> * A2A 同时提供同步请求-响应（`tasks/send`）与流式更新（`tasks/sendSubscribe`），以满足不同通信需求。  
> * 协议支持多轮对话，含 `input-required` 状态，使智能体可请求补充信息并在交互中保持上下文。  
> * A2A 鼓励模块化架构：专精智能体可在不同端口独立运行，便于扩展与分布式部署。  
> * Trickle AI 等工具有助于可视化与追踪 A2A 通信，便于监控、调试与优化多智能体系统。  
> * A2A 是管理不同智能体间任务与工作流的高层协议；模型上下文协议（MCP）则为 LLM 对接外部资源提供标准化接口。

## Conclusions

> ## 结论

The Inter-Agent Communication (A2A) protocol establishes a vital, open standard to overcome the inherent isolation of individual AI agents. By providing a common HTTP-based framework, it ensures seamless collaboration and interoperability between agents built on different platforms, such as Google ADK, LangGraph, or CrewAI. A core component is the Agent Card, which serves as a digital identity, clearly defining an agent's capabilities and enabling dynamic discovery by other agents. The protocol's flexibility supports various interaction patterns, including synchronous requests, asynchronous polling, and real-time streaming, catering to a wide range of application needs.

> 智能体间通信（A2A）协议建立了一项重要的开放标准，以克服单个 AI 智能体的固有孤立。通过共同的 HTTP 框架，它保障基于 Google ADK、LangGraph、CrewAI 等不同平台的智能体之间的无缝协作与互操作性。核心是 Agent Card，作为数字身份清晰定义能力并支持被其他智能体动态发现。协议的灵活性覆盖同步请求、异步轮询与实时流式等多种交互模式，适配广泛的应用需求。

This enables the creation of modular and scalable architectures where specialized agents can be combined to orchestrate complex automated workflows. Security is a fundamental aspect, with built-in mechanisms like mTLS and explicit authentication requirements to protect communications. While complementing other standards like MCP, A2A's unique focus is on the high-level coordination and task delegation between agents. The strong backing from major technology companies and the availability of practical implementations highlight its growing importance. This protocol paves the way for developers to build more sophisticated, distributed, and intelligent multi-agent systems. Ultimately, A2A is a foundational pillar for fostering an innovative and interoperable ecosystem of collaborative AI.

> 由此可构建模块化、可扩展的架构，组合专精智能体编排复杂自动化工作流。安全是根本：mTLS 与明确的认证要求等机制保护通信。在补充 MCP 等标准的同时，A2A 的独特焦点是智能体之间的高层协调与任务委派。大型科技公司的支持与可落地的实现凸显其日益重要。该协议为开发者构建更复杂、分布式、更智能的多智能体系统铺路；归根结底，A2A 是培育协作式 AI 创新与互操作生态的基石之一。

## References

1. Chen, B. (2025, April 22). *How to Build Your First Google A2A Project: A Step-by-Step Tutorial*. Trickle.so Blog. [https://www.trickle.so/blog/how-to-build-google-a2a-project](https://www.trickle.so/blog/how-to-build-google-a2a-project)
2. Google A2A GitHub Repository. [https://github.com/google-a2a/A2A](https://github.com/google-a2a/A2A)
3. Google Agent Development Kit (ADK) [https://google.github.io/adk-docs/](https://google.github.io/adk-docs/)
4. Getting Started with Agent-to-Agent (A2A) Protocol: [https://codelabs.developers.google.com/intro-a2a-purchasing-concierge\#0](https://codelabs.developers.google.com/intro-a2a-purchasing-concierge#0)
5. Google AgentDiscovery \- [https://a2a-protocol.org/latest/](https://a2a-protocol.org/latest/)
6. Communication between different AI frameworks such as LangGraph, CrewAI, and Google ADK [https://www.trickle.so/blog/how-to-build-google-a2a-project](https://www.trickle.so/blog/how-to-build-google-a2a-project#setting-up-your-a2a-development-environment)
7. Designing Collaborative Multi-Agent Systems with the A2A Protocol [https://www.oreilly.com/radar/designing-collaborative-multi-agent-systems-with-the-a2a-protocol/](https://www.oreilly.com/radar/designing-collaborative-multi-agent-systems-with-the-a2a-protocol/)
