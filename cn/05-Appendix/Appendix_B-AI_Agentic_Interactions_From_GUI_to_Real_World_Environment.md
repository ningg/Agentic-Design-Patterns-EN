# Appendix B - AI Agentic Interactions: From GUI to Real World environment

> 附录 B：AI 智能体交互——从图形界面到真实世界环境

AI agents are increasingly performing complex tasks by interacting with digital interfaces and the physical world. Their ability to perceive, process, and act within these varied environments is fundamentally transforming automation, human-computer interaction, and intelligent systems. This appendix explores how agents interact with computers and their environments, highlighting advancements and projects.

> 智能体正越来越多地通过与数字界面和物理世界交互来完成复杂任务。其在多样环境中感知、处理并行动的能力，正在从根本上改变自动化、人机交互与智能系统。本附录探讨智能体如何与计算机及其环境交互，并突出相关进展与项目。

## Interaction: Agents with Computers

> ## 交互：智能体与计算机

The evolution of AI from conversational partners to active, task-oriented agents is being driven by Agent-Computer Interfaces (ACIs). These interfaces allow AI to interact directly with a computer's Graphical User Interface (GUI), enabling it to perceive and manipulate visual elements like icons and buttons just as a human would. This new method moves beyond the rigid, developer-dependent scripts of traditional automation that relied on APIs and system calls. By using the visual "front door" of software, AI can now automate complex digital tasks in a more flexible and powerful way, a process that involves several key stages:

> AI 从对话伙伴演进为主动、面向任务的智能体，其驱动力来自智能体–计算机接口（ACI）。这些接口使 AI 能直接与计算机的图形用户界面（GUI）交互，像人一样感知并操作图标、按钮等视觉元素。新方法超越了依赖 API 与系统调用、僵硬且依赖开发者的传统自动化脚本。通过使用软件的视觉“正门”，AI 能以更灵活、更强大的方式自动化复杂数字任务，这一过程包含若干关键阶段：

- **Visual Perception:** The agent first captures a visual representation of the screen, essentially taking a screenshot.  
- **GUI Element Recognition:** It then analyzes this image to distinguish between various GUI elements. It must learn to "see" the screen not as a mere collection of pixels, but as a structured layout with interactive components, discerning a clickable "Submit" button from a static banner image or an editable text field from a simple label.  
- **Contextual Interpretation:** The ACI module, acting as a bridge between the visual data and the agent's core intelligence (often a Large Language Model or LLM), interprets these elements within the context of the task. It understands that a magnifying glass icon typically means "search" or that a series of radio buttons represents a choice. This module is crucial for enhancing the LLM's reasoning, allowing it to form a plan based on visual evidence.  
- **Dynamic Action and Response:** The agent then programmatically controls the mouse and keyboard to execute its plan—clicking, typing, scrolling, and dragging. Critically, it must constantly monitor the screen for visual feedback, dynamically responding to changes, loading screens, pop-up notifications, or errors to successfully navigate multi-step workflows.

> - **视觉感知：** 智能体首先捕获屏幕的视觉表示，本质上即截屏。  
> - **GUI 元素识别：** 随后分析图像以区分各类 GUI 元素。它必须学会把屏幕“看成”带交互组件的结构化布局，而非像素堆砌；区分可点击的“提交”按钮与静态横幅、可编辑文本框与纯标签。  
> - **语境解释：** ACI 模块在视觉数据与智能体核心智能（通常为大语言模型或 LLM）之间充当桥梁，在任务语境下解释这些元素；理解放大镜图标通常表示“搜索”、一组单选按钮表示选择等。该模块对增强 LLM 推理至关重要，使其能基于视觉证据形成计划。  
> - **动态行动与响应：** 智能体再以编程方式控制鼠标与键盘执行计划——点击、输入、滚动、拖拽。关键是持续监视屏幕上的视觉反馈，动态响应变化、加载界面、弹窗或错误，以顺利完成多步工作流。

This technology is no longer theoretical. Several leading AI labs have developed functional agents that demonstrate the power of GUI interaction:

> 该技术已非纸上谈兵。多家领先 AI 实验室已推出可工作的智能体，展示 GUI 交互的力量：

**ChatGPT Operator (OpenAI):** Envisioned as a digital partner, ChatGPT Operator is designed to automate tasks across a wide range of applications directly from the desktop. It understands on-screen elements, enabling it to perform actions like transferring data from a spreadsheet into a customer relationship management (CRM) platform, booking a complex travel itinerary across airline and hotel websites, or filling out detailed online forms without needing specialized API access for each service. This makes it a universally adaptable tool aimed at boosting both personal and enterprise productivity by taking over repetitive digital chores.

> **ChatGPT Operator（OpenAI）：** 定位为数字伙伴，旨在从桌面直接跨多种应用自动化任务。它能理解屏幕元素，从而执行如将电子表格数据转入客户关系管理（CRM）平台、在航司与酒店网站预订复杂行程、填写详细在线表单等操作，而无需为每项服务单独接入 API。通过接管重复性数字杂务，它成为面向个人与企业生产力、具有广泛适应性的工具。

**Google Project Mariner:** As a research prototype, Project Mariner operates as an agent within the Chrome browser (see Fig. 1). Its purpose is to understand a user's intent and autonomously carry out web-based tasks on their behalf. For example, a user could ask it to find three apartments for rent within a specific budget and neighborhood; Mariner would then navigate to real estate websites, apply the filters, browse the listings, and extract the relevant information into a document. This project represents Google's exploration into creating a truly helpful and "agentive" web experience where the browser actively works for the user.

> **Google Project Mariner：** 作为研究原型，Mariner 在 Chrome 浏览器内以智能体方式运行（见图 1）。其目标是理解用户意图并代其自主完成基于网页的任务。例如，用户可要求它在特定预算与社区内找三处出租公寓；Mariner 会访问房产网站、应用筛选、浏览房源并将相关信息提取到文档中。该项目体现 Google 在探索真正有用、“智能体化”的网页体验——让浏览器主动为用户工作。

Interaction between Agent and the Web Browser

Fig.1: Interaction between and Agent and the Web Browser

> 图 1：智能体与网页浏览器之间的交互

**Anthropic's Computer Use:** This feature empowers Anthropic's AI model, Claude, to become a direct user of a computer's desktop environment. By capturing screenshots to perceive the screen and programmatically controlling the mouse and keyboard, Claude can orchestrate workflows that span multiple, unconnected applications. A user could ask it to analyze data in a PDF report, open a spreadsheet application to perform calculations on that data, generate a chart, and then paste that chart into an email draft—a sequence of tasks that previously required constant human input.

> **Anthropic 的 Computer Use：** 该能力使 Anthropic 的模型 Claude 成为桌面环境的直接“用户”。通过截屏感知屏幕并以编程方式控制鼠标与键盘，Claude 可编排跨多个互不关联应用的工作流。例如，分析 PDF 报告中的数据、打开电子表格计算、生成图表再粘贴到邮件草稿——这类序列以往需要持续人工介入。

**Browser Use**: This  is an open-source library that provides a high-level API for programmatic browser automation. It enables AI agents to interface with web pages by granting them access to and control over the Document Object Model (DOM). The API abstracts the intricate, low-level commands of browser control protocols, into a more simplified and intuitive set of functions. This allows an agent to perform complex sequences of actions, including data extraction from nested elements, form submissions, and automated navigation across multiple pages. As a result, the library facilitates the transformation of unstructured web data into a structured format that an AI agent can systematically process and utilize for analysis or decision-making.

> **Browser Use：** 这是一个开源库，为程序化浏览器自动化提供高层 API。它通过赋予智能体访问与控制文档对象模型（DOM）的能力，使其能与网页交互。API 将浏览器控制协议中繁琐的低层命令抽象为更简单、更直观的一组函数，使智能体能执行复杂动作序列，包括从嵌套元素提取数据、提交表单、跨多页自动导航等，从而将非结构化网页数据转为可供 AI 系统化处理并用于分析或决策的结构化格式。

## Interaction: Agents with the Environment

> ## 交互：智能体与环境

Beyond the confines of a computer screen, AI agents are increasingly designed to interact with complex, dynamic environments, often mirroring the real world. This requires sophisticated perception, reasoning, and actuation capabilities.

> 超越屏幕边界，智能体越来越多地被设计为与复杂、动态、常映射真实世界的环境交互，这需要成熟的感知、推理与执行能力。

Google's **Project Astra** is a prime example of an initiative pushing the boundaries of agent interaction with the environment. Astra aims to create a universal AI agent that is helpful in everyday life, leveraging multimodal inputs (sight, sound, voice) and outputs to understand and interact with the world contextually. This project focuses on rapid understanding, reasoning, and response, allowing the agent to "see" and "hear" its surroundings through cameras and microphones and engage in natural conversation while providing real-time assistance. Astra's vision is an agent that can seamlessly assist users with tasks ranging from finding lost items to debugging code, by understanding the environment it observes. This moves beyond simple voice commands to a truly embodied understanding of the user's immediate physical context.

> Google 的 **Project Astra** 是推动智能体与环境交互边界的典型倡议。Astra 旨在打造在日常生活中有用的通用 AI 智能体，利用多模态输入（视、听、语音）与输出，在语境中理解并与世界交互。项目强调快速理解、推理与响应，使智能体通过摄像头与麦克风“看见”“听见”周遭，在自然对话中提供实时协助。其愿景是：通过理解所观察环境，无缝协助从寻找失物到调试代码等任务，超越简单语音指令，走向对用户即时物理语境的真正具身理解。

Google's **Gemini Live**, transforms standard AI interactions into a fluid and dynamic conversation. Users can speak to the AI and receive responses in a natural-sounding voice with minimal delay, and can even interrupt or change topics mid-sentence, prompting the AI to adapt immediately. The interface expands beyond voice, allowing users to incorporate visual information by using their phone's camera, sharing their screen, or uploading files for a more context-aware discussion. More advanced versions can even perceive a user's tone of voice and intelligently filter out irrelevant background noise to better understand the conversation. These capabilities combine to create rich interactions, such as receiving live instructions on a task by simply pointing a camera at it.

> Google 的 **Gemini Live** 将标准 AI 交互变为流畅、动态的会话。用户可与 AI 对话并以自然音色、低延迟获得回应，甚至可在句中打断或换题，促使 AI 立即适应。界面不止于语音：用户可用手机摄像头、共享屏幕或上传文件纳入视觉信息，使讨论更贴合语境。更先进的版本还能感知用户语气并智能滤除无关背景噪声以更好理解对话。这些能力共同支持丰富交互，例如将摄像头对准任务即可获得实时操作指导。

OpenAI's **GPT-4o model** is an alternative designed for "omni" interaction, meaning it can reason across voice, vision, and text. It processes these inputs with low latency that mirrors human response times, which allows for real-time conversations. For example, users can show the AI a live video feed to ask questions about what is happening, or use it for language translation. OpenAI provides developers with a "Realtime API" to build applications requiring low-latency, speech-to-speech interactions.

> OpenAI 的 **GPT-4o 模型** 面向“全模态（omni）”交互设计，可在语音、视觉与文本间联合推理。它以接近人类反应时间的低延迟处理这些输入，支持实时对话。例如，用户可展示实时视频流并询问正在发生什么，或用于语言翻译。OpenAI 为开发者提供 “Realtime API”，以构建需要低延迟语音到语音交互的应用。

OpenAI's **ChatGPT Agent** represents a significant architectural advancement over its predecessors, featuring an integrated framework of new capabilities. Its design incorporates several key functional modalities: the capacity for autonomous navigation of the live internet for real-time data extraction, the ability to dynamically generate and execute computational code for tasks like data analysis, and the functionality to interface directly with third-party software applications. The synthesis of these functions allows the agent to orchestrate and complete complex, sequential workflows from a singular user directive. It can therefore autonomously manage entire processes, such as performing market analysis and generating a corresponding presentation, or planning logistical arrangements and executing the necessary transactions. In parallel with the launch, OpenAI has proactively addressed the emergent safety considerations inherent in such a system. An accompanying "System Card" delineates the potential operational hazards associated with an AI capable of performing actions online, acknowledging the new vectors for misuse. To mitigate these risks, the agent's architecture includes engineered safeguards, such as requiring explicit user authorization for certain classes of actions and deploying robust content filtering mechanisms. The company is now engaging its initial user base to further refine these safety protocols through a feedback-driven, iterative process.

> OpenAI 的 **ChatGPT Agent** 相对前代在架构上有显著进步，整合了新能力框架。其设计包含若干关键功能模态：自主浏览实时互联网以提取数据、动态生成并执行计算代码（如数据分析）、直接与第三方软件对接。这些能力的综合使智能体能从单一用户指令编排并完成复杂顺序工作流，从而自主管理全流程，例如做市场分析并生成相应演示文稿，或规划物流并执行必要交易。与发布同步，OpenAI 主动应对此类系统固有的新兴安全考量；随附的 “System Card” 勾画了能在网上执行操作的 AI 可能带来的运行风险，承认新的滥用途径。为缓解风险，架构内置工程化防护，如对某类操作要求用户明确授权、部署强健的内容过滤机制。公司正通过反馈驱动的迭代过程，与早期用户共同细化这些安全协议。

**Seeing AI,** a complimentary mobile application from Microsoft, empowers individuals who are blind or have low vision by offering real-time narration of their surroundings. The app leverages artificial intelligence through the device's camera to identify and describe various elements, including objects, text, and even people. Its core functionalities encompass reading documents, recognizing currency, identifying products through barcodes, and describing scenes and colors. By providing enhanced access to visual information, Seeing AI ultimately fosters greater independence for visually impaired users.

> **Seeing AI** 是微软推出的免费移动应用，通过实时旁白周围环境，赋能视障或低视力人士。应用借助设备摄像头与 AI 识别并描述物体、文本乃至人物等。核心功能包括朗读文档、识别货币、通过条码识别商品、描述场景与颜色等。通过增强对视觉信息的获取，Seeing AI 最终有助于视障用户提升独立性。

**Anthropic's Claude 4 Series** Anthropic's Claude 4 is another alternative with capabilities for advanced reasoning and analysis. Though historically focused on text, Claude 4 includes robust vision capabilities, allowing it to process information from images, charts, and documents. The model is suited for handling complex, multi-step tasks and providing detailed analysis. While the real-time conversational aspect is not its primary focus compared to other models, its underlying intelligence is designed for building highly capable AI agents.

> **Anthropic 的 Claude 4 系列** Claude 4 是另一具备高级推理与分析能力的选择。虽历史上偏重文本，Claude 4 具备强健的视觉能力，可处理图像、图表与文档中的信息。该模型适合处理复杂多步任务并提供细致分析。与其他模型相比，实时对话并非其首要侧重，但其底层智能面向构建高能力 AI 智能体而设计。

## Vibe Coding: Intuitive Development with AI

> ## Vibe Coding：与 AI 的直觉式开发

Beyond direct interaction with GUIs and the physical world, a new paradigm is emerging in how developers build software with AI: "vibe coding." This approach moves away from precise, step-by-step instructions and instead relies on a more intuitive, conversational, and iterative interaction between the developer and an AI coding assistant. The developer provides a high-level goal, a desired "vibe," or a general direction, and the AI generates code to match.

> 除与 GUI 及物理世界的直接交互外，开发者用 AI 构建软件的方式也在出现新范式：“vibe coding”。它不再依赖精确逐步指令，而更多依靠开发者与 AI 编程助手之间直觉化、对话式、迭代的互动。开发者给出高层目标、期望的“气质（vibe）”或大方向，由 AI 生成相应代码。

This process is characterized by:

> 该过程的特点包括：

- **Conversational Prompts:** Instead of writing detailed specifications, a developer might say, "Create a simple, modern-looking landing page for a new app," or, "Refactor this function to be more Pythonic and readable." The AI interprets the "vibe" of "modern" or "Pythonic" and generates the corresponding code.  
- **Iterative Refinement:** The initial output from the AI is often a starting point. The developer then provides feedback in natural language, such as, "That's a good start, but can you make the buttons blue?" or, "Add some error handling to that." This back-and-forth continues until the code meets the developer's expectations.  
- **Creative Partnership:** In vibe coding, the AI acts as a creative partner, suggesting ideas and solutions that the developer may not have considered. This can accelerate the development process and lead to more innovative outcomes.  
- **Focus on "What" not "How":** The developer focuses on the desired outcome (the "what") and leaves the implementation details (the "how") to the AI. This allows for rapid prototyping and exploration of different approaches without getting bogged down in boilerplate code.  
- **Optional Memory Banks:** To maintain context across longer interactions, developers can use "memory banks" to store key information, preferences, or constraints. For example, a developer might save a specific coding style or a set of project requirements to the AI's memory, ensuring that future code generations remain consistent with the established "vibe" without needing to repeat the instructions.

> - **对话式提示：** 不写冗长规格，开发者可以说“为新应用做一个简洁现代的落地页”，或“把这个函数改得更 Pythonic、更易读”。AI 解读“现代”“Pythonic”等气质并生成对应代码。  
> - **迭代打磨：** AI 的初稿常只是起点；开发者再用自然语言反馈，如“不错，能把按钮改成蓝色吗？”或“那里加点错误处理”，往复直至满足预期。  
> - **创意伙伴：** 在 vibe coding 中，AI 扮演创意伙伴，提出开发者可能未想到的点子与方案，可加速开发并带来更具创新性的结果。  
> - **关注“做什么”而非“怎么做”：** 开发者聚焦期望结果（what），把实现细节（how）交给 AI，便于快速原型与探索不同路径，而不陷入样板代码。  
> - **可选记忆库：** 为在长对话中保持语境，可用“记忆库”保存关键信息、偏好或约束；例如保存特定代码风格或项目需求，使后续生成与既定“气质”一致而无需重复说明。

Vibe coding is becoming increasingly popular with the rise of powerful AI models like GPT-4, Claude, and Gemini, which are integrated into development environments. These tools are not just auto-completing code; they are actively participating in the creative process of software development, making it more accessible and efficient. This new way of working is changing the nature of software engineering, emphasizing creativity and high-level thinking over rote memorization of syntax and APIs.

> 随着 GPT-4、Claude、Gemini 等强大模型融入开发环境，vibe coding 日益流行。这些工具不仅是自动补全，而是积极参与软件开发的创意过程，使开发更易上手、更高效。这种工作方式正在改变软件工程的面貌：更强调创意与高层思考，而非死记语法与 API。

## Key takeaways

> ## 要点

- AI agents are evolving from simple automation to visually controlling software through graphical user interfaces, much like a human would.  
- The next frontier is real-world interaction, with projects like Google's Astra using cameras and microphones to see, hear, and understand their physical surroundings.  
- Leading technology companies are converging these digital and physical capabilities to create universal AI assistants that operate seamlessly across both domains.  
- This shift is creating a new class of proactive, context-aware AI companions capable of assisting with a vast range of tasks in users' daily lives.

> - 智能体正从简单自动化演进为像人一样通过图形用户界面视觉化操控软件。  
> - 下一前沿是真实世界交互，如 Google Astra 等项目用摄像头与麦克风感知、聆听并理解物理环境。  
> - 领先科技公司正融合数字与物理能力，打造在两个领域无缝运作的通用 AI 助手。  
> - 这一转变正在催生一类主动、语境感知的 AI 伙伴，能在用户日常生活中协助广泛任务。

## Conclusion

> ## 结语

Agents are undergoing a significant transformation, moving from basic automation to sophisticated interaction with both digital and physical environments. By leveraging visual perception to operate Graphical User Interfaces, these agents can now manipulate software just as a human would, bypassing the need for traditional APIs. Major technology labs are pioneering this space with agents capable of automating complex, multi-application workflows directly on a user's desktop. Simultaneously, the next frontier is expanding into the physical world, with initiatives like Google's Project Astra using cameras and microphones to contextually engage with their surroundings. These advanced systems are designed for multimodal, real-time understanding that mirrors human interaction.

> 智能体正经历重大转型：从基础自动化走向与数字与物理环境的复杂交互。借助视觉感知操作 GUI，它们能像人一样操控软件，绕过对传统 API 的依赖。大型技术实验室正引领该领域，使用户桌面上能自动化跨多应用的复杂工作流。同时，下一前沿伸向物理世界，如 Google Project Astra 等倡议用摄像头与麦克风在语境中与周遭互动。这些先进系统面向多模态、实时、贴近人类交互的理解而设计。

The ultimate vision is a convergence of these digital and physical capabilities, creating universal AI assistants that operate seamlessly across all of a user's environments. This evolution is also reshaping software creation itself through "vibe coding," a more intuitive and conversational partnership between developers and AI. This new method prioritizes high-level goals and creative intent, allowing developers to focus on the desired outcome rather than implementation details. This shift accelerates development and fosters innovation by treating AI as a creative partner. Ultimately, these advancements are paving the way for a new era of proactive, context-aware AI companions capable of assisting with a vast array of tasks in our daily lives.

> 终极愿景是融合数字与物理能力，打造在用户各类环境中无缝运作的通用 AI 助手。这一演进也通过 “vibe coding” 重塑软件创造本身——开发者与 AI 之间更直觉、更对话式的协作。新方法优先高层目标与创意意图，使开发者聚焦期望结果而非实现细节；把 AI 视为创意伙伴可加速开发、促进创新。归根结底，这些进展正为新时代铺路：主动、语境感知的 AI 伙伴能在日常生活中协助极其广泛的任务。

## References

> 参考文献：以下条目保留英文与原始链接，不作逐条翻译。

1. Open AI Operator, [https://openai.com/index/introducing-operator/](https://openai.com/index/introducing-operator/)
2. Open AI ChatGPT Agent: [https://openai.com/index/introducing-chatgpt-agent/](https://openai.com/index/introducing-chatgpt-agent/)
3. Browser Use: [https://docs.browser-use.com/introduction](https://docs.browser-use.com/introduction)
4. Project Mariner, [https://deepmind.google/models/project-mariner/](https://deepmind.google/models/project-mariner/)
5. Anthropic Computer use: [https://docs.anthropic.com/en/docs/build-with-claude/computer-use](https://docs.anthropic.com/en/docs/build-with-claude/computer-use)
6. Project Astra, [https://deepmind.google/models/project-astra/](https://deepmind.google/models/project-astra/)
7. Gemini Live, [https://gemini.google/overview/gemini-live/?hl=en](https://gemini.google/overview/gemini-live/?hl=en)
8. OpenAI's GPT-4,  [https://openai.com/index/gpt-4-research/](https://openai.com/index/gpt-4-research/)
9. Claude 4, [https://www.anthropic.com/news/claude-4](https://www.anthropic.com/news/claude-4)