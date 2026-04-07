# Glossary

## Fundamental Concepts

**Prompt:** A prompt is the input, typically in the form of a question, instruction, or statement, that a user provides to an AI model to elicit a response. The quality and structure of the prompt heavily influence the model's output, making prompt engineering a key skill for effectively using AI.

> **提示（Prompt）：** 提示是用户向 AI 模型提供的输入，通常以问题、指令或陈述的形式出现，用以引出模型的回应。提示的质量与结构会强烈影响模型输出，因此提示工程是有效使用 AI 的关键技能。

**Context Window:** The context window is the maximum number of tokens an AI model can process at once, including both the input and its generated output. This fixed size is a critical limitation, as information outside the window is ignored, while larger windows enable more complex conversations and document analysis.

> **上下文窗口（Context Window）：** 上下文窗口是 AI 模型一次能处理的最大 token 数量，包括输入与模型生成的输出。这一固定上限是关键约束：窗口外的信息会被忽略，而更大的窗口则支持更复杂的对话与文档分析。

**In-Context Learning:** In-context learning is an AI's ability to learn a new task from examples provided directly in the prompt, without requiring any retraining. This powerful feature allows a single, general-purpose model to be adapted to countless specific tasks on the fly.

> **上下文学习（In-Context Learning）：** 上下文学习指 AI 仅根据提示中直接给出的示例学习新任务，而无需重新训练。这一能力使单个通用模型能够即时适配大量具体任务。

**Zero-Shot, One-Shot, & Few-Shot Prompting:** These are prompting techniques where a model is given zero, one, or a few examples of a task to guide its response. Providing more examples generally helps the model better understand the user's intent and improves its accuracy for the specific task.

> **零样本、单样本与少样本提示（Zero-Shot, One-Shot, & Few-Shot Prompting）：** 这类提示技术向模型提供零个、一个或少量任务示例以引导其回答。通常示例越多，模型越能把握用户意图，并在该任务上提高准确性。

**Multimodality:** Multimodality is an AI's ability to understand and process information across multiple data types like text, images, and audio. This allows for more versatile and human-like interactions, such as describing an image or answering a spoken question.

> **多模态（Multimodality）：** 多模态指 AI 理解并处理多种数据类型（如文本、图像、音频）的能力，从而支持更灵活、更接近人类的交互，例如描述图像或回答语音提问。

**Grounding:** Grounding is the process of connecting a model's outputs to verifiable, real-world information sources to ensure factual accuracy and reduce hallucinations. This is often achieved with techniques like RAG to make AI systems more trustworthy.

> **接地（Grounding）：** 接地是将模型输出与可验证的真实世界信息源对齐的过程，以提高事实准确性并减少幻觉。常见做法包括使用 RAG 等技术，使 AI 系统更可信。

## Core AI Model Architectures

**Transformers:** The Transformer is the foundational neural network architecture for most modern LLMs. Its key innovation is the self-attention mechanism, which efficiently processes long sequences of text and captures complex relationships between words.

> **Transformer：** Transformer 是大多数现代 LLM 的基础神经网络架构。其核心创新是自注意力机制，能够高效处理长文本序列并捕捉词与词之间的复杂关系。

**Recurrent Neural Network (RNN):** The Recurrent Neural Network is a foundational architecture that preceded the Transformer. RNNs process information sequentially, using loops to maintain a "memory" of previous inputs, which made them suitable for tasks like text and speech processing.

> **循环神经网络（RNN）：** RNN 是早于 Transformer 的一类基础架构。RNN 按顺序处理信息，通过循环结构维持对先前输入的「记忆」，因而适用于文本与语音等任务。

**Mixture of Experts (MoE):** Mixture of Experts is an efficient model architecture where a "router" network dynamically selects a small subset of "expert" networks to handle any given input. This allows models to have a massive number of parameters while keeping computational costs manageable.

> **混合专家（MoE）：** MoE 是一种高效架构：由「路由」网络动态地为每个输入选择一小部分「专家」网络。这样模型可以拥有大量参数，同时控制计算成本。

**Diffusion Models:** Diffusion models are generative models that excel at creating high-quality images. They work by adding random noise to data and then training a model to meticulously reverse the process, allowing them to generate novel data from a random starting point.

> **扩散模型（Diffusion Models）：** 扩散模型是擅长生成高质量图像的生成式模型。其做法是对数据加入随机噪声，再训练模型细致地逆转这一过程，从而从随机起点生成新数据。

**Mamba:** Mamba is a recent AI architecture using a Selective State Space Model (SSM) to process sequences with high efficiency, especially for very long contexts. Its selective mechanism allows it to focus on relevant information while filtering out noise, making it a potential alternative to the Transformer.

> **Mamba：** Mamba 是较新的架构，采用选择性状态空间模型（SSM）高效处理序列，尤其适用于极长上下文。其选择性机制能聚焦相关信息并滤除噪声，因而可能成为 Transformer 的替代方案之一。

## The LLM Development Lifecycle

The development of a powerful language model follows a distinct sequence. It begins with Pre-training, where a massive base model is built by training it on a vast dataset of general internet text to learn language, reasoning, and world knowledge. Next is Fine-tuning, a specialization phase where the general model is further trained on smaller, task-specific datasets to adapt its capabilities for a particular purpose. The final stage is Alignment, where the specialized model's behavior is adjusted to ensure its outputs are helpful, harmless, and aligned with human values.

> 强大语言模型的开发遵循清晰的阶段：首先是**预训练（Pre-training）**，在海量通用互联网文本上训练基础模型，学习语言、推理与世界知识；其次是**微调（Fine-tuning）**，用较小、面向任务的数据进一步训练通用模型，使其能力适配特定用途；最后是**对齐（Alignment）**，调整专用模型的行为，使输出有益、无害并符合人类价值观。

**Pre-training Techniques:** Pre-training is the initial phase where a model learns general knowledge from vast amounts of data. The top techniques for this involve different objectives for the model to learn from. The most common is Causal Language Modeling (CLM), where the model predicts the next word in a sentence. Another is Masked Language Modeling (MLM), where the model fills in intentionally hidden words in a text. Other important methods include Denoising Objectives, where the model learns to restore a corrupted input to its original state, Contrastive Learning, where it learns to distinguish between similar and dissimilar pieces of data, and Next Sentence Prediction (NSP), where it determines if two sentences logically follow each other.

> **预训练技术：** 预训练是模型从海量数据中学习通用知识的阶段，常用目标包括：因果语言建模（CLM），预测句中下一个词；掩码语言建模（MLM），填补文本中被故意遮住的词；此外还有去噪目标（从损坏输入恢复原状）、对比学习（区分相似与相异样本）、以及下一句预测（NSP，判断两句是否前后衔接）等。

**Fine-tuning Techniques:** Fine-tuning is the process of adapting a general pre-trained model to a specific task using a smaller, specialized dataset. The most common approach is Supervised Fine-Tuning (SFT), where the model is trained on labeled examples of correct input-output pairs. A popular variant is Instruction Tuning, which focuses on training the model to better follow user commands. To make this process more efficient, Parameter-Efficient Fine-Tuning (PEFT) methods are used, with top techniques including LoRA (Low-Rank Adaptation), which only updates a small number of parameters, and its memory-optimized version, QLoRA. Another technique, Retrieval-Augmented Generation (RAG), enhances the model by connecting it to an external knowledge source during the fine-tuning or inference stage.

> **微调技术：** 微调用较小、专用的数据集将通用预训练模型适配到具体任务。最常见的是监督微调（SFT），用标注好的输入—输出对训练；常见变体是指令微调，强调更好遵循用户指令。为提升效率可采用参数高效微调（PEFT），例如 LoRA（低秩适配）仅更新少量参数，以及内存优化版 QLoRA。检索增强生成（RAG）则在微调或推理阶段连接外部知识源以增强模型。

**Alignment & Safety Techniques:** Alignment is the process of ensuring an AI model's behavior aligns with human values and expectations, making it helpful and harmless. The most prominent technique is Reinforcement Learning from Human Feedback (RLHF), where a "reward model" trained on human preferences guides the AI's learning process, often using an algorithm like Proximal Policy Optimization (PPO) for stability. Simpler alternatives have emerged, such as Direct Preference Optimization (DPO), which bypasses the need for a separate reward model, and Kahneman-Tversky Optimization (KTO), which simplifies data collection further. To ensure safe deployment, Guardrails are implemented as a final safety layer to filter outputs and block harmful actions in real-time.

> **对齐与安全：** 对齐是使模型行为符合人类价值观与期望、做到有益且无害的过程。主流方法包括基于人类反馈的强化学习（RLHF），用在人类偏好上训练的「奖励模型」引导学习，常配合近端策略优化（PPO）等算法。更简化的做法有直接偏好优化（DPO，无需单独奖励模型）与 Kahneman–Tversky 优化（KTO，进一步简化数据收集）。为安全部署可设置护栏（Guardrails）作为最后防线，过滤输出并实时阻止有害行为。

## Enhancing AI Agent Capabilities

AI agents are systems that can perceive their environment and take autonomous actions to achieve goals. Their effectiveness is enhanced by robust reasoning frameworks.

> AI 智能体是能够感知环境并自主采取行动以达成目标的系统；其效果往往依赖强健的推理框架。

**Chain of Thought (CoT):** This prompting technique encourages a model to explain its reasoning step-by-step before giving a final answer. This process of "thinking out loud" often leads to more accurate results on complex reasoning tasks.

> **思维链（CoT）：** 该提示技术鼓励模型在给出最终答案前先逐步说明推理过程。这种「出声思考」式过程往往能在复杂推理任务上得到更准确的结果。

**Tree of Thoughts (ToT):** Tree of Thoughts is an advanced reasoning framework where an agent explores multiple reasoning paths simultaneously, like branches on a tree. It allows the agent to self-evaluate different lines of thought and choose the most promising one to pursue, making it more effective at complex problem-solving.

> **思维树（ToT）：** ToT 是一种进阶推理框架：智能体同时探索多条推理路径（如树的分支），可自我评估不同思路并选择最有希望的方向，从而在复杂问题求解上更有效。

**ReAct (Reason and Act):** ReAct is an agent framework that combines reasoning and acting in a loop. The agent first "thinks" about what to do, then takes an "action" using a tool, and uses the resulting observation to inform its next thought, making it highly effective at solving complex tasks.

> **ReAct（推理与行动）：** ReAct 将推理与行动结合在循环中：智能体先「思考」要做什么，再用工具执行「行动」，并根据观察结果更新下一步思考，因而在复杂任务上非常有效。

**Planning:** This is an agent's ability to break down a high-level goal into a sequence of smaller, manageable sub-tasks. The agent then creates a plan to execute these steps in order, allowing it to handle complex, multi-step assignments.

> **规划：** 指智能体将高层目标分解为一系列较小、可管理的子任务，并制定按顺序执行的计划，从而处理复杂、多步骤的任务。

**Deep Research:** Deep research refers to an agent's capability to autonomously explore a topic in-depth by iteratively searching for information, synthesizing findings, and identifying new questions. This allows the agent to build a comprehensive understanding of a subject far beyond a single search query.

> **深度研究：** 指智能体通过迭代检索、综合结论并提出新问题来自主深入探索某一主题的能力，从而建立远超单次搜索查询的全面理解。

**Critique Model:** A critique model is a specialized AI model trained to review, evaluate, and provide feedback on the output of another AI model. It acts as an automated critic, helping to identify errors, improve reasoning, and ensure the final output meets a desired quality standard.

> **评判模型：** 评判模型是专门训练用来审查、评估并对另一模型输出给出反馈的 AI 模型，相当于自动化的批评者，有助于发现错误、改进推理并确保最终输出达到预期质量标准。