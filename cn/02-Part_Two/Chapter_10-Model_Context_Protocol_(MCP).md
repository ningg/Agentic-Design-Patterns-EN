# Chapter 10: Model Context Protocol

> 第 10 章：模型上下文协议（MCP）

To enable LLMs to function effectively as agents, their capabilities must extend beyond multimodal generation. Interaction with the external environment is necessary, including access to current data, utilization of external software, and execution of specific operational tasks. The Model Context Protocol (MCP) addresses this need by providing a standardized interface for LLMs to interface with external resources. This protocol serves as a key mechanism to facilitate consistent and predictable integration.

> 要使 LLM 有效充当智能体，能力须超越多模态生成；必须与外部环境交互——获取最新数据、使用外部软件、执行具体操作。模型上下文协议（MCP）通过为 LLM 连接外部资源提供标准化接口来满足这一需求；该协议是实现一致、可预测集成的关键机制。

## MCP Pattern Overview

> ## MCP 模式概览

Imagine a universal adapter that allows any LLM to plug into any external system, database, or tool without a custom integration for each one. That's essentially what the Model Context Protocol (MCP) is. It's an open standard designed to standardize how LLMs like Gemini, OpenAI's GPT models, Mixtral, and Claude communicate with external applications, data sources, and tools. Think of it as a universal connection mechanism that simplifies how LLMs obtain context, execute actions, and interact with various systems.

> 想象一种通用适配器，让任意 LLM 无需为每个系统单独集成即可接入外部系统、数据库或工具——这本质上就是 MCP。它是开放标准，旨在统一 Gemini、OpenAI GPT、Mixtral、Claude 等 LLM 与外部应用、数据源和工具的通信方式；可视为简化 LLM 获取上下文、执行动作并与各系统交互的通用连接机制。

MCP operates on a client-server architecture. It defines how different elements—data (referred to as resources), interactive templates (which are essentially prompts), and actionable functions (known as tools)—are exposed by an MCP server. These are then consumed by an MCP client, which could be an LLM host application or an AI agent itself. This standardized approach dramatically reduces the complexity of integrating LLMs into diverse operational environments.

> MCP 采用客户端—服务器架构：规定数据（称为 resources）、交互模板（实质为 prompts）与可执行函数（称为 tools）如何由 MCP 服务器暴露，再由 MCP 客户端（可为 LLM 宿主应用或 AI 智能体本身）消费。这种标准化显著降低将 LLM 集成到多样运行环境的复杂度。

However, MCP is a contract for an "agentic interface," and its effectiveness depends heavily on the design of the underlying APIs it exposes. There is a risk that developers simply wrap pre-existing, legacy APIs without modification, which can be suboptimal for an agent. For example, if a ticketing system's API only allows retrieving full ticket details one by one, an agent asked to summarize high-priority tickets will be slow and inaccurate at high volumes. To be truly effective, the underlying API should be improved with deterministic features like filtering and sorting to help the non-deterministic agent work efficiently. This highlights that agents do not magically replace deterministic workflows; they often require stronger deterministic support to succeed.

> 然而，MCP 只是「智能体接口」的契约，成效很大程度上取决于其暴露的底层 API 设计。风险在于开发者仅原封不动封装遗留 API，对智能体未必合适。例如工单系统 API 若只能逐条拉取完整工单，要在高并发下总结高优先级工单就会又慢又不准。要真正有效，底层 API 应增强过滤、排序等确定性能力，辅助非确定性的智能体高效工作。这说明智能体并不会魔法般取代确定性工作流；它们往往更需要更强的确定性支撑才能成功。

Furthermore, MCP can wrap an API whose input or output is still not inherently understandable by the agent. An API is only useful if its data format is agent-friendly, a guarantee that MCP itself does not enforce. For instance, creating an MCP server for a document store that returns files as PDFs is mostly useless if the consuming agent cannot parse PDF content. The better approach would be to first create an API that returns a textual version of the document, such as Markdown, which the agent can actually read and process. This demonstrates that developers must consider not just the connection, but the nature of the data being exchanged to ensure true compatibility.

> 此外，MCP 可包装输入/输出仍非智能体天然可理解的 API；只有数据格式对智能体友好，API 才有用，而 MCP 本身并不保证这一点。例如文档库 MCP 若返回 PDF，而消费端智能体不能解析 PDF，则几乎无用。更好做法是提供返回 Markdown 等文本形态的 API，使智能体能读能处理。这表明开发者须同时考虑连接与交换数据的形态，以确保真正兼容。

## MCP vs. Tool Function Calling

> ## MCP 与工具函数调用

The Model Context Protocol (MCP) and tool function calling are distinct mechanisms that enable LLMs to interact with external capabilities (including tools) and execute actions. While both serve to extend LLM capabilities beyond text generation, they differ in their approach and level of abstraction.

> MCP 与工具函数调用是两种不同的机制，都使 LLM 能与外部能力（含工具）交互并执行动作；二者都扩展 LLM 超越纯文本生成的能力，但在方法与抽象层次上不同。

Tool function calling can be thought of as a direct request from an LLM to a specific, pre-defined tool or function. Note that in this context we use the words "tool" and "function” interchangeably. This interaction is characterized by a one-to-one communication model, where the LLM formats a request based on its understanding of a user's intent requiring external action. The application code then executes this request and returns the result to the LLM. This process is often proprietary and varies across different LLM providers.

> 工具函数调用可视为 LLM 对特定预定义工具/函数的直接请求；此处「tool」与「function」混用。其特征是一对一通信：LLM 根据对用户需外部行动的理解格式化请求，应用代码执行后把结果返回 LLM。该过程常为专有实现，随提供商而异。

In contrast, the Model Context Protocol (MCP) operates as a standardized interface for LLMs to discover, communicate with, and utilize external capabilities. It functions as an open protocol that facilitates interaction with a wide range of tools and systems, aiming to establish an ecosystem where any compliant tool can be accessed by any compliant LLM. This fosters interoperability, composability and reusability across different systems and implementations. By adopting a federated model, we significantly improve interoperability and unlock the value of existing assets. This strategy allows us to bring disparate and legacy services into a modern ecosystem simply by wrapping them in an MCP-compliant interface. These services continue to operate independently, but can now be composed into new applications and workflows, with their collaboration orchestrated by LLMs. This fosters agility and reusability without requiring costly rewrites of foundational systems.

> 相比之下，MCP 作为标准化接口，供 LLM 发现、通信并利用外部能力；它是开放协议，促进与广泛工具与系统交互，目标建立「任意合规工具可被任意合规 LLM 访问」的生态，提升互操作、组合与复用。采用联邦模型可显著改善互操作性并释放存量资产价值：用 MCP 合规接口包裹异构与遗留服务即可纳入现代生态；服务仍独立运行，但可被组合进新应用与工作流，由 LLM 编排协作，在不必昂贵重写基础系统的前提下获得敏捷与复用。

Here's a breakdown of the fundamental distinctions between MCP and tool function calling:

> MCP 与工具函数调用的基本区别如下：

| Feature | Tool Function Calling | Model Context Protocol (MCP) |
| ----- | ----- | ----- |
| **Standardization** | Proprietary and vendor-specific. The format and implementation differ across LLM providers. | An open, standardized protocol, promoting interoperability between different LLMs and tools. |
| **Scope** | A direct mechanism for an LLM to request the execution of a specific, predefined function. | A broader framework for how LLMs and external tools discover and communicate with each other. |
| **Architecture** | A one-to-one interaction between the LLM and the application's tool-handling logic. | A client-server architecture where LLM-powered applications (clients) can connect to and utilize various MCP servers (tools). |
| **Discovery** | The LLM is explicitly told which tools are available within the context of a specific conversation. | Enables dynamic discovery of available tools. An MCP client can query a server to see what capabilities it offers. |
| **Reusability** | Tool integrations are often tightly coupled with the specific application and LLM being used. | Promotes the development of reusable, standalone "MCP servers" that can be accessed by any compliant application. |

> | 特性 | 工具函数调用 | 模型上下文协议（MCP） |
> | ----- | ----- | ----- |
> | **标准化** | 专有、因厂商而异；格式与实现随 LLM 提供商不同。 | 开放标准化协议，促进不同 LLM 与工具互操作。 |
> | **范围** | LLM 请求执行特定预定义函数的直接机制。 | LLM 与外部工具如何发现与通信的更广泛框架。 |
> | **架构** | LLM 与应用内工具处理逻辑的一对一交互。 | 客户端—服务器架构：LLM 应用（客户端）连接并使用多个 MCP 服务器（工具）。 |
> | **发现** | 在特定对话上下文中显式告知 LLM 有哪些工具。 | 支持动态发现；MCP 客户端可查询服务器能力清单。 |
> | **复用性** | 集成常与特定应用和 LLM 紧耦合。 | 促进可复用、独立的「MCP 服务器」，任意合规应用可访问。 |

Think of tool function calling as giving an AI a specific set of custom-built tools, like a particular wrench and screwdriver. This is efficient for a workshop with a fixed set of tasks. MCP (Model Context Protocol), on the other hand, is like creating a universal, standardized power outlet system. It doesn't provide the tools itself, but it allows any compliant tool from any manufacturer to plug in and work, enabling a dynamic and ever-expanding workshop.

> 工具函数调用好比给 AI 一套定制扳手与螺丝刀，适合任务固定的车间；MCP 则像统一标准的电源插座系统——本身不提供工具，但让任意厂商的合规设备即插即用，构成动态扩展的车间。

In short, function calling provides direct access to a few specific functions, while MCP is the standardized communication framework that lets LLMs discover and use a vast range of external resources. For simple applications, specific tools are enough; for complex, interconnected AI systems that need to adapt, a universal standard like MCP is essential.

> 简言之，函数调用提供对少数特定函数的直接访问；MCP 则是让 LLM 发现并使用大量外部资源的标准化通信框架。简单应用专用工具即可；复杂、互联且需适应的 AI 系统则离不开 MCP 这类通用标准。

## Additional considerations for MCP

> ## MCP 的额外考量

While MCP presents a powerful framework, a thorough evaluation requires considering several crucial aspects that influence its suitability for a given use case. Let's see some aspects in more details:

> MCP 虽是强大框架，全面评估仍需考量影响其是否适合具体用例的若干要点。下面稍细说明：

* **Tool vs. Resource vs. Prompt**: It's important to understand the specific roles of these components. A resource is static data (e.g., a PDF file, a database record). A tool is an executable function that performs an action (e.g., sending an email, querying an API). A prompt is a template that guides the LLM in how to interact with a resource or tool, ensuring the interaction is structured and effective.  
* **Discoverability**: A key advantage of MCP is that an MCP client can dynamically query a server to learn what tools and resources it offers. This "just-in-time" discovery mechanism is powerful for agents that need to adapt to new capabilities without being redeployed.  
* **Security**: Exposing tools and data via any protocol requires robust security measures. An MCP implementation must include authentication and authorization to control which clients can access which servers and what specific actions they are permitted to perform.  
* **Implementation**: While MCP is an open standard, its implementation can be complex. However, providers are beginning to simplify this process. For example, some model providers like Anthropic or FastMCP offer SDKs that abstract away much of the boilerplate code, making it easier for developers to create and connect MCP clients and servers.  
* **Error Handling**: A comprehensive error-handling strategy is critical. The protocol must define how errors (e.g., tool execution failure, unavailable server, invalid request) are communicated back to the LLM so it can understand the failure and potentially try an alternative approach.  
* **Local vs. Remote Server**: MCP servers can be deployed locally on the same machine as the agent or remotely on a different server. A local server might be chosen for speed and security with sensitive data, while a remote server architecture allows for shared, scalable access to common tools across an organization.  
* **On-demand vs. Batch**: MCP can support both on-demand, interactive sessions and larger-scale batch processing. The choice depends on the application, from a real-time conversational agent needing immediate tool access to a data analysis pipeline that processes records in batches.  
* **Transportation Mechanism**: The protocol also defines the underlying transport layers for communication. For local interactions, it uses JSON-RPC over STDIO (standard input/output) for efficient inter-process communication. For remote connections, it leverages web-friendly protocols like Streamable HTTP and Server-Sent Events (SSE) to enable persistent and efficient client-server communication.

> * **Tool / Resource / Prompt：** 须分清角色——resource 多为静态数据（如 PDF、数据库记录）；tool 为可执行动作（如发邮件、调 API）；prompt 为引导 LLM 如何与 resource/tool 交互的模板，使交互结构化、有效。  
> * **可发现性：** MCP 客户端可动态查询服务器提供的工具与资源；这种「即时」发现对需在不重部署的情况下适应新能力的智能体很有力。  
> * **安全：** 经任意协议暴露工具与数据都需强安全措施；MCP 实现须含认证与授权，控制谁能连哪些服务器、允许哪些操作。  
> * **实现：** MCP 虽开放，实现可较复杂；提供商正简化流程，如 Anthropic、FastMCP 等提供 SDK 封装样板代码，便于创建与连接客户端/服务器。  
> * **错误处理：** 须有完整策略；协议须规定如何把错误（工具执行失败、服务不可用、非法请求等）传回 LLM，使其理解失败并可能换路。  
> * **本地 vs 远程服务器：** 可与智能体同机本地部署，也可远程；本地利于速度与敏感数据安全，远程利于组织内共享、可扩展访问通用工具。  
> * **按需 vs 批处理：** MCP 可支持交互式按需会话与大规模批处理；视应用而定——从需即时工具访问的对话智能体到批量处理记录的分析流水线。  
> * **传输机制：** 协议定义底层传输；本地交互常用 STDIO 上的 JSON-RPC 做进程间通信；远程则可用 Streamable HTTP、SSE 等 Web 友好协议实现持久、高效的客户端—服务器通信。

The Model Context Protocol uses a client-server model to standardize information flow. Understanding component interaction is key to MCP's advanced agentic behavior:

> MCP 用客户端—服务器模型标准化信息流。理解组件交互是掌握其高级智能体行为的关键：

1. **Large Language Model (LLM)**: The core intelligence. It processes user requests, formulates plans, and decides when it needs to access external information or perform an action.  
2. **MCP Client**: This is an application or wrapper around the LLM. It acts as the intermediary, translating the LLM's intent into a formal request that conforms to the MCP standard. It is responsible for discovering, connecting to, and communicating with MCP Servers.  
3. **MCP Server**: This is the gateway to the external world. It exposes a set of tools, resources, and prompts to any authorized MCP Client. Each server is typically responsible for a specific domain, such as a connection to a company's internal database, an email service, or a public API.  
4. ​​**Optional Third-Party (3P) Service:** This represents the actual external tool, application, or data source that the MCP Server manages and exposes. It is the ultimate endpoint that performs the requested action, such as querying a proprietary database, interacting with a SaaS platform, or calling a public weather API.

> 1. **大语言模型（LLM）：** 核心智能；处理用户请求、制定计划、决定何时需外部信息或执行动作。  
> 2. **MCP 客户端：** 围绕 LLM 的应用或包装层；作中介，将 LLM 意图译为符合 MCP 的正式请求；负责发现、连接并与 MCP 服务器通信。  
> 3. **MCP 服务器：** 通向外部世界的网关；向授权客户端暴露 tools、resources、prompts；通常每服务器负责一域，如内网数据库、邮件服务或公共 API。  
> 4. **可选第三方（3P）服务：** MCP 服务器管理并暴露的实际外部工具、应用或数据源；是最终执行动作的端点，如查专有库、操作 SaaS、调天气 API 等。

The interaction flows as follows:

> 交互流程如下：

1. **Discovery**: The MCP Client, on behalf of the LLM, queries an MCP Server to ask what capabilities it offers. The server responds with a manifest listing its available tools (e.g., send_email), resources (e.g., customer_database), and prompts.  
2. **Request Formulation**: The LLM determines that it needs to use one of the discovered tools. For instance, it decides to send an email. It formulates a request, specifying the tool to use (send_email) and the necessary parameters (recipient, subject, body).  
3. **Client Communication**: The MCP Client takes the LLM's formulated request and sends it as a standardized call to the appropriate MCP Server.  
4. **Server Execution**: The MCP Server receives the request. It authenticates the client, validates the request, and then executes the specified action by interfacing with the underlying software (e.g., calling the send() function of an email API).  
5. **Response and Context Update**: After execution, the MCP Server sends a standardized response back to the MCP Client. This response indicates whether the action was successful and includes any relevant output (e.g., a confirmation ID for the sent email). The client then passes this result back to the LLM, updating its context and enabling it to proceed with the next step of its task.

> 1. **发现：** 客户端代表 LLM 查询 MCP 服务器能力；服务器返回清单，列 tools（如 send_email）、resources（如 customer_database）、prompts 等。  
> 2. **请求构造：** LLM 决定使用某已发现工具（如发邮件），构造请求：指定工具（send_email）与参数（收件人、主题、正文）。  
> 3. **客户端通信：** 客户端将 LLM 构造的请求作为标准化调用发给对应 MCP 服务器。  
> 4. **服务器执行：** 服务器收请求后认证客户端、校验请求，再通过底层软件执行指定动作（如调用邮件 API 的 send()）。  
> 5. **响应与上下文更新：** 执行后服务器向客户端返回标准化响应，表明成功与否及输出（如邮件确认 ID）；客户端将结果回传 LLM，更新上下文以继续下一步。

## Practical Applications & Use Cases

> ## 实践应用与用例

MCP significantly broadens AI/LLM capabilities, making them more versatile and powerful. Here are nine key use cases:

> MCP 显著扩展 AI/LLM 能力，使其更通用、更强。以下是九个关键用例：

* **Database Integration:** MCP allows LLMs and agents to seamlessly access and interact with structured data in databases. For instance, using the MCP Toolbox for Databases, an agent can query Google BigQuery datasets to retrieve real-time information, generate reports, or update records, all driven by natural language commands.  
* **Generative Media Orchestration:** MCP enables agents to integrate with advanced generative media services. Through MCP Tools for Genmedia Services, an agent can orchestrate workflows involving Google's Imagen for image generation, Google's Veo for video creation, Google's Chirp 3 HD for realistic voices, or Google's Lyria for music composition, allowing for dynamic content creation within AI applications.  
* **External API Interaction:** MCP provides a standardized way for LLMs to call and receive responses from any external API. This means an agent can fetch live weather data, pull stock prices, send emails, or interact with CRM systems, extending its capabilities far beyond its core language model.  
* **Reasoning-Based Information Extraction:** Leveraging an LLM's strong reasoning skills, MCP facilitates effective, query-dependent information extraction that surpasses conventional search and retrieval systems. Instead of a traditional search tool returning an entire document, an agent can analyze the text and extract the precise clause, figure, or statement that directly answers a user's complex question.  
* **Custom Tool Development:** Developers can build custom tools and expose them via an MCP server (e.g., using FastMCP). This allows specialized internal functions or proprietary systems to be made available to LLMs and other agents in a standardized, easily consumable format, without needing to modify the LLM directly.  
* **Standardized LLM-to-Application Communication:** MCP ensures a consistent communication layer between LLMs and the applications they interact with. This reduces integration overhead, promotes interoperability between different LLM providers and host applications, and simplifies the development of complex agentic systems.  
* **Complex Workflow Orchestration:** By combining various MCP-exposed tools and data sources, agents can orchestrate highly complex, multi-step workflows. An agent could, for example, retrieve customer data from a database, generate a personalized marketing image, draft a tailored email, and then send it, all by interacting with different MCP services.  
* **IoT Device Control:** MCP can facilitate LLM interaction with Internet of Things (IoT) devices. An agent could use MCP to send commands to smart home appliances, industrial sensors, or robotics, enabling natural language control and automation of physical systems.  
* **Financial Services Automation:** In financial services, MCP could enable LLMs to interact with various financial data sources, trading platforms, or compliance systems. An agent might analyze market data, execute trades, generate personalized financial advice, or automate regulatory reporting, all while maintaining secure and standardized communication.

> * **数据库集成：** 使 LLM/智能体无缝访问并操作数据库中的结构化数据；例如用 MCP Toolbox for Databases，智能体可用自然语言查 BigQuery、生成报表或更新记录。  
> * **生成式媒体编排：** 与先进生成式媒体服务集成；通过 Genmedia 的 MCP 工具，可编排 Imagen（图）、Veo（视频）、Chirp 3 HD（语音）、Lyria（音乐）等工作流，在 AI 应用内动态创作内容。  
> * **外部 API 交互：** 标准化调用任意外部 API 并接收响应；智能体可拉天气、股价、发邮件、操作 CRM 等，远超核心语言模型本身。  
> * **基于推理的信息抽取：** 利用 LLM 推理能力，实现依赖查询的有效信息抽取，超越传统「整篇返回」的检索；智能体可分析文本并抽出直接回答复杂问题的条款、图表或陈述。  
> * **自定义工具开发：** 开发者可自建工具并通过 MCP 服务器暴露（如 FastMCP）；内部专用函数或专有系统以标准、易消费格式提供给 LLM/智能体，无需改模型本身。  
> * **LLM 与应用通信标准化：** 在 LLM 与其应用间提供一致通信层，降低集成成本、促进不同模型与宿主应用互操作，简化复杂智能体系统开发。  
> * **复杂工作流编排：** 组合多种 MCP 暴露的工具与数据源，编排高复杂多步流程；例如从库中取客户数据、生成个性化营销图、起草定制邮件并发送，分别调用不同 MCP 服务。  
> * **物联网设备控制：** 促进 LLM 与 IoT 交互；智能体可通过 MCP 向智能家居、工业传感器或机器人发令，实现自然语言控制与物理系统自动化。  
> * **金融服务自动化：** 使 LLM 与金融数据源、交易平台或合规系统交互；可分析行情、执行交易、生成个性化理财建议或自动化监管报送，并保持安全、标准化通信。

In short, the Model Context Protocol (MCP) enables agents to access real-time information from databases, APIs, and web resources. It also allows agents to perform actions like sending emails, updating records, controlling devices, and executing complex tasks by integrating and processing data from various sources. Additionally, MCP supports media generation tools for AI applications.

> 简言之，MCP 使智能体能从数据库、API 与网络资源获取实时信息，并能发邮件、更新记录、控制设备、通过整合多源数据执行复杂任务；同时支持 AI 应用中的媒体生成工具。

## Hands-On Code Example with ADK

> ## 使用 ADK 的动手代码示例

This section outlines how to connect to a local MCP server that provides file system operations, enabling an ADK  agent to interact with the local file system.

> 本节说明如何连接提供文件系统操作的本地 MCP 服务器，使 ADK 智能体能与本地文件系统交互。

### Agent Setup with MCPToolset

> ### 使用 MCPToolset 配置智能体

To configure an agent for file system interaction, an `agent.py` file must be created (e.g., at `./adk_agent_samples/mcp_agent/agent.py`). The `MCPToolset` is instantiated within the `tools` list of the `LlmAgent` object. It is crucial to replace `"/path/to/your/folder"` in the `args` list with the absolute path to a directory on the local system that the MCP server can access. This directory will be the root for the file system operations performed by the agent.

> 要配置文件交互智能体，需创建 `agent.py`（例如 `./adk_agent_samples/mcp_agent/agent.py`）。在 `LlmAgent` 的 `tools` 列表中实例化 `MCPToolset`。务必把 `args` 中的 `"/path/to/your/folder"` 换成本地 MCP 服务器可访问目录的**绝对路径**；该目录将作为智能体文件操作的根。

```python
import os

from google.adk.agents import LlmAgent
from google.adk.tools.mcp_tool.mcp_toolset import MCPToolset, StdioServerParameters


# Create a reliable absolute path to a folder named 'mcp_managed_files'
# within the same directory as this agent script.
# This ensures the agent works out-of-the-box for demonstration.
# For production, you would point this to a more persistent and secure location.
TARGET_FOLDER_PATH = os.path.join(
    os.path.dirname(os.path.abspath(__file__)),
    "mcp_managed_files",
)

# Ensure the target directory exists before the agent needs it.
os.makedirs(TARGET_FOLDER_PATH, exist_ok=True)

root_agent = LlmAgent(
    model="gemini-2.0-flash",
    name="filesystem_assistant_agent",
    instruction=(
        "Help the user manage their files. You can list files, read files, and write files. "
        f"You are operating in the following directory: {TARGET_FOLDER_PATH}"
    ),
    tools=[
        MCPToolset(
            connection_params=StdioServerParameters(
                command="npx",
                args=[
                    "-y",  # Argument for npx to auto-confirm install
                    "@modelcontextprotocol/server-filesystem",
                    # This MUST be an absolute path to a folder.
                    TARGET_FOLDER_PATH,
                ],
            ),
            # Optional: You can filter which tools from the MCP server are exposed.
            # For example, to only allow reading:
            # tool_filter=['list_directory', 'read_file']
        )
    ],
)
```

`npx` (Node Package Execute), bundled with npm (Node Package Manager) versions 5.2.0 and later, is a utility that enables direct execution of Node.js packages from the npm registry. This eliminates the need for global installation. In essence, `npx` serves as an npm package runner, and it is commonly used to run many community MCP servers, which are distributed as Node.js packages.

> `npx`（Node Package Execute）随 npm 5.2.0 及更高版本提供，可直接从 npm 注册表运行 Node 包，无需全局安装；本质上它是 npm 的包运行器，常用于运行以 Node 包形式分发的社区 MCP 服务器。

Creating an `__init__.py` file is necessary to ensure the agent.py file is recognized as part of a discoverable Python package for the Agent Development Kit (ADK). This file should reside in the same directory as [agent.py](http://agent.py).

> 需创建 `__init__.py`，使 `agent.py` 被 ADK 识别为可发现 Python 包的一部分；该文件应与 [agent.py](http://agent.py) 同目录。

```python
# ./adk_agent_samples/mcp_agent/__init__.py 
from . import agent
```

Certainly, other supported commands are available for use. For example, connecting to python3 can be achieved as follows:

> 当然还可使用其他受支持命令。例如可如下连接 `python3`：

```python
connection_params = StdioConnectionParams(
    server_params={
        "command": "python3",
        "args": ["./agent/mcp_server.py"],
        "env": {
            "SERVICE_ACCOUNT_PATH": SERVICE_ACCOUNT_PATH,
            "DRIVE_FOLDER_ID": DRIVE_FOLDER_ID,
        },
    }
)
```

UVX, in the context of Python, refers to a command-line tool that utilizes uv to execute commands in a temporary, isolated Python environment. Essentially, it allows you to run Python tools and packages without needing to install them globally or within your project's environment. You can run it via the MCP server.

> 在 Python 语境下，UVX 指用 `uv` 在临时隔离环境中执行命令的 CLI 工具；可在不全局安装、也不装入项目环境的情况下运行 Python 工具与包；可通过 MCP 服务器调用。

```python
connection_params = StdioConnectionParams(
    server_params={
        "command": "uvx",
        "args": ["mcp-google-sheets@latest"],
        "env": {
            "SERVICE_ACCOUNT_PATH": SERVICE_ACCOUNT_PATH,
            "DRIVE_FOLDER_ID": DRIVE_FOLDER_ID,
        },
    }
)
```

Once the MCP Server is created, the next step is to connect to it.

> MCP 服务器创建后，下一步是连接它。

## Connecting the MCP Server with ADK Web

> ## 用 ADK Web 连接 MCP 服务器

To begin, execute 'adk web'. Navigate to the parent directory of mcp_agent (e.g., adk_agent_samples) in your terminal and run:

> 首先执行 `adk web`。在终端进入 `mcp_agent` 的父目录（如 `adk_agent_samples`）并运行：

```python
cd ./adk_agent_samples # Or your equivalent parent directory 
adk web
```

Once the ADK Web UI has loaded in your browser, select the `filesystem_assistant_agent` from the agent menu. Next, experiment with prompts such as:

> ADK Web UI 在浏览器加载后，在智能体菜单中选择 `filesystem_assistant_agent`，可尝试如下提示：

* "Show me the contents of this folder."  
* "Read the `sample.txt` file." (This assumes `sample.txt` is located at `TARGET_FOLDER_PATH`.)  
* "What's in `another_file.md`?"

> * 「显示此文件夹内容。」  
> * 「读取 `sample.txt`。」（假定该文件在 `TARGET_FOLDER_PATH`。）  
> * 「`another_file.md` 里有什么？」

## Creating an MCP Server with FastMCP

> ## 用 FastMCP 创建 MCP 服务器

FastMCP is a high-level Python framework designed to streamline the development of MCP servers. It provides an abstraction layer that simplifies protocol complexities, allowing developers to focus on core logic.

> FastMCP 是用于简化 MCP 服务器开发的高级 Python 框架；提供抽象层以简化协议细节，使开发者聚焦核心逻辑。

The library enables rapid definition of tools, resources, and prompts using simple Python decorators. A significant advantage is its automatic schema generation, which intelligently interprets Python function signatures, type hints, and documentation strings to construct necessary AI model interface specifications. This automation minimizes manual configuration and reduces human error.

> 该库可用简单 Python 装饰器快速定义 tools、resources、prompts；一大优势是自动模式生成——根据函数签名、类型注解与文档字符串构建 AI 模型接口规范，减少手工配置与人为错误。

Beyond basic tool creation, FastMCP facilitates advanced architectural patterns like server composition and proxying. This enables modular development of complex, multi-component systems and seamless integration of existing services into an AI-accessible framework. Additionally, FastMCP includes optimizations for efficient, distributed, and scalable AI-driven applications.

> 除基础工具创建外，FastMCP 支持服务器组合、代理等高级架构模式，便于模块化开发复杂多组件系统，并将现有服务平滑接入 AI 可访问框架；并含面向高效、分布式、可扩展 AI 应用的优化。

## Server setup with FastMCP

> ## 用 FastMCP 搭建服务器

## To illustrate, consider a basic "greet" tool provided by the server. ADK agents and other MCP clients can interact with this tool using HTTP once it is active

> ## 举例：服务器提供基础 `greet` 工具；FastMCP 服务启动后，ADK 智能体与其他 MCP 客户端可通过 HTTP 调用该工具

```python
# fastmcp_server.py
# This script demonstrates how to create a simple MCP server using FastMCP.
# It exposes a single tool that generates a greeting.
# 1. Make sure you have FastMCP installed:
# pip install fastmcp

from fastmcp import FastMCP, Client


# Initialize the FastMCP server.
mcp_server = FastMCP()


# Define a simple tool function.
# The `@mcp_server.tool` decorator registers this Python function as an MCP tool.
# The docstring becomes the tool's description for the LLM.
@mcp_server.tool
def greet(name: str) -> str:
    """
    Generates a personalized greeting.

    Args:
        name: The name of the person to greet.

    Returns:
        A greeting string.
    """
    return f"Hello, {name}! Nice to meet you."


# Or if you want to run it from the script:
if __name__ == "__main__":
    mcp_server.run(
        transport="http",
        host="127.0.0.1",
        port=8000,
    )
```

This Python script defines a single function called greet, which takes a person's name and returns a personalized greeting. The @tool() decorator above this function automatically registers it as a tool that an AI or another program can use. The function's documentation string and type hints are used by FastMCP to tell the Agent how the tool works, what inputs it needs, and what it will return.

> 该脚本定义 `greet(name)`，返回个性化问候；`@mcp_server.tool` 将其注册为 AI 或其他程序可调用的工具；文档字符串与类型注解供 FastMCP 生成工具说明，告知智能体如何调用、需要何输入、返回何物。

When the script is executed, it starts the FastMCP server, which listens for requests on localhost:8000. This makes the greet function available as a network service. An  agent could then be configured to connect to this server and use the greet tool to generate greetings as part of a larger task. The server runs continuously until it is manually stopped.

> 运行脚本即启动 FastMCP 服务器，在 localhost:8000 监听请求，使 `greet` 成为网络服务；智能体可配置为连接该服务器并在更大任务中使用 `greet`。服务器持续运行直至手动停止。

## Consuming the FastMCP Server with an ADK Agent

> ## 用 ADK 智能体消费 FastMCP 服务器

An ADK agent can be set up as an MCP client to use a running FastMCP server. This requires configuring HttpServerParameters with the FastMCP server's network address, which is usually <http://localhost:8000>.

> ADK 智能体可配置为 MCP 客户端以使用已运行的 FastMCP 服务器；需用 `HttpServerParameters` 配置服务器地址，通常为 <http://localhost:8000>。

A `tool_filter` parameter can be included to restrict the agent's tool usage to specific tools offered by the server, such as 'greet'. When prompted with a request like "Greet John Doe," the agent's embedded LLM identifies the 'greet' tool available via MCP, invokes it with the argument "John Doe," and returns the server's response. This process demonstrates the integration of user-defined tools exposed through MCP with an ADK agent.

> 可使用 `tool_filter` 将智能体限制在服务器提供的特定工具（如 `greet`）。当用户说「向 John Doe 问好」时，内嵌 LLM 识别 MCP 上的 `greet` 并以参数调用，返回服务器响应；展示用户自定义 MCP 工具与 ADK 智能体的集成。

To establish this configuration, an agent file (e.g., agent.py located in ./adk_agent_samples/fastmcp_client_agent/) is required. This file will instantiate an ADK agent and use HttpServerParameters to establish a connection with the operational FastMCP server.

> 需准备智能体文件（如 `./adk_agent_samples/fastmcp_client_agent/agent.py`），实例化 ADK 智能体并用 `HttpServerParameters` 连接运行中的 FastMCP 服务器。

```python
# ./adk_agent_samples/fastmcp_client_agent/agent.py
import os

from google.adk.agents import LlmAgent
from google.adk.tools.mcp_tool.mcp_toolset import MCPToolset, HttpServerParameters


# Define the FastMCP server's address.
# Make sure your fastmcp_server.py (defined previously) is running on this port.
FASTMCP_SERVER_URL = "http://localhost:8000"

root_agent = LlmAgent(
    model="gemini-2.0-flash",  # Or your preferred model
    name="fastmcp_greeter_agent",
    instruction='You are a friendly assistant that can greet people by their name. Use the "greet" tool.',
    tools=[
        MCPToolset(
            connection_params=HttpServerParameters(
                url=FASTMCP_SERVER_URL,
            ),
            # Optional: Filter which tools from the MCP server are exposed
            # For this example, we're expecting only 'greet'
            tool_filter=["greet"],
        )
    ],
)
```

The script defines an Agent named `fastmcp_greeter_agent` that uses a Gemini language model. It's given a specific instruction to act as a friendly assistant whose purpose is to greet people. Crucially, the code equips this agent with a tool to perform its task. It configures an MCPToolset to connect to a separate server running on localhost:8000, which is expected to be the FastMCP server from the previous example. The agent is specifically granted access to the greet tool hosted on that server. In essence, this code sets up the client side of the system, creating an intelligent agent that understands its goal is to greet people and knows exactly which external tool to use to accomplish it.

> 脚本定义名为 `fastmcp_greeter_agent` 的智能体，使用 Gemini；指令为友好助手、按姓名问候他人。关键是配置 `MCPToolset` 连接 localhost:8000 上运行的 FastMCP 服务器（即前例），并仅暴露 `greet`。本质是搭建客户端：智能体明白目标是问候，并知用哪一外部工具完成。

Creating an `__init__.py` file within the `fastmcp_client_agent` directory is necessary. This ensures the agent is recognized as a discoverable Python package for the ADK.

> 须在 `fastmcp_client_agent` 目录创建 `__init__.py`，以便 ADK 将智能体识别为可发现包。

To begin, open a new terminal and run `python fastmcp_server.py` to start the FastMCP server. Next, go to the parent directory of `fastmcp_client_agent` (for example, `adk_agent_samples`) in your terminal and execute `adk web`. Once the ADK Web UI loads in your browser, select the `fastmcp_greeter_agent` from the agent menu. You can then test it by entering a prompt like "Greet John Doe." The agent will use the `greet` tool on your FastMCP server to create a response.

> 新开终端运行 `python fastmcp_server.py` 启动 FastMCP；再进入 `fastmcp_client_agent` 父目录（如 `adk_agent_samples`）执行 `adk web`；在 Web UI 中选 `fastmcp_greeter_agent`，输入如「Greet John Doe」测试；智能体会调用 FastMCP 上的 `greet` 生成回复。

## At a Glance

> ## 一览

**What:** To function as effective agents, LLMs must move beyond simple text generation. They require the ability to interact with the external environment to access current data and utilize external software. Without a standardized communication method, each integration between an LLM and an external tool or data source becomes a custom, complex, and non-reusable effort. This ad-hoc approach hinders scalability and makes building complex, interconnected AI systems difficult and inefficient.

> **问题：** 作为有效智能体，LLM 须超越简单文本生成，能与外部环境交互以获取最新数据并使用外部软件。若无标准化通信方式，每次与外部工具或数据源的集成都是定制、复杂且难复用的；这种临时拼凑阻碍扩展，使构建复杂互联 AI 系统困难低效。

**Why:** The Model Context Protocol (MCP) offers a standardized solution by acting as a universal interface between LLMs and external systems. It establishes an open, standardized protocol that defines how external capabilities are discovered and used. Operating on a client-server model, MCP allows servers to expose tools, data resources, and interactive prompts to any compliant client. LLM-powered applications act as these clients, dynamically discovering and interacting with available resources in a predictable manner. This standardized approach fosters an ecosystem of interoperable and reusable components, dramatically simplifying the development of complex agentic workflows.

> **思路：** MCP 作为 LLM 与外部系统之间的通用接口提供标准化解法；以开放协议定义如何发现与使用外部能力；在客户端—服务器模型下，服务器向任意合规客户端暴露 tools、数据资源与交互式 prompts，LLM 应用作为客户端可动态、可预期地发现与使用资源，培育可互操作、可复用组件生态，大幅简化复杂智能体工作流开发。

**Rule of thumb:** Use the Model Context Protocol (MCP) when building complex, scalable, or enterprise-grade agentic systems that need to interact with a diverse and evolving set of external tools, data sources, and APIs. It is ideal when interoperability between different LLMs and tools is a priority, and when agents require the ability to dynamically discover new capabilities without being redeployed. For simpler applications with a fixed and limited number of predefined functions, direct tool function calling may be sufficient.

> **经验法则：** 构建需与多样、演进中的外部工具、数据源和 API 交互的复杂、可扩展或企业级智能体系统时使用 MCP；当不同 LLM 与工具互操作是重点，且智能体需在不重部署的情况下动态发现新能力时尤为理想。若应用简单、仅固定少量预定义函数，直接工具函数调用可能足够。

**Visual summary:**

> **图示摘要：**

![Model Context Protocol](../assets-new/Model_Context_Protocol.png)

Fig.1: Model Context protocol

> 图 1：模型上下文协议

## Key Takeaways

> ## 要点

These are the key takeaways:

> 要点如下：

* The Model Context Protocol (MCP) is an open standard facilitating standardized communication between LLMs and external applications, data sources, and tools.  
* It employs a client-server architecture, defining the methods for exposing and consuming resources, prompts, and tools.  
* The Agent Development Kit (ADK) supports both utilizing existing MCP servers and exposing ADK tools via an MCP server.  
* FastMCP simplifies the development and management of MCP servers, particularly for exposing tools implemented in Python.  
* MCP Tools for Genmedia Services allows agents to integrate with Google Cloud's generative media capabilities (Imagen, Veo, Chirp 3 HD, Lyria).  
* MCP enables LLMs and agents to interact with real-world systems, access dynamic information, and perform actions beyond text generation.

> * MCP 是促进 LLM 与外部应用、数据源和工具标准化通信的开放标准。  
> * 采用客户端—服务器架构，规定如何暴露与消费 resources、prompts、tools。  
> * ADK 既支持使用现有 MCP 服务器，也支持通过 MCP 服务器暴露 ADK 工具。  
> * FastMCP 简化 MCP 服务器的开发与管理，尤适于用 Python 实现工具。  
> * Genmedia 的 MCP 工具使智能体能集成 Google Cloud 生成式媒体能力（Imagen、Veo、Chirp 3 HD、Lyria）。  
> * MCP 使 LLM/智能体能与现实系统交互、访问动态信息并执行超越文本生成的动作。

## Conclusion

> ## 结语

The Model Context Protocol (MCP) is an open standard that facilitates communication between Large Language Models (LLMs) and external systems. It employs a client-server architecture, enabling LLMs to access resources, utilize prompts, and execute actions through standardized tools. MCP allows LLMs to interact with databases, manage generative media workflows, control IoT devices, and automate financial services. Practical examples demonstrate setting up agents to communicate with MCP servers, including filesystem servers and servers built with FastMCP, illustrating its integration with the Agent Development Kit (ADK). MCP is a key component for developing interactive AI agents that extend beyond basic language capabilities.

> MCP 是促进 LLM 与外部系统通信的开放标准；采用客户端—服务器架构，使 LLM 能通过标准化 tools 访问 resources、使用 prompts 并执行动作。MCP 使 LLM 能操作数据库、编排生成式媒体工作流、控制 IoT、自动化金融服务等。实践示例展示如何配置智能体连接 MCP 服务器（含文件系统服务器与 FastMCP 搭建的服务器），说明其与 ADK 的集成。MCP 是开发超越基础语言能力的交互式 AI 智能体的关键组件。

## References

1. Model Context Protocol (MCP) Documentation. (Latest). *Model Context Protocol (MCP)*. [https://google.github.io/adk-docs/mcp/](https://google.github.io/adk-docs/mcp/)  
2. FastMCP Documentation. FastMCP. [https://github.com/jlowin/fastmcp](https://github.com/jlowin/fastmcp)  
3. MCP Tools for Genmedia Services. *MCP Tools for Genmedia Services*. [https://google.github.io/adk-docs/mcp/\#mcp-servers-for-google-cloud-genmedia](https://google.github.io/adk-docs/mcp/#mcp-servers-for-google-cloud-genmedia)  
4. MCP Toolbox for Databases Documentation. (Latest). *MCP Toolbox for Databases*. [https://google.github.io/adk-docs/mcp/databases/](https://google.github.io/adk-docs/mcp/databases/)
