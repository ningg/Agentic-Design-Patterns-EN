# Appendix A: Advanced Prompting Techniques

> 附录 A：高级提示技术

## Introduction to Prompting

> ## 提示简介

Prompting, the primary interface for interacting with language models, is the process of crafting inputs to guide the model towards generating a desired output. This involves structuring requests, providing relevant context, specifying the output format, and demonstrating expected response types. Well-designed prompts can maximize the potential of language models, resulting in accurate, relevant, and creative responses. In contrast, poorly designed prompts can lead to ambiguous, irrelevant, or erroneous outputs.

> 提示（Prompting）是与语言模型交互的主要界面，指设计输入以引导模型生成期望输出的过程。这包括组织请求、提供相关语境、指定输出格式，并示范期望的回应类型。设计良好的提示能充分发挥语言模型的潜力，得到准确、相关且富有创意的回答；设计不当则易导致含糊、无关或错误的输出。

The objective of prompt engineering is to consistently elicit high-quality responses from language models. This requires understanding the capabilities and limitations of the models and effectively communicating intended goals. It involves developing expertise in communicating with AI by learning how to best instruct it.

> 提示工程的目标是稳定地从语言模型获得高质量回答。这需要理解模型的能力与局限，并有效传达意图目标；也意味着通过学习如何最好地“指挥”AI，来培养与 AI 沟通的专业能力。

This appendix details various prompting techniques that extend beyond basic interaction methods. It explores methodologies for structuring complex requests, enhancing the model's reasoning abilities, controlling output formats, and integrating external information. These techniques are applicable to building a range of applications, from simple chatbots to complex multi-agent systems, and can improve the performance and reliability of agentic applications.

> 本附录介绍多种超越基础交互的提示技术，探讨如何组织复杂请求、增强模型推理、控制输出格式以及整合外部信息。这些技术可用于从简单聊天机器人到复杂多智能体系统的各类应用，并有助于提升智能体应用的性能与可靠性。

Agentic patterns, the architectural structures for building intelligent systems, are detailed in the main chapters. These patterns define how agents plan, utilize tools, manage memory, and collaborate. The efficacy of these agentic systems is contingent upon their ability to interact meaningfully with language models.

> 智能体模式（构建智能系统的架构结构）在正文中详述；它们定义智能体如何规划、使用工具、管理记忆与协作。这些智能体系统能否奏效，取决于其与语言模型能否进行有意义的交互。

## Core Prompting Principles

> ## 核心提示原则

Core Principles for Effective Prompting of Language Models:

> 对语言模型进行有效提示的核心原则：

Effective prompting rests on fundamental principles guiding communication with language models, applicable across various models and task complexities. Mastering these principles is essential for consistently generating useful and accurate responses.

> 有效提示建立在指导人与语言模型沟通的基本原则之上，适用于不同模型与任务复杂度。掌握这些原则，才能持续产生有用且准确的回答。

**Clarity and Specificity**: Instructions should be unambiguous and precise. Language models interpret patterns; multiple interpretations may lead to unintended responses. Define the task, desired output format, and any limitations or requirements. Avoid vague language or assumptions. Inadequate prompts yield ambiguous and inaccurate responses, hindering meaningful output.

> **清晰与具体：** 指令应无歧义且精确。语言模型依赖模式解读；多种理解可能导致非预期回答。应明确任务、期望输出格式以及限制或要求；避免模糊表述或隐含假设。不足的提示会产生含糊、不准确的回答，阻碍有效输出。

**Conciseness**: While specificity is crucial, it should not compromise conciseness. Instructions should be direct. Unnecessary wording or complex sentence structures can confuse the model or obscure the primary instruction. Prompts should be simple; what is confusing to the user is likely confusing to the model. Avoid intricate language and superfluous information. Use direct phrasing and active verbs to clearly delineate the desired action. Effective verbs include: Act, Analyze, Categorize, Classify, Contrast, Compare, Create, Describe, Define, Evaluate, Extract, Find, Generate, Identify, List, Measure, Organize, Parse, Pick, Predict, Provide, Rank, Recommend, Return, Retrieve, Rewrite, Select, Show, Sort, Summarize, Translate, Write.

> **简洁：** 具体很重要，但不应以冗长为代价。指令应直截了当。多余措辞或复杂句式可能迷惑模型或掩盖主要指令。提示宜简单——让用户困惑的，往往也会让模型困惑。避免绕弯与冗余信息，用直接措辞和主动动词标明期望动作。常用有效动词包括：Act、Analyze、Categorize、Classify、Contrast、Compare、Create、Describe、Define、Evaluate、Extract、Find、Generate、Identify、List、Measure、Organize、Parse、Pick、Predict、Provide、Rank、Recommend、Return、Retrieve、Rewrite、Select、Show、Sort、Summarize、Translate、Write。

**Using Verbs:** Verb choice is a key prompting tool. Action verbs indicate the expected operation. Instead of "Think about summarizing this," a direct instruction like "Summarize the following text" is more effective. Precise verbs guide the model to activate relevant training data and processes for that specific task.

> **使用动词：** 动词选择是关键提示手段。动作动词标明期望的操作。与其说“想想怎么总结这段”，不如直接说“总结以下文本”。精确的动词有助于激活与该任务相关的训练知识与处理路径。

**Instructions Over Constraints:** Positive instructions are generally more effective than negative constraints. Specifying the desired action is preferred to outlining what not to do. While constraints have their place for safety or strict formatting, excessive reliance can cause the model to focus on avoidance rather than the objective. Frame prompts to guide the model directly. Positive instructions align with human guidance preferences and reduce confusion.

> **指令优于约束：** 正面说明“要做什么”通常比罗列“不要做什么”更有效。在安全或严格格式等场景下约束有其位置，但过度依赖会让模型把注意力放在规避而非目标上。应用提示直接引导模型；正面指令更符合人类指导习惯，也减少误解。

**Experimentation and Iteration:** Prompt engineering is an iterative process. Identifying the most effective prompt requires multiple attempts. Begin with a draft, test it, analyze the output, identify shortcomings, and refine the prompt. Model variations, configurations (like temperature or top-p), and slight phrasing changes can yield different results. Documenting attempts is vital for learning and improvement. Experimentation and iteration are necessary to achieve the desired performance.

> **实验与迭代：** 提示工程是迭代过程，最有效的提示往往需要多次尝试。从草稿开始，测试、分析输出、找出不足并改进提示；不同模型变体、配置（如 temperature、top-p）以及细微措辞变化都会带来不同结果。记录尝试对学习改进至关重要；要达到期望表现，实验与迭代必不可少。

These principles form the foundation of effective communication with language models. By prioritizing clarity, conciseness, action verbs, positive instructions, and iteration, a robust framework is established for applying more advanced prompting techniques.

> 这些原则构成与语言模型有效沟通的基础。优先保证清晰、简洁、动作动词、正面指令与迭代，便能为运用更高级的提示技术打下稳固框架。

## Basic Prompting Techniques

> ## 基础提示技术

Building on core principles, foundational techniques provide language models with varying levels of information or examples to direct their responses. These methods serve as an initial phase in prompt engineering and are effective for a wide spectrum of applications.

> 在核心原则之上，基础技术通过提供不同程度的信息或示例来引导模型回答，是提示工程的起步阶段，适用于广泛的应用场景。

### Zero-Shot Prompting

> ### 零样本提示（Zero-Shot）

Zero-shot prompting is the most basic form of prompting, where the language model is provided with an instruction and input data without any examples of the desired input-output pair. It relies entirely on the model's pre-training to understand the task and generate a relevant response. Essentially, a zero-shot prompt consists of a task description and initial text to begin the process.

> 零样本提示是最基础的形式：只给指令与输入，不提供期望的输入—输出示例对。它完全依赖预训练来理解任务并生成相关回答；本质上由任务描述与起始文本构成。

* **When to use:** Zero-shot prompting is often sufficient for tasks that the model has likely encountered extensively during its training, such as simple question answering, text completion, or basic summarization of straightforward text. It's the quickest approach to try first.  
* **Example:**  
  Translate the following English sentence to French: 'Hello, how are you?'

> * **何时使用：** 对模型在训练中可能大量见过的任务（如简单问答、续写、对直白文本做基础摘要）往往足够；也是应最先尝试的最快路径。  
> * **示例：**  
>   将下列英文句子译成法语：'Hello, how are you?'

### One-Shot Prompting

> ### 单样本提示（One-Shot）

One-shot prompting involves providing the language model with a single example of the input and the corresponding desired output prior to presenting the actual task. This method serves as an initial demonstration to illustrate the pattern the model is expected to replicate. The purpose is to equip the model with a concrete instance that it can use as a template to effectively execute the given task.

> 单样本提示在呈现真实任务前，先提供一个输入与对应期望输出的示例，作为示范以说明模型应复现的模式，让模型有具体模板可依。

* **When to use:** One-shot prompting is useful when the desired output format or style is specific or less common. It gives the model a concrete instance to learn from. It can improve performance compared to zero-shot for tasks requiring a particular structure or tone.  
* **Example:**  
  Translate the following English sentences to Spanish:  
  English: 'Thank you.'  
  Spanish: 'Gracias.'

  English: 'Please.'  
  Spanish:

> * **何时使用：** 当期望的输出格式或风格较特殊、较少见时很有用；给模型一个具体实例学习，相对零样本在需要特定结构或语气时往往更好。  
> * **示例：**  
>   将下列英文句子译成西班牙语：  
>   English: 'Thank you.'  
>   Spanish: 'Gracias.'  
>  
>   English: 'Please.'  
>   Spanish:

### Few-Shot Prompting

> ### 少样本提示（Few-Shot）

Few-shot prompting enhances one-shot prompting by supplying several examples, typically three to five, of input-output pairs. This aims to demonstrate a clearer pattern of expected responses, improving the likelihood that the model will replicate this pattern for new inputs. This method provides multiple examples to guide the model to follow a specific output pattern.

> 少样本提示在单样本基础上提供若干（通常三到五组）输入—输出对，以更清晰地展示期望模式，提高模型对新输入复现该模式的可能性。

* **When to use:** Few-shot prompting is particularly effective for tasks where the desired output requires adhering to a specific format, style, or exhibiting nuanced variations. It's excellent for tasks like classification, data extraction with specific schemas, or generating text in a particular style, especially when zero-shot or one-shot don't yield consistent results. Using at least three to five examples is a general rule of thumb, adjusting based on task complexity and model token limits.  
* **Importance of Example Quality and Diversity:** The effectiveness of few-shot prompting heavily relies on the quality and diversity of the examples provided. Examples should be accurate, representative of the task, and cover potential variations or edge cases the model might encounter. High-quality, well-written examples are crucial; even a small mistake can confuse the model and result in undesired output. Including diverse examples helps the model generalize better to unseen inputs.  
* **Mixing Up Classes in Classification Examples:** When using few-shot prompting for classification tasks (where the model needs to categorize input into predefined classes), it's a best practice to mix up the order of the examples from different classes. This prevents the model from potentially overfitting to the specific sequence of examples and ensures it learns to identify the key features of each class independently, leading to more robust and generalizable performance on unseen data.  
* **Evolution to "Many-Shot" Learning:** As modern LLMs like Gemini get stronger with long context modeling, they are becoming highly effective at utilizing "many-shot" learning. This means optimal performance for complex tasks can now be achieved by including a much larger number of examples—sometimes even hundreds—directly within the prompt, allowing the model to learn more intricate patterns.  
* **Example:**  
  Classify the sentiment of the following movie reviews as POSITIVE, NEUTRAL, or NEGATIVE:

  Review: "The acting was superb and the story was engaging."  
  Sentiment: POSITIVE

  Review: "It was okay, nothing special."  
  Sentiment: NEUTRAL

  Review: "I found the plot confusing and the characters unlikable."  
  Sentiment: NEGATIVE

  Review: "The visuals were stunning, but the dialogue was weak."  
  Sentiment:

> * **何时使用：** 当输出需严格遵循特定格式、风格或呈现细微变化时特别有效；适合分类、按模式抽取数据、按特定文风生成等，尤其在零样本/单样本不稳定时。一般建议至少三到五例，并按任务复杂度与 token 上限调整。  
> * **示例质量与多样性的重要性：** 少样本效果高度依赖示例质量与多样性。示例应准确、具代表性，并覆盖模型可能遇到的变体或边界情况；写得好的示例至关重要，小错误也可能误导模型。多样化示例有助于更好泛化到未见输入。  
> * **分类任务中打乱类别顺序：** 用于分类时，最佳实践是打乱不同类别的示例顺序，避免模型过拟合于示例顺序，促使其独立学习各类关键特征，从而在未见数据上更稳健、可泛化。  
> * **向“多样本”演进：** 随着 Gemini 等现代 LLM 长上下文能力增强，“多样本”学习越来越有效；复杂任务有时可在提示中直接放入大量（甚至数百）示例，以学习更精细的模式。  
> * **示例：**  
>   将下列影评情感分类为 POSITIVE、NEUTRAL 或 NEGATIVE：  
>  
>   Review: "The acting was superb and the story was engaging."  
>   Sentiment: POSITIVE  
>  
>   Review: "It was okay, nothing special."  
>   Sentiment: NEUTRAL  
>  
>   Review: "I found the plot confusing and the characters unlikable."  
>   Sentiment: NEGATIVE  
>  
>   Review: "The visuals were stunning, but the dialogue was weak."  
>   Sentiment:

Understanding when to apply zero-shot, one-shot, and few-shot prompting techniques, and thoughtfully crafting and organizing examples, are essential for enhancing the effectiveness of agentic systems. These basic methods serve as the groundwork for various prompting strategies.

> 理解何时采用零样本、单样本与少样本，并认真设计与组织示例，对提升智能体系统效果至关重要；这些基础方法是各类提示策略的基石。

## Structuring Prompts

> ## 组织提示的结构

Beyond the basic techniques of providing examples, the way you structure your prompt plays a critical role in guiding the language model. Structuring involves using different sections or elements within the prompt to provide distinct types of information, such as instructions, context, or examples, in a clear and organized manner. This helps the model parse the prompt correctly and understand the specific role of each piece of text.

> 除提供示例外，提示的组织方式对引导模型至关重要。结构化指在提示中用不同区块或元素清晰呈现指令、语境、示例等信息，帮助模型正确解析并理解各部分作用。

### System Prompting

> ### 系统提示（System Prompting）

System prompting sets the overall context and purpose for a language model, defining its intended behavior for an interaction or session. This involves providing instructions or background information that establish rules, a persona, or overall behavior. Unlike specific user queries, a system prompt provides foundational guidelines for the model's responses. It influences the model's tone, style, and general approach throughout the interaction. For example, a system prompt can instruct the model to consistently respond concisely and helpfully or ensure responses are appropriate for a general audience. System prompts are also utilized for safety and toxicity control by including guidelines such as maintaining respectful language.

> 系统提示为语言模型设定交互或会话的整体语境与目的，规定预期行为：通过指令或背景建立规则、人格或总体风格。与具体用户问题不同，它为回答提供基础性指引，影响语气、风格与整体取向；也可用于安全与毒性控制（如保持尊重用语）。

Furthermore, to maximize their effectiveness, system prompts can undergo automatic prompt optimization through LLM-based iterative refinement. Services like the Vertex AI Prompt Optimizer facilitate this by systematically improving prompts based on user-defined metrics and target data, ensuring the highest possible performance for a given task.

> 为提升效果，系统提示还可经由基于 LLM 的迭代优化自动改进；Vertex AI Prompt Optimizer 等服务可依据用户定义指标与目标数据系统改进提示，以在特定任务上尽量提高表现。

* **Example:**  
  You are a helpful and harmless AI assistant. Respond to all queries in a polite and informative manner. Do not generate content that is harmful, biased, or inappropriate

> * **示例：**  
>   You are a helpful and harmless AI assistant. Respond to all queries in a polite and informative manner. Do not generate content that is harmful, biased, or inappropriate

### Role Prompting

> ### 角色提示（Role Prompting）

Role prompting assigns a specific character, persona, or identity to the language model, often in conjunction with system or contextual prompting. This involves instructing the model to adopt the knowledge, tone, and communication style associated with that role. For example, prompts such as "Act as a travel guide" or "You are an expert data analyst" guide the model to reflect the perspective and expertise of that assigned role. Defining a role provides a framework for the tone, style, and focused expertise, aiming to enhance the quality and relevance of the output. The desired style within the role can also be specified, for instance, "a humorous and inspirational style."

> 角色提示为语言模型指定人物、人格或身份，常与系统或语境提示配合，使其采用该角色相关的知识、语气与沟通风格。例如 “担任导游” 或 “你是资深数据分析师” 可引导模型从该视角输出；也可进一步指定风格，如幽默且鼓舞人心。

* **Example:**  
  Act as a seasoned travel blogger. Write a short, engaging paragraph about the best hidden gem in Rome.

> * **示例：**  
>   Act as a seasoned travel blogger. Write a short, engaging paragraph about the best hidden gem in Rome.

### Using Delimiters

> ### 使用分隔符

Effective prompting involves clear distinction of instructions, context, examples, and input for language models. Delimiters, such as triple backticks (```), XML tags (<instruction>, <context>), or markers (---), can be utilized to visually and programmatically separate these sections. This practice, widely used in prompt engineering, minimizes misinterpretation by the model, ensuring clarity regarding the role of each part of the prompt.

> 有效提示需清晰区分指令、语境、示例与输入。可用三重反引号（```）、XML 标签（如 `<instruction>`、`<context>`）或标记（---）等在视觉与程序上分隔各段，减少模型误读，明确各部分职责。

* **Example:**  
  <instruction>Summarize the following article, focusing on the main arguments presented by the author.</instruction>  
  <article>  
  [Insert the full text of the article here]  
  </article>

> * **示例：**  
>   <instruction>Summarize the following article, focusing on the main arguments presented by the author.</instruction>  
>   <article>  
>   [Insert the full text of the article here]  
>   </article>

## Contextual Engineering

> ## 语境工程（Contextual Engineering）

Context engineering, unlike static system prompts, dynamically provides background information crucial for tasks and conversations. This ever-changing information helps models grasp nuances, recall past interactions, and integrate relevant details, leading to grounded responses and smoother exchanges. Examples include previous dialogue, relevant documents (as in Retrieval Augmented Generation), or specific operational parameters. For instance, when discussing a trip to Japan, one might ask for three family-friendly activities in Tokyo, leveraging the existing conversational context. In agentic systems, context engineering is fundamental to core agent behaviors like memory persistence, decision-making, and coordination across sub-tasks. Agents with dynamic contextual pipelines can sustain goals over time, adapt strategies, and collaborate seamlessly with other agents or tools—qualities essential for long-term autonomy. This methodology posits that the quality of a model's output depends more on the richness of the provided context than on the model's architecture. It signifies a significant evolution from traditional prompt engineering, which primarily focused on optimizing the phrasing of immediate user queries. Context engineering expands its scope to include multiple layers of information.

> 与静态系统提示不同，语境工程动态提供任务与对话所需背景信息，帮助模型把握细微差别、回忆过往交互并整合相关细节，使回答更贴地、交流更顺畅。例如历史对话、相关文档（如 RAG）、或运行参数。在智能体系统中，语境工程支撑记忆持久、决策与子任务协调等核心行为；动态语境管线有助于长期维持目标、调整策略并与其他智能体或工具协作。该方法强调：输出质量更多取决于所供语境的丰富度，而非仅取决于模型架构；相对传统提示工程主要优化当下问句措辞，语境工程把范围扩展到多层信息。

These layers include:

> 这些层次包括：

* **System prompts:** Foundational instructions that define the AI's operational parameters (e.g., "You are a technical writer; your tone must be formal and precise").  
* **External data:**  
  * **Retrieved documents:** Information actively fetched from a knowledge base to inform responses (e.g., pulling technical specifications).  
  * **Tool outputs:** Results from the AI using an external API for real-time data (e.g., querying a calendar for availability).  
* **Implicit data:** Critical information such as user identity, interaction history, and environmental state. Incorporating implicit context presents challenges related to privacy and ethical data management. Therefore, robust governance is essential for context engineering, especially in sectors like enterprise, healthcare, and finance.

> * **系统提示：** 定义 AI 运行参数的基础指令（例如 “你是技术写作者；语气须正式、精确”）。  
> * **外部数据：**  
>   * **检索文档：** 从知识库主动取回以支撑回答的信息（如拉取技术规格）。  
>   * **工具输出：** 调用外部 API 得到的实时数据（如查日历可用时段）。  
> * **隐式数据：** 用户身份、交互历史、环境状态等关键信息。纳入隐式语境涉及隐私与伦理数据管理挑战，因此尤其在企业、医疗、金融等领域需要健全治理。

The core principle is that even advanced models underperform with a limited or poorly constructed view of their operational environment. This practice reframes the task from merely answering a question to building a comprehensive operational picture for the agent. For example, a context-engineered agent would integrate a user's calendar availability (tool output), the professional relationship with an email recipient (implicit data), and notes from previous meetings (retrieved documents) before responding to a query. This enables the model to generate highly relevant, personalized, and pragmatically useful outputs. The "engineering" aspect involves creating robust pipelines to fetch and transform this data at runtime and establishing feedback loops to continually improve context quality.

> 核心原则是：即便先进模型，若对其运行环境视图狭窄或构建不当，表现也会下降。该实践把任务从“回答问题”重构为“为智能体构建完整运行图景”。例如整合用户日历（工具输出）、与收件人的职业关系（隐式数据）、过往会议笔记（检索文档）后再作答，可产生高度相关、个性化且务实有用的输出。“工程”侧则指在运行时拉取与转换数据的稳健管线，以及持续改进语境质量的反馈闭环。

To implement this, specialized tuning systems, such as Google's Vertex AI prompt optimizer, can automate the improvement process at scale. By systematically evaluating responses against sample inputs and predefined metrics, these tools can enhance model performance and adapt prompts and system instructions across different models without extensive manual rewriting. Providing an optimizer with sample prompts, system instructions, and a template allows it to programmatically refine contextual inputs, offering a structured method for implementing the necessary feedback loops for sophisticated Context Engineering.  
This structured approach differentiates a rudimentary AI tool from a more sophisticated, contextually-aware system. It treats context as a primary component, emphasizing what the agent knows, when it knows it, and how it uses that information. This practice ensures the model has a well-rounded understanding of the user's intent, history, and current environment. Ultimately, Context Engineering is a crucial methodology for transforming stateless chatbots into highly capable, situationally-aware systems.

> 实现上，Google Vertex AI prompt optimizer 等专用调优系统可规模化自动改进；通过对样例输入与预定义指标系统评估回答，可提升表现并在不同模型间适配提示与系统指令而无需大量手工改写。向优化器提供样例提示、系统指令与模板，可程序化精炼语境输入，为复杂语境工程建立结构化反馈闭环。  
> 这种结构化路径区分简陋 AI 工具与更成熟、具语境感知能力的系统：把语境视为首要组件，强调智能体知道什么、何时知道、如何使用。它确保模型对用户意图、历史与当前环境有周全理解；归根结底，语境工程是把无状态聊天机器人转变为高能力、情境感知系统的关键方法。

## Structured Output

> ## 结构化输出

Often, the goal of prompting is not just to get a free-form text response, but to extract or generate information in a specific, machine-readable format. Requesting structured output, such as JSON, XML, CSV, or Markdown tables, is a crucial structuring technique. By explicitly asking for the output in a particular format and potentially providing a schema or example of the desired structure, you guide the model to organize its response in a way that can be easily parsed and used by other parts of your agentic system or application. Returning JSON objects for data extraction is beneficial as it forces the model to create a structure and can limit hallucinations. Experimenting with output formats is recommended, especially for non-creative tasks like extracting or categorizing data.

> 提示的目标常不仅是自由文本，而是以可机读格式抽取或生成信息。明确要求 JSON、XML、CSV 或 Markdown 表等结构化输出是关键技巧；可配合模式或示例，引导模型组织回答，便于智能体系统其他部分解析使用。抽取类任务返回 JSON 有助于强制结构与抑制幻觉。尤其对非创意任务（抽取、分类等），建议多试验输出格式。

* **Example:**  
  Extract the following information from the text below and return it as a JSON object with keys `name`, `address`, and `phone.number`.

  Text: "Contact John Smith at 123 Main St, Anytown, CA or call (555) 123-4567."

> * **示例：**  
>   Extract the following information from the text below and return it as a JSON object with keys `name`, `address`, and `phone.number`.  
>  
>   Text: "Contact John Smith at 123 Main St, Anytown, CA or call (555) 123-4567."

Effectively utilizing system prompts, role assignments, contextual information, delimiters, and structured output significantly enhances the clarity, control, and utility of interactions with language models, providing a strong foundation for developing reliable agentic systems. Requesting structured output is crucial for creating pipelines where the language model's output serves as the input for subsequent system or processing steps.

> 有效运用系统提示、角色、语境信息、分隔符与结构化输出，可显著提升与语言模型交互的清晰度、可控性与实用性，为构建可靠智能体系统奠定基础；结构化输出对构建“模型输出作为下游步骤输入”的流水线尤为关键。

**Leveraging Pydantic for an Object-Oriented Facade:** A powerful technique for enforcing structured output and enhancing interoperability is to use the LLM's generated data to populate instances of Pydantic objects. Pydantic is a Python library for data validation and settings management using Python type annotations. By defining a Pydantic model, you create a clear and enforceable schema for your desired data structure. This approach effectively provides an object-oriented facade to the prompt's output, transforming raw text or semi-structured data into validated, type-hinted Python objects.

> **用 Pydantic 做面向对象门面：** 强化结构化输出与互操作性的一种有力做法，是用 LLM 生成数据填充 Pydantic 对象。Pydantic 是基于 Python 类型注解做数据校验与配置管理的库；定义模型即得到清晰可执行的期望结构模式，相当于为提示输出提供 OO 门面，把原始文本或半结构化数据变为经校验、带类型提示的对象。

You can directly parse a JSON string from an LLM into a Pydantic object using the `model.validate.json` method. This is particularly useful as it combines parsing and validation in a single step.

> 可直接使用 `model.validate.json` 方法将 LLM 的 JSON 字符串解析为 Pydantic 对象；一步同时完成解析与校验，尤为实用。

```python
from pydantic import BaseModel, EmailStr, Field, ValidationError
from typing import List, Optional
from datetime import date


# --- Pydantic Model Definition (from above) ---
class User(BaseModel):
    name: str = Field(..., description="The full name of the user.")
    email: EmailStr = Field(..., description="The user's email address.")
    date_of_birth: Optional[date] = Field(None, description="The user's date of birth.")
    interests: List[str] = Field(default_factory=list, description="A list of the user's interests.")


# --- Hypothetical LLM Output ---
llm_output_json = """
{
    "name": "Alice Wonderland",
    "email": "alice.w@example.com",
    "date_of_birth": "1995-07-21",
    "interests": [
        "Natural Language Processing",
        "Python Programming",
        "Gardening"
    ]
}
"""


# --- Parsing and Validation ---
try:
    # Use the model_validate_json class method to parse the JSON string.
    # This single step parses the JSON and validates the data against the User model.
    user_object = User.model_validate_json(llm_output_json)

    # Now you can work with a clean, type-safe Python object.
    print("Successfully created User object!")
    print(f"Name: {user_object.name}")
    print(f"Email: {user_object.email}")
    print(f"Date of Birth: {user_object.date_of_birth}")
    print(f"First Interest: {user_object.interests[0]}")

    # You can access the data like any other Python object attribute.
    # Pydantic has already converted the 'date_of_birth' string to a datetime.date object.
    print(f"Type of date_of_birth: {type(user_object.date_of_birth)}")
except ValidationError as e:
    # If the JSON is malformed or the data doesn't match the model's types,
    # Pydantic will raise a ValidationError.
    print("Failed to validate JSON from LLM.")
    print(e)
```

This Python code demonstrates how to use the Pydantic library to define a data model and validate JSON data. It defines a User model with fields for name, email, date of birth, and interests, including type hints and descriptions. The code then parses a hypothetical JSON output from a Large Language Model (LLM) using the `model.validate.json` method of the User model. This method handles both JSON parsing and data validation according to the model's structure and types. Finally, the code accesses the validated data from the resulting Python object and includes error handling for ValidationError in case the JSON is invalid.

> 上述代码演示如何用 Pydantic 定义数据模型并校验 JSON：User 模型含姓名、邮箱、出生日期与兴趣等字段及类型与描述；用 User 模型的 `model.validate.json` 方法解析假设的 LLM JSON 输出，同时按结构与类型校验；最后访问已校验对象并在 JSON 无效时捕获 `ValidationError`。

For XML data, the xmltodict library can be used to convert the XML into a dictionary, which can then be passed to a Pydantic model for parsing. By using Field aliases in your Pydantic model, you can seamlessly map the often verbose or attribute-heavy structure of XML to your object's fields.

> 对 XML 数据，可用 xmltodict 转为字典再交给 Pydantic 解析；在模型中使用 `Field` 别名，可把冗长或属性繁多的 XML 结构映射到对象字段。

This methodology is invaluable for ensuring the interoperability of LLM-based components with other parts of a larger system. When an LLM's output is encapsulated within a Pydantic object, it can be reliably passed to other functions, APIs, or data processing pipelines with the assurance that the data conforms to the expected structure and types. This practice of "parse, don't validate" at the boundaries of your system components leads to more robust and maintainable applications.

> 该方法对保证基于 LLM 的组件与更大系统其他部分的互操作极有价值：输出封装在 Pydantic 对象中，可可靠地传给函数、API 或数据处理流水线，并确信结构与类型符合预期。在系统边界“解析即校验”（parse, don't validate）的做法使应用更稳健、更易维护。

Effectively utilizing system prompts, role assignments, contextual information, delimiters, and structured output significantly enhances the clarity, control, and utility of interactions with language models, providing a strong foundation for developing reliable agentic systems. Requesting structured output is crucial for creating pipelines where the language model's output serves as the input for subsequent system or processing steps.

> 再次强调：系统提示、角色、语境、分隔符与结构化输出的有效运用，能显著提升交互的清晰、可控与实用，并为可靠智能体系统打基础；结构化输出是构建下游流水线输入的关键。

Structuring Prompts Beyond the basic techniques of providing examples, the way you structure your prompt plays a critical role in guiding the language model. Structuring involves using different sections or elements within the prompt to provide distinct types of information, such as instructions, context, or examples, in a clear and organized manner. This helps the model parse the prompt correctly and understand the specific role of each piece of text.

> （原文重述“组织提示”段落）除提供示例外，提示结构对引导语言模型至关重要：用不同区块清晰呈现指令、语境、示例等信息，帮助模型正确解析并理解各部分作用。

# Reasoning and Thought Process Techniques

> # 推理与思维过程技术

Large language models excel at pattern recognition and text generation but often face challenges with tasks requiring complex, multi-step reasoning. This appendix focuses on techniques designed to enhance these reasoning capabilities by encouraging models to reveal their internal thought processes. Specifically, it addresses methods to improve logical deduction, mathematical computation, and planning.

> 大语言模型擅长模式识别与文本生成，但在需要复杂多步推理的任务上常遇困难。本附录聚焦通过促使模型展现内部思维过程来增强推理能力，涵盖改进逻辑演绎、数学运算与规划等方法。

## Chain of Thought (CoT)

> ## 思维链（Chain of Thought, CoT）

The Chain of Thought (CoT) prompting technique is a powerful method for improving the reasoning abilities of language models by explicitly prompting the model to generate intermediate reasoning steps before arriving at a final answer. Instead of just asking for the result, you instruct the model to "think step by step." This process mirrors how a human might break down a problem into smaller, more manageable parts and work through them sequentially.

> 思维链提示通过明确要求模型在给出最终答案前生成中间推理步骤，以提升推理能力；不只索要结果，而是指示其“逐步思考”，类似人类把问题拆小并按序推进。

CoT helps the LLM generate more accurate answers, particularly for tasks that require some form of calculation or logical deduction, where models might otherwise struggle and produce incorrect results. By generating these intermediate steps, the model is more likely to stay on track and perform the necessary operations correctly.

> CoT 有助于 LLM 在需要计算或逻辑演绎的任务上生成更准确答案；否则模型易跑偏或算错。中间步骤使模型更可能沿正确路径完成必要运算。

There are two main variations of CoT:

> CoT 主要有两种变体：

* **Zero-Shot CoT:** This involves simply adding the phrase "Let's think step by step" (or similar phrasing) to your prompt without providing any examples of the reasoning process. Surprisingly, for many tasks, this simple addition can significantly improve the model's performance by triggering its ability to expose its internal reasoning trace.  
  * **Example (Zero-Shot CoT):**  
    If a train travels at 60 miles per hour and covers a distance of 240 miles, how long did the journey take? Let's think step by step.

* **Few-Shot CoT:** This combines CoT with few-shot prompting. You provide the model with several examples where both the input, the step-by-step reasoning process, and the final output are shown. This gives the model a clearer template for how to perform the reasoning and structure its response, often leading to even better results on more complex tasks compared to zero-shot CoT.  
  * **Example (Few-Shot CoT):**  
    Q: The sum of three consecutive integers is 36. What are the integers?  
    A: Let the first integer be x. The next consecutive integer is x+1, and the third is x+2. The sum is x + (x+1) + (x+2) \= 3x + 3. We know the sum is 36, so 3x + 3 \= 36. Subtract 3 from both sides: 3x \= 33. Divide by 3: x \= 11. The integers are 11, 11+1=12, and 11+2=13. The integers are 11, 12, and 13.

    Q: Sarah has 5 apples, and she buys 8 more. She eats 3 apples. How many apples does she have left? Let's think step by step.  
    A: Let's think step by step. Sarah starts with 5 apples. She buys 8 more, so she adds 8 to her initial amount: 5 + 8 \= 13 apples. Then, she eats 3 apples, so we subtract 3 from the total: 13 - 3 \= 10. Sarah has 10 apples left. The answer is 10.

> * **零样本 CoT：** 在提示中加入 “Let's think step by step”（或类似措辞），不提供推理过程示例；对许多任务，这一简单补充就能显著提升表现，促使模型展开内部推理痕迹。  
>   * **示例（零样本 CoT）：**  
>     If a train travels at 60 miles per hour and covers a distance of 240 miles, how long did the journey take? Let's think step by step.  
> * **少样本 CoT：** 将 CoT 与少样本结合，提供多组含输入、逐步推理与最终输出的示例，给模型更清晰的推理与结构模板，复杂任务上常优于零样本 CoT。  
>   * **示例（少样本 CoT）：**  
>     Q: The sum of three consecutive integers is 36. What are the integers?  
>     A: Let the first integer be x. The next consecutive integer is x+1, and the third is x+2. The sum is x + (x+1) + (x+2) \= 3x + 3. We know the sum is 36, so 3x + 3 \= 36. Subtract 3 from both sides: 3x \= 33. Divide by 3: x \= 11. The integers are 11, 11+1=12, and 11+2=13. The integers are 11, 12, and 13.  
>  
>     Q: Sarah has 5 apples, and she buys 8 more. She eats 3 apples. How many apples does she have left? Let's think step by step.  
>     A: Let's think step by step. Sarah starts with 5 apples. She buys 8 more, so she adds 8 to her initial amount: 5 + 8 \= 13 apples. Then, she eats 3 apples, so we subtract 3 from the total: 13 - 3 \= 10. Sarah has 10 apples left. The answer is 10.

CoT offers several advantages. It is relatively low-effort to implement and can be highly effective with off-the-shelf LLMs without requiring fine-tuning. A significant benefit is the increased interpretability of the model's output; you can see the reasoning steps it followed, which helps in understanding why it arrived at a particular answer and in debugging if something went wrong. Additionally, CoT appears to improve the robustness of prompts across different versions of language models, meaning the performance is less likely to degrade when a model is updated. The main disadvantage is that generating the reasoning steps increases the length of the output, leading to higher token usage, which can increase costs and response time.

> CoT 的优点包括实现成本相对较低、无需微调即可在现成 LLM 上往往很有效；输出可解释性高，便于理解答案由来与排错；在不同版本模型间似乎更稳健。主要缺点是推理步骤拉长输出、增加 token 与费用、延长响应时间。

Best practices for CoT include ensuring the final answer is presented *after* the reasoning steps, as the generation of the reasoning influences the subsequent token predictions for the answer. Also, for tasks with a single correct answer (like mathematical problems), setting the model's temperature to 0 (greedy decoding) is recommended when using CoT to ensure deterministic selection of the most probable next token at each step.

> CoT 最佳实践：最终答案应放在推理步骤*之后*，因推理生成会影响后续对答案的 token 预测。对单一正确答案类任务（如数学题），使用 CoT 时建议 temperature 设为 0（贪心解码），使每步选最可能 token 更确定。

## Self-Consistency

> ## 自洽性（Self-Consistency）

Building on the idea of Chain of Thought, the Self-Consistency technique aims to improve the reliability of reasoning by leveraging the probabilistic nature of language models. Instead of relying on a single greedy reasoning path (as in basic CoT), Self-Consistency generates multiple diverse reasoning paths for the same problem and then selects the most consistent answer among them.

> 在思维链之上，自洽性利用语言模型的概率性：不只走一条贪心推理路径，而是对同一问题生成多条不同推理路径，再从中选出最一致的答案。

Self-Consistency involves three main steps:

> 自洽性包含三个主要步骤：

1. **Generating Diverse Reasoning Paths:** The same prompt (often a CoT prompt) is sent to the LLM multiple times. By using a higher temperature setting, the model is encouraged to explore different reasoning approaches and generate varied step-by-step explanations.  
2. **Extract the Answer:** The final answer is extracted from each of the generated reasoning paths.  
3. **Choose the Most Common Answer:** A majority vote is performed on the extracted answers. The answer that appears most frequently across the diverse reasoning paths is selected as the final, most consistent answer.

> 1. **生成多样推理路径：** 同一提示（常为 CoT）多次送入 LLM；较高 temperature 鼓励探索不同推理与逐步说明。  
> 2. **抽取答案：** 从每条路径中抽取最终答案。  
> 3. **选取最常见答案：** 对抽取结果多数表决，出现次数最多的作为最终自洽答案。

This approach improves the accuracy and coherence of responses, particularly for tasks where multiple valid reasoning paths might exist or where the model might be prone to errors in a single attempt. The benefit is a pseudo-probability likelihood of the answer being correct, increasing overall accuracy. However, the significant cost is the need to run the model multiple times for the same query, leading to much higher computation and expense.

> 该方法可提升准确与连贯性，尤其适用于存在多条合理路径或单次易错的任务；带来答案正确性的“伪概率”提升。代价是同一查询需多次运行模型，计算与费用显著增加。

* **Example (Conceptual):**  
  * *Prompt:* "Is the statement 'All birds can fly' true or false? Explain your reasoning."  
  * *Model Run 1 (High Temp):* Reasons about most birds flying, concludes True.  
  * *Model Run 2 (High Temp):* Reasons about penguins and ostriches, concludes False.  
  * *Model Run 3 (High Temp):* Reasons about birds *in general*, mentions exceptions briefly, concludes True.  
  * *Self-Consistency Result:* Based on majority vote (True appears twice), the final answer is "True". (Note: A more sophisticated approach would weigh the reasoning quality).

> * **示例（概念性）：**  
>   * *Prompt:* "Is the statement 'All birds can fly' true or false? Explain your reasoning."  
>   * *Model Run 1 (High Temp):* Reasons about most birds flying, concludes True.  
>   * *Model Run 2 (High Temp):* Reasons about penguins and ostriches, concludes False.  
>   * *Model Run 3 (High Temp):* Reasons about birds *in general*, mentions exceptions briefly, concludes True.  
>   * *Self-Consistency Result:* Based on majority vote (True appears twice), the final answer is "True". (Note: A more sophisticated approach would weigh the reasoning quality).

## Step-Back Prompting

> ## 退一步提示（Step-Back Prompting）

Step-back prompting enhances reasoning by first asking the language model to consider a general principle or concept related to the task before addressing specific details. The response to this broader question is then used as context for solving the original problem.

> 退一步提示先让模型思考与任务相关的普遍原则或概念，再处理具体细节；对宽泛问题的回答再作为解原题的语境。

This process allows the language model to activate relevant background knowledge and wider reasoning strategies. By focusing on underlying principles or higher-level abstractions, the model can generate more accurate and insightful answers, less influenced by superficial elements. Initially considering general factors can provide a stronger basis for generating specific creative outputs. Step-back prompting encourages critical thinking and the application of knowledge, potentially mitigating biases by emphasizing general principles.

> 该过程有助于激活背景知识与更广的推理策略；聚焦底层原则或高层抽象，可减少表面信息干扰，先生成更扎实基础再产出具体创意。退一步提示鼓励批判性思考与知识运用，并可能通过强调一般原则减轻某些偏见。

* **Example:**  
  * *Prompt 1 (Step-Back):* "What are the key factors that make a good detective story?"  
  * *Model Response 1:* (Lists elements like red herrings, compelling motive, flawed protagonist, logical clues, satisfying resolution).  
  * *Prompt 2 (Original Task + Step-Back Context):* "Using the key factors of a good detective story [insert Model Response 1 here], write a short plot summary for a new mystery novel set in a small town."

> * **示例：**  
>   * *Prompt 1 (Step-Back):* "What are the key factors that make a good detective story?"  
>   * *Model Response 1:* (Lists elements like red herrings, compelling motive, flawed protagonist, logical clues, satisfying resolution).  
>   * *Prompt 2 (Original Task + Step-Back Context):* "Using the key factors of a good detective story [insert Model Response 1 here], write a short plot summary for a new mystery novel set in a small town."

## Tree of Thoughts (ToT)

> ## 思维树（Tree of Thoughts, ToT）

Tree of Thoughts (ToT) is an advanced reasoning technique that extends the Chain of Thought method. It enables a language model to explore multiple reasoning paths concurrently, instead of following a single linear progression. This technique utilizes a tree structure, where each node represents a "thought"—a coherent language sequence acting as an intermediate step. From each node, the model can branch out, exploring alternative reasoning routes.

> 思维树是扩展思维链的高级技术：允许模型并行探索多条推理路径，而非单线推进。用树结构表示，每节点是一个作为中间步骤的连贯“思维”片段，可从节点分叉探索替代路径。

ToT is particularly suited for complex problems that require exploration, backtracking, or the evaluation of multiple possibilities before arriving at a solution. While more computationally demanding and intricate to implement than the linear Chain of Thought method, ToT can achieve superior results on tasks necessitating deliberate and exploratory problem-solving. It allows an agent to consider diverse perspectives and potentially recover from initial errors by investigating alternative branches within the "thought tree."

> ToT 适合需要探索、回溯或在多种可能间权衡的复杂问题；比线性 CoT 更耗算力、实现更复杂，但在需审慎与探索式解题的任务上可更优；智能体可考虑多种视角，并在“思维树”其他分支上从初始错误中恢复。

* **Example (Conceptual):** For a complex creative writing task like "Develop three different possible endings for a story based on these plot points," ToT would allow the model to explore distinct narrative branches from a key turning point, rather than just generating one linear continuation.

> * **示例（概念性）：** 对“基于这些情节点发展三种不同结局”这类复杂创作任务，ToT 可从关键转折点分叉探索不同叙事分支，而非只生成一条线性续写。

These reasoning and thought process techniques are crucial for building agents capable of handling tasks that go beyond simple information retrieval or text generation. By prompting models to expose their reasoning, consider multiple perspectives, or step back to general principles, we can significantly enhance their ability to perform complex cognitive tasks within agentic systems.

> 这些推理与思维技术对构建超越简单检索或生成的智能体至关重要；通过暴露推理、多视角或退一步到一般原则，可显著提升其在智能体系统中完成复杂认知任务的能力。

# Action and Interaction Techniques

> # 行动与交互技术

Intelligent agents possess the capability to actively engage with their environment, beyond generating text. This includes utilizing tools, executing external functions, and participating in iterative cycles of observation, reasoning, and action. This section examines prompting techniques designed to enable these active behaviors.

> 智能体不仅能生成文本，还能主动与环境互动：使用工具、执行外部函数，并参与观察—推理—行动的迭代循环。本节讨论支持这些主动行为的提示技术。

## Tool Use / Function Calling

> ## 工具使用 / 函数调用

A crucial ability for an agent is using external tools or calling functions to perform actions beyond its internal capabilities. These actions may include web searches, database access, sending emails, performing calculations, or interacting with external APIs. Effective prompting for tool use involves designing prompts that instruct the model on the appropriate timing and methodology for tool utilization.

> 智能体的关键能力之一是使用外部工具或调用函数完成内部无法直接完成的动作：如搜索、访问数据库、发邮件、计算或调用 API。有效提示需说明何时、如何调用工具。

Modern language models often undergo fine-tuning for "function calling" or "tool use." This enables them to interpret descriptions of available tools, including their purpose and parameters. Upon receiving a user request, the model can determine the necessity of tool use, identify the appropriate tool, and format the required arguments for its invocation. The model does not execute the tool directly. Instead, it generates a structured output, typically in JSON format, specifying the tool and its parameters. An agentic system then processes this output, executes the tool, and provides the tool's result back to the model, integrating it into the ongoing interaction.

> 现代语言模型常针对“函数调用/工具使用”微调，能解读工具描述（用途与参数）；收到请求后可判断是否需要工具、选何工具、如何格式化参数。模型通常不直接执行工具，而是生成结构化输出（多为 JSON）指明工具与参数；智能体系统执行工具并把结果回传模型以继续交互。

* **Example:**  
  You have access to a weather tool that can get the current weather for a specified city. The tool is called '`get.current.weather`' and takes a '`city`' parameter (string).

  User: What's the weather like in London right now?

  * *Expected Model Output (Function Call):*  
    {  
      "tool.code": "get.current.weather",  
      "tool.name": "get.current.weather",  
      "parameters": {  
        "city": "London"  
      }  
    }

> * **示例：**  
>   You have access to a weather tool that can get the current weather for a specified city. The tool is called '`get.current.weather`' and takes a '`city`' parameter (string).  
>  
>   User: What's the weather like in London right now?  
>  
>   * *Expected Model Output (Function Call):*  
>     {  
>       "tool.code": "get.current.weather",  
>       "tool.name": "get.current.weather",  
>       "parameters": {  
>         "city": "London"  
>       }  
>     }

## ReAct (Reason & Act)

> ## ReAct（推理与行动）

ReAct, short for Reason and Act, is a prompting paradigm that combines Chain of Thought-style reasoning with the ability to perform actions using tools in an interleaved manner. ReAct mimics how humans operate – we reason verbally and take actions to gather more information or make progress towards a goal.

> ReAct（Reason and Act）将类 CoT 推理与交错使用工具执行行动结合，模仿人类边想边做、用行动获取信息或向目标推进。

The ReAct pattern involves a loop:

> ReAct 模式是一个循环：

1. **Thought:** The model generates a thought process, explaining its current understanding and plan.  
2. **Action:** Based on the thought, the model decides to perform an action, often using a tool (e.g., Search, Calculator, API call). It outputs the name of the tool and the required input.  
3. **Observation:** The agentic system executes the tool and provides the result (Observation) back to the model.  
4. The loop continues with the model generating a new "Thought" based on the latest "Observation," leading to further "Actions" and "Observations" until the task is complete and the model outputs a "Final Answer."

> 1. **Thought：** 模型生成思考，说明当前理解与计划。  
> 2. **Action：** 据思考决定行动，常通过工具（如 Search、Calculator、API），输出工具名与输入。  
> 3. **Observation：** 智能体系统执行工具，将结果作为 Observation 返回模型。  
> 4. 循环继续：模型基于最新 Observation 再生成 Thought，反复 Action/Observation，直至任务完成并输出 **Final Answer**。

This interleaved process of thinking and acting allows the agent to dynamically gather information, react to tool outputs, and refine its approach, making it particularly effective for tasks requiring interaction with dynamic environments or external knowledge sources.

> 交错思考与行动使智能体能动态收集信息、响应工具输出并调整策略，适合与动态环境或外部知识源交互的任务。

* **Example (Illustrative ReAct Trace):**  
  User: What is the capital of France and its current population?

  Thought: The user is asking for two pieces of information: the capital of France and its population. I can use a search tool to find this information. I will start by confirming the capital, although I am likely to know it.  
  Action: Search({"query": "capital of France"})  
  Observation: Paris

  Thought: Okay, the capital is Paris. Now I need to find the population of Paris.  
  Action: Search({"query": "current population of Paris"})  
  Observation: The population of Paris was estimated to be around 2.1 million people in 2023.

  Thought: I have found both pieces of information. I can now provide the final answer to the user.  
  Final Answer: The capital of France is Paris, and its estimated population in 2023 was around 2.1 million people.

> * **示例（说明性 ReAct 轨迹）：**  
>   User: What is the capital of France and its current population?  
>  
>   Thought: The user is asking for two pieces of information: the capital of France and its population. I can use a search tool to find this information. I will start by confirming the capital, although I am likely to know it.  
>   Action: Search({"query": "capital of France"})  
>   Observation: Paris  
>  
>   Thought: Okay, the capital is Paris. Now I need to find the population of Paris.  
>   Action: Search({"query": "current population of Paris"})  
>   Observation: The population of Paris was estimated to be around 2.1 million people in 2023.  
>  
>   Thought: I have found both pieces of information. I can now provide the final answer to the user.  
>   Final Answer: The capital of France is Paris, and its estimated population in 2023 was around 2.1 million people.

These techniques are vital for building agents that can actively engage with the world, retrieve real-time information, and perform tasks that require interacting with external systems.

> 这些技术对构建能主动接触世界、获取实时信息并与外部系统交互的智能体至关重要。

## Advanced Techniques

> ## 进阶技术

Beyond the foundational, structural, and reasoning patterns, there are several other prompting techniques that can further enhance the capabilities and efficiency of agentic systems. These range from using AI to optimize prompts to incorporating external knowledge and tailoring responses based on user characteristics.

> 除基础、结构与推理模式外，还有多种提示技术可进一步提升智能体系统的能力与效率：从用 AI 优化提示，到整合外部知识、按用户特征定制回答等。

### Automatic Prompt Engineering (APE)

> ### 自动提示工程（APE）

Recognizing that crafting effective prompts can be a complex and iterative process, Automatic Prompt Engineering (APE) explores using language models themselves to generate, evaluate, and refine prompts. This method aims to automate the prompt writing process, potentially enhancing model performance without requiring extensive human effort in prompt design.

> 鉴于有效提示往往复杂且需迭代，APE 探索用语言模型自身生成、评估与精炼提示，旨在自动化撰写过程，在减少人工设计负担的同时提升表现。

The general idea is to have a "meta-model" or a process that takes a task description and generates multiple candidate prompts. These prompts are then evaluated based on the quality of the output they produce on a given set of inputs (perhaps using metrics like BLEU or ROUGE, or human evaluation). The best-performing prompts can be selected, potentially refined further, and used for the target task. Using an LLM to generate variations of a user query for training a chatbot is an example of this.

> 一般思路是“元模型”或流程接收任务描述，生成多份候选提示；在一组输入上根据产出质量（如 BLEU/ROUGE 或人工评估）评估，择优并可能继续精炼后用于目标任务。用 LLM 生成用户查询变体以训练聊天机器人即为一例。

* **Example (Conceptual):** A developer provides a description: "I need a prompt that can extract the date and sender from an email." An APE system generates several candidate prompts. These are tested on sample emails, and the prompt that consistently extracts the correct information is selected.

> * **示例（概念性）：** 开发者描述：“我需要一个能从邮件中提取日期与发件人的提示。”APE 系统生成多份候选，在样例邮件上测试，选出能稳定抽对信息的那份。

Of course. Here is a rephrased and slightly expanded explanation of programmatic prompt optimization using frameworks like DSPy:

> 下面是对 DSPy 等框架中程序化提示优化的改写与略作扩展说明：

Another powerful prompt optimization technique, notably promoted by the DSPy framework, involves treating prompts not as static text but as programmatic modules that can be automatically optimized. This approach moves beyond manual trial-and-error and into a more systematic, data-driven methodology.

> 另一有力技术（DSPy 等大力倡导）把提示视为可自动优化的程序模块，而非静态文本，从而超越手工试错，进入更系统的数据驱动方法。

The core of this technique relies on two key components:

> 该技术核心依赖两大组件：

1. **A Goldset (or High-Quality Dataset):** This is a representative set of high-quality input-and-output pairs. It serves as the "ground truth" that defines what a successful response looks like for a given task.  
2. **An Objective Function (or Scoring Metric):** This is a function that automatically evaluates the LLM's output against the corresponding "golden" output from the dataset. It returns a score indicating the quality, accuracy, or correctness of the response.

> 1. **金标集（高质量数据集）：** 代表性高质量输入—输出对，作为定义任务成功回答样貌的“真值”。  
> 2. **目标函数（评分指标）：** 自动将 LLM 输出与数据集中对应金标比较并返回质量/正确性分数。

Using these components, an optimizer, such as a Bayesian optimizer, systematically refines the prompt. This process typically involves two main strategies, which can be used independently or in concert:

> 在此之上，贝叶斯优化器等可系统精炼提示；常见两大策略可单独或联合使用：

* **Few-Shot Example Optimization:** Instead of a developer manually selecting examples for a few-shot prompt, the optimizer programmatically samples different combinations of examples from the goldset. It then tests these combinations to identify the specific set of examples that most effectively guides the model toward generating the desired outputs.

* **Instructional Prompt Optimization:** In this approach, the optimizer automatically refines the prompt's core instructions. It uses an LLM as a "meta-model" to iteratively mutate and rephrase the prompt's text—adjusting the wording, tone, or structure—to discover which phrasing yields the highest scores from the objective function.

> * **少样本示例优化：** 不由开发者手工选例，优化器从金标集中程序化抽样不同示例组合并测试，找出最能引导模型产出期望结果的那一组。  
> * **指令文本优化：** 优化器自动精炼核心指令，用 LLM 作“元模型”迭代改写措辞、语气或结构，以发现目标函数得分最高的表述。

The ultimate goal for both strategies is to maximize the scores from the objective function, effectively "training" the prompt to produce results that are consistently closer to the high-quality goldset. By combining these two approaches, the system can simultaneously optimize *what instructions* to give the model and *which examples* to show it, leading to a highly effective and robust prompt that is machine-optimized for the specific task.

> 两策略终极目标都是最大化目标函数分数，相当于“训练”提示使其稳定逼近高质量金标；联合使用可同时优化*给模型的指令*与*展示的示例*，得到针对任务经机器优化的高效稳健提示。

### Iterative Prompting / Refinement

> ### 迭代提示 / 精炼

This technique involves starting with a simple, basic prompt and then iteratively refining it based on the model's initial responses. If the model's output isn't quite right, you analyze the shortcomings and modify the prompt to address them. This is less about an automated process (like APE) and more about a human-driven iterative design loop.

> 从简单提示起步，根据模型初次回答迭代改进；输出不理想则分析短板并改提示。这更偏人工驱动的设计循环，而非 APE 式全自动。

* **Example:**  
  * *Attempt 1:* "Write a product description for a new type of coffee maker." (Result is too generic).  
  * *Attempt 2:* "Write a product description for a new type of coffee maker. Highlight its speed and ease of cleaning." (Result is better, but lacks detail).  
  * *Attempt 3:* "Write a product description for the 'SpeedClean Coffee Pro'. Emphasize its ability to brew a pot in under 2 minutes and its self-cleaning cycle. Target busy professionals." (Result is much closer to desired).

> * **示例：**  
>   * *Attempt 1:* "Write a product description for a new type of coffee maker." (Result is too generic).  
>   * *Attempt 2:* "Write a product description for a new type of coffee maker. Highlight its speed and ease of cleaning." (Result is better, but lacks detail).  
>   * *Attempt 3:* "Write a product description for the 'SpeedClean Coffee Pro'. Emphasize its ability to brew a pot in under 2 minutes and its self-cleaning cycle. Target busy professionals." (Result is much closer to desired).

### Providing Negative Examples

> ### 提供反例

While the principle of "Instructions over Constraints" generally holds true, there are situations where providing negative examples can be helpful, albeit used carefully. A negative example shows the model an input and an *undesired* output, or an input and an output that *should not* be generated. This can help clarify boundaries or prevent specific types of incorrect responses.

> 尽管“指令优于约束”大体成立，在谨慎使用的前提下，反例有时有用：展示输入与*不期望*输出，或不应生成的输出，以划清边界、抑制特定错误类型。

* **Example:**  
  Generate a list of popular tourist attractions in Paris. Do NOT include the Eiffel Tower.

  Example of what NOT to do:  
  Input: List popular landmarks in Paris.  
  Output: The Eiffel Tower, The Louvre, Notre Dame Cathedral.

> * **示例：**  
>   Generate a list of popular tourist attractions in Paris. Do NOT include the Eiffel Tower.  
>  
>   Example of what NOT to do:  
>   Input: List popular landmarks in Paris.  
>   Output: The Eiffel Tower, The Louvre, Notre Dame Cathedral.

### Using Analogies

> ### 使用类比

Framing a task using an analogy can sometimes help the model understand the desired output or process by relating it to something familiar. This can be particularly useful for creative tasks or explaining complex roles.

> 用类比框定任务，有时能帮助模型借熟悉事物理解期望输出或流程；对创意任务或解释复杂角色特别有用。

* **Example:**  
  Act as a "data chef". Take the raw ingredients (data points) and prepare a "summary dish" (report) that highlights the key flavors (trends) for a business audience.

> * **示例：**  
>   Act as a "data chef". Take the raw ingredients (data points) and prepare a "summary dish" (report) that highlights the key flavors (trends) for a business audience.

### Factored Cognition / Decomposition

> ### 因子化认知 / 分解

For very complex tasks, it can be effective to break down the overall goal into smaller, more manageable sub-tasks and prompt the model separately on each sub-task. The results from the sub-tasks are then combined to achieve the final outcome. This is related to prompt chaining and planning but emphasizes the deliberate decomposition of the problem.

> 对极复杂任务，可把总目标拆成更小可管理的子任务并分别提示，再合并结果。与提示链、规划相关，但更强调有意识的问题分解。

* **Example:** To write a research paper:  
  * Prompt 1: "Generate a detailed outline for a paper on the impact of AI on the job market."  
  * Prompt 2: "Write the introduction section based on this outline: [insert outline intro]."  
  * Prompt 3: "Write the section on 'Impact on White-Collar Jobs' based on this outline: [insert outline section]." (Repeat for other sections).  
  * Prompt N: "Combine these sections and write a conclusion."

> * **示例：** 撰写研究论文时：  
>   * Prompt 1: "Generate a detailed outline for a paper on the impact of AI on the job market."  
>   * Prompt 2: "Write the introduction section based on this outline: [insert outline intro]."  
>   * Prompt 3: "Write the section on 'Impact on White-Collar Jobs' based on this outline: [insert outline section]." (Repeat for other sections).  
>   * Prompt N: "Combine these sections and write a conclusion."

### Retrieval Augmented Generation (RAG)

> ### 检索增强生成（RAG）

RAG is a powerful technique that enhances language models by giving them access to external, up-to-date, or domain-specific information during the prompting process. When a user asks a question, the system first retrieves relevant documents or data from a knowledge base (e.g., a database, a set of documents, the web). This retrieved information is then included in the prompt as context, allowing the language model to generate a response grounded in that external knowledge. This mitigates issues like hallucination and provides access to information the model wasn't trained on or that is very recent. This is a key pattern for agentic systems that need to work with dynamic or proprietary information.

> RAG 在提示过程中为语言模型提供外部、最新或领域专属信息以增强能力。用户提问时，系统先从知识库（数据库、文档集、网页等）检索相关材料，再作为语境写入提示，使回答锚定在外部知识上，减轻幻觉并覆盖训练未含或极新的信息；对需处理动态或专有数据的智能体系统是关键模式。

* **Example:**  
  * *User Query:* "What are the new features in the latest version of the Python library 'X'?"  
  * *System Action:* Search a documentation database for "Python library X latest features".  
  * *Prompt to LLM:* "Based on the following documentation snippets: [insert retrieved text], explain the new features in the latest version of Python library 'X'."

> * **示例：**  
>   * *User Query:* "What are the new features in the latest version of the Python library 'X'?"  
>   * *System Action:* Search a documentation database for "Python library X latest features".  
>   * *Prompt to LLM:* "Based on the following documentation snippets: [insert retrieved text], explain the new features in the latest version of Python library 'X'."

### Persona Pattern (User Persona)

> ### 人格模式（用户人格）

While role prompting assigns a persona to the *model*, the Persona Pattern involves describing the user or the target audience for the model's output. This helps the model tailor its response in terms of language, complexity, tone, and the kind of information it provides.

> 角色提示把人格赋给*模型*；人格模式则描述用户或目标受众，帮助模型在语言、难度、语气与信息类型上定制回答。

* **Example:**  
  You are explaining quantum physics. The target audience is a high school student with no prior knowledge of the subject. Explain it simply and use analogies they might understand.

  Explain quantum physics: [Insert basic explanation request]

> * **示例：**  
>   You are explaining quantum physics. The target audience is a high school student with no prior knowledge of the subject. Explain it simply and use analogies they might understand.  
>  
>   Explain quantum physics: [Insert basic explanation request]

These advanced and supplementary techniques provide further tools for prompt engineers to optimize model behavior, integrate external information, and tailor interactions for specific users and tasks within agentic workflows.

> 这些进阶与补充技术为提示工程师在智能体工作流中优化模型行为、整合外部信息、按用户与任务定制交互提供了更多工具。

## Using Google Gems

> ## 使用 Google Gems

Google's AI "Gems" (see Fig. 1) represent a user-configurable feature within its large language model architecture. Each "Gem" functions as a specialized instance of the core Gemini AI, tailored for specific, repeatable tasks. Users create a Gem by providing it with a set of explicit instructions, which establishes its operational parameters. This initial instruction set defines the Gem's designated purpose, response style, and knowledge domain. The underlying model is designed to consistently adhere to these pre-defined directives throughout a conversation.

> Google 的 AI “Gems”（见图 1）是其大语言模型架构中的用户可配置能力。每个 “Gem” 是核心 Gemini 的专用实例，面向特定可重复任务。用户通过一组明确指令创建 Gem，从而设定运行参数：界定用途、回答风格与知识域；底层模型被设计为在对话中持续遵循这些预定义指令。

This allows for the creation of highly specialized AI agents for focused applications. For example, a Gem can be configured to function as a code interpreter that only references specific programming libraries. Another could be instructed to analyze data sets, generating summaries without speculative commentary. A different Gem might serve as a translator adhering to a particular formal style guide. This process creates a persistent, task-specific context for the artificial intelligence.

> 由此可为专注场景打造高度专化的 AI 智能体。例如：配置为仅引用特定库的代码解释器；或分析数据集并生成摘要、不做臆测性评论；或按特定正式体例做翻译。该过程为 AI 建立持久、任务专属的语境。

Consequently, the user avoids the need to re-establish the same contextual information with each new query. This methodology reduces conversational redundancy and improves the efficiency of task execution. The resulting interactions are more focused, yielding outputs that are consistently aligned with the user's initial requirements. This framework allows for applying fine-grained, persistent user direction to a generalist AI model. Ultimately, Gems enable a shift from general-purpose interaction to specialized, pre-defined AI functionalities.

> 用户因此不必在每次新查询时重复建立相同语境；减少对话冗余、提高任务执行效率；交互更聚焦，输出更稳定对齐初始需求。该框架把细粒度、持久的用户导向施加于通才模型；归根结底，Gems 推动从通用交互转向专化、预定义的 AI 能力。

![Example of Google Gem Usage](../assets-new/Example_of_Google_Gem_Usage.png)

Fig.1: Example of Google Gem usage.

> 图 1：Google Gem 使用示例。

## Using LLMs to Refine Prompts (The Meta Approach)

> ## 用 LLM 精炼提示（元方法）

We've explored numerous techniques for crafting effective prompts, emphasizing clarity, structure, and providing context or examples. This process, however, can be iterative and sometimes challenging. What if we could leverage the very power of large language models, like Gemini, to help us *improve* our prompts? This is the essence of using LLMs for prompt refinement – a "meta" application where AI assists in optimizing the instructions given to AI.

> 我们已讨论多种有效提示技巧，强调清晰、结构以及语境与示例。但该过程往往迭代且有时费力。若像 Gemini 这样的大语言模型能帮我们*改进*提示呢？这就是用 LLM 做提示精炼的本质——“元”应用：由 AI 协助优化给 AI 的指令。

This capability is particularly "cool" because it represents a form of AI self-improvement or at least AI-assisted human improvement in interacting with AI. Instead of solely relying on human intuition and trial-and-error, we can tap into the LLM's understanding of language, patterns, and even common prompting pitfalls to get suggestions for making our prompts better. It turns the LLM into a collaborative partner in the prompt engineering process.

> 这很“酷”，因为它体现某种 AI 自改进，或至少是 AI 辅助人类更好与 AI 交互。除依赖直觉与试错外，还可借助 LLM 对语言、模式乃至常见提示陷阱的理解来获得改进建议，使其成为提示工程中的协作伙伴。

How does this work in practice? You can provide a language model with an existing prompt that you're trying to improve, along with the task you want it to accomplish and perhaps even examples of the output you're currently getting (and why it's not meeting your expectations). You then prompt the LLM to analyze the prompt and suggest improvements.

> 实践中：把你希望改进的现有提示、要完成的任务、以及当前输出样例（及为何不达标）提供给模型，再请其分析提示并给出改进建议。

A model like Gemini, with its strong reasoning and language generation capabilities, can analyze your existing prompt for potential areas of ambiguity, lack of specificity, or inefficient phrasing. It can suggest incorporating techniques we've discussed, such as adding delimiters, clarifying the desired output format, suggesting a more effective persona, or recommending the inclusion of few-shot examples.

> 具备强推理与语言生成能力的模型（如 Gemini）可检视现有提示中的歧义、不够具体或低效措辞，并建议采用分隔符、澄清输出格式、更有效人格或加入少样本等我们已讨论过的技巧。

The benefits of this meta-prompting approach include:

> 元提示做法的好处包括：

* **Accelerated Iteration:** Get suggestions for improvement much faster than pure manual trial and error.  
* **Identification of Blind Spots:** An LLM might spot ambiguities or potential misinterpretations in your prompt that you overlooked.  
* **Learning Opportunity:** By seeing the types of suggestions the LLM makes, you can learn more about what makes prompts effective and improve your own prompt engineering skills.  
* **Scalability:** Potentially automate parts of the prompt optimization process, especially when dealing with a large number of prompts.

> * **加速迭代：** 比纯手工试错更快获得改进建议。  
> * **发现盲区：** LLM 可能指出你忽略的歧义或易被误解之处。  
> * **学习机会：** 观察其建议类型，可更深理解有效提示要素并提升自身提示工程能力。  
> * **可扩展性：** 在提示数量大时，可部分自动化优化流程。

It's important to note that the LLM's suggestions are not always perfect and should be evaluated and tested, just like any manually engineered prompt. However, it provides a powerful starting point and can significantly streamline the refinement process.

> 需注意：LLM 建议并非总是完美，应像手工提示一样评估与测试；但它仍是强起点，能显著简化精炼流程。

* **Example Prompt for Refinement:**  
  Analyze the following prompt for a language model and suggest ways to improve it to consistently extract the main topic and key entities (people, organizations, locations) from news articles. The current prompt sometimes misses entities or gets the main topic wrong.

  Existing Prompt:  
  "Summarize the main points and list important names and places from this article: [insert article text]"

  Suggestions for Improvement:

> * **用于精炼的示例提示：**  
>   Analyze the following prompt for a language model and suggest ways to improve it to consistently extract the main topic and key entities (people, organizations, locations) from news articles. The current prompt sometimes misses entities or gets the main topic wrong.  
>  
>   Existing Prompt:  
>   "Summarize the main points and list important names and places from this article: [insert article text]"  
>  
>   Suggestions for Improvement:

In this example, we're using the LLM to critique and enhance another prompt. This meta-level interaction demonstrates the flexibility and power of these models, allowing us to build more effective agentic systems by first optimizing the fundamental instructions they receive. It's a fascinating loop where AI helps us talk better to AI.

> 此例中用 LLM 批评并增强另一则提示。这种元层交互展现模型的灵活与强大：先优化其收到的基础指令，以构建更有效的智能体系统——形成“AI 帮我们更好与 AI 对话”的有趣闭环。

## Prompting for Specific Tasks

> ## 面向特定任务的提示

While the techniques discussed so far are broadly applicable, some tasks benefit from specific prompting considerations. These are particularly relevant in the realm of code and multimodal inputs.

> 前述技巧普适性强，但部分任务需要专门考量，尤其在代码与多模态输入领域。

### Code Prompting

> ### 代码提示

Language models, especially those trained on large code datasets, can be powerful assistants for developers. Prompting for code involves using LLMs to generate, explain, translate, or debug code. Various use cases exist:

> 在大量代码数据上训练的模型可成为开发者强助手。代码提示包括生成、解释、翻译或调试代码等用例：

* **Prompts for writing code:** Asking the model to generate code snippets or functions based on a description of the desired functionality.  
  * **Example:** "Write a Python function that takes a list of numbers and returns the average."  
* **Prompts for explaining code:** Providing a code snippet and asking the model to explain what it does, line by line or in a summary.  
  * **Example:** "Explain the following JavaScript code snippet: [insert code]."  
* **Prompts for translating code:** Asking the model to translate code from one programming language to another.  
  * **Example:** "Translate the following Java code to C++: [insert code]."  
* **Prompts for debugging and reviewing code:** Providing code that has an error or could be improved and asking the model to identify issues, suggest fixes, or provide refactoring suggestions.  
  * **Example:** "The following Python code is giving a 'NameError'. What is wrong and how can I fix it? [insert code and traceback]."

> * **写代码：** 据功能描述生成片段或函数。  
>   * **示例：** "Write a Python function that takes a list of numbers and returns the average."  
> * **解释代码：** 提供片段并要求逐行或概要说明。  
>   * **示例：** "Explain the following JavaScript code snippet: [insert code]."  
> * **翻译代码：** 从一种语言译到另一种。  
>   * **示例：** "Translate the following Java code to C++: [insert code]."  
> * **调试与审阅：** 提供有错或可改进的代码，请其定位问题、建议修复或重构。  
>   * **示例：** "The following Python code is giving a 'NameError'. What is wrong and how can I fix it? [insert code and traceback]."

Effective code prompting often requires providing sufficient context, specifying the desired language and version, and being clear about the functionality or issue.

> 有效代码提示通常需提供充分语境、指明语言与版本，并清楚说明功能或问题。

### Multimodal Prompting

> ### 多模态提示

While the focus of this appendix and much of current LLM interaction is text-based, the field is rapidly moving towards multimodal models that can process and generate information across different modalities (text, images, audio, video, etc.). Multimodal prompting involves using a combination of inputs to guide the model. This refers to using multiple input formats instead of just text.

> 本附录与当前多数交互仍以文本为主，但领域正快速走向可处理多模态（文本、图像、音频、视频等）的模型。多模态提示指组合多种输入格式引导模型，而非仅用文本。

* **Example:** Providing an image of a diagram and asking the model to explain the process shown in the diagram (Image Input + Text Prompt). Or providing an image and asking the model to generate a descriptive caption (Image Input + Text Prompt -> Text Output).

> * **示例：** 提供示意图并请解释图中流程（图像 + 文本）；或提供图像并请生成描述性标题（图像 + 文本 → 文本）。

As multimodal capabilities become more sophisticated, prompting techniques will evolve to effectively leverage these combined inputs and outputs.

> 随着多模态能力成熟，提示技术也将演进，以更好利用组合输入与输出。

## Best Practices and Experimentation

> ## 最佳实践与实验

Becoming a skilled prompt engineer is an iterative process that involves continuous learning and experimentation. Several valuable best practices are worth reiterating and emphasizing:

> 成为熟练提示工程师需要持续学习与实验。以下最佳实践值得重申：

* **Provide Examples:** Providing one or few-shot examples is one of the most effective ways to guide the model.  
* **Design with Simplicity:** Keep your prompts concise, clear, and easy to understand. Avoid unnecessary jargon or overly complex phrasing.  
* **Be Specific about the Output:** Clearly define the desired format, length, style, and content of the model's response.  
* **Use Instructions over Constraints:** Focus on telling the model what you want it to do rather than what you don't want it to do.  
* **Control the Max Token Length:** Use model configurations or explicit prompt instructions to manage the length of the generated output.  
* **Use Variables in Prompts:** For prompts used in applications, use variables to make them dynamic and reusable, avoiding hardcoding specific values.  
* **Experiment with Input Formats and Writing Styles:** Try different ways of phrasing your prompt (question, statement, instruction) and experiment with different tones or styles to see what yields the best results.  
* **For Few-Shot Prompting with Classification Tasks, Mix Up the Classes:** Randomize the order of examples from different categories to prevent overfitting.  
* **Adapt to Model Updates:** Language models are constantly being updated. Be prepared to test your existing prompts on new model versions and adjust them to leverage new capabilities or maintain performance.  
* **Experiment with Output Formats:** Especially for non-creative tasks, experiment with requesting structured output like JSON or XML.  
* **Experiment Together with Other Prompt Engineers:** Collaborating with others can provide different perspectives and lead to discovering more effective prompts.  
* **CoT Best Practices:** Remember specific practices for Chain of Thought, such as placing the answer after the reasoning and setting temperature to 0 for tasks with a single correct answer.  
* **Document the Various Prompt Attempts:** This is crucial for tracking what works, what doesn't, and why. Maintain a structured record of your prompts, configurations, and results.  
* **Save Prompts in Codebases:** When integrating prompts into applications, store them in separate, well-organized files for easier maintenance and version control.  
* **Rely on Automated Tests and Evaluation:** For production systems, implement automated tests and evaluation procedures to monitor prompt performance and ensure generalization to new data.

> * **提供示例：** 单样本或少样本是最有效引导方式之一。  
> * **简洁设计：** 提示宜短、清晰、易懂；避免不必要术语或过度复杂句式。  
> * **明确输出：** 清楚定义格式、长度、风格与内容。  
> * **指令优于约束：** 侧重说明要做什么，而非不要做什么。  
> * **控制最大 token：** 用配置或显式指令管理生成长度。  
> * **使用变量：** 应用中的提示用变量实现动态与复用，避免硬编码。  
> * **试验输入形式与文风：** 尝试提问、陈述、指令等不同说法与语气。  
> * **分类少样本打乱类别：** 随机化不同类别示例顺序以防过拟合。  
> * **适配模型更新：** 新版本中复测并调整提示以利用新能力或维持表现。  
> * **试验输出格式：** 非创意任务可多试 JSON、XML 等结构化输出。  
> * **与他人协作实验：** 协作带来不同视角，更易发现更有效提示。  
> * **CoT 实践：** 答案置于推理之后；单答案任务可将 temperature 设为 0。  
> * **记录尝试：** 结构化记录提示、配置与结果，追踪有效/无效及原因。  
> * **在代码库中保存提示：** 分文件、有条理存放，便于维护与版本控制。  
> * **依赖自动化测试与评估：** 生产系统应监控提示表现并检验对新数据的泛化。

Prompt engineering is a skill that improves with practice. By applying these principles and techniques, and by maintaining a systematic approach to experimentation and documentation, you can significantly enhance your ability to build effective agentic systems.

> 提示工程靠练习成长。坚持原则与技术，并以系统方式实验与文档化，可显著提升构建有效智能体系统的能力。

## Conclusion

> ## 结语

This appendix provides a comprehensive overview of prompting, reframing it as a disciplined engineering practice rather than a simple act of asking questions. Its central purpose is to demonstrate how to transform general-purpose language models into specialized, reliable, and highly capable tools for specific tasks. The journey begins with non-negotiable core principles like clarity, conciseness, and iterative experimentation, which are the bedrock of effective communication with AI. These principles are critical because they reduce the inherent ambiguity in natural language, helping to steer the model's probabilistic outputs toward a single, correct intention. Building on this foundation, basic techniques such as zero-shot, one-shot, and few-shot prompting serve as the primary methods for demonstrating expected behavior through examples. These methods provide varying levels of contextual guidance, powerfully shaping the model's response style, tone, and format. Beyond just examples, structuring prompts with explicit roles, system-level instructions, and clear delimiters provides an essential architectural layer for fine-grained control over the model.

> 本附录全面梳理提示，将其定位为严谨的工程实践，而非简单提问。核心目的是展示如何把通用语言模型转化为面向特定任务、可靠且高能力的工具。起点是不可妥协的原则：清晰、简洁与迭代实验——这是与 AI 有效沟通的基石；它们降低自然语言固有歧义，把模型的概率输出引向单一、正确的意图。在此基础上，零样本、单样本、少样本是透过示例示范期望行为的主要手段，以不同程度的语境引导强力塑造风格、语气与格式。除示例外，用显式角色、系统级指令与清晰分隔符组织提示，构成细粒度控制模型所必需的架构层。

The importance of these techniques becomes paramount in the context of building autonomous agents, where they provide the control and reliability necessary for complex, multi-step operations. For an agent to effectively create and execute a plan, it must leverage advanced reasoning patterns like Chain of Thought and Tree of Thoughts. These sophisticated methods compel the model to externalize its logical steps, systematically breaking down complex goals into a sequence of manageable sub-tasks. The operational reliability of the entire agentic system hinges on the predictability of each component's output. This is precisely why requesting structured data like JSON, and programmatically validating it with tools such as Pydantic, is not a mere convenience but an absolute necessity for robust automation. Without this discipline, the agent’s internal cognitive components cannot communicate reliably, leading to catastrophic failures within an automated workflow. Ultimately, these structuring and reasoning techniques are what successfully convert a model's probabilistic text generation into a deterministic and trustworthy cognitive engine for an agent.

> 在构建自主智能体时，这些技术尤为关键：它们提供复杂多步操作所需的控制与可靠性。智能体要有效制定并执行计划，须借助思维链、思维树等高级推理模式，迫使模型外化逻辑步骤，把复杂目标系统拆为可管理子任务序列。整个智能体系统的运行可靠性取决于各组件输出的可预测性。因此，要求 JSON 等结构化数据并用 Pydantic 等工具程序化校验，不是可有可无的便利，而是稳健自动化的必要条件；缺乏该纪律，智能体内部认知组件无法可靠互通，自动化工作流可能灾难性失败。归根结底，结构与推理技术把模型的概率性文本生成，转化为智能体可用、更确定且可信的“认知引擎”。

Furthermore, these prompts are what grant an agent its crucial ability to perceive and act upon its environment, bridging the gap between digital thought and real-world interaction. Action-oriented frameworks like ReAct and native function calling are the vital mechanisms that serve as the agent's hands, allowing it to use tools, query APIs, and manipulate data. In parallel, techniques like Retrieval Augmented Generation (RAG) and the broader discipline of Context Engineering function as the agent's senses. They actively retrieve relevant, real-time information from external knowledge bases, ensuring the agent’s decisions are grounded in current, factual reality. This critical capability prevents the agent from operating in a vacuum, where it would be limited to its static and potentially outdated training data. Mastering this full spectrum of prompting is therefore the definitive skill that elevates a generalist language model from a simple text generator into a truly sophisticated agent, capable of performing complex tasks with autonomy, awareness, and intelligence.

> 此外，正是这些提示赋予智能体感知并作用于环境的关键能力，连接数字推理与现实交互。ReAct、原生函数调用等行动框架如同智能体的“手”，使其能使用工具、查询 API、操作数据；并行地，RAG 与更广义的语境工程如同“感官”，从外部知识库主动取回相关实时信息，使决策锚定当前事实。这避免智能体仅在静态、可能过时的训练数据真空中运行。因而，掌握提示的全谱技能，是把通才语言模型从简单文本生成器提升为具备自主、觉知与智能、能执行复杂任务的成熟智能体的决定性能力。

## References

Here is a list of resources for further reading and deeper exploration of prompt engineering techniques:

1. Prompt Engineering, [https://www.kaggle.com/whitepaper-prompt-engineering](https://www.kaggle.com/whitepaper-prompt-engineering)
2. Chain-of-Thought Prompting Elicits Reasoning in Large Language Models, [https://arxiv.org/abs/2201.11903](https://arxiv.org/abs/2201.11903)
3. Self-Consistency Improves Chain of Thought Reasoning in Language Models,  [https://arxiv.org/pdf/2203.11171](https://arxiv.org/pdf/2203.11171)
4. ReAct: Synergizing Reasoning and Acting in Language Models, [https://arxiv.org/abs/2210.03629](https://arxiv.org/abs/2210.03629)  
5. Tree of Thoughts: Deliberate Problem Solving with Large Language Models,  [https://arxiv.org/pdf/2305.10601](https://arxiv.org/pdf/2305.10601)
6. Take a Step Back: Evoking Reasoning via Abstraction in Large Language Models, [https://arxiv.org/abs/2310.06117](https://arxiv.org/abs/2310.06117)
7. DSPy: Programming—not prompting—Foundation Models [https://github.com/stanfordnlp/dspy](https://github.com/stanfordnlp/dspy)
