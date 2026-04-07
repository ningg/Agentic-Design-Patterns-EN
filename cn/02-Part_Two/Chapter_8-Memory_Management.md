# Chapter 8: Memory Management

> 第 8 章：记忆管理

Effective memory management is crucial for intelligent agents to retain information. Agents require different types of memory, much like humans, to operate efficiently. This chapter delves into memory management, specifically addressing the immediate (short-term) and persistent (long-term) memory requirements of agents.

> 有效的记忆管理对智能体保留信息至关重要。智能体需要像人类一样多种类型的记忆才能高效运作。本章深入记忆管理，专门讨论即时（短期）与持久（长期）记忆需求。

In agent systems, memory refers to an agent's ability to retain and utilize information from past interactions, observations, and learning experiences. This capability allows agents to make informed decisions, maintain conversational context, and improve over time. Agent memory is generally categorized into two main types:

> 这使智能体能做知情决策、维持对话上下文并随时间改进。智能体记忆通常分为两大类：

* **Short-Term Memory (Contextual Memory):** Similar to working memory, this holds information currently being processed or recently accessed. For agents using large language models (LLMs), short-term memory primarily exists within the context window. This window contains recent messages, agent replies, tool usage results, and agent reflections from the current interaction, all of which inform the LLM's subsequent responses and actions. The context window has a limited capacity, restricting the amount of recent information an agent can directly access. Efficient short-term memory management involves keeping the most relevant information within this limited space, possibly through techniques like summarizing older conversation segments or emphasizing key details. The advent of models with 'long context' windows simply expands the size of this short-term memory, allowing more information to be held within a single interaction. However, this context is still ephemeral and is lost once the session concludes, and it can be costly and inefficient to process every time. Consequently, agents require separate memory types to achieve true persistence, recall information from past interactions, and build a lasting knowledge base.  
* **Long-Term Memory (Persistent Memory):** This acts as a repository for information agents need to retain across various interactions, tasks, or extended periods, akin to long-term knowledge bases. Data is typically stored outside the agent's immediate processing environment, often in databases, knowledge graphs, or vector databases. In vector databases, information is converted into numerical vectors and stored, enabling agents to retrieve data based on semantic similarity rather than exact keyword matches, a process known as semantic search. When an agent needs information from long-term memory, it queries the external storage, retrieves relevant data, and integrates it into the short-term context for immediate use, thus combining prior knowledge with the current interaction.

> * **短期记忆（情境记忆）：** 类似工作记忆，保存当前处理或最近访问的信息。对使用 LLM 的智能体，短期记忆主要在上下文窗口内：含近期消息、智能体回复、工具结果与当前轮反思等，驱动后续响应与动作。窗口容量有限；高效管理需保留最相关信息，可对旧对话摘要或突出要点。「长上下文」模型只是扩大这一短期记忆的容量，但会话结束仍会丢失，且每次全量处理可能昂贵低效，因此仍需其他记忆类型以实现真正持久、跨轮回忆与长期知识库。  
> * **长期记忆（持久记忆）：** 作为跨多轮交互、任务或长时段需保留信息的仓库，类似长期知识库；数据常存在智能体即时处理环境之外，如数据库、知识图谱或向量库。向量库将信息转为数值向量存储，支持按语义相似检索（语义搜索）。需要时智能体查询外部存储，取回相关数据并入短期上下文，把先验与当前交互结合。

## Practical Applications & Use Cases

> ## 实践应用与用例

Memory management is vital for agents to track information and perform intelligently over time. This is essential for agents to surpass basic question-answering capabilities. Applications include:

> 记忆管理对智能体跟踪信息、长期保持智能表现至关重要；要超越简单问答，离不开记忆。应用包括：

* **Chatbots and Conversational AI:** Maintaining conversation flow relies on short-term memory. Chatbots require remembering prior user inputs to provide coherent responses. Long-term memory enables chatbots to recall user preferences, past issues, or prior discussions, offering personalized and continuous interactions.  
* **Task-Oriented Agents:** Agents managing multi-step tasks need short-term memory to track previous steps, current progress, and overall goals. This information might reside in the task's context or temporary storage. Long-term memory is crucial for accessing specific user-related data not in the immediate context.  
* **Personalized Experiences:** Agents offering tailored interactions utilize long-term memory to store and retrieve user preferences, past behaviors, and personal information. This allows agents to adapt their responses and suggestions.  
* **Learning and Improvement:** Agents can refine their performance by learning from past interactions. Successful strategies, mistakes, and new information are stored in long-term memory, facilitating future adaptations. Reinforcement learning agents store learned strategies or knowledge in this way.  
* **Information Retrieval (RAG):** Agents designed for answering questions access a knowledge base, their long-term memory, often implemented within Retrieval Augmented Generation (RAG). The agent retrieves relevant documents or data to inform its responses.  
* **Autonomous Systems:** Robots or self-driving cars require memory for maps, routes, object locations, and learned behaviors. This involves short-term memory for immediate surroundings and long-term memory for general environmental knowledge.

> * **聊天机器人与对话 AI：** 对话流畅依赖短期记忆；需记住先前用户输入以连贯回复。长期记忆可召回用户偏好、历史问题或过往讨论，实现个性化与连续交互。  
> * **任务导向智能体：** 多步任务需短期记忆跟踪已完成步骤、当前进度与总体目标（信息可在任务上下文或临时存储）。长期记忆用于访问不在即时上下文中的用户相关数据。  
> * **个性化体验：** 长期记忆存储并检索用户偏好、过往行为与个人信息，使智能体能调整回复与建议。  
> * **学习与改进：** 从过往交互学习以精炼表现；成功策略、错误与新信息存入长期记忆以利未来适应；强化学习智能体亦以此存储策略或知识。  
> * **信息检索（RAG）：** 问答型智能体访问知识库作为长期记忆，常在检索增强生成（RAG）中实现；检索相关文档或数据以支撑回答。  
> * **自主系统：** 机器人或自动驾驶需地图、路线、物体位置与习得行为等记忆；短期用于近邻环境，长期用于一般环境知识。

Memory enables agents to maintain history, learn, personalize interactions, and manage complex, time-dependent problems.

> 记忆使智能体能维护历史、学习、个性化交互，并管理复杂、时间相关的问题。

## Hands-On Code: Memory Management in Google Agent Developer Kit (ADK)

> ## 动手代码：Google Agent Developer Kit（ADK）中的记忆管理

The Google Agent Developer Kit (ADK) offers a structured method for managing context and memory, including components for practical application. A solid grasp of ADK's Session, State, and Memory is vital for building agents that need to retain information.

> ADK 提供管理上下文与记忆的结构化方法，含可落地组件；欲构建需保留信息的智能体，须扎实掌握 Session、State 与 Memory。

Just as in human interactions, agents require the ability to recall previous exchanges to conduct coherent and natural conversations. ADK simplifies context management through three core concepts and their associated services.

> 如同人际交流，智能体需要回忆先前往来才能进行连贯、自然的对话。ADK 通过三个核心概念及其服务简化上下文管理。

Every interaction with an agent can be considered a unique conversation thread. Agents might need to access data from earlier interactions. ADK structures this as follows:

> 每次与智能体的交互可视为独立对话线程；智能体可能需要访问更早交互的数据。ADK 结构如下：

* **Session:** An individual chat thread that logs messages and actions (Events) for that specific interaction, also storing temporary data (State) relevant to that conversation.  
* **State (`session.state`):** Data stored within a Session, containing information relevant only to the current, active chat thread.  
* **Memory:** A searchable repository of information sourced from various past chats or external sources, serving as a resource for data retrieval beyond the immediate conversation.

> * **Session：** 单条聊天线程，记录该次交互的消息与动作（Events），并保存与该对话相关的临时数据（State）。  
> * **State（`session.state`）：** 存放在 Session 内、仅与当前活跃聊天线程相关的数据。  
> * **Memory：** 可检索的知识库，信息来自过往多轮聊天或外部来源，用于超越当前对话的数据获取。

ADK provides dedicated services for managing critical components essential for building complex, stateful, and context-aware agents. The SessionService manages chat threads (Session objects) by handling their initiation, recording, and termination, while the MemoryService oversees the storage and retrieval of long-term knowledge (Memory).

> ADK 提供专用服务管理构建复杂、有状态、情境感知智能体的关键组件：`SessionService` 负责会话的创建、记录与结束；`MemoryService` 负责长期知识（Memory）的存储与检索。

Both the SessionService and MemoryService offer various configuration options, allowing users to choose storage methods based on application needs. In-memory options are available for testing purposes, though data will not persist across restarts. For persistent storage and scalability, ADK also supports database and cloud-based services.

> 二者均有多样配置：可选用内存实现做测试（重启不持久）；生产可扩展场景下 ADK 也支持数据库与云端服务。

### Session: Keeping Track of Each Chat

> ### Session：跟踪每一次聊天

A Session object in ADK is designed to track and manage individual chat threads. Upon initiation of a conversation with an agent, the SessionService generates a Session object, represented as `google.adk.sessions.Session`. This object encapsulates all data relevant to a specific conversation thread, including unique identifiers (`id`, `app\_name`, `user\_id`), a chronological record of events as Event objects, a storage area for session-specific temporary data known as state, and a timestamp indicating the last update (`last\_update\_time`). Developers typically interact with Session objects indirectly through the SessionService. The SessionService is responsible for managing the lifecycle of conversation sessions, which includes initiating new sessions, resuming previous sessions, recording session activity (including state updates), identifying active sessions, and managing the removal of session data. The ADK provides several SessionService implementations with varying storage mechanisms for session history and temporary data, such as the InMemorySessionService, which is suitable for testing but does not provide data persistence across application restarts.

> ADK 中 `Session` 用于跟踪单条聊天线程。开始对话时 `SessionService` 创建 `google.adk.sessions.Session`，封装该线程的标识（`id`、`app_name`、`user_id`）、按时间排序的 `Event` 记录、会话级临时 state，以及 `last_update_time` 等。开发者通常通过 `SessionService` 间接使用 `Session`；后者负责会话生命周期（新建、恢复、记录含 state 的活动、识别活动会话、删除会话数据）。ADK 提供多种 `SessionService` 实现（如 `InMemorySessionService` 适于测试但重启不持久）。

```python
# Example: Using InMemorySessionService 
# This is suitable for local development and testing where data 
# persistence across application restarts is not required. 
from google.adk.sessions import InMemorySessionService
session_service = InMemorySessionService()
```

> 示例：本地开发与测试可用 `InMemorySessionService`（应用重启不持久）。

Then there's DatabaseSessionService if you want reliable saving to a database you manage.

> 若需可靠落库，可使用 `DatabaseSessionService`；需配置数据库 URL（如 SQLite、PostgreSQL），并安装 `google-adk[sqlalchemy]` 与相应驱动。

```python
# Example: Using DatabaseSessionService 
# This is suitable for production or development requiring persistent storage. 
# You need to configure a database URL (e.g., for SQLite, PostgreSQL, etc.). 
# Requires: pip install google-adk[sqlalchemy] and a database driver (e.g., psycopg2 for PostgreSQL) 
from google.adk.sessions import DatabaseSessionService 
# Example using a local SQLite file: 
db_url = "sqlite:///./my_agent_data.db"
session_service = DatabaseSessionService(db_url=db_url)
```

Besides, there's VertexAiSessionService which uses Vertex AI infrastructure for scalable production on Google Cloud.

> 另有 `VertexAiSessionService`，在 Google Cloud 上利用 Vertex AI 基础设施做可扩展生产部署；需 `google-adk[vertexai]` 与 GCP 配置/认证，调用时注意 `app_name` 与 Reasoning Engine 资源对应。

```python
# Example: Using VertexAiSessionService
# This is suitable for scalable production on Google Cloud Platform, leveraging
# Vertex AI infrastructure for session management.
# Requires: pip install google-adk[vertexai] and GCP setup/authentication

from google.adk.sessions import VertexAiSessionService


PROJECT_ID = "your-gcp-project-id"  # Replace with your GCP project ID
LOCATION = "us-central1"  # Replace with your desired GCP location

# The app_name used with this service should correspond to the Reasoning Engine ID or name
REASONING_ENGINE_APP_NAME = (
    "projects/your-gcp-project-id/locations/us-central1/reasoningEngines/your-engine-id"
)  # Replace with your Reasoning Engine resource name

session_service = VertexAiSessionService(project=PROJECT_ID, location=LOCATION)

# When using this service, pass REASONING_ENGINE_APP_NAME to service methods:
# session_service.create_session(app_name=REASONING_ENGINE_APP_NAME, ...)
# session_service.get_session(app_name=REASONING_ENGINE_APP_NAME, ...)
# session_service.append_event(session, event, app_name=REASONING_ENGINE_APP_NAME)
# session_service.delete_session(app_name=REASONING_ENGINE_APP_NAME, ...)
```

Choosing an appropriate SessionService is crucial as it determines how the agent's interaction history and temporary data are stored and their persistence.

> 选择合适的 `SessionService` 决定交互历史与临时数据如何存储及是否持久。

Each message exchange involves a cyclical process: A message is received, the Runner retrieves or establishes a Session using the SessionService, the agent processes the message using the Session's context (state and historical interactions), the agent generates a response and may update the state, the Runner encapsulates this as an Event, and the `session\_service.append\_event` method records the new event and updates the state in storage. The Session then awaits the next message. Ideally, the `delete\_session` method is employed to terminate the session when the interaction concludes. This process illustrates how the SessionService maintains continuity by managing the Session-specific history and temporary data.

> 选择合适的 `SessionService` 决定交互历史与临时数据如何存储及是否持久。每轮消息循环大致为：收消息 → Runner 用 `SessionService` 获取/建立 `Session` → 智能体在 state 与历史上下文中处理 → 生成回复并可能更新 state → Runner 封装为 `Event`，`session_service.append_event` 写入存储。理想情况下交互结束调用 `delete_session`。由此 `SessionService` 通过管理会话专属历史与临时数据保持连续性。

### State: The Session's Scratchpad

> ### State：会话便笺簿

In the ADK, each Session, representing a chat thread, includes a state component akin to an agent's temporary working memory for the duration of that specific conversation. While session.events logs the entire chat history, session.state stores and updates dynamic data points relevant to the active chat.

> 在 ADK 中，每个代表聊天线程的 `Session` 包含 `state` 组件，类似该对话持续期间的临时工作记忆；`session.events` 记录完整聊天历史，`session.state` 存储并更新与当前活跃聊天相关的动态数据点。

Fundamentally, session.state operates as a dictionary, storing data as key-value pairs. Its core function is to enable the agent to retain and manage details essential for coherent dialogue, such as user preferences, task progress, incremental data collection, or conditional flags influencing subsequent agent actions.

> 本质上 `session.state` 是字典，以键值对保存数据，支撑连贯对话所需的偏好、任务进度、增量采集或影响后续动作的条件标记等。

The state’s structure comprises string keys paired with values of serializable Python types, including strings, numbers, booleans, lists, and dictionaries containing these basic types. State is dynamic, evolving throughout the conversation. The permanence of these changes depends on the configured SessionService.

> 键为字符串，值为可序列化的 Python 基本类型及其列表/字典；state 随对话演变，是否持久取决于所选 `SessionService`。

State organization can be achieved using key prefixes to define data scope and persistence. Keys without prefixes are session-specific.

* The user: prefix associates data with a user ID across all sessions.
* The app: prefix designates data shared among all users of the application.
* The temp: prefix indicates data valid only for the current processing turn and is not persistently stored.

> 可用键前缀划分作用域与持久性：无前缀为会话级；`user:` 跨会话与用户 ID 关联；`app:` 应用内全局共享；`temp:` 仅当前处理轮有效、不持久保存。

The agent accesses all state data through a single session.state dictionary. The SessionService handles data retrieval, merging, and persistence. State should be updated upon adding an Event to the session history via `session\_service.append\_event()`. This ensures accurate tracking, proper saving in persistent services, and safe handling of state changes.

> 智能体通过单一 `session.state` 访问；`SessionService` 负责检索、合并与持久化。应在通过 `session_service.append_event()` 追加 `Event` 时更新 state，以保证追踪准确、持久服务正确落库与安全变更。

#### 1. The Simple Way: Using `output\_key` (for Agent Text Replies)

> #### 1. 简单方式：使用 `output_key`（保存智能体文本回复）

This is the easiest method if you just want to save your agent's final text response directly into the state. When you set up your LlmAgent, just tell it the output\_key you want to use. The Runner sees this and automatically creates the necessary actions to save the response to the state when it appends the event. Let's look at a code example demonstrating state update via `output\_key`.

> 若只需把智能体最终文本回复写入 state，最简单做法是在配置 `LlmAgent` 时指定 `output_key`；`Runner` 在 `append_event` 时会自动生成带 `state_delta` 的动作以保存该回复。下面示例演示通过 `output_key` 更新 state。

```python
# Import necessary classes from the Google Agent Developer Kit (ADK)
from google.adk.agents import LlmAgent
from google.adk.sessions import InMemorySessionService, Session
from google.adk.runners import Runner
from google.genai.types import Content, Part


# Define an LlmAgent with an output_key.
greeting_agent = LlmAgent(
 name="Greeter",
 model="gemini-2.0-flash",
 instruction="Generate a short, friendly greeting.",
 output_key="last_greeting",
)


# --- Setup Runner and Session ---
app_name, user_id, session_id = "state_app", "user1", "session1"

session_service = InMemorySessionService()

runner = Runner(
    agent=greeting_agent,
    app_name=app_name,
    session_service=session_service,
)

session = session_service.create_session(
    app_name=app_name,
    user_id=user_id,
    session_id=session_id,
)

print(f"Initial state: {session.state}")


# --- Run the Agent ---
user_message = Content(parts=[Part(text="Hello")])

print("\n--- Running the agent ---")
for event in runner.run(
    user_id=user_id,
    session_id=session_id,
    new_message=user_message,
):
    if event.is_final_response():
        print("Agent responded.")


# --- Check Updated State ---
# Correctly check the state after the runner has finished processing all events.
updated_session = session_service.get_session(app_name, user_id, session_id)
print(f"\nState after agent run: {updated_session.state}")
```

Behind the scenes, the Runner sees your `output\_key` and automatically creates the necessary actions with a `state\_delta` when it calls `append\_event`.

> 幕后：`Runner` 识别 `output_key` 后，在调用 `append_event` 时会自动创建含 `state_delta` 的必要动作。

#### 2. The Standard Way: Using `EventActions.state\_delta` (for More Complicated Updates)

> #### 2. 标准方式：使用 `EventActions.state_delta`（更复杂的更新）

For times when you need to do more complex things – like updating several keys at once, saving things that aren't just text, targeting specific scopes like user: or app:, or making updates that aren't tied to the agent's final text reply – you'll manually build a dictionary of your state changes (the `state\_delta`) and include it within the EventActions of the Event you're appending. Let's look at one example:

> 若需一次更新多键、保存非纯文本、针对 `user:`/`app:` 等作用域，或与最终文本无关的更新，需手工构造 `state_delta` 字典，并在追加的 `Event` 的 `EventActions` 中携带。示例如下：

```python
import time

from google.adk.tools.tool_context import ToolContext
from google.adk.sessions import InMemorySessionService


# --- Define the Recommended Tool-Based Approach ---
def log_user_login(tool_context: ToolContext) -> dict:
    """
    Updates the session state upon a user login event.
    This tool encapsulates all state changes related to a user login.

    Args:
        tool_context: Automatically provided by ADK, gives access to session state.

    Returns:
        A dictionary confirming the action was successful.
    """
    # Access the state directly through the provided context.
    state = tool_context.state

    # Get current values or defaults, then update the state.
    # This is much cleaner and co-locates the logic.
    login_count = state.get("user:login_count", 0) + 1
    state["user:login_count"] = login_count
    state["task_status"] = "active"
    state["user:last_login_ts"] = time.time()
    state["temp:validation_needed"] = True

    print("State updated from within the `log_user_login` tool.")

    return {
        "status": "success",
        "message": f"User login tracked. Total logins: {login_count}.",
    }


# --- Demonstration of Usage ---
# In a real application, an LLM Agent would decide to call this tool.
# Here, we simulate a direct call for demonstration purposes.

# 1. Setup
session_service = InMemorySessionService()
app_name, user_id, session_id = "state_app_tool", "user3", "session3"

session = session_service.create_session(
    app_name=app_name,
    user_id=user_id,
    session_id=session_id,
    state={"user:login_count": 0, "task_status": "idle"},
)

print(f"Initial state: {session.state}")

# 2. Simulate a tool call (in a real app, the ADK Runner does this)
# We create a ToolContext manually just for this standalone example.
from google.adk.tools.tool_context import InvocationContext

mock_context = ToolContext(
    invocation_context=InvocationContext(
        app_name=app_name,
        user_id=user_id,
        session_id=session_id,
        session=session,
        session_service=session_service,
    )
)

# 3. Execute the tool
log_user_login(mock_context)

# 4. Check the updated state
updated_session = session_service.get_session(app_name, user_id, session_id)
print(f"State after tool execution: {updated_session.state}")

# Expected output will show the same state change as the "Before" case,
# but the code organization is significantly cleaner and more robust.
```

This code demonstrates a tool-based approach for managing user session state in an application. It defines a function *log\_user\_login*, which acts as a tool. This tool is responsible for updating the session state when a user logs in.  
The function takes a ToolContext object, provided by the ADK, to access and modify the session's state dictionary. Inside the tool, it increments a *user:login\_count*, sets the t*ask\_status* to "active", records the *user:last\_login\_ts (timestamp)*, and adds a temporary flag temp:validation\_needed.

> 该示例展示基于工具管理用户会话状态：`log_user_login` 作为工具在用户登录时更新 state；通过 ADK 提供的 `ToolContext` 读写 `state` 字典，递增 `user:login_count`、置 `task_status` 为 active、记录 `user:last_login_ts`、设置临时标记 `temp:validation_needed`。

The demonstration part of the code simulates how this tool would be used. It sets up an in-memory session service and creates an initial session with some predefined state. A ToolContext is then manually created to mimic the environment in which the ADK Runner would execute the tool. The `log\_user\_login` function is called with this mock context. Finally, the code retrieves the session again to show that the state has been updated by the tool's execution. The goal is to show how encapsulating state changes within tools makes the code cleaner and more organized compared to directly manipulating state outside of tools.

> 演示部分模拟工具调用：建内存 `SessionService`、带初始 state 的会话、手工构造 `ToolContext` 以模仿 `Runner` 环境，调用 `log_user_login` 后再取会话验证 state 已更新；意在说明把状态变更封装在工具内比在外部直接改 state 更清晰、可维护。

Note that direct modification of the `session.state` dictionary after retrieving a session is strongly discouraged as it bypasses the standard event processing mechanism. Such direct changes will not be recorded in the session's event history, may not be persisted by the selected `SessionService`, could lead to concurrency issues, and will not update essential metadata such as timestamps. The recommended methods for updating the session state are using the `output\_key` parameter on an `LlmAgent` (specifically for the agent's final text responses) or including state changes within `EventActions.state\_delta` when appending an event via `session\_service.append\_event()`. The `session.state` should primarily be used for reading existing data.

> **注意：** 取出会话后直接改 `session.state` 强烈不推荐——会绕过标准事件流，历史可能无记录、持久化可能失效、并发风险增加，且元数据（如时间戳）不更新。推荐通过 `LlmAgent` 的 `output_key`（针对最终文本）或在 `session_service.append_event()` 时使用 `EventActions.state_delta` 更新；`session.state` 主要用于读取。

To recap, when designing your state, keep it simple, use basic data types, give your keys clear names and use prefixes correctly, avoid deep nesting, and always update state using the append\_event process.

> 小结：设计 state 宜简单、用基础类型、键名清晰且前缀正确、避免过深嵌套，并始终通过 `append_event` 流程更新。

## Memory: Long-Term Knowledge with MemoryService

> ## Memory：用 MemoryService 管理长期知识

In agent systems, the Session component maintains a record of the current chat history (events) and temporary data (state) specific to a single conversation. However, for agents to retain information across multiple interactions or access external data, long-term knowledge management is necessary. This is facilitated by the MemoryService.

> `Session` 记录单次对话的聊天历史（events）与临时数据（state）；要跨多轮保留信息或访问外部数据，需要长期知识管理，由 `MemoryService` 承担。

```python
# Example: Using InMemoryMemoryService
# This is suitable for local development and testing where data
# persistence across application restarts is not required.
# Memory content is lost when the app stops.

from google.adk.memory import InMemoryMemoryService

memory_service = InMemoryMemoryService()
```

> 示例：`InMemoryMemoryService` 适于本地与测试（应用停止后记忆丢失）。

Session and State can be conceptualized as short-term memory for a single chat session, whereas the Long-Term Knowledge managed by the MemoryService functions as a persistent and searchable repository. This repository may contain information from multiple past interactions or external sources. The MemoryService, as defined by the BaseMemoryService interface, establishes a standard for managing this searchable, long-term knowledge. Its primary functions include adding information, which involves extracting content from a session and storing it using the add\_session\_to\_memory method, and retrieving information, which allows an agent to query the store and receive relevant data using the search\_memory method.

> 可把 `Session`/`State` 视为单会话的短期记忆；`MemoryService` 管理的长期知识是可持久、可检索的仓库，可含多轮历史或外部来源。`BaseMemoryService` 约定标准：`add_session_to_memory` 从会话抽取内容写入，`search_memory` 供智能体查询取回相关数据。

The ADK offers several implementations for creating this long-term knowledge store. The InMemoryMemoryService provides a temporary storage solution suitable for testing purposes, but data is not preserved across application restarts. For production environments, the VertexAiRagMemoryService is typically utilized. This service leverages Google Cloud's Retrieval Augmented Generation (RAG) service, enabling scalable, persistent, and semantic search capabilities (Also, refer to the chapter 14 on RAG).

> ADK 提供多种实现：`InMemoryMemoryService` 临时、适于测试；生产常用 `VertexAiRagMemoryService`，基于 Google Cloud RAG，支持可扩展、持久与语义检索（另见第 14 章）。

```python
# Example: Using VertexAiRagMemoryService
# This is suitable for scalable production on GCP, leveraging
# Vertex AI RAG (Retrieval Augmented Generation) for persistent,
# searchable memory.
# Requires: pip install google-adk[vertexai], GCP
# setup/authentication, and a Vertex AI RAG Corpus.

from google.adk.memory import VertexAiRagMemoryService


# The resource name of your Vertex AI RAG Corpus
RAG_CORPUS_RESOURCE_NAME = (
    "projects/your-gcp-project-id/locations/us-central1/ragCorpora/your-corpus-id"
)  # Replace with your Corpus resource name

# Optional configuration for retrieval behavior
SIMILARITY_TOP_K = 5  # Number of top results to retrieve
VECTOR_DISTANCE_THRESHOLD = 0.7  # Threshold for vector similarity

memory_service = VertexAiRagMemoryService(
    rag_corpus=RAG_CORPUS_RESOURCE_NAME,
    similarity_top_k=SIMILARITY_TOP_K,
    vector_distance_threshold=VECTOR_DISTANCE_THRESHOLD,
)

# When using this service, methods like add_session_to_memory
# and search_memory will interact with the specified Vertex AI
# RAG Corpus.
```

> `add_session_to_memory` 与 `search_memory` 将与指定 Vertex AI RAG Corpus 交互。

## Hands-on code: Memory Management in LangChain and LangGraph

> ## 动手代码：LangChain 与 LangGraph 中的记忆管理

In LangChain and LangGraph, Memory is a critical component for creating intelligent and natural-feeling conversational applications. It allows an AI agent to remember information from past interactions, learn from feedback, and adapt to user preferences. LangChain's memory feature provides the foundation for this by referencing a stored history to enrich current prompts and then recording the latest exchange for future use. As agents handle more complex tasks, this capability becomes essential for both efficiency and user satisfaction.

> 在 LangChain/LangGraph 中，Memory 是构建自然、智能对话应用的关键；智能体可记住过往交互、从反馈学习并适应偏好。LangChain 的记忆能力通过引用已存历史丰富当前提示并记录最新轮次，为更复杂任务提供效率与体验基础。

**Short-Term Memory:** This is thread-scoped, meaning it tracks the ongoing conversation within a single session or thread. It provides immediate context, but a full history can challenge an LLM's context window, potentially leading to errors or poor performance. LangGraph manages short-term memory as part of the agent's state, which is persisted via a checkpointer, allowing a thread to be resumed at any time.

**Long-Term Memory:** This stores user-specific or application-level data across sessions and is shared between conversational threads. It is saved in custom "namespaces" and can be recalled at any time in any thread. LangGraph provides stores to save and recall long-term memories, enabling agents to retain knowledge indefinitely.

> **短期记忆：** 线程级，跟踪单会话/线程内对话；提供即时上下文，但完整历史可能撑满上下文窗口导致错误或低效。LangGraph 将短期记忆作为智能体 state 的一部分，经 checkpointer 持久化，可随时恢复线程。  
> **长期记忆：** 跨会话保存用户级或应用级数据，在线程间共享；存于自定义「命名空间」，任意线程可随时召回。LangGraph 的 store 支持长期记忆的写入与读取，使知识可长期保留。

LangChain provides several tools for managing conversation history, ranging from manual control to automated integration within chains.

**ChatMessageHistory: Manual Memory Management.** For direct and simple control over a conversation's history outside of a formal chain, the ChatMessageHistory class is ideal. It allows for the manual tracking of dialogue exchanges.

> LangChain 提供从手工管理到链内自动集成的多种对话历史工具。  
> **ChatMessageHistory：** 在正式链之外想直接、简单地管历史时适用，可手工跟踪对话轮次。

```python
from langchain.memory import ChatMessageHistory


# Initialize the history object
history = ChatMessageHistory()

# Add user and AI messages
history.add_user_message("I'm heading to New York next week.")
history.add_ai_message("Great! It's a fantastic city.")

# Access the list of messages
print(history.messages)
```

> 示例：初始化 `ChatMessageHistory`，添加用户/AI 消息并打印消息列表。

**ConversationBufferMemory: Automated Memory for Chains**. For integrating memory directly into chains, ConversationBufferMemory is a common choice. It holds a buffer of the conversation and makes it available to your prompt. Its behavior can be customized with two key parameters:

* `memory\_key`: A string that specifies the variable name in your prompt that will hold the chat history. It defaults to "history".  
* `return\_messages`: A boolean that dictates the format of the history.  
  * If `False` (the default), it returns a single formatted string, which is ideal for standard LLMs.  
  * If `True`, it returns a list of message objects, which is the recommended format for Chat Models.

> **ConversationBufferMemory：** 将记忆直接接入链时的常见选择；维护对话缓冲供提示使用。关键参数：`memory_key`（提示中存放历史的变量名，默认 `history`）；`return_messages`（`False` 返回单段格式化字符串，适合传统 LLM；`True` 返回消息对象列表，推荐用于 Chat 模型）。

```python
from langchain.memory import ConversationBufferMemory


# Initialize memory
memory = ConversationBufferMemory()

# Save a conversation turn
memory.save_context(
    {"input": "What's the weather like?"},
    {"output": "It's sunny today."},
)

# Load the memory as a string
print(memory.load_memory_variables({}))
```

> 示例：`save_context` 保存一轮对话，`load_memory_variables` 以字符串形式读出记忆。

Integrating this memory into an LLMChain allows the model to access the conversation's history and provide contextually relevant responses

> 将记忆接入 `LLMChain` 后，模型可访问历史并做情境相关回复。

```python
from langchain_openai import OpenAI
from langchain.chains import LLMChain
from langchain.prompts import PromptTemplate
from langchain.memory import ConversationBufferMemory


# 1. Define LLM and Prompt
llm = OpenAI(temperature=0)

template = """You are a helpful travel agent.
Previous conversation: {history}
New question: {question}
Response:"""
prompt = PromptTemplate.from_template(template)

# 2. Configure Memory
# The memory_key "history" matches the variable in the prompt
memory = ConversationBufferMemory(memory_key="history")

# 3. Build the Chain
conversation = LLMChain(llm=llm, prompt=prompt, memory=memory)

# 4. Run the Conversation
response = conversation.predict(question="I want to book a flight.")
print(response)

response = conversation.predict(question="My name is Sam, by the way.")
print(response)

response = conversation.predict(question="What was my name again?")
print(response)
```

For improved effectiveness with chat models, it is recommended to use a structured list of message objects by setting \`return\_messages=True\`.

> 配合 Chat 模型时，建议设 `return_messages=True`，使用结构化消息列表。

```python
from langchain_openai import ChatOpenAI
from langchain.chains import LLMChain
from langchain.memory import ConversationBufferMemory
from langchain_core.prompts import (
    ChatPromptTemplate,
    MessagesPlaceholder,
    SystemMessagePromptTemplate,
    HumanMessagePromptTemplate,
)


# 1. Define Chat Model and Prompt
llm = ChatOpenAI()

prompt = ChatPromptTemplate(
    messages=[
        SystemMessagePromptTemplate.from_template("You are a friendly assistant."),
        MessagesPlaceholder(variable_name="chat_history"),
        HumanMessagePromptTemplate.from_template("{question}"),
    ]
)

# 2. Configure Memory
# return_messages=True is essential for chat models
memory = ConversationBufferMemory(memory_key="chat_history", return_messages=True)

# 3. Build the Chain
conversation = LLMChain(llm=llm, prompt=prompt, memory=memory)

# 4. Run the Conversation
response = conversation.predict(question="Hi, I'm Jane.")
print(response)

response = conversation.predict(question="Do you remember my name?")
print(response)
```

> 示例：`ChatPromptTemplate` 与 `MessagesPlaceholder` 配合 `return_messages=True` 的 `ConversationBufferMemory` 构建对话链。

**Types of Long-Term Memory**: Long-term memory allows systems to retain information across different conversations, providing a deeper level of context and personalization. It can be broken down into three types analogous to human memory:

* **Semantic Memory: Remembering Facts:** This involves retaining specific facts and concepts, such as user preferences or domain knowledge. It is used to ground an agent's responses, leading to more personalized and relevant interactions. This information can be managed as a continuously updated user "profile" (a JSON document) or as a "collection" of individual factual documents.  
* **Episodic Memory: Remembering Experiences:** This involves recalling past events or actions. For AI agents, episodic memory is often used to remember how to accomplish a task. In practice, it's frequently implemented through few-shot example prompting, where an agent learns from past successful interaction sequences to perform tasks correctly.  
* **Procedural Memory: Remembering Rules:**  This is the memory of how to perform tasks—the agent's core instructions and behaviors, often contained in its system prompt. It's common for agents to modify their own prompts to adapt and improve. An effective technique is "Reflection," where an agent is prompted with its current instructions and recent interactions, then asked to refine its own instructions.

> **长期记忆类型：**  
> * **语义记忆（事实）：** 保留用户偏好、领域知识等事实与概念，可做成持续更新的用户「档案」（JSON）或事实文档集合，使回复更个性化、更贴题。  
> * **情景记忆（经历）：** 回忆过去事件或动作；对 AI 智能体常体现为「如何做某事」，实践中多用 few-shot 示例，从成功交互序列学习。  
> * **程序性记忆（规则）：** 执行任务的方式——核心指令与行为，常在系统提示中；智能体可自改提示以适应改进；「反思」技术：把当前指令与近期交互交给模型，让其精炼自身指令。

Below is pseudo-code demonstrating how an agent might use reflection to update its procedural memory stored in a LangGraph BaseStore

> 以下为伪代码，展示智能体如何用反思更新存放在 LangGraph `BaseStore` 中的程序性记忆：

```python
# Node that updates the agent's instructions
def update_instructions(state: State, store: BaseStore):
    namespace = ("instructions",)

    # Get the current instructions from the store
    current_instructions = store.search(namespace)[0]

    # Create a prompt to ask the LLM to reflect on the conversation
    # and generate new, improved instructions
    prompt = prompt_template.format(
        instructions=current_instructions.value["instructions"],
        conversation=state["messages"],
    )

    # Get the new instructions from the LLM
    output = llm.invoke(prompt)
    new_instructions = output["new_instructions"]

    # Save the updated instructions back to the store
    store.put(("agent_instructions",), "agent_a", {"instructions": new_instructions})


# Node that uses the instructions to generate a response
def call_model(state: State, store: BaseStore):
    namespace = ("agent_instructions",)

    # Retrieve the latest instructions from the store
    instructions = store.get(namespace, key="agent_a")[0]

    # Use the retrieved instructions to format the prompt
    prompt = prompt_template.format(
        instructions=instructions.value["instructions"]
    )
    # ... application logic continues
```

LangGraph stores long-term memories as JSON documents in a store. Each memory is organized under a custom namespace (like a folder) and a distinct key (like a filename). This hierarchical structure allows for easy organization and retrieval of information. The following code demonstrates how to use InMemoryStore to put, get, and search for memories.

> LangGraph 将长期记忆以 JSON 文档存入 store；每条记忆位于自定义 namespace（类似文件夹）与独立 key（类似文件名）下，便于组织与检索。以下示例演示 `InMemoryStore` 的 `put`、`get` 与 `search`。

```python
from langgraph.store.memory import InMemoryStore


# A placeholder for a real embedding function
def embed(texts: list[str]) -> list[list[float]]:
    # In a real application, use a proper embedding model
    return [[1.0, 2.0] for _ in texts]


# Initialize an in-memory store. For production, use a database-backed store.
store = InMemoryStore(index={"embed": embed, "dims": 2})

# Define a namespace for a specific user and application context
user_id = "my-user"
application_context = "chitchat"
namespace = (user_id, application_context)

# 1. Put a memory into the store
store.put(
    namespace,
    "a-memory",  # The key for this memory
    {
        "rules": [
            "User likes short, direct language",
            "User only speaks English & python",
        ],
        "my-key": "my-value",
    },
)

# 2. Get the memory by its namespace and key
item = store.get(namespace, "a-memory")
print("Retrieved Item:", item)

# 3. Search for memories within the namespace, filtering by content
# and sorting by vector similarity to the query.
items = store.search(
    namespace,
    filter={"my-key": "my-value"},
    query="language preferences",
)
print("Search Results:", items)
```

> 示例：带占位嵌入函数的内存 store，在 namespace 下写入、按键读取、按过滤与向量相似查询。

## Vertex Memory Bank

> ## Vertex Memory Bank

Memory Bank, a managed service in the Vertex AI Agent Engine, provides agents with persistent, long-term memory. The service uses Gemini models to asynchronously analyze conversation histories to extract key facts and user preferences.

> Vertex AI Agent Engine 中的托管服务 Memory Bank 为智能体提供持久长期记忆；用 Gemini 异步分析对话历史，抽取关键事实与用户偏好。

This information is stored persistently, organized by a defined scope like user ID, and intelligently updated to consolidate new data and resolve contradictions. Upon starting a new session, the agent retrieves relevant memories through either a full data recall or a similarity search using embeddings. This process allows an agent to maintain continuity across sessions and personalize responses based on recalled information.

> 数据持久保存，按用户 ID 等作用域组织，并智能合并新信息与消解矛盾。新会话开始时可全量回忆或基于嵌入做相似检索，以跨会话保持连贯并按回忆个性化回复。

The agent's runner interacts with the VertexAiMemoryBankService, which is initialized first. This service handles the automatic storage of memories generated during the agent's conversations. Each memory is tagged with a unique USER\_ID and APP\_NAME, ensuring accurate retrieval in the future.

> `Runner` 与先初始化的 `VertexAiMemoryBankService` 交互，自动存储对话中产生的记忆；每条记忆带 `USER_ID` 与 `APP_NAME` 标签以便准确检索。

```python
from google.adk.memory import VertexAiMemoryBankService


agent_engine_id = agent_engine.api_resource.name.split("/")[-1]

memory_service = VertexAiMemoryBankService(
    project="PROJECT_ID",
    location="LOCATION",
    agent_engine_id=agent_engine_id,
)

session = await session_service.get_session(
    app_name=app_name,
    user_id="USER_ID",
    session_id=session.id,
)

await memory_service.add_session_to_memory(session)
```

> 示例：用 Agent Engine 资源初始化 `VertexAiMemoryBankService`，取会话后 `add_session_to_memory`。

Memory Bank offers seamless integration with the Google ADK, providing an immediate out-of-the-box experience. For users of other agent frameworks, such as LangGraph and CrewAI, Memory Bank also offers support through direct API calls. Online code examples demonstrating these integrations are readily available for interested readers.

> Memory Bank 与 Google ADK 集成顺畅、开箱即用；LangGraph、CrewAI 等框架用户也可通过直接 API 调用使用；网上有集成示例可供参考。

## At a Glance

> ## 一览

**What**: Agentic systems need to remember information from past interactions to perform complex tasks and provide coherent experiences. Without a memory mechanism, agents are stateless, unable to maintain conversational context, learn from experience, or personalize responses for users. This fundamentally limits them to simple, one-shot interactions, failing to handle multi-step processes or evolving user needs. The core problem is how to effectively manage both the immediate, temporary information of a single conversation and the vast, persistent knowledge gathered over time.

> **问题：** 智能体系统需记住过往交互才能完成复杂任务、提供连贯体验；无记忆则无状态、难维持上下文、难从经验学习或个性化。核心矛盾是如何同时管好单轮对话的即时临时信息与长期积累的大量持久知识。

**Why:** The standardized solution is to implement a dual-component memory system that distinguishes between short-term and long-term storage. Short-term, contextual memory holds recent interaction data within the LLM's context window to maintain conversational flow. For information that must persist, long-term memory solutions use external databases, often vector stores, for efficient, semantic retrieval. Agentic frameworks like the Google ADK provide specific components to manage this, such as Session for the conversation thread and State for its temporary data. A dedicated MemoryService is used to interface with the long-term knowledge base, allowing the agent to retrieve and incorporate relevant past information into its current context.

> **思路：** 标准做法是双组件记忆——区分短期与长期。短期情境记忆把近期交互放在 LLM 上下文窗口内维持对话流；需持久的信息用外部数据库（常为向量库）做高效语义检索。Google ADK 等框架用 `Session` 管线程、`State` 管临时数据，用 `MemoryService` 对接可检索的长期知识库，把相关历史并入当前上下文。

**Rule of thumb:** Use this pattern when an agent needs to do more than answer a single question. It is essential for agents that must maintain context throughout a conversation, track progress in multi-step tasks, or personalize interactions by recalling user preferences and history. Implement memory management whenever the agent is expected to learn or adapt based on past successes, failures, or newly acquired information.

> **经验法则：** 智能体不止回答单问时即用本模式；需在对话中保持上下文、在多步任务中跟踪进度、或通过回忆偏好与历史做个性化时必不可少；若预期基于成败或新信息学习适应，也应实现记忆管理。

**Visual summary:**

> **图示摘要：**

![Memory Management Design Pattern](../assets-new/Memory_Management_Design_Pattern.png)

Fig.1: Memory management design pattern

> 图 1：记忆管理设计模式

## Key Takeaways

> ## 要点

To quickly recap the main points about memory management:

* Memory is super important for agents to keep track of things, learn, and personalize interactions.  
* Conversational AI relies on both short-term memory for immediate context within a single chat and long-term memory for persistent knowledge across multiple sessions.  
* Short-term memory (the immediate stuff) is temporary, often limited by the LLM's context window or how the framework passes context.  
* Long-term memory (the stuff that sticks around) saves info across different chats using outside storage like vector databases and is accessed by searching.  
* Frameworks like ADK have specific parts like Session (the chat thread), State (temporary chat data), and MemoryService (the searchable long-term knowledge) to manage memory.  
* ADK's SessionService handles the whole life of a chat session, including its history (events) and temporary data (state).  
* ADK's session.state is a dictionary for temporary chat data. Prefixes (user:, app:, temp:) tell you where the data belongs and if it sticks around.  
* In ADK, you should update state by using EventActions.state\_delta or output\_key when adding events, not by changing the state dictionary directly.  
* ADK's MemoryService is for putting info into long-term storage and letting agents search it, often using tools.  
* LangChain offers practical tools like ConversationBufferMemory to automatically inject the history of a single conversation into a prompt, enabling an agent to recall immediate context.  
* LangGraph enables advanced, long-term memory by using a store to save and retrieve semantic facts, episodic experiences, or even updatable procedural rules across different user sessions.  
* Memory Bank is a managed service that provides agents with persistent, long-term memory by automatically extracting, storing, and recalling user-specific information to enable personalized, continuous conversations across frameworks like Google's ADK, LangGraph, and CrewAI.

> 快速回顾：记忆对跟踪、学习与个性化至关重要；对话 AI 需短期上下文与跨会话长期知识；短期常受上下文窗口或框架传参限制；长期多存于向量库等外部存储并以检索访问；ADK 用 `Session`/`State`/`MemoryService` 分工；`SessionService` 管会话生命周期与 events/state；`session.state` 为字典，前缀 `user:`/`app:`/`temp:` 标明归属与持久性；应通过 `EventActions.state_delta` 或 `output_key` 更新 state，避免直接改字典；`MemoryService` 负责写入与检索长期知识；LangChain 的 `ConversationBufferMemory` 等可把单会话历史注入提示；LangGraph 的 store 支持语义/情景/可更新程序性规则等高级长期记忆；Memory Bank 是托管长期记忆服务，自动抽取、存储与召回用户信息，可与 ADK、LangGraph、CrewAI 等配合。

## Conclusion

> ## 结语

This chapter dove into the really important job of memory management for agent systems, showing the difference between the short-lived context and the knowledge that sticks around for a long time. We talked about how these types of memory are set up and where you see them used in building smarter agents that can remember things. We took a detailed look at how Google ADK gives you specific pieces like Session, State, and MemoryService to handle this. Now that we've covered how agents can remember things, both short-term and long-term, we can move on to how they can learn and adapt. The next pattern ​​"Learning and Adaptation" is about an agent changing how it thinks, acts, or what it knows, all based on new experiences or data.

> 本章深入智能体系统的记忆管理，区分易逝上下文与长期留存的知识，并说明这些记忆类型如何配置、在更「会记」的智能体中如何出现；详解 Google ADK 的 `Session`、`State` 与 `MemoryService`。在理解短长期记忆之后，下一模式「学习与适应」讨论智能体如何基于新经验或数据改变思考、行为或所知。

## References

1. ADK Memory, [https://google.github.io/adk-docs/sessions/memory/](https://google.github.io/adk-docs/sessions/memory/)
2. LangGraph Memory, [https://langchain-ai.github.io/langgraph/concepts/memory/](https://langchain-ai.github.io/langgraph/concepts/memory/)
3. Vertex AI Agent Engine Memory Bank, [https://cloud.google.com/blog/products/ai-machine-learning/vertex-ai-memory-bank-in-public-preview](https://cloud.google.com/blog/products/ai-machine-learning/vertex-ai-memory-bank-in-public-preview)
