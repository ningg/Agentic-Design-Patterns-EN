# Chapter 17: Reasoning Techniques

> 第十七章：推理技术

This chapter delves into advanced reasoning methodologies for intelligent agents, focusing on multi-step logical inferences and problem-solving. These techniques go beyond simple sequential operations, making the agent's internal reasoning explicit. This allows agents to break down problems, consider intermediate steps, and reach more robust and accurate conclusions.  A core principle among these advanced methods is the allocation of increased computational resources during inference. This means granting the agent, or the underlying LLM, more processing time or steps to process a query and generate a response. Rather than a quick, single pass, the agent can engage in iterative refinement, explore multiple solution paths, or utilize external tools. This extended processing time during inference often significantly enhances accuracy, coherence, and robustness, especially for complex problems requiring deeper analysis and deliberation.

> 本章深入探讨面向智能体的高级推理方法，聚焦多步逻辑推断与问题求解。这些技术超越简单顺序操作，使智能体内部推理外显化，从而拆解问题、考虑中间步骤并得到更稳健、准确的结论。高级方法的共同核心之一是在推理阶段分配更多计算资源——给予智能体或其底层 LLM 更多处理时间或步数来处理查询并生成响应。相较一次性快速通过，智能体可进行迭代改进、探索多条路径或调用外部工具。延长推理期处理时间往往能显著提升准确性、连贯性与稳健性，尤其对需要更深入分析与斟酌的复杂问题。

## Practical Applications & Use Cases

> ## 实际应用与用例

Practical applications include:

> 实际应用包括：

* **Complex Question Answering:** Facilitating the resolution of multi-hop queries, which necessitate the integration of data from diverse sources and the execution of logical deductions, potentially involving the examination of multiple reasoning paths, and benefiting from extended inference time to synthesize information.  
* **Mathematical Problem Solving:** Enabling the division of mathematical problems into smaller, solvable components, illustrating the step-by-step process, and employing code execution for precise computations, where prolonged inference enables more intricate code generation and validation.  
* **Code Debugging and Generation:** Supporting an agent's explanation of its rationale for generating or correcting code, pinpointing potential issues sequentially, and iteratively refining the code based on test results (Self-Correction), leveraging extended inference time for thorough debugging cycles.  
* **Strategic Planning:** Assisting in the development of comprehensive plans through reasoning across various options, consequences, and preconditions, and adjusting plans based on real-time feedback (ReAct), where extended deliberation can lead to more effective and reliable plans.  
* **Medical Diagnosis:** Aiding an agent in systematically assessing symptoms, test outcomes, and patient histories to reach a diagnosis, articulating its reasoning at each phase, and potentially utilizing external instruments for data retrieval (ReAct). Increased inference time allows for a more comprehensive differential diagnosis.  
* **Legal Analysis:** Supporting the analysis of legal documents and precedents to formulate arguments or provide guidance, detailing the logical steps taken, and ensuring logical consistency through self-correction. Increased inference time allows for more in-depth legal research and argument construction.

> * **复杂问答：** 支持多跳查询的求解，需整合多源数据并执行逻辑推断，可能涉及多条推理路径的考察，并受益于更长推理时间以综合信息。  
> * **数学解题：** 将数学题拆为更小可解部分，展示逐步过程，并用代码执行做精确计算；更长推理时间支持更复杂的代码生成与校验。  
> * **代码调试与生成：** 支持智能体解释生成或修正代码的理由、顺序定位潜在问题，并基于测试结果迭代改进代码（自我纠正）；更长推理时间支撑更充分的调试循环。  
> * **战略规划：** 通过在多种选项、后果与前提间推理协助制定全面计划，并基于实时反馈调整计划（ReAct）；更长斟酌可带来更有效、可靠的计划。  
> * **医学诊断：** 帮助智能体系统评估症状、检查结果与病史以形成诊断，在各阶段阐明推理，并可借助外部工具检索数据（ReAct）；更长推理时间有助于更全面的鉴别诊断。  
> * **法律分析：** 支持分析法律文件与判例以形成论证或提供指引，详述逻辑步骤并通过自我纠正保证一致性；更长推理时间支持更深入研究与论证构建。

## Reasoning techniques

> ## 推理技术

To start, let's delve into the core reasoning techniques used to enhance the problem-solving abilities of AI models..

> 首先探讨用于增强 AI 模型解题能力的核心推理技术。

**Chain-of-Thought (CoT)** prompting significantly enhances LLMs complex reasoning abilities by mimicking a step-by-step thought process (see Fig. 1). Instead of providing a direct answer, CoT prompts guide the model to generate a sequence of intermediate reasoning steps. This explicit breakdown allows LLMs to tackle complex problems by decomposing them into smaller, more manageable sub-problems. This technique markedly improves the model's performance on tasks requiring multi-step reasoning, such as arithmetic, common sense reasoning, and symbolic manipulation. A primary advantage of CoT is its ability to transform a difficult, single-step problem into a series of simpler steps, thereby increasing the transparency of the LLM's reasoning process. This approach not only boosts accuracy but also offers valuable insights into the model's decision-making, aiding in debugging and comprehension.  CoT can be implemented using various strategies, including offering few-shot examples that demonstrate step-by-step reasoning or simply instructing the model to "think step by step." Its effectiveness stems from its ability to guide the model's internal processing toward a more deliberate and logical progression. As a result, Chain-of-Thought has become a cornerstone technique for enabling advanced reasoning capabilities in contemporary LLMs. This enhanced transparency and breakdown of complex problems into manageable sub-problems is particularly important for autonomous agents, as it enables them to perform more reliable and auditable actions in complex environments.  

> **思维链（Chain-of-Thought, CoT）** 提示通过模仿逐步思考过程显著增强 LLM 的复杂推理能力（见图 1）。CoT 不直接给答案，而是引导模型生成一系列中间推理步骤，将难题分解为更小、更易处理的子问题，从而提升算术、常识推理、符号操作等多步任务表现。CoT 的主要优势之一是把困难的单步问题转化为多步简单步骤，提高推理过程透明度，既提升准确率也有助于理解决策与调试。实现方式包括 few-shot 示范逐步推理，或简单指示「逐步思考」。其有效性来自引导内部处理走向更有意识、更符合逻辑的推进。思维链已成为当代 LLM 高级推理的基石技术；对自主智能体尤为重要，因其在复杂环境中带来更可靠、可审计的行为。

![COT: Chain of Thought](../assets-new/COT_Chain_of_Thought.png)  

Fig. 1: CoT prompt alongside the detailed, step-by-step response generated by the agent.

> 图 1：CoT 提示与智能体生成的分步详细回答

Let's see an example.  It begins with a set of instructions that tell the AI how to think, defining its persona and a clear five-step process to follow. This is the prompt that initiates structured thinking.

> 下面看一个例子：先有一套指示 AI 如何思考的说明，定义角色与清晰的五步流程，即启动结构化思考的提示。

Following that, the example shows the CoT process in action. The section labeled "Agent's Thought Process" is the internal monologue where the model executes the instructed steps. This is the literal "chain of thought." Finally, the "Agent's Final Answer" is the polished, comprehensive output generated as a result of that careful, step-by-step reasoning process

> 随后示例展示 CoT 的执行：标为「Agent's Thought Process」的部分是模型按指示执行步骤的内心独白，即字面意义上的「思维链」；「Agent's Final Answer」则是经逐步推理后整理输出的最终答案。

```markdown
You are an Information Retrieval Agent. Your goal is to answer the user's question comprehensively and accurately by thinking step-by-step. 

Here's the process you must follow: 
1.  **Analyze the Query:** Understand the core subject and specific requirements of the user's question. Identify key entities, keywords, and the type of information being sought. 
2.  **Formulate Search Queries (for Knowledge Base):** Based on your analysis, generate a list of precise search queries that you would use to retrieve relevant information from a knowledge base or external tools. 
3.  **Simulate Information Retrieval (Self-Correction/Reasoning):** For each search query, mentally consider what kind of information you expect to find. If you were to retrieve the content, what would be the most relevant snippets? Think about potential ambiguities or missing pieces. 
4.  **Synthesize Information:** Based on the simulated retrieval and your understanding of the user's original query, synthesize the gathered information into a coherent and complete answer. Ensure all aspects of the query are addressed. 
5.  **Review and Refine:** Before finalizing, critically evaluate your answer. Is it accurate? Is it comprehensive? Is it easy to understand? Is it concise? If not, identify what needs to be improved and how. 

**User Query:** "Explain the main differences between classical computers and quantum computers, and briefly describe a potential application of quantum computing." 

**Agent's Thought Process (Internal CoT Output - encouraged by the prompt):** 

**Thought 1 (Analyze Query):** 
The user wants two things: 
    1.  Main differences between classical and quantum computers. 
    2.  One potential application of quantum computing. Keywords: classical computers, quantum computers, differences, potential application. 

**Thought 2 (Formulate Search Queries):** 
    - "differences classical vs quantum computers" 
    - "how quantum computers work" 
    - "how classical computers work" 
    - "applications of quantum computing" 
    
**Thought 3 (Simulate Information Retrieval & Identify Key Concepts):** 
    - From "differences": Expect concepts like bits vs. qubits, superposition, entanglement, probabilistic nature, computational power for specific problems. 
    - From "how they work": Classical uses transistors/binary. Quantum uses quantum mechanics. 
    - From "applications": Expect drug discovery, material science, cryptography, optimization. 

**Thought 4 (Synthesize Information):** 
Classical computers use bits (0 or 1), processing information sequentially. Quantum computers use qubits, which can be 0, 1, or both simultaneously (superposition), and can be entangled, allowing for vastly different computational approaches. This enables them to solve certain problems (like factoring large numbers or simulating complex molecules) far more efficiently than classical computers. A potential application is in drug discovery, where quantum computers could simulate molecular interactions with unprecedented accuracy, accelerating the development of new medicines. 

**Thought 5 (Review and Refine):** 
    - Differences are covered (bits vs qubits, superposition, entanglement, processing). 
    - Application is given (drug discovery). - Is it brief? Yes. - Is it clear? Yes. - Looks good. 

**Agent's Final Answer (Output to User):** 
Classical computers process information using bits, which can be either a 0 or a 1 at any given time, performing operations sequentially. In contrast, quantum computers utilize qubits, which can exist in multiple states simultaneously through superposition and can be linked through entanglement, allowing for exponentially more complex computations. This fundamental difference enables quantum machines to tackle certain problems, such as simulating molecular structures or breaking complex encryption, that are intractable for even the most powerful classical supercomputers. A significant potential application of quantum computing lies in drug discovery, where its ability to precisely model molecular behavior could revolutionize the development of new pharmaceuticals.
```

**Tree-of-Thought (ToT)** is a reasoning technique that builds upon Chain-of-Thought (CoT). It allows large language models to explore multiple reasoning paths by branching into different intermediate steps, forming a tree structure (see Fig. 2\) This approach supports complex problem-solving by enabling backtracking, self-correction, and exploration of alternative solutions. Maintaining a tree of possibilities allows the model to evaluate various reasoning trajectories before finalizing an answer. This iterative process enhances the model's ability to handle challenging tasks that require strategic planning and decision-making.  

> **思维树（Tree-of-Thought, ToT）** 在 CoT 之上构建，允许 LLM 通过在不同中间步骤分支探索多条推理路径，形成树形结构（见图 2）。该方法通过回溯、自我纠正与探索替代解支持复杂问题求解；在定稿前评估多种推理轨迹，迭代过程增强模型在需战略规划与决策的任务上的表现。

![TOT: Tree of Thought](../assets-new/TOT_Tree_of_Thought.png)

Fig.2: Example of Tree of Thoughts

> 图 2：思维树示例

**Self-correction**, also known as self-refinement, is a crucial aspect of an agent's reasoning process, particularly within Chain-of-Thought prompting. It involves the agent's internal evaluation of its generated content and intermediate thought processes. This critical review enables the agent to identify ambiguities, information gaps, or inaccuracies in its understanding or solutions. This iterative cycle of reviewing and refining allows the agent to adjust its approach, improve response quality, and ensure accuracy and thoroughness before delivering a final output. This internal critique enhances the agent's capacity to produce reliable and high-quality results, as demonstrated in examples within the dedicated Chapter 4.

> **自我纠正（Self-correction）** 亦称自我精炼，是智能体推理过程的关键环节，尤其在 CoT 中：智能体对生成内容与中间思考做内部评估，发现歧义、信息缺口或理解/解答中的不准确之处；通过审阅—改进的迭代调整策略、提升回答质量，并在输出前确保准确与完备。内部批判提升可靠性与高质量结果的能力；专章（第 4 章）中有更多示例。

This example demonstrates a systematic process of self-correction, crucial for refining AI-generated content. It involves an iterative loop of drafting, reviewing against original requirements, and implementing specific improvements. The illustration begins by outlining the AI's function as a "Self-Correction Agent" with a defined five-step analytical and revision workflow. Following this, a subpar "Initial Draft" of a social media post is presented. The "Self-Correction Agent's Thought Process" forms the core of the demonstration. Here, the Agent critically evaluates the draft according to its instructions, pinpointing weaknesses such as low engagement and a vague call to action. It then suggests concrete enhancements, including the use of more impactful verbs and emojis. The process concludes with the "Final Revised Content," a polished and notably improved version that integrates the self-identified adjustments.

> 本例展示系统化的自我纠正流程，对改进 AI 生成内容至关重要：起草—对照原始要求审阅—落实具体改进的迭代循环。说明先界定「Self-Correction Agent」及五步分析与修订工作流；再给出一则欠佳的社交媒体帖「Initial Draft」；核心是「Self-Correction Agent's Thought Process」——按指示批判草稿，指出参与度低、行动号召弱等问题，并提出更强动词与表情符号等具体改进；最后给出整合自我改进的「Final Revised Content」。

```markdown
You are a highly critical and detail-oriented Self-Correction Agent. Your task is to review a previously generated piece of content against its original requirements and identify areas for improvement. Your goal is to refine the content to be more accurate, comprehensive, engaging, and aligned with the prompt. 

Here's the process you must follow for self-correction: 

1.  **Understand Original Requirements:** Review the initial prompt/requirements that led to the content's creation. What was the *original intent*? What were the key constraints or goals? 
2.  **Analyze Current Content:** Read the provided content carefully. 
3.  **Identify Discrepancies/Weaknesses:** Compare the current content against the original requirements. Look for:    
    * **Accuracy Issues:** Are there any factual errors or misleading statements?    
    * **Completeness Gaps:** Does it fully address all aspects of the original prompt? Is anything missing?    
    * **Clarity & Coherence:** Is the language clear, concise, and easy to understand? Does it flow logically?    
    * **Tone & Style:** Does it match the desired tone and style (e.g., professional, engaging, concise)?    
    * **Engagement:** Is it captivating? Does it hold the reader's attention?    
    * **Redundancy/Verbosity:** Can any parts be condensed or removed without losing meaning? 
4.  **Propose Specific Improvements:** For each identified weakness, suggest concrete and actionable changes. Do not just state the problem; propose a solution. 
5.  **Generate Revised Content:** Based on your proposed improvements, rewrite the original content to incorporate all the necessary changes. Ensure the revised content is polished and ready for final use. 

**Original Prompt/Requirements:** "Write a short, engaging social media post (max 150 characters) announcing a new eco-friendly product line: 'GreenTech Gadgets'." 

**Initial Draft (Content to be corrected):** "We have new products. They are green and techy. Buy GreenTech Gadgets now!" 

**Self-Correction Agent's Thought Process (Internal CoT Output - encouraged by the prompt):** 

**Thought 1 (Understand Original Requirements):** 
    - Short, engaging social media post. 
    - Max 150 characters. 
    - Announce "GreenTech Gadgets" - a new eco-friendly product line. 

**Thought 2 (Analyze Current Content):** 
"We have new products. They are green and techy. Buy GreenTech Gadgets now!" (64 characters) 

**Thought 3 (Identify Discrepancies/Weaknesses):** - **Engaging:** Not very engaging. Sounds generic. - **Eco-friendly:** Implied by "green," but not explicitly highlighted as a benefit. - **Call to Action:** "Buy now!" is okay, but could be more compelling. - **Conciseness:** It's short, but could use stronger verbs/phrasing. - **Impact:** Lacks excitement for a new product launch. 

**Thought 4 (Propose Specific Improvements):** - Make it more dynamic and exciting. - Emphasize "eco-friendly" and "innovation." - Use stronger verbs and more active voice. - Add a clear, engaging call to action. - Ensure it stays under 150 characters. **Thought 5 (Generate Revised Content):** Original: "We have new products. They are green and techy. Buy GreenTech Gadgets now!" Revised idea 1: "🌱 Discover GreenTech Gadgets! Our new eco-friendly line blends innovation with sustainability. Go green, go smart! Shop now! #EcoFriendly #GreenTech" (148 characters) This revision directly addresses eco-friendliness, uses emojis for engagement, adds a stronger call to action, and includes relevant hashtags while staying within the character limit. **Self-Correction Agent's Final Revised Content (Output to User):** 🌱 Discover GreenTech Gadgets! Our new eco-friendly line blends innovation with sustainability. Go green, go smart! Shop now! #EcoFriendly #GreenTech
```

Fundamentally, this technique integrates a quality control measure directly into the Agent's content generation, yielding more refined, precise, and superior results that more effectively meet intricate user demands.

> 从根本上，该技术将质量控制直接嵌入智能体内容生成，产出更精炼、精确、优质的成果，更好满足复杂用户需求。

**Program-Aided Language Models (PALMs)** integrate LLMs with symbolic reasoning capabilities. This integration allows the LLM to generate and execute code, such as Python, as part of its problem-solving process. PALMs offload complex calculations, logical operations, and data manipulation to a deterministic programming environment. This approach utilizes the strengths of traditional programming for tasks where LLMs might exhibit limitations in accuracy or consistency. When faced with symbolic challenges, the model can produce code, execute it, and convert the results into natural language. This hybrid methodology combines the LLM's understanding and generation abilities with precise computation, enabling the model to address a wider range of complex problems with potentially increased reliability and accuracy. This is important for agents as it allows them to perform more accurate and reliable actions by leveraging precise computation alongside their understanding and generation capabilities. An example is the use of external tools within Google's ADK for generating code.

> **程序辅助语言模型（PALMs）** 将 LLM 与符号推理结合，使 LLM 在解题过程中生成并执行 Python 等代码，把复杂计算、逻辑与数据操作卸载到确定性编程环境，弥补 LLM 在精度或一致性上的不足；面对符号任务可写代码、执行并将结果转回自然语言。混合方法结合理解与生成与精确计算，扩展可解问题范围并可能提高可靠性与准确性；对智能体而言，可在理解生成之外借助精确计算采取更准确、可靠的动作。谷歌 ADK 中通过外部工具生成代码即为一例。

```python
from google.adk.tools import agent_tool
from google.adk.agents import Agent
from google.adk.tools import google_search
from google.adk.code_executors import BuiltInCodeExecutor


search_agent = Agent(
    model="gemini-2.0-flash",
    name="SearchAgent",
    instruction="""
    You're a specialist in Google Search
    """,
    tools=[google_search],
)

coding_agent = Agent(
    model="gemini-2.0-flash",
    name="CodeAgent",
    instruction="""
    You're a specialist in Code Execution
    """,
    code_executor=BuiltInCodeExecutor(),
)

root_agent = Agent(
    name="RootAgent",
    model="gemini-2.0-flash",
    description="Root Agent",
    tools=[
        agent_tool.AgentTool(agent=search_agent),
        agent_tool.AgentTool(agent=coding_agent),
    ],
)
```

**Reinforcement Learning with Verifiable Rewards (RLVR):** While effective, the standard Chain-of-Thought (CoT) prompting used by many LLMs is a somewhat basic approach to reasoning. It generates a single, predetermined line of thought without adapting to the complexity of the problem. To overcome these limitations, a new class of specialized "reasoning models" has been developed. These models operate differently by dedicating a variable amount of "thinking" time before providing an answer. This "thinking" process produces a more extensive and dynamic Chain-of-Thought that can be thousands of tokens long. This extended reasoning allows for more complex behaviors like self-correction and backtracking, with the model dedicating more effort to harder problems. The key innovation enabling these models is a training strategy called Reinforcement Learning from Verifiable Rewards (RLVR). By training the model on problems with known correct answers (like math or code), it learns through trial and error to generate effective, long-form reasoning. This allows the model to evolve its problem-solving abilities without direct human supervision. Ultimately, these reasoning models don't just produce an answer; they generate a "reasoning trajectory" that demonstrates advanced skills like planning, monitoring, and evaluation. This enhanced ability to reason and strategize is fundamental to the development of autonomous AI agents, which can break down and solve complex tasks with minimal human intervention.

> **可验证奖励的强化学习（RLVR）：** 许多 LLM 使用的标准 CoT 虽有效，但相对基础：生成单一、固定的思路，未随问题复杂度调整。为克服局限，出现了一类专门的「推理模型」：在给出答案前投入可变的「思考」时间，产生更长、更动态的思维链（可达数千 token），支持自我纠正与回溯等更复杂行为，并对更难问题投入更多努力。支撑这些模型的关键训练策略是可验证奖励的强化学习（RLVR）：在已知正确答案的问题（如数学、代码）上通过试错学习生成长形式有效推理，使模型在无直接人类监督下演进解题能力。这类模型不仅产出答案，还产生展示规划、监控与评估等高级技能的「推理轨迹」；更强的推理与策略能力对开发能在最少人工干预下分解并解决复杂任务的自主 AI 智能体至关重要。

**ReAct** (Reasoning and Acting, see Fig. 3, where KB stands for Knowledge Base) is a paradigm that integrates Chain-of-Thought (CoT) prompting with an agent's ability to interact with external environments through tools. Unlike generative models that produce a final answer, a ReAct agent reasons about which actions to take. This reasoning phase involves an internal planning process, similar to CoT, where the agent determines its next steps, considers available tools, and anticipates outcomes. Following this, the agent acts by executing a tool or function call, such as querying a database, performing a calculation, or interacting with an API.

> **ReAct**（推理与行动，见图 3，KB 表示知识库）将 CoT 与智能体通过工具与外部环境交互的能力结合。与直接产出最终答案的生成模型不同，ReAct 智能体推理应采取何种行动：推理阶段类似 CoT 的内部规划——确定下一步、考虑可用工具并预判结果；随后通过执行工具或函数调用（查库、计算、调 API 等）行动。

![REACT: Reasoning and Act](../assets-new/REACT_Reasoning_and_Act.png)

Fig.3: Reasoning and Act

> 图 3：推理与行动（ReAct）

ReAct operates in an interleaved manner: the agent executes an action, observes the outcome, and incorporates this observation into subsequent reasoning. This iterative loop of “Thought, Action, Observation, Thought...” allows the agent to dynamically adapt its plan, correct errors, and achieve goals requiring multiple interactions with the environment. This provides a more robust and flexible problem-solving approach compared to linear CoT, as the agent responds to real-time feedback. By combining language model understanding and generation with the capability to use tools, ReAct enables agents to perform complex tasks requiring both reasoning and practical execution. This approach is crucial for agents as it allows them to not only reason but also to practically execute steps and interact with dynamic environments.

> ReAct 以交错方式运作：执行行动—观察结果—将观察纳入后续推理。「思考、行动、观察、思考……」的迭代循环使智能体能动态调整计划、纠正错误，并完成需与环境多次交互的目标。相较线性 CoT，该方法更稳健灵活，因智能体响应实时反馈。结合语言模型的理解与生成与工具使用能力，ReAct 使智能体能承担需推理与实际执行并重的复杂任务；对智能体至关重要，因其不仅推理，还能在动态环境中切实执行步骤。

**CoD** (Chain of Debates) is a formal AI framework proposed by Microsoft where multiple, diverse models collaborate and argue to solve a problem, moving beyond a single AI's "chain of thought." This system operates like an AI council meeting, where different models present initial ideas, critique each other's reasoning, and exchange counterarguments. The primary goal is to enhance accuracy, reduce bias, and improve the overall quality of the final answer by leveraging collective intelligence. Functioning as an AI version of peer review, this method creates a transparent and trustworthy record of the reasoning process. Ultimately, it represents a shift from a solitary Agent providing an answer to a collaborative team of Agents working together to find a more robust and validated solution.

> **CoD（辩论链）** 是微软提出的正式 AI 框架：多个异质模型协作与辩论解题，超越单个 AI 的「思维链」。系统类似 AI 理事会：不同模型提出初稿、互评推理并交换反方论证；目标是通过集体智慧提高准确率、降低偏见、改进最终答案质量。作为 AI 版的同行评审，该方法形成透明、可信的推理记录，体现从单一智能体给答案到多智能体协作寻求更稳健、经核验解的转变。

**GoD** (Graph of Debates)  is an advanced Agentic framework that reimagines discussion as a dynamic, non-linear network rather than a simple chain. In this model, arguments are individual nodes connected by edges that signify relationships like 'supports' or 'refutes,' reflecting the multi-threaded nature of real debate. This structure allows new lines of inquiry to dynamically branch off, evolve independently, and even merge over time. A conclusion is reached not at the end of a sequence, but by identifying the most robust and well-supported cluster of arguments within the entire graph. In this context, "well-supported" refers to knowledge that is firmly established and verifiable. This can include information considered to be ground truth, which means it is inherently correct and widely accepted as fact. Additionally, it encompasses factual evidence obtained through search grounding, where information is validated against external sources and real-world data. Finally, it also pertains to a consensus reached by multiple models during a debate, indicating a high degree of agreement and confidence in the information presented. This comprehensive approach ensures a more robust and reliable foundation for the information being discussed. This approach provides a more holistic and realistic model for complex, collaborative AI reasoning.

> **GoD（辩论图）** 是高级智能体框架：将讨论视为动态非线性网络而非简单链条。论证为节点，边表示「支持」「反驳」等关系，反映真实辩论的多线程特性；新探究线索可动态分支、独立演化甚至随时间合并。结论不在序列末端得出，而在全图中识别最稳健、证据最充分的论证簇。「充分支持」指牢固且可核验的知识：可含被视为 ground truth 的公认事实、经搜索接地（对外部源与现实数据校验）的事实证据，或多模型辩论达成的高共识与高置信信息。该方法为讨论信息提供更稳健可靠的基础，为复杂协作式 AI 推理提供更整体、更现实的模型。

**MASS (optional advanced topic):** An in-depth analysis of the design of multi-agent systems reveals that their effectiveness is critically dependent on both the quality of the prompts used to program individual agents and the topology that dictates their interactions. The complexity of designing these systems is significant, as it involves a vast and intricate search space. To address this challenge, a novel framework called Multi-Agent System Search (MASS) was developed to automate and optimize the design of MAS.

> **MASS（可选进阶主题）：** 对多智能体系统（MAS）设计的深入分析表明，其成效关键取决于编程各智能体的提示质量以及支配交互的拓扑；设计复杂度很高，涉及庞大而错综的搜索空间。为应对挑战，提出了多智能体系统搜索（MASS）框架，以自动化并优化 MAS 设计。

MASS employs a multi-stage optimization strategy that systematically navigates the complex design space by interleaving prompt and topology optimization (see Fig. 4)

> MASS 采用多阶段优化策略，通过交错进行提示与拓扑优化系统地在复杂设计空间中导航（见图 4）。

**1. Block-Level Prompt Optimization:** The process begins with a local optimization of prompts for individual agent types, or "blocks," to ensure each component performs its role effectively before being integrated into a larger system. This initial step is crucial as it ensures that the subsequent topology optimization builds upon well-performing agents, rather than suffering from the compounding impact of poorly configured ones. For example, when optimizing for the HotpotQA dataset, the prompt for a "Debator" agent is creatively framed to instruct it to act as an "expert fact-checker for a major publication". Its optimized task is to meticulously review proposed answers from other agents, cross-reference them with provided context passages, and identify any inconsistencies or unsupported claims. This specialized role-playing prompt, discovered during block-level optimization, aims to make the debator agent highly effective at synthesizing information before it's even placed into a larger workflow

> **1. 块级提示优化：** 先对各类智能体或「块」的提示做局部优化，确保各组件在并入大系统前能有效履职；该步至关重要，使后续拓扑优化建立在表现良好的智能体之上，而非被错误配置层层放大。例如针对 HotpotQA，「Debator」智能体的提示被创意地设定为「某主流媒体的专家事实核查员」：优化后的任务是细致审阅其他智能体提出的答案、与给定上下文对照并指出不一致或无依据主张。块级优化发现的这种角色扮演式提示，旨在使辩论者在进入更大工作流之前就能高效综合信息。

**2. Workflow Topology Optimization:** Following local optimization, MASS optimizes the workflow topology by selecting and arranging different agent interactions from a customizable design space. To make this search efficient, MASS employs an influence-weighted method. This method calculates the "incremental influence" of each topology by measuring its performance gain relative to a baseline agent and uses these scores to guide the search toward more promising combinations. For instance, when optimizing for the MBPP coding task, the topology search discovers that a specific hybrid workflow is most effective. The best-found topology is not a simple structure but a combination of an iterative refinement process with external tool use. Specifically, it consists of one predictor agent that engages in several rounds of reflection, with its code being verified by one executor agent that runs the code against test cases. This discovered workflow shows that for coding, a structure that combines iterative self-correction with external verification is superior to simpler MAS designs

> **2. 工作流拓扑优化：** 在局部优化之后，MASS 从可定制设计空间中选择并排列不同智能体交互以优化工作流拓扑。为提高搜索效率，采用影响加权法：相对基线智能体度量每种拓扑的「增量影响」（性能增益），用得分引导搜索走向更有前景的组合。例如针对 MBPP 编码任务，拓扑搜索发现某混合工作流最有效：最佳拓扑非简单结构，而是迭代精炼与外部工具使用的结合——具体包含一个预测智能体进行多轮反思，并由一个执行智能体针对测试用例运行代码做验证。该发现表明对编码任务，结合迭代自我纠正与外部验证的结构优于更简单的 MAS 设计。

![MASS: Multi-Agent System Search](../assets-new/MASS_Multi_Agent_System_Search.png)

Fig. 4: (Courtesy of the Authors): The Multi-Agent System Search (MASS) Framework is a three-stage optimization process that navigates a search space encompassing optimizable prompts (instructions and demonstrations) and configurable agent building blocks (Aggregate, Reflect, Debate, Summarize, and Tool-use). The first stage, Block-level Prompt Optimization, independently optimizes prompts for each agent module. Stage two, Workflow Topology Optimization, samples valid system configurations from an influence-weighted design space, integrating the optimized prompts. The final stage, Workflow-level Prompt Optimization, involves a second round of prompt optimization for the entire multi-agent system after the optimal workflow from Stage two has been identified

> 图 4（作者提供）：多智能体系统搜索（MASS）框架为三阶段优化过程，搜索空间包含可优化提示（指令与示例）与可配置智能体构建块（聚合、反思、辩论、摘要与工具使用）。第一阶段为块级提示优化，独立优化各模块提示；第二阶段为工作流拓扑优化，从影响加权设计空间中采样有效系统配置并整合已优化提示；第三阶段为工作流级提示优化，在确定第二阶段最优工作流后，对整个 MAS 再做一轮提示优化。

**3. Workflow-Level Prompt Optimization:** The final stage involves a global optimization of the entire system's prompts. After identifying the best-performing topology, the prompts are fine-tuned as a single, integrated entity to ensure they are tailored for orchestration and that agent interdependencies are optimized. As an example, after finding the best topology for the DROP dataset, the final optimization stage refines the "Predictor" agent's prompt. The final, optimized prompt is highly detailed, beginning by providing the agent with a summary of the dataset itself, noting its focus on "extractive question answering" and "numerical information". It then includes few-shot examples of correct question-answering behavior and frames the core instruction as a high-stakes scenario: "You are a highly specialized AI tasked with extracting critical numerical information for an urgent news report. A live broadcast is relying on your accuracy and speed". This multi-faceted prompt, combining meta-knowledge, examples, and role-playing, is tuned specifically for the final workflow to maximize accuracy

> **3. 工作流级提示优化：** 最后阶段对整个系统的提示做全局优化：在确定最佳拓扑后，将提示作为单一整合实体微调，以适配编排并优化智能体间依赖。例如针对 DROP 数据集找到最佳拓扑后，最终阶段精炼「Predictor」智能体提示：优化后的提示非常细致，先摘要数据集本身，强调「抽取式问答」与「数值信息」；再包含正确问答行为的 few-shot 示例，并将核心指令框定为高风险场景：「你是高度专业化的 AI，负责为紧急新闻报道抽取关键数值信息，直播正依赖你的准确与速度」。融合元知识、示例与角色扮演的多面提示针对最终工作流调优以最大化准确率。

Key Findings and Principles: Experiments demonstrate that MAS optimized by MASS significantly outperform existing manually designed systems and other automated design methods across a range of tasks. The key design principles for effective MAS, as derived from this research, are threefold

> 主要发现与原则：实验表明，经 MASS 优化的 MAS 在多种任务上显著优于现有人工设计系统与其他自动化设计方法。由此研究提炼的有效 MAS 设计原则有三条：

* Optimize individual agents with high-quality prompts before composing them.  
* Construct MAS by composing influential topologies rather than exploring an unconstrained search space.  
* Model and optimize the interdependencies between agents through a final, workflow-level joint optimization.

> * 在组合前先以高质量提示优化各智能体。  
> * 通过组合高影响拓扑构建 MAS，而非在无约束搜索空间中盲目探索。  
> * 通过最终工作流级联合优化建模并优化智能体间依赖。

Building on our discussion of key reasoning techniques, let's first examine a core performance principle: the Scaling Inference Law for LLMs. This law states that a model's performance predictably improves as the computational resources allocated to it increase. We can see this principle in action in complex systems like Deep Research, where an AI agent leverages these resources to autonomously investigate a topic by breaking it down into sub-questions, using Web search as a tool, and synthesizing its findings.

> 在关键推理技术讨论基础上，先看一条核心性能原则：LLM 的推理扩展定律——模型性能随分配的计算资源增加而可预期地提升。在 Deep Research 等复杂系统中可见该原则：AI 智能体利用这些资源自主调研主题，拆成子问题、以网络搜索为工具并综合发现。

**Deep Research.** The term "Deep Research" describes a category of AI Agentic tools designed to act as tireless, methodical research assistants. Major platforms in this space include Perplexity AI, Google's Gemini research capabilities, and OpenAI's advanced functions within ChatGPT (see Fig.5).

> **深度研究（Deep Research）。** 指一类旨在充当不知疲倦、有条理的研究助手的 AI 智能体工具。该领域主要平台包括 Perplexity AI、谷歌 Gemini 的研究能力，以及 ChatGPT 内 OpenAI 的高级功能（见图 5）。

![Google Deep Research for Information Gathering](../assets-new/Google_Deep_Research_for_Information_Gathering.png)

Fig. 5: Google Deep Research for Information Gathering

> 图 5：谷歌深度研究用于信息收集

A fundamental shift introduced by these tools is the change in the search process itself. A standard search provides immediate links, leaving the work of synthesis to you. Deep Research operates on a different model. Here, you task an AI with a complex query and grant it a "time budget"—usually a few minutes. In return for this patience, you receive a detailed report.

> 这些工具带来的根本变化是搜索过程本身：常规搜索立即给链接，综合工作留给你；深度研究采用不同模式——你给 AI 复杂查询并授予「时间预算」（通常数分钟），以这份耐心换取详细报告。

During this time, the AI works on your behalf in an agentic way. It autonomously performs a series of sophisticated steps that would be incredibly time-consuming for a person:

> 在此期间，AI 以智能体方式代你工作，自主执行一系列对人而言极其耗时的复杂步骤：

1. Initial Exploration: It runs multiple, targeted searches based on your initial prompt.  
2. Reasoning and Refinement: It reads and analyzes the first wave of results, synthesizes the findings, and critically identifies gaps, contradictions, or areas that require more detail.  
3. Follow-up Inquiry: Based on its internal reasoning, it conducts new, more nuanced searches to fill those gaps and deepen its understanding.  
4. Final Synthesis: After several rounds of this iterative searching and reasoning, it compiles all the validated information into a single, cohesive, and structured summary.

> 1. 初始探索：基于初始提示运行多次定向搜索。  
> 2. 推理与精炼：阅读分析首轮结果，综合发现并批判性识别缺口、矛盾或需更多细节之处。  
> 3. 跟进查询：依据内部推理开展更细致的新搜索以填补缺口、加深理解。  
> 4. 最终综合：经多轮迭代搜索与推理后，将已核验信息汇编为单一、连贯、结构化的摘要。

This systematic approach ensures a comprehensive and well-reasoned response, significantly enhancing the efficiency and depth of information gathering, thereby facilitating more agentic decision-making.

> 该系统化方法保证全面且理由充分的回应，显著提升信息收集效率与深度，从而支持更具智能体特征的决策。

## Scaling Inference Law

> ## 推理扩展定律

This critical principle dictates the relationship between an LLM's performance and the computational resources allocated during its operational phase, known as inference. The Inference Scaling Law differs from the more familiar scaling laws for training, which focus on how model quality improves with increased data volume and computational power during a model's creation. Instead, this law specifically examines the dynamic trade-offs that occur when an LLM is actively generating an output or answer.

> 该原则阐明 LLM 性能与其运行阶段（推理）所分配计算资源之间的关系。推理扩展定律不同于更熟悉的训练扩展定律——后者关注创建模型时数据量与算力增加如何提升质量；前者专门考察 LLM 积极生成输出或答案时的动态权衡。

A cornerstone of this law is the revelation that superior results can frequently be achieved from a comparatively smaller LLM by augmenting the computational investment at inference time. This doesn't necessarily mean using a more powerful GPU, but rather employing more sophisticated or resource-intensive inference strategies. A prime example of such a strategy is instructing the model to generate multiple potential answers—perhaps through techniques like diverse beam search or self-consistency methods—and then employing a selection mechanism to identify the most optimal output. This iterative refinement or multiple-candidate generation process demands more computational cycles but can significantly elevate the quality of the final response.

> 该定律的基石之一是：通过在推理时增加计算投入，较小 LLM 也常能取得更优结果——未必指更强 GPU，而是指更复杂或更耗资源的推理策略；例如让模型生成多个候选答案（如多样化束搜索或自洽法）再用选择机制挑出最优输出。迭代改进或多候选生成消耗更多计算周期，但可显著提升最终响应质量。

This principle offers a crucial framework for informed and economically sound decision-making in the deployment of Agents systems. It challenges the intuitive notion that a larger model will always yield better performance. The law posits that a smaller model, when granted a more substantial "thinking budget" during inference, can occasionally surpass the performance of a much larger model that relies on a simpler, less computationally intensive generation process. The "thinking budget" here refers to the additional computational steps or complex algorithms applied during inference, allowing the smaller model to explore a wider range of possibilities or apply more rigorous internal checks before settling on an answer.

> 该原则为部署智能体系统时的知情、经济决策提供重要框架，挑战「模型越大一定越好」的直觉：较小模型若在推理期获得更充足的「思考预算」，有时可超越依赖更简单、更省算力生成过程的更大模型。「思考预算」指推理阶段额外的计算步数或复杂算法，使较小模型在定案前能探索更广可能性或做更严内部检查。

Consequently, the Scaling Inference Law becomes fundamental to constructing efficient and cost-effective Agentic systems. It provides a methodology for meticulously balancing several interconnected factors:

> 因此，推理扩展定律成为构建高效、经济的智能体系统的基础，提供细致平衡若干相互关联因素的方法：

* **Model Size:** Smaller models are inherently less demanding in terms of memory and storage.  
* **Response Latency:** While increased inference-time computation can add to latency, the law helps identify the point at which the performance gains outweigh this increase, or how to strategically apply computation to avoid excessive delays.  
* **Operational Cost:** Deploying and running larger models typically incurs higher ongoing operational costs due to increased power consumption and infrastructure requirements. The law demonstrates how to optimize performance without unnecessarily escalating these costs.

> * **模型规模：** 较小模型在内存与存储上天然需求更低。  
> * **响应延迟：** 推理期计算增加可能拉高延迟，定律有助于判断性能收益何时超过延迟增加，或如何策略性投入计算以避免过度延迟。  
> * **运营成本：** 更大模型的部署与运行通常因功耗与基础设施带来更高持续成本；定律展示如何在不过度推高成本的情况下优化性能。

By understanding and applying the Scaling Inference Law, developers and organizations can make strategic choices that lead to optimal performance for specific agentic applications, ensuring that computational resources are allocated where they will have the most significant impact on the quality and utility of the LLM's output. This allows for more nuanced and economically viable approaches to AI deployment, moving beyond a simple "bigger is better" paradigm.

> 理解与运用推理扩展定律，开发者与组织可针对具体智能体应用做出战略选择，将计算资源分配到对 LLM 输出质量与效用影响最大的环节，从而在 AI 部署上采取更细致、经济上更可行的路径，超越简单的「越大越好」范式。

## Hands-On Code Example

> ## 动手代码示例

The DeepSearch code, open-sourced by Google, is available through the gemini-fullstack-langgraph-quickstart repository (Fig. 6). This repository provides a template for developers to construct full-stack AI agents using Gemini 2.5 and the LangGraph orchestration framework. This open-source stack facilitates experimentation with agent-based architectures and can be integrated with local LLLMs such as Gemma. It utilizes Docker and modular project scaffolding for rapid prototyping. It should be noted that this release serves as a well-structured demonstration and is not intended as a production-ready backend.

> 谷歌开源的 DeepSearch 代码见 gemini-fullstack-langgraph-quickstart 仓库（图 6）。该仓库为开发者提供模板，用 Gemini 2.5 与 LangGraph 编排框架构建全栈 AI 智能体；开源栈便于试验基于智能体的架构，并可与 Gemma 等本地 LLM 集成；使用 Docker 与模块化脚手架快速原型。需注意该发布为结构良好的演示，并非生产级后端。

![Example of DeepSearch with multiple Reflection Steps](../assets-new/Example_of_DeepSearch_with_multiple_Reflection_Steps.png)


Fig. 6: (Courtesy of authors) Example of DeepSearch with multiple Reflection steps

> 图 6（作者提供）：含多轮反思步骤的 DeepSearch 示例

This project provides a full-stack application featuring a React frontend and a LangGraph backend, designed for advanced research and conversational AI. A LangGraph agent dynamically generates search queries using Google Gemini models and integrates web research via the Google Search API. The system employs reflective reasoning to identify knowledge gaps, refine searches iteratively, and synthesize answers with citations. The frontend and backend support hot-reloading. The project's structure includes separate frontend/ and backend/ directories. Requirements for setup include Node.js, npm, Python 3.8+, and a Google Gemini API key. After configuring the API key in the backend's .env file, dependencies for both the backend (using pip install .) and frontend (npm install) can be installed. Development servers can be run concurrently with make dev or individually. The backend agent, defined in backend/src/agent/graph.py, generates initial search queries, conducts web research, performs knowledge gap analysis, refines queries iteratively, and synthesizes a cited answer using a Gemini model. Production deployment involves the backend server delivering a static frontend build and requires Redis for streaming real-time output and a Postgres database for managing data. A Docker image can be built and run using docker-compose up, which also requires a LangSmith API key for the docker-compose.yml example. The application utilizes React with Vite, Tailwind CSS, Shadcn UI, LangGraph, and Google Gemini. The project is licensed under the Apache License 2.0.

> 该项目提供 React 前端与 LangGraph 后端的全栈应用，面向高级研究与对话式 AI。LangGraph 智能体用谷歌 Gemini 动态生成检索查询并通过 Google Search API 做网络研究；系统用反思推理识别知识缺口、迭代精炼搜索并综合带引用的答案。前后端支持热重载；目录分为 frontend/ 与 backend/。环境需 Node.js、npm、Python 3.8+ 与 Google Gemini API 密钥；在 backend 的 .env 配置密钥后，可分别用 pip install . 与 npm install 安装依赖；开发可用 make dev 同时启动或分别启动。后端智能体定义于 backend/src/agent/graph.py：生成初始查询、执行网络研究、做知识缺口分析、迭代精炼查询并用 Gemini 综合带引用答案。生产部署由后端提供静态前端构建；需 Redis 流式实时输出、Postgres 管理数据；可用 docker-compose up 构建运行镜像，示例 docker-compose.yml 还需 LangSmith API 密钥。技术栈含 React、Vite、Tailwind CSS、Shadcn UI、LangGraph、Google Gemini；项目以 Apache License 2.0 许可。

| ``# Create our Agent Graph builder = StateGraph(OverallState, config_schema=Configuration) # Define the nodes we will cycle between builder.add_node("generate_query", generate_query) builder.add_node("web_research", web_research) builder.add_node("reflection", reflection) builder.add_node("finalize_answer", finalize_answer) # Set the entrypoint as `generate_query` # This means that this node is the first one called builder.add_edge(START, "generate_query") # Add conditional edge to continue with search queries in a parallel branch builder.add_conditional_edges(    "generate_query", continue_to_web_research, ["web_research"] ) # Reflect on the web research builder.add_edge("web_research", "reflection") # Evaluate the research builder.add_conditional_edges(    "reflection", evaluate_research, ["web_research", "finalize_answer"] ) # Finalize the answer builder.add_edge("finalize_answer", END) graph = builder.compile(name="pro-search-agent")`` |
| :---- |

Fig.4: Example of DeepSearch with LangGraph (code from backend/src/agent/graph.py)

> 图 4：DeepSearch 与 LangGraph 示例（代码来自 backend/src/agent/graph.py）

## So, what do agents think?

> ## 那么，智能体如何「思考」？

In summary, an agent's thinking process is a structured approach that combines reasoning and acting to solve problems. This method allows an agent to explicitly plan its steps, monitor its progress, and interact with external tools to gather information.

> 总之，智能体的思考过程是结合推理与行动解决问题的结构化方法：可显式规划步骤、监控进度并与外部工具交互以收集信息。

At its core, the agent's "thinking" is facilitated by a powerful LLM. This LLM generates a series of thoughts that guide the agent's subsequent actions. The process typically follows a thought-action-observation loop:

> 核心是强大的 LLM 促成「思考」：生成一系列思想指导后续行动；过程通常遵循思考—行动—观察循环：

1. **Thought:** The agent first generates a textual thought that breaks down the problem, formulates a plan, or analyzes the current situation. This internal monologue makes the agent's reasoning process transparent and steerable.  
2. **Action:** Based on the thought, the agent selects an action from a predefined, discrete set of options. For example, in a question-answering scenario, the action space might include searching online, retrieving information from a specific webpage, or providing a final answer.  
3. **Observation:** The agent then receives feedback from its environment based on the action taken. This could be the results of a web search or the content of a webpage.

> 1. **思考：** 智能体首先生成文本化思考，拆解问题、形成计划或分析现状；内心独白使推理透明、可引导。  
> 2. **行动：** 基于思考从预定义离散选项中选行动；例如问答场景中可包括联网搜索、从特定网页取信息或给出最终答案。  
> 3. **观察：** 智能体根据行动从环境获得反馈，如搜索结果或网页内容。

This cycle repeats, with each observation informing the next thought, until the agent determines that it has reached a final solution and performs a "finish" action.

> 循环重复，每次观察指导下一次思考，直至智能体认定已得最终解并执行「结束」动作。

The effectiveness of this approach relies on the advanced reasoning and planning capabilities of the underlying LLM. To guide the agent, the ReAct framework often employs few-shot learning, where the LLM is provided with examples of human-like problem-solving trajectories. These examples demonstrate how to effectively combine thoughts and actions to solve similar tasks.

> 该方法的有效性依赖底层 LLM 的高级推理与规划能力。ReAct 常用 few-shot 学习，向 LLM 提供类人解题轨迹示例，展示如何有效组合思考与行动以解类似任务。

The frequency of an agent's thoughts can be adjusted depending on the task. For knowledge-intensive reasoning tasks like fact-checking, thoughts are typically interleaved with every action to ensure a logical flow of information gathering and reasoning. In contrast, for decision-making tasks that require many actions, such as navigating a simulated environment, thoughts may be used more sparingly, allowing the agent to decide when thinking is necessary

> 思考频率可按任务调整：知识密集型推理（如事实核查）通常每次行动都穿插思考以保证信息收集与推理的逻辑流；而需大量行动的决策任务（如模拟环境导航）可更节制地使用思考，由智能体自行判断何时需要思考。

## At a Glance

> ## 速览

**What**: Complex problem-solving often requires more than a single, direct answer, posing a significant challenge for AI. The core problem is enabling AI agents to tackle multi-step tasks that demand logical inference, decomposition, and strategic planning. Without a structured approach, agents may fail to handle intricacies, leading to inaccurate or incomplete conclusions. These advanced reasoning methodologies aim to make an agent's internal "thought" process explicit, allowing it to systematically work through challenges.

> **是什么：** 复杂解题往往不能靠单一直接回答，对 AI 构成重大挑战；核心问题是使智能体能处理需要逻辑推断、分解与战略规划的多步任务。缺乏结构化方法时，智能体可能无法应对细节，导致结论不准或不完整。这些高级推理方法旨在外显智能体内部「思考」过程，使其系统性地应对挑战。

**Why:** The standardized solution is a suite of reasoning techniques that provide a structured framework for an agent's problem-solving process. Methodologies like Chain-of-Thought (CoT) and Tree-of-Thought (ToT) guide LLMs to break down problems and explore multiple solution paths. Self-Correction allows for the iterative refinement of answers, ensuring higher accuracy. Agentic frameworks like ReAct integrate reasoning with action, enabling agents to interact with external tools and environments to gather information and adapt their plans. This combination of explicit reasoning, exploration, refinement, and tool use creates more robust, transparent, and capable AI systems.

> **为什么：** 标准化方案是一套为智能体解题过程提供结构化框架的推理技术。CoT、ToT 等引导 LLM 拆解问题并探索多条路径；自我纠正支持迭代改进答案以提高准确率；ReAct 等智能体框架将推理与行动结合，使智能体能与外部工具和环境交互以收集信息并调整计划。显式推理、探索、改进与工具使用相结合，造就更稳健、透明、能力更强的 AI 系统。

**Rule of Thumb:** Use these reasoning techniques when a problem is too complex for a single-pass answer and requires decomposition, multi-step logic, interaction with external data sources or tools, or strategic planning and adaptation. They are ideal for tasks where showing the "work" or thought process is as important as the final answer.

> **经验法则：** 当问题复杂到无法一次作答、需要分解、多步逻辑、与外部数据源或工具交互，或战略规划与适应时，宜使用这些推理技术。若展示「演算过程」或思考过程与最终答案同等重要，尤为适用。

**Visual Summary:**

> **图示摘要：**

![Reasoning Design Pattern](../assets-new/Reasoning_Design_Pattern.png)

Fig. 7: Reasoning design pattern

> 图 7：推理设计模式

## Key Takeaways

> ## 要点

* By making their reasoning explicit, agents can formulate transparent, multi-step plans, which is the foundational capability for autonomous action and user trust.  
* The ReAct framework provides agents with their core operational loop, empowering them to move beyond mere reasoning and interact with external tools to dynamically act and adapt within an environment.  
* The Scaling Inference Law implies an agent's performance is not just about its underlying model size, but its allocated "thinking time," allowing for more deliberate and higher-quality autonomous actions.  
* Chain-of-Thought (CoT) serves as an agent's internal monologue, providing a structured way to formulate a plan by breaking a complex goal into a sequence of manageable actions.  
* Tree-of-Thought and Self-Correction give agents the crucial ability to deliberate, allowing them to evaluate multiple strategies, backtrack from errors, and improve their own plans before execution.  
* Collaborative frameworks like Chain of Debates (CoD) signal the shift from solitary agents to multi-agent systems, where teams of agents can reason together to tackle more complex problems and reduce individual biases.  
* Applications like Deep Research demonstrate how these techniques culminate in agents that can execute complex, long-running tasks, such as in-depth investigation, completely autonomously on a user's behalf.  
* To build effective teams of agents, frameworks like MASS automate the optimization of how individual agents are instructed and how they interact, ensuring the entire multi-agent system performs optimally.  
* By integrating these reasoning techniques, we build agents that are not just automated but truly autonomous, capable of being trusted to plan, act, and solve complex problems without direct supervision.

> * 外显推理使智能体能形成透明、多步计划，这是自主行动与用户信任的基础能力。  
> * ReAct 为智能体提供核心运行循环，使其超越纯推理，能与外部工具交互并在环境中动态行动与适应。  
> * 推理扩展定律表明智能体性能不仅取决于底层模型规模，还取决于分配的「思考时间」，从而支持更审慎、更高质量的自主行动。  
> * CoT 作为智能体内心独白，提供将复杂目标拆为可管理动作序列的结构化规划方式。  
> * 思维树与自我纠正赋予智能体斟酌能力：评估多策略、从错误回溯、在执行前改进自身计划。  
> * 辩论链（CoD）等协作框架标志从孤立智能体到多智能体系统的转变，团队可共同推理以应对更复杂问题并降低个体偏见。  
> * 深度研究等应用展示这些技术如何汇聚为可完全自主、长时间执行深入调研等复杂任务的智能体。  
> * 为构建高效智能体团队，MASS 等框架自动化优化各智能体的指令与交互方式，使整个 MAS 表现更优。  
> * 整合这些推理技术，可构建不仅是自动化、而且真正自主的智能体，使其能在无直接监督下被信任地规划、行动并解决复杂问题。

## Conclusions

> ## 结论

Modern AI is evolving from passive tools into autonomous agents, capable of tackling complex goals through structured reasoning. This agentic behavior begins with an internal monologue, powered by techniques like Chain-of-Thought (CoT), which allows an agent to formulate a coherent plan before acting. True autonomy requires deliberation, which agents achieve through Self-Correction and Tree-of-Thought (ToT), enabling them to evaluate multiple strategies and independently improve their own work. The pivotal leap to fully agentic systems comes from the ReAct framework, which empowers an agent to move beyond thinking and start acting by using external tools. This establishes the core agentic loop of thought, action, and observation, allowing the agent to dynamically adapt its strategy based on environmental feedback.

> 现代 AI 正从被动工具演进为能通过结构化推理应对复杂目标的自主智能体。智能体行为始于由 CoT 等技术驱动的内心独白，使智能体在行动前形成连贯计划。真正自主需要斟酌：智能体通过自我纠正与 ToT 评估多策略并独立改进自身工作。迈向完全智能体系统的关键一跃来自 ReAct——使智能体超越思考，通过外部工具开始行动，建立思考—行动—观察的核心循环，并据环境反馈动态调整策略。

An agent's capacity for deep deliberation is fueled by the Scaling Inference Law, where more computational "thinking time" directly translates into more robust autonomous actions. The next frontier is the multi-agent system, where frameworks like Chain of Debates (CoD) create collaborative agent societies that reason together to achieve a common goal. This is not theoretical; agentic applications like Deep Research already demonstrate how autonomous agents can execute complex, multi-step investigations on a user's behalf. The overarching goal is to engineer reliable and transparent autonomous agents that can be trusted to independently manage and solve intricate problems. Ultimately, by combining explicit reasoning with the power to act, these methodologies are completing the transformation of AI into truly agentic problem-solvers.

> 智能体深度斟酌能力由推理扩展定律驱动：更多计算「思考时间」直接转化为更稳健的自主行动。下一前沿是多智能体系统：CoD 等框架构建协作式智能体社会，共同推理以达成共同目标。这并非空谈：深度研究等应用已展示自主智能体如何代用户执行复杂多步调研。总目标是工程化可靠、透明的自主智能体，使其能被信任地独立管理与解决棘手问题。归根结底，显式推理与行动能力相结合，正推动 AI 完成向真正智能体式问题求解者的转变。

## References

Relevant research includes:

1. "Chain-of-Thought Prompting Elicits Reasoning in Large Language Models" by Wei et al. (2022)  
2. "Tree of Thoughts: Deliberate Problem Solving with Large Language Models" by Yao et al. (2023)  
3. "Program-Aided Language Models" by Gao et al. (2023)  
4. "ReAct: Synergizing Reasoning and Acting in Language Models" by Yao et al. (2023)  
5. Inference Scaling Laws: An Empirical Analysis of Compute-Optimal Inference for LLM Problem-Solving, 2024  
6. Multi-Agent Design: Optimizing Agents with Better Prompts and Topologies, [https://arxiv.org/abs/2502.02533](https://arxiv.org/abs/2502.02533)
