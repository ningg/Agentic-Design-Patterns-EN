# Appendix E - AI Agents on the CLI

> **附录 E：命令行上的 AI 智能体**

## Introduction

> ## 引言

​​The developer's command line, long a bastion of precise, imperative commands, is undergoing a profound transformation. It is evolving from a simple shell into an intelligent, collaborative workspace powered by a new class of tools: AI Agent Command-Line Interfaces (CLIs). These agents move beyond merely executing commands; they understand natural language, maintain context about your entire codebase, and can perform complex, multi-step tasks that automate significant parts of the development lifecycle.

> 开发者的命令行长期是精确、命令式指令的堡垒，如今正经历深刻变革：从简单 shell 演进为由一类新工具——AI 智能体命令行界面（CLI）——驱动的智能协作工作空间。这些智能体不止执行命令，还能理解自然语言、维护对整个代码库的上下文，并能完成复杂多步任务，自动化开发生命周期中的大量环节。

This guide provides an in-depth look at four leading players in this burgeoning field, exploring their unique strengths, ideal use cases, and distinct philosophies to help you determine which tool best fits your workflow. It is important to note that many of the example use cases provided for a specific tool can often be accomplished by the other agents as well. The key differentiator between these tools frequently lies in the quality, efficiency, and nuance of the results they are able to achieve for a given task. There are specific benchmarks designed to measure these capabilities, which will be discussed in the following sections.

> 本指南深入介绍该新兴领域的四个主要参与者，探讨其各自优势、适用场景与理念差异，帮助你判断哪款工具最契合自己的工作流。需注意：为某一工具列举的许多示例用例，其他智能体往往也能完成；工具之间的关键差异，常常体现在对特定任务所能达到的结果质量、效率与细腻度上。下文将讨论用于衡量这些能力的专门基准测试。

## Claude CLI (Claude Code)

> ## Claude CLI（Claude Code）

Anthropic's Claude CLI is engineered as a high-level coding agent with a deep, holistic understanding of a project's architecture. Its core strength is its "agentic" nature, allowing it to create a mental model of your repository for complex, multi-step tasks. The interaction is highly conversational, resembling a pair programming session where it explains its plans before executing. This makes it ideal for professional developers working on large-scale projects involving significant refactoring or implementing features with broad architectural impacts.

> Anthropic 的 Claude CLI 被设计为高层编码智能体，能整体、深入地理解项目架构。其核心优势在于「智能体」属性：可为复杂多步任务在仓库上建立心智模型。交互高度对话化，类似结对编程——执行前会说明计划。因此适合从事大规模项目、重大重构或具有广泛架构影响功能实现的专业开发者。

**Example Use Cases:**

> **示例用例：**

1. **Large-Scale Refactoring:** You can instruct it: "Our current user authentication relies on session cookies. Refactor the entire codebase to use stateless JWTs, updating the login/logout endpoints, middleware, and frontend token handling." Claude will then read all relevant files and perform the coordinated changes.  
> 1. **大规模重构：** 可指示：「我们当前用户认证依赖会话 cookie。将整个代码库重构为使用无状态 JWT，更新登录/登出端点、中间件与前端令牌处理。」Claude 会阅读相关文件并协调完成修改。  
2. **API Integration:** After being provided with an OpenAPI specification for a new weather service, you could say: "Integrate this new weather API. Create a service module to handle the API calls, add a new component to display the weather, and update the main dashboard to include it."  
> 2. **API 集成：** 在提供新天气服务的 OpenAPI 规范后，可说：「集成这个新的天气 API。创建服务模块处理 API 调用，新增展示天气的组件，并更新主仪表板以包含该功能。」  
3. **Documentation Generation**: Pointing it to a complex module with poorly documented code, you can ask: "Analyze the `./src/utils/data_processing.js` file. Generate comprehensive TSDoc comments for every function, explaining its purpose, parameters, and return value."  
> 3. **文档生成：** 指向文档不足的复杂模块，可要求：「分析 `./src/utils/data_processing.js` 文件。为每个函数生成完整 TSDoc 注释，说明用途、参数与返回值。」

Claude CLI functions as a specialized coding assistant, with inherent tools for core development tasks, including file ingestion, code structure analysis, and edit generation. Its deep integration with Git facilitates direct branch and commit management. The agent's extensibility is mediated by the Multi-tool Control Protocol (MCP), enabling users to define and integrate custom tools. This allows for interactions with private APIs, database queries, and execution of project-specific scripts. This architecture positions the developer as the arbiter of the agent's functional scope, effectively characterizing Claude as a reasoning engine augmented by user-defined tooling.

> Claude CLI 作为专业编码助手，内置文件摄取、代码结构分析与编辑生成等核心开发能力。与 Git 深度集成便于直接管理分支与提交。智能体的可扩展性通过多工具控制协议（MCP）实现，用户可定义并集成自定义工具，从而对接私有 API、数据库查询与项目特定脚本。该架构使开发者成为智能体功能边界的裁定者，实质上把 Claude 刻画为由用户定义工具增强的推理引擎。

## Gemini CLI

> ## Gemini CLI

Google's Gemini CLI is a versatile, open-source AI agent designed for power and accessibility. It stands out with the advanced Gemini 2.5 Pro model, a massive context window, and multimodal capabilities (processing images and text). Its open-source nature, generous free tier, and "Reason and Act" loop make it a transparent, controllable, and excellent all-rounder for a broad audience, from hobbyists to enterprise developers, especially those within the Google Cloud ecosystem.

> Google 的 Gemini CLI 是面向能力与易用性的多功能开源 AI 智能体。其突出点包括先进的 Gemini 2.5 Pro 模型、超大上下文窗口以及多模态能力（处理图像与文本）。开源、慷慨的免费额度与「推理—行动」循环使其透明、可控，是从爱好者到企业开发者（尤其身处 Google Cloud 生态者）的出色全能选择。

**Example Use Cases:**

> **示例用例：**

1. **Multimodal Development:** You provide a screenshot of a web component from a design file (gemini describe component.png) and instruct it: "Write the HTML and CSS code to build a React component that looks exactly like this. Make sure it's responsive."  
> 1. **多模态开发：** 提供设计稿中某 Web 组件的截图（gemini describe component.png）并指示：「编写 HTML 与 CSS，构建外观与此完全一致的 React 组件，并确保响应式。」  
2. **Cloud Resource Management:** Using its built-in Google Cloud integration, you can command: "Find all GKE clusters in the production project that are running versions older than 1.28 and generate a gcloud command to upgrade them one by one."  
> 2. **云资源管理：** 借助内置 Google Cloud 集成，可命令：「找出生产项目中所有运行版本低于 1.28 的 GKE 集群，并生成逐个升级的 gcloud 命令。」  
3. **Enterprise Tool Integration (via MCP):** A developer provides Gemini with a custom tool called get-employee-details that connects to the company's internal HR API. The prompt is: "Draft a welcome document for our new hire. First, use the get-employee-details --id=E90210 tool to fetch their name and team, and then populate the welcome_template.md with that information."  
> 3. **企业工具集成（经 MCP）：** 开发者为 Gemini 提供名为 get-employee-details、连接公司内部 HR API 的自定义工具。提示为：「为新员工起草欢迎文档。先用 get-employee-details --id=E90210 获取其姓名与团队，再将信息填入 welcome_template.md。」  
4. **Large-Scale Refactoring**: A developer needs to refactor a large Java codebase to replace a deprecated logging library with a new, structured logging framework. They can use Gemini with a prompt like: Read all *.java files in the 'src/main/java' directory. For each file, replace all instances of the 'org.apache.log4j' import and its 'Logger' class with 'org.slf4j.Logger' and 'LoggerFactory'. Rewrite the logger instantiation and all .info(), .debug(), and .error() calls to use the new structured format with key-value pairs.  
> 4. **大规模重构：** 开发者需将大型 Java 代码库中已弃用的日志库替换为新的结构化日志框架，可使用类似提示：读取 `src/main/java` 下所有 `*.java` 文件；对每个文件，将所有 `org.apache.log4j` 导入及其 `Logger` 类替换为 `org.slf4j.Logger` 与 `LoggerFactory`；重写 logger 实例化及所有 `.info()`、`.debug()`、`.error()` 调用，改用带键值对的新结构化格式。

Gemini CLI is equipped with a suite of built-in tools that allow it to interact with its environment. These include tools for file system operations (like reading and writing), a shell tool for running commands, and tools for accessing the internet via web fetching and searching. For broader context, it uses specialized tools to read multiple files at once and a memory tool to save information for later sessions. This functionality is built on a secure foundation: sandboxing isolates the model's actions to prevent risk, while MCP servers act as a bridge, enabling Gemini to safely connect to your local environment or other APIs.

> Gemini CLI 配备一组内置工具以与环境交互，包括文件系统读写、用于运行命令的 shell 工具，以及通过抓取与搜索访问互联网的工具。为获取更广上下文，还提供一次读取多文件的工具及跨会话保存信息的记忆工具。这些能力建立在安全基础之上：沙箱隔离模型行为以降低风险；MCP 服务器作为桥梁，使 Gemini 能安全连接本地环境或其他 API。

## Aider

> ## Aider

Aider is an open-source AI coding assistant that acts as a true pair programmer by working directly on your files and committing changes to Git. Its defining feature is its directness; it applies edits, runs tests to validate them, and automatically commits every successful change. Being model-agnostic, it gives users complete control over cost and capabilities. Its git-centric workflow makes it perfect for developers who value efficiency, control, and a transparent, auditable trail of all code modifications.

> Aider 是开源 AI 编码助手，通过直接修改文件并向 Git 提交变更，扮演真正的结对程序员。其鲜明特点是直接：应用编辑、运行测试验证，并在每次成功后自动提交。与具体模型解耦，用户可完全掌控成本与能力。以 Git 为中心的工作流适合重视效率、可控性以及所有代码变更可追溯、可审计的开发者。

**Example Use Cases:**

> **示例用例：**

1. **Test-Driven Development (TDD):** A developer can say: "Create a failing test for a function that calculates the factorial of a number." After Aider writes the test and it fails, the next prompt is: "Now, write the code to make the test pass." Aider implements the function and runs the test again to confirm.  
> 1. **测试驱动开发（TDD）：** 开发者可说：「为计算数字阶乘的函数写一个会失败的测试。」Aider 写好测试并失败后，下一句提示：「现在编写使测试通过的代码。」Aider 实现函数并再次运行测试确认。  
2. **Precise Bug Squashing:** Given a bug report, you can instruct Aider: "The `calculate_total` function in billing.py fails on leap years. Add the file to the context, fix the bug, and verify your fix against the existing test suite."  
> 2. **精准修 bug：** 根据缺陷报告可指示：「`billing.py` 中的 `calculate_total` 在闰年出错。把该文件加入上下文，修复问题，并用现有测试套件验证。」  
3. **Dependency Updates:** You could instruct it: "Our project uses an outdated version of the 'requests' library. Please go through all Python files, update the import statements and any deprecated function calls to be compatible with the latest version, and then update requirements.txt."  
> 3. **依赖更新：** 可指示：「项目使用的 `requests` 库版本过旧。请遍历所有 Python 文件，更新 import 与已弃用调用以兼容最新版，并更新 requirements.txt。」

## GitHub Copilot CLI

> ## GitHub Copilot CLI

GitHub Copilot CLI extends the popular AI pair programmer into the terminal, with its primary advantage being its native, deep integration with the GitHub ecosystem. It understands the context of a project *within GitHub*. Its agent capabilities allow it to be assigned a GitHub issue, work on a fix, and submit a pull request for human review.

> GitHub Copilot CLI 将广受欢迎的 AI 结对编程能力延伸到终端，主要优势是与 GitHub 生态的原生深度集成。它能理解项目在 *GitHub 内*的上下文。其智能体能力可承接 GitHub issue、着手修复并提交拉取请求供人工审阅。

**Example Use Cases:**

> **示例用例：**

1. **Automated Issue Resolution:** A manager assigns a bug ticket (e.g., "Issue #123: Fix off-by-one error in pagination") to the Copilot agent. The agent then checks out a new branch, writes the code, and submits a pull request referencing the issue, all without manual developer intervention.  
> 1. **自动化处理 Issue：** 管理者将缺陷单（如「Issue #123：修复分页的 off-by-one 错误」）指派给 Copilot 智能体；智能体检出分支、编写代码并提交引用该 issue 的 PR，全程无需开发者手动介入。  
2. **Repository-Aware Q\&A:** A new developer on the team can ask: "Where in this repository is the database connection logic defined, and what environment variables does it require?" Copilot CLI uses its awareness of the entire repo to provide a precise answer with file paths.  
> 2. **仓库感知问答：** 新成员可问：「本仓库中数据库连接逻辑在哪里定义，需要哪些环境变量？」Copilot CLI 利用对整个仓库的感知给出含文件路径的精确答案。  
3. **Shell Command Helper:** When unsure about a complex shell command, a user can ask: gh? find all files larger than 50MB, compress them, and place them in an archive folder. Copilot will generate the exact shell command needed to perform the task.  
> 3. **Shell 命令助手：** 面对复杂 shell 命令不确定时，用户可问：gh? find all files larger than 50MB, compress them, and place them in an archive folder。Copilot 会生成完成任务所需的确切 shell 命令。

## Terminal-Bench: A Benchmark for AI Agents in Command-Line Interfaces

> ## Terminal-Bench：命令行界面中 AI 智能体的基准测试

Terminal-Bench is a novel evaluation framework designed to assess the proficiency of AI agents in executing complex tasks within a command-line interface. The terminal is identified as an optimal environment for AI agent operation due to its text-based, sandboxed nature. The initial release, Terminal-Bench-Core-v0, comprises 80 manually curated tasks spanning domains such as scientific workflows and data analysis. To ensure equitable comparisons, Terminus, a minimalistic agent, was developed to serve as a standardized testbed for various language models. The framework is designed for extensibility, allowing for the integration of diverse agents through containerization or direct connections. Future developments include enabling massively parallel evaluations and incorporating established benchmarks. The project encourages open-source contributions for task expansion and collaborative framework enhancement.

> Terminal-Bench 是用于评估 AI 智能体在命令行界面中执行复杂任务熟练度的新型评估框架。终端因其基于文本、可沙箱化的特性，被视为智能体运行的理想环境。初始版本 Terminal-Bench-Core-v0 包含 80 道人工精选任务，覆盖科学工作流与数据分析等领域。为保证公平比较，开发了极简智能体 Terminus，作为多种语言模型的标准化试验台。框架可扩展，支持通过容器化或直接连接集成不同智能体。未来计划包括大规模并行评估与纳入既有基准。项目欢迎开源贡献以扩充任务并共同完善框架。

## Conclusion

> ## 结论

The emergence of these powerful AI command-line agents marks a fundamental shift in software development, transforming the terminal into a dynamic and collaborative environment. As we've seen, there is no single "best" tool; instead, a vibrant ecosystem is forming where each agent offers a specialized strength. The ideal choice depends entirely on the developer's needs: Claude for complex architectural tasks, Gemini for versatile and multimodal problem-solving, Aider for git-centric and direct code editing, and GitHub Copilot for seamless integration into the GitHub workflow. As these tools continue to evolve, proficiency in leveraging them will become an essential skill, fundamentally changing how developers build, debug, and manage software.

> 这些强大的 AI 命令行智能体的出现标志着软件开发的根本性转变，使终端成为动态、协作的环境。如我们所见，没有唯一的「最佳」工具；相反，一个充满活力的生态正在形成，各智能体各有所长。理想选择完全取决于开发者需求：复杂架构任务选 Claude，多用途与多模态解题选 Gemini，以 Git 为中心的直接改代码选 Aider，与 GitHub 工作流无缝衔接选 GitHub Copilot。随着工具持续演进，熟练运用它们将成为核心技能，从根本上改变开发者构建、调试与管理软件的方式。

## References

1. Anthropic. *Claude*. [https://docs.anthropic.com/en/docs/claude-code/cli-reference](https://docs.anthropic.com/en/docs/claude-code/cli-reference)
2. Google Gemini Cli [https://github.com/google-gemini/gemini-cli](https://github.com/google-gemini/gemini-cli)
3. Aider. [https://aider.chat/](https://aider.chat/)  
4. GitHub *Copilot CLI* [https://docs.github.com/en/copilot/github-copilot-enterprise/copilot-cli](https://docs.github.com/en/copilot/github-copilot-enterprise/copilot-cli)  
5. Terminal Bench: [https://www.tbench.ai/](https://www.tbench.ai/)
