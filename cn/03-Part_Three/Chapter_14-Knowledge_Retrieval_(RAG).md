# Chapter 14: Knowledge Retrieval (RAG)

LLMs exhibit substantial capabilities in generating human-like text. However, their knowledge base is typically confined to the data on which they were trained, limiting their access to real-time information, specific company data, or highly specialized details. Knowledge Retrieval (RAG, or  Retrieval Augmented Generation), addresses this limitation. RAG enables LLMs to access and integrate external, current, and context-specific information, thereby enhancing the accuracy, relevance, and factual basis of their outputs.

> 大语言模型在生成类人文本方面能力突出，但其知识库通常局限于训练数据，难以获取实时信息、特定企业数据或高度专业的细节。知识检索（RAG，即检索增强生成，Retrieval Augmented Generation）针对这一局限：使 LLM 能够访问并整合外部的、当前的、与语境相关的信息，从而提升输出的准确性、相关性与事实依据。

For AI agents, this is crucial as it allows them to ground their actions and responses in real-time, verifiable data beyond their static training. This capability enables them to perform complex tasks accurately, such as accessing the latest company policies to answer a specific question or checking current inventory before placing an order. By integrating external knowledge, RAG transforms agents from simple conversationalists into effective, data-driven tools capable of executing meaningful work.

> 对 AI 智能体而言，这一点至关重要：使其行为与回应能锚定在超越静态训练、可实时核验的数据上。由此它们能更准确地执行复杂任务，例如查阅最新公司政策以回答具体问题，或在下单前核对当前库存。通过整合外部知识，RAG 将智能体从简单对话者转变为能有效执行有意义工作的数据驱动型工具。

## Knowledge Retrieval (RAG) Pattern Overview

The Knowledge Retrieval (RAG) pattern significantly enhances the capabilities of LLMs by granting them access to external knowledge bases before generating a response. Instead of relying solely on their internal, pre-trained knowledge, RAG allows LLMs to "look up" information, much like a human might consult a book or search the internet. This process empowers LLMs to provide more accurate, up-to-date, and verifiable answers.

> 「知识检索（RAG）」模式通过在生成回应之前让 LLM 访问外部知识库，显著增强其能力。RAG 使 LLM 不仅依赖内部预训练知识，还能「查阅」信息——类似人类翻书或上网搜索——从而提供更准确、更新且可核验的答案。

When a user poses a question or gives a prompt to an AI system using RAG, the query isn't sent directly to the LLM. Instead, the system first scours a vast external knowledge base—a highly organized library of documents, databases, or web pages—for relevant information. This search is not a simple keyword match; it's a "semantic search" that understands the user's intent and the meaning behind their words. This initial search pulls out the most pertinent snippets or "chunks" of information. These extracted pieces are then "augmented," or added, to the original prompt, creating a richer, more informed query. Finally, this enhanced prompt is sent to the LLM. With this additional context, the LLM can generate a response that is not only fluent and natural but also factually grounded in the retrieved data.

> 当用户向使用 RAG 的 AI 系统提问或给出提示时，查询不会直接发给 LLM。系统首先在庞大的外部知识库——高度组织的文档、数据库或网页集合——中搜寻相关信息。这种搜索不是简单关键词匹配，而是理解用户意图与词语背后含义的「语义搜索」。初次检索会抽出最相关的片段或「块」（chunks）；这些片段再被「增强」——即并入原始提示——形成更丰富、信息更充分的查询。最后，这一增强后的提示才发送给 LLM。借助额外语境，LLM 生成的回应不仅流畅自然，还能在事实上锚定于检索到的数据。

The RAG framework provides several significant benefits. It allows LLMs to access up-to-date information, thereby overcoming the constraints of their static training data. This approach also reduces the risk of "hallucination"—the generation of false information—by grounding responses in verifiable data. Moreover, LLMs can utilize specialized knowledge found in internal company documents or wikis. A vital advantage of this process is the capability to offer "citations," which pinpoint the exact source of information, thereby enhancing the trustworthiness and verifiability of the AI's responses..

> RAG 框架带来若干重要收益：使 LLM 能获取最新信息，突破静态训练数据的限制；通过将回应锚定在可核验数据上，降低「幻觉」（编造虚假信息）的风险；还能利用公司内部文档或维基中的专业知识。该过程的一大优势是可提供「引用」，精确指向信息来源，从而增强 AI 回应的可信度与可验证性。

To fully appreciate how RAG functions, it's essential to understand a few core concepts (see Fig.1):

> 要完整理解 RAG 如何运作，需掌握若干核心概念（见图 1）：

### Embeddings

In the context of LLMs, embeddings are numerical representations of text, such as words, phrases, or entire documents. These representations are in the form of a vector, which is a list of numbers. The key idea is to capture the semantic meaning and the relationships between different pieces of text in a mathematical space. Words or phrases with similar meanings will have embeddings that are closer to each other in this vector space. For instance, imagine a simple 2D graph. The word "cat" might be represented by the coordinates (2, 3), while "kitten" would be very close at (2.1, 3.1). In contrast, the word "car" would have a distant coordinate like (8, 1), reflecting its different meaning. In reality, these embeddings are in a much higher-dimensional space with hundreds or even thousands of dimensions, allowing for a very nuanced understanding of language.

> 在 LLM 语境中，嵌入（embeddings）是文本（词、短语或整篇文档）的数值表示，通常以向量（数字列表）形式存在。核心思想是在数学空间中捕捉语义及不同文本片段之间的关系：含义相近的词或短语，其向量在该空间中彼此更近。例如简单二维图中，「cat」可能在 (2, 3)，「kitten」在 (2.1, 3.1) 附近；而「car」可能在 (8, 1) 等较远位置，反映语义差异。现实中嵌入处于高维空间（数百乃至数千维），以支持对语言的细致理解。

### Text Similarity

Text similarity refers to the measure of how alike two pieces of text are. This can be at a surface level, looking at the overlap of words (lexical similarity), or at a deeper, meaning-based level. In the context of RAG, text similarity is crucial for finding the most relevant information in the knowledge base that corresponds to a user's query. For instance, consider the sentences: "What is the capital of France?" and "Which city is the capital of France?". While the wording is different, they are asking the same question. A good text similarity model would recognize this and assign a high similarity score to these two sentences, even though they only share a few words. This is often calculated using the embeddings of the texts.

> 文本相似度衡量两段文本有多相像：可以是表层用词重叠（词汇相似度），也可以是更深层的语义层面。在 RAG 中，文本相似度对于在知识库中找到与用户查询最相关的信息至关重要。例如「What is the capital of France?」与「Which city is the capital of France?」措辞不同但问的是同一问题；良好的文本相似度模型会识别这一点并给出高分，即便共享词不多。这常通过文本的嵌入向量来计算。

### Semantic Similarity and Distance

Semantic similarity is a more advanced form of text similarity that focuses purely on the meaning and context of the text, rather than just the words used. It aims to understand if two pieces of text convey the same concept or idea. Semantic distance is the inverse of this; a high semantic similarity implies a low semantic distance, and vice versa. In RAG, semantic search relies on finding documents with the smallest semantic distance to the user's query. For instance, the phrases "a furry feline companion" and "a domestic cat" have no words in common besides "a". However, a model that understands semantic similarity would recognize that they refer to the same thing and would consider them to be highly similar. This is because their embeddings would be very close in the vector space, indicating a small semantic distance. This is the "smart search" that allows RAG to find relevant information even when the user's wording doesn't exactly match the text in the knowledge base.

> 语义相似度是更进阶的文本相似度形式，关注含义与语境而非仅用词。它旨在判断两段文本是否表达同一概念或想法。语义距离与之相反：语义相似度高则语义距离小，反之亦然。在 RAG 中，语义搜索依赖找到与用户查询语义距离最小的文档。例如「a furry feline companion」与「a domestic cat」除「a」外几乎无共同词，但理解语义的模型会认定二者高度相似，因其嵌入在向量空间中非常接近、语义距离小。正是这种「智能搜索」使 RAG 即使用户措辞与知识库原文不完全一致也能找到相关信息。

![RAG Core Concept: Chunking, Embeddings, and Vector Database](../assets-new/RAG_Core_Concepts_Chunking_Embeddings_and_Vector_Database.png)

Fig.1: RAG Core Concepts: Chunking, Embeddings, and Vector Database

> 图 1：RAG 核心概念：分块、嵌入与向量数据库

### Chunking of Documents

Chunking is the process of breaking down large documents into smaller, more manageable pieces, or "chunks." For a RAG system to work efficiently, it cannot feed entire large documents into the LLM. Instead, it processes these smaller chunks. The way documents are chunked is important for preserving the context and meaning of the information. For instance, instead of treating a 50-page user manual as a single block of text, a chunking strategy might break it down into sections, paragraphs, or even sentences. For instance, a section on "Troubleshooting" would be a separate chunk from the "Installation Guide." When a user asks a question about a specific problem, the RAG system can then retrieve the most relevant troubleshooting chunk, rather than the entire manual. This makes the retrieval process faster and the information provided to the LLM more focused and relevant to the user's immediate need. Once documents are chunked, the RAG system must employ a retrieval technique to find the most relevant pieces for a given query. The primary method is vector search, which uses embeddings and semantic distance to find chunks that are conceptually similar to the user's question. An older, but still valuable, technique is BM25, a keyword-based algorithm that ranks chunks based on term frequency without understanding semantic meaning. To get the best of both worlds, hybrid search approaches are often used, combining the keyword precision of BM25 with the contextual understanding of semantic search. This fusion allows for more robust and accurate retrieval, capturing both literal matches and conceptual relevance.

> 分块（chunking）是将大文档拆成更小、更易处理的「块」的过程。RAG 要高效工作，不能把整份大文档一次性喂给 LLM，而是处理这些较小的块。如何分块对保留信息与语境至关重要。例如不必把 50 页用户手册当作单一文本块，而可按章节、段落甚至句子切分；「故障排除」与「安装指南」应是不同块。用户询问具体问题时，RAG 可检索最相关的故障排除块，而非整本手册，从而加快检索并使提供给 LLM 的信息更聚焦、更贴合即时需求。文档分块后，RAG 需用检索技术为给定查询找到最相关片段。主要方法是向量搜索：用嵌入与语义距离找到与用户问题概念相近的块。较老但仍有用的是 BM25：基于词频排序、不理解语义。为兼取二者之长，常采用混合检索，将 BM25 的关键词精度与语义搜索的语境理解结合，使检索更稳健、更准确，既捕获字面匹配也捕获概念相关。

### Vector Databases

A vector database is a specialized type of database designed to store and query embeddings efficiently. After documents are chunked and converted into embeddings, these high-dimensional vectors are stored in a vector database. Traditional retrieval techniques, like keyword-based search, are excellent at finding documents containing exact words from a query but lack a deep understanding of language. They wouldn't recognize that "furry feline companion" means "cat." This is where vector databases excel. They are built specifically for semantic search. By storing text as numerical vectors, they can find results based on conceptual meaning, not just keyword overlap. When a user's query is also converted into a vector, the database uses highly optimized algorithms (like HNSW \- Hierarchical Navigable Small World) to rapidly search through millions of vectors and find the ones that are "closest" in meaning. This approach is far superior for RAG because it uncovers relevant context even if the user's phrasing is completely different from the source documents. In essence, while other techniques search for words, vector databases search for meaning. This technology is implemented in various forms, from managed databases like Pinecone and Weaviate to open-source solutions such as Chroma DB, Milvus, and Qdrant. Even existing databases can be augmented with vector search capabilities, as seen with Redis, Elasticsearch, and Postgres (using the pgvector extension). The core retrieval mechanisms are often powered by libraries like Meta AI's FAISS or Google Research's ScaNN, which are fundamental to the efficiency of these systems.

> 向量数据库是专门用于高效存储与查询嵌入的一类数据库。文档分块并转为嵌入后，这些高维向量存入向量数据库。传统检索（如关键词搜索）擅长找含查询词的文档，但缺乏对语言的深层理解，无法识别「furry feline companion」意指「猫」。向量数据库正擅长于此：为语义搜索而构建。将文本存为数值向量后，可按概念含义而非仅关键词重叠找结果。用户查询同样向量化后，数据库用高度优化的算法（如 HNSW——分层可导航小世界）在数百万向量中快速找出含义上「最近」的结果。对 RAG 而言这远为优越，即使用户表述与源文档完全不同也能发现相关语境。简言之：其他技术搜词，向量库搜义。实现形式多样：托管库如 Pinecone、Weaviate；开源如 Chroma DB、Milvus、Qdrant；亦可在 Redis、Elasticsearch、Postgres（pgvector 扩展）等现有系统上增强向量检索。核心检索常由 Meta FAISS、Google ScaNN 等库驱动，是这些系统效率的基础。

### RAG's Challenges

Despite its power, the RAG pattern is not without its challenges. A primary issue arises when the information needed to answer a query is not confined to a single chunk but is spread across multiple parts of a document or even several documents. In such cases, the retriever might fail to gather all the necessary context, leading to an incomplete or inaccurate answer. The system's effectiveness is also highly dependent on the quality of the chunking and retrieval process; if irrelevant chunks are retrieved, it can introduce noise and confuse the LLM. Furthermore, effectively synthesizing information from potentially contradictory sources remains a significant hurdle for these systems.  Besides that, another challenge is that RAG requires the entire knowledge base to be pre-processed and stored in specialized databases, such as vector or graph databases, which is a considerable undertaking. Consequently, this knowledge requires periodic reconciliation to remain up-to-date, a crucial task when dealing with evolving sources like company wikis. This entire process can have a noticeable impact on performance, increasing latency, operational costs, and the number of tokens used in the final prompt.

> 尽管强大，RAG 模式仍有挑战。首要问题之一是：回答所需信息可能不在单一块内，而分散在文档多处甚至多份文档中；此时检索器可能无法收齐必要语境，导致回答不完整或不准确。系统效果也高度依赖分块与检索质量；若检索到无关块，会引入噪声并干扰 LLM。此外，有效综合可能相互矛盾来源的信息仍是难点。再者，RAG 要求对整个知识库预处理并存入专用数据库（向量库或图数据库等），工程量大；知识还需定期对齐更新，对企业维基等不断变化的数据源尤为关键。全过程对性能影响明显：增加延迟、运营成本与最终提示中的 token 用量。

In summary,  the Retrieval-Augmented Generation (RAG) pattern represents a significant leap forward in making AI more knowledgeable and reliable. By seamlessly integrating an external knowledge retrieval step into the generation process, RAG addresses some of the core limitations of standalone LLMs. The foundational concepts of embeddings and semantic similarity, combined with retrieval techniques like keyword and hybrid search, allow the system to intelligently find relevant information, which is made manageable through strategic chunking. This entire retrieval process is powered by specialized vector databases designed to store and efficiently query millions of embeddings at scale. While challenges in retrieving fragmented or contradictory information persist, RAG empowers LLMs to produce answers that are not only contextually appropriate but also anchored in verifiable facts, fostering greater trust and utility in AI.  

> 总之，检索增强生成（RAG）模式在推动 AI 更博学、更可靠方面是一次重要跃迁。通过在生成流程中无缝整合外部知识检索步骤，RAG 回应了独立 LLM 的部分核心局限。嵌入与语义相似度等基础概念，结合关键词与混合检索等技术，使系统能智能找到相关信息；再通过策略性分块使这一切可管理。整个检索过程由专为大规模存储与高效查询数百万嵌入而设计的向量数据库驱动。尽管碎片化或矛盾信息的检索挑战仍在，RAG 使 LLM 能产出既贴合语境又锚定可验证事实的回答，增强对 AI 的信任与实用价值。

### Graph RAG

GraphRAG is an advanced form of Retrieval-Augmented Generation that utilizes a knowledge graph instead of a simple vector database for information retrieval. It answers complex queries by navigating the explicit relationships (edges) between data entities (nodes) within this structured knowledge base. A key advantage is its ability to synthesize answers from information fragmented across multiple documents, a common failing of traditional RAG. By understanding these connections, GraphRAG provides more contextually accurate and nuanced responses.

> GraphRAG 是检索增强生成的一种高级形态：用知识图谱而非简单向量库做信息检索。它在结构化知识库中沿实体（节点）之间的显式关系（边）导航，以回答复杂查询。一大优势是能综合分散在多份文档中的信息——这正是传统 RAG 的常见短板。理解这些连接后，GraphRAG 可提供更准确、更细致的语境化回答。

Use cases include complex financial analysis, connecting companies to market events, and scientific research for discovering relationships between genes and diseases. The primary drawback, however, is the significant complexity, cost, and expertise required to build and maintain a high-quality knowledge graph. This setup is also less flexible and can introduce higher latency compared to simpler vector search systems. The system's effectiveness is entirely dependent on the quality and completeness of the underlying graph structure. Consequently, GraphRAG offers superior contextual reasoning for intricate questions but at a much higher implementation and maintenance cost. In summary, it excels where deep, interconnected insights are more critical than the speed and simplicity of standard RAG.

> 用例包括复杂金融分析（连接公司与市场事件）、科学研究（发现基因与疾病关系）等。主要缺点则是构建与维护高质量知识图谱需要大量复杂度、成本与专业能力；相较简单向量搜索，灵活性更低、延迟可能更高。系统效果完全依赖底层图结构的质量与完整性。因此 GraphRAG 在复杂问题上语境推理更强，但实施与维护成本高得多。简言之：在深度互联洞见比标准 RAG 的速度与简洁更重要时，它表现突出。

### Agentic RAG

An evolution of this pattern, known as **Agentic RAG** (see Fig.2), introduces a reasoning and decision-making layer to significantly enhance the reliability of information extraction. Instead of just retrieving and augmenting, an "agent"—a specialized AI component—acts as a critical gatekeeper and refiner of knowledge. Rather than passively accepting the initially retrieved data, this agent actively interrogates its quality, relevance, and completeness, as illustrated by the following scenarios.

> 该模式的一种演进称为 **Agentic RAG**（见图 2）：引入推理与决策层，以显著提升信息抽取的可靠性。除检索与增强外，「智能体」——专门的 AI 组件——充当知识的把关者与精炼者。它不被动接受初次检索结果，而是主动审视其质量、相关性与完整性，以下场景可说明这一点。

First, an agent excels at reflection and source validation. If a user asks, "What is our company's policy on remote work?" a standard RAG might pull up a 2020 blog post alongside the official 2025 policy document. The agent, however, would analyze the documents' metadata, recognize the 2025 policy as the most current and authoritative source, and discard the outdated blog post before sending the correct context to the LLM for a precise answer.

> 首先，智能体擅长反思与来源校验。若用户问：「我们公司远程办公政策是什么？」标准 RAG 可能同时拉出 2020 年博文与 2025 年正式政策。智能体则会分析文档元数据，认定 2025 政策为最新权威来源，丢弃过时博文，再将正确语境交给 LLM 以给出精确回答。

![Agentic RAG Introduces Reasoning Agent](../assets-new/Agentic_RAG_Introduces_Reasoning_Agent.png)

Fig.2: Agentic RAG introduces a reasoning agent that actively evaluates, reconciles, and refines retrieved information to ensure a more accurate and trustworthy final response.

> 图 2：Agentic RAG 引入推理智能体，主动评估、协调并精炼检索信息，以确保最终回应更准确、更可信。

Second, an agent is adept at reconciling knowledge conflicts. Imagine a financial analyst asks, "What was Project Alpha's Q1 budget?" The system retrieves two documents: an initial proposal stating a €50,000 budget and a finalized financial report listing it as €65,000. An Agentic RAG would identify this contradiction, prioritize the financial report as the more reliable source, and provide the LLM with the verified figure, ensuring the final answer is based on the most accurate data.

> 其次，智能体善于调和知识冲突。假设金融分析师问：「Alpha 项目 Q1 预算是多少？」系统检索到两份文档：初稿写 5 万欧元，已定稿财务报告写 6.5 万欧元。Agentic RAG 会识别矛盾，将财务报告视为更可靠来源，向 LLM 提供已核实数字，使最终答案基于最准确数据。

Third, an agent can perform multi-step reasoning to synthesize complex answers. If a user asks, "How do our product's features and pricing compare to Competitor X's?" the agent would decompose this into separate sub-queries. It would initiate distinct searches for its own product's features, its pricing, Competitor X's features, and Competitor X's pricing. After gathering these individual pieces of information, the agent would synthesize them into a structured, comparative context before feeding it to the LLM, enabling a comprehensive response that a simple retrieval could not have produced.

> 第三，智能体可进行多步推理以综合复杂答案。若用户问：「我们产品的功能与定价与 X 竞品相比如何？」智能体会将其拆成多个子查询，分别检索本产品功能、定价、X 的功能与定价；收集各片段后，先综合为结构化对比语境再交给 LLM，从而得到简单检索无法给出的全面回答。

Fourth, an agent can identify knowledge gaps and use external tools. Suppose a user asks, "What was the market's immediate reaction to our new product launched yesterday?" The agent searches the internal knowledge base, which is updated weekly, and finds no relevant information. Recognizing this gap, it can then activate a tool—such as a live web-search API—to find recent news articles and social media sentiment. The agent then uses this freshly gathered external information to provide an up-to-the-minute answer, overcoming the limitations of its static internal database.

> 第四，智能体能识别知识缺口并调用外部工具。假设用户问：「我们昨天上市的新品，市场即时反应如何？」智能体检索每周更新的内部知识库却无所获；识别缺口后，可启用工具（如实时联网搜索 API）查找最新新闻与社媒情绪，再用这些外部信息给出即时回答，克服静态内部库的局限。

### Challenges of Agentic RAG

While powerful, the agentic layer introduces its own set of challenges. The primary drawback is a significant increase in complexity and cost. Designing, implementing, and maintaining the agent's decision-making logic and tool integrations requires substantial engineering effort and adds to computational expenses. This complexity can also lead to increased latency, as the agent's cycles of reflection, tool use, and multi-step reasoning take more time than a standard, direct retrieval process. Furthermore, the agent itself can become a new source of error; a flawed reasoning process could cause it to get stuck in useless loops, misinterpret a task, or improperly discard relevant information, ultimately degrading the quality of the final response.

> 尽管强大，智能体层也带来自身挑战。主要缺点是复杂度与成本显著上升：设计、实现与维护智能体的决策逻辑与工具集成需要大量工程投入，并增加计算开销。复杂度也可能提高延迟，因为反思、工具使用与多步推理的循环比标准直连检索更耗时。此外，智能体本身可能成为新的误差源：有缺陷的推理可能使其陷入无效循环、误解任务或错误丢弃相关信息，最终损害回应质量。

### In Summary

Agentic RAG represents a sophisticated evolution of the standard retrieval pattern, transforming it from a passive data pipeline into an active, problem-solving framework. By embedding a reasoning layer that can evaluate sources, reconcile conflicts, decompose complex questions, and use external tools, agents dramatically improve the reliability and depth of the generated answers. This advancement makes the AI more trustworthy and capable, though it comes with important trade-offs in system complexity, latency, and cost that must be carefully managed.

> 总之，Agentic RAG 是标准检索模式的精密演进，将其从被动数据管道转变为主动问题解决框架。嵌入可评估来源、调和冲突、分解复杂问题并使用外部工具的推理层后，智能体显著提升了生成回答的可靠性与深度。这使 AI 更可信、更强，但也在系统复杂度、延迟与成本上带来必须审慎权衡的代价。

## Practical Applications & Use Cases

Knowledge Retrieval (RAG) is changing how Large Language Models (LLMs) are utilized across various industries, enhancing their ability to provide more accurate and contextually relevant responses.

> 知识检索（RAG）正在改变各行业使用大语言模型（LLM）的方式，增强其提供更准确、更贴合语境回应的能力。

Applications include:

> 应用包括：

* **Enterprise Search and Q\&A:** Organizations can develop internal chatbots that respond to employee inquiries using internal documentation such as HR policies, technical manuals, and product specifications. The RAG system extracts relevant sections from these documents to inform the LLM's response.  
* **Customer Support and Helpdesks:** RAG-based systems can offer precise and consistent responses to customer queries by accessing information from product manuals, frequently asked questions (FAQs), and support tickets. This can reduce the need for direct human intervention for routine issues.  
* **Personalized Content Recommendation:** Instead of basic keyword matching, RAG can identify and retrieve content (articles, products) that is semantically related to a user's preferences or previous interactions, leading to more relevant recommendations.  
* **News and Current Events Summarization:** LLMs can be integrated with real-time news feeds. When prompted about a current event, the RAG system retrieves recent articles, allowing the LLM to produce an up-to-date summary.

> * **企业搜索与问答：** 组织可开发内部聊天机器人，基于 HR 政策、技术手册、产品规格等内部文档回答员工问询；RAG 从这些文档中提取相关段落以支撑 LLM 回应。  
> * **客户支持与工单：** 基于 RAG 的系统可通过产品手册、常见问题（FAQ）、工单等提供精确、一致的客户答复，减少对常规问题的人工介入。  
> * **个性化内容推荐：** 超越简单关键词匹配，RAG 可检索与用户偏好或历史交互语义相关的内容（文章、商品等），使推荐更相关。  
> * **新闻与时事摘要：** LLM 可与实时新闻源集成；被问及当前事件时，RAG 检索近期文章，使 LLM 能生成与时俱进的摘要。

By incorporating external knowledge, RAG extends the capabilities of LLMs beyond simple communication to function as knowledge processing systems.

> 通过纳入外部知识，RAG 将 LLM 的能力从简单沟通扩展到作为知识处理系统运作。

## Hands-On Code Example (ADK)

To illustrate the Knowledge Retrieval (RAG) pattern,  let's see three examples.

> 为说明知识检索（RAG）模式，下面看三个示例。

First, is how to use Google Search to do RAG and ground LLMs to search results. Since RAG involves accessing external information, the Google Search tool is a direct example of a built-in retrieval mechanism that can augment an LLM's knowledge.

> 首先是如何用 Google 搜索做 RAG，并将 LLM 锚定在搜索结果上。由于 RAG 涉及访问外部信息，Google 搜索工具是直接的内置检索机制示例，可用于增强 LLM 知识。

```python
from google.adk.tools import google_search
from google.adk.agents import Agent


search_agent = Agent(
    name="research_assistant",
    model="gemini-2.0-flash-exp",
    instruction="You help users research topics. When asked, use the Google Search tool",
    tools=[google_search],
)
```

Second, this section explains how to utilize Vertex AI RAG capabilities within the Google ADK. The code provided demonstrates the initialization of VertexAiRagMemoryService from the ADK. This allows for establishing a connection to a Google Cloud Vertex AI RAG Corpus. The service is configured by specifying the corpus resource name and optional parameters such as `SIMILARITY_TOP_K` and `VECTOR_DISTANCE_THRESHOLD`. These parameters influence the retrieval process. `SIMILARITY_TOP_K` defines the number of top similar results to be retrieved. `VECTOR_DISTANCE_THRESHOLD` sets a limit on the semantic distance for the retrieved results. This setup enables agents to perform scalable and persistent semantic knowledge retrieval from the designated RAG Corpus. The process effectively integrates Google Cloud's RAG functionalities into an ADK agent, thereby supporting the development of responses grounded in factual data.

> 其次说明如何在 Google ADK 中使用 Vertex AI RAG 能力。代码演示了从 ADK 初始化 `VertexAiRagMemoryService`，从而连接到 Google Cloud 上的 Vertex AI RAG 语料库。通过指定语料资源名以及可选参数（如 `SIMILARITY_TOP_K` 与 `VECTOR_DISTANCE_THRESHOLD`）配置服务；这些参数影响检索过程。`SIMILARITY_TOP_K` 定义返回的最相似结果条数上限；`VECTOR_DISTANCE_THRESHOLD` 对检索结果的语义距离设限。该配置使智能体能从指定 RAG 语料库进行可扩展、持久化的语义知识检索，将 Google Cloud 的 RAG 能力接入 ADK 智能体，支持基于事实数据的回应开发。

```python
# Import the necessary VertexAiRagMemoryService class from the google.adk.memory module.
from google.adk.memory import VertexAiRagMemoryService


RAG_CORPUS_RESOURCE_NAME = "projects/your-gcp-project-id/locations/us-central1/ragCorpora/your-corpus-id"

# Define an optional parameter for the number of top similar results to retrieve.
# This controls how many relevant document chunks the RAG service will return.
SIMILARITY_TOP_K = 5

# Define an optional parameter for the vector distance threshold.
# This threshold determines the maximum semantic distance allowed for retrieved results;
# results with a distance greater than this value might be filtered out.
VECTOR_DISTANCE_THRESHOLD = 0.7

# Initialize an instance of VertexAiRagMemoryService.
# This sets up the connection to your Vertex AI RAG Corpus.
# - rag_corpus: Specifies the unique identifier for your RAG Corpus.
# - similarity_top_k: Sets the maximum number of similar results to fetch.
# - vector_distance_threshold: Defines the similarity threshold for filtering results.
memory_service = VertexAiRagMemoryService(
    rag_corpus=RAG_CORPUS_RESOURCE_NAME,
    similarity_top_k=SIMILARITY_TOP_K,
    vector_distance_threshold=VECTOR_DISTANCE_THRESHOLD,
)
```

## Hands-On Code Example (LangChain)

Third, let's walk through a complete example using LangChain.

> 第三，用 LangChain 走一遍完整示例。

```python
import os
import requests
from typing import List, Dict, Any, TypedDict

from langchain_community.document_loaders import TextLoader
from langchain_core.documents import Document
from langchain_core.prompts import ChatPromptTemplate
from langchain_core.output_parsers import StrOutputParser
from langchain_community.embeddings import OpenAIEmbeddings
from langchain_community.vectorstores import Weaviate
from langchain_openai import ChatOpenAI
from langchain.text_splitter import CharacterTextSplitter
from langchain.schema.runnable import RunnablePassthrough
from langgraph.graph import StateGraph, END

import weaviate
from weaviate.embedded import EmbeddedOptions
import dotenv


# Load environment variables (e.g., OPENAI_API_KEY)
dotenv.load_dotenv()

# Set your OpenAI API key (ensure it's loaded from .env or set here)
# os.environ["OPENAI_API_KEY"] = "YOUR_OPENAI_API_KEY"


# --- 1. Data Preparation (Preprocessing) ---

# Load data
url = "https://github.com/langchain-ai/langchain/blob/master/docs/docs/how_to/state_of_the_union.txt"
res = requests.get(url)
with open("state_of_the_union.txt", "w") as f:
    f.write(res.text)

loader = TextLoader("./state_of_the_union.txt")
documents = loader.load()

# Chunk documents
text_splitter = CharacterTextSplitter(chunk_size=500, chunk_overlap=50)
chunks = text_splitter.split_documents(documents)

# Embed and store chunks in Weaviate
client = weaviate.Client(embedded_options=EmbeddedOptions())

vectorstore = Weaviate.from_documents(
    client=client,
    documents=chunks,
    embedding=OpenAIEmbeddings(),
    by_text=False,
)

# Define the retriever
retriever = vectorstore.as_retriever()

# Initialize LLM
llm = ChatOpenAI(model_name="gpt-3.5-turbo", temperature=0)


# --- 2. Define the State for LangGraph ---
class RAGGraphState(TypedDict):
    question: str
    documents: List[Document]
    generation: str


# --- 3. Define the Nodes (Functions) ---
def retrieve_documents_node(state: RAGGraphState) -> RAGGraphState:
    """Retrieves documents based on the user's question."""
    question = state["question"]
    documents = retriever.invoke(question)
    return {"documents": documents, "question": question, "generation": ""}


def generate_response_node(state: RAGGraphState) -> RAGGraphState:
    """Generates a response using the LLM based on retrieved documents."""
    question = state["question"]
    documents = state["documents"]

    # Prompt template from the PDF
    template = """You are an assistant for question-answering tasks. Use the following pieces of retrieved context to answer the question. If you don't know the answer, just say that you don't know. Use three sentences maximum and keep the answer concise.
Question: {question}
Context: {context}
Answer: """
    prompt = ChatPromptTemplate.from_template(template)

    # Format the context from the documents
    context = "\n\n".join([doc.page_content for doc in documents])

    # Create the RAG chain
    rag_chain = prompt | llm | StrOutputParser()

    # Invoke the chain
    generation = rag_chain.invoke({"context": context, "question": question})

    return {"question": question, "documents": documents, "generation": generation}


# --- 4. Build the LangGraph Graph ---
workflow = StateGraph(RAGGraphState)

# Add nodes
workflow.add_node("retrieve", retrieve_documents_node)
workflow.add_node("generate", generate_response_node)

# Set the entry point
workflow.set_entry_point("retrieve")

# Add edges (transitions)
workflow.add_edge("retrieve", "generate")
workflow.add_edge("generate", END)

# Compile the graph
app = workflow.compile()


# --- 5. Run the RAG Application ---
if __name__ == "__main__":
    print("\n--- Running RAG Query ---")
    query = "What did the president say about Justice Breyer"
    inputs = {"question": query}
    for s in app.stream(inputs):
        print(s)

    print("\n--- Running another RAG Query ---")
    query_2 = "What did the president say about the economy?"
    inputs_2 = {"question": query_2}
    for s in app.stream(inputs_2):
        print(s)
```

This Python code illustrates a Retrieval-Augmented Generation (RAG) pipeline implemented with LangChain and LangGraph. The process begins with the creation of a knowledge base derived from a text document, which is segmented into chunks and transformed into embeddings. These embeddings are then stored in a Weaviate vector store, facilitating efficient information retrieval. A StateGraph in LangGraph is utilized to manage the workflow between two key functions: `retrieve_documents_node` and `generate_response_node`. The `retrieve_documents_node` function queries the vector store to identify relevant document chunks based on the user's input. Subsequently, the `generate_response_node` function utilizes the retrieved information and a predefined prompt template to produce a response using an OpenAI Large Language Model (LLM). The `app.stream` method allows the execution of queries through the RAG pipeline, demonstrating the system's capacity to generate contextually relevant outputs.

> 该 Python 代码展示了用 LangChain 与 LangGraph 实现的检索增强生成（RAG）流水线。流程从基于文本文档构建知识库开始：文档被切分为块并转为嵌入，嵌入存入 Weaviate 向量库以支持高效检索。LangGraph 中的 `StateGraph` 用于管理 `retrieve_documents_node` 与 `generate_response_node` 之间的工作流。`retrieve_documents_node` 根据用户输入查询向量库以找到相关文档块；随后 `generate_response_node` 结合检索结果与预定义提示模板，用 OpenAI 大语言模型生成回应。`app.stream` 方法支持经 RAG 流水线执行查询，展示系统生成语境相关输出的能力。

## At Glance

**What:** LLMs possess impressive text generation abilities but are fundamentally limited by their training data. This knowledge is static, meaning it doesn't include real-time information or private, domain-specific data. Consequently, their responses can be outdated, inaccurate, or lack the specific context required for specialized tasks. This gap restricts their reliability for applications demanding current and factual answers.

> **是什么：** LLM 文本生成能力令人印象深刻，但根本上受训练数据限制。知识是静态的，不包含实时信息或私有、领域专属数据，因此回应可能过时、不准确，或缺乏专业任务所需的特定语境，从而限制其在需要最新、事实性答案的应用中的可靠性。

**Why:** The Retrieval-Augmented Generation (RAG) pattern provides a standardized solution by connecting LLMs to external knowledge sources. When a query is received, the system first retrieves relevant information snippets from a specified knowledge base. These snippets are then appended to the original prompt, enriching it with timely and specific context. This augmented prompt is then sent to the LLM, enabling it to generate a response that is accurate, verifiable, and grounded in external data. This process effectively transforms the LLM from a closed-book reasoner into an open-book one, significantly enhancing its utility and trustworthiness.

> **为什么：** 检索增强生成（RAG）模式通过将 LLM 与外部知识源连接，提供标准化方案。收到查询后，系统先从指定知识库检索相关片段，再将其附加到原始提示上，以时效性与具体语境丰富提示。增强后的提示再发给 LLM，使其能生成准确、可核验、锚定外部数据的回应。这一过程将 LLM 从「闭卷推理者」变为「开卷推理者」，显著提升实用性与可信度。

**Rule of Thumb:** Use this pattern when you need an LLM to answer questions or generate content based on specific, up-to-date, or proprietary information that was not part of its original training data. It is ideal for building Q\&A systems over internal documents, customer support bots, and applications requiring verifiable, fact-based responses with citations.

> **经验法则：** 当需要 LLM 基于特定、最新或专有信息（未包含在其原始训练中）回答问题或生成内容时使用该模式。适用于基于内部文档的问答系统、客户支持机器人，以及需要可核验、基于事实并带引用的应用。

**Visual Summary:**

> **可视化摘要：**

![Knowledge Retrieval Pattern Database](../assets-new/Knowledge_Retrieval_Pattern_Database.png)

Knowledge Retrieval pattern: an AI agent to query and retrieve information from structured databases

> 知识检索模式：AI 智能体从结构化数据库中查询并检索信息

![Knowledge Retrieval Pattern Search](../assets-new/Knowledge_Retrieval_Pattern_Search.png)

Fig. 3: Knowledge Retrieval pattern: an AI agent to find and synthesize information from the public internet in response to user queries.

> 图 3：知识检索模式：AI 智能体应用户查询从公共互联网查找并综合信息

## Key Takeaways

* Knowledge Retrieval (RAG) enhances LLMs by allowing them to access external, up-to-date, and specific information.  
* The process involves Retrieval (searching a knowledge base for relevant snippets) and Augmentation (adding these snippets to the LLM's prompt).  
* RAG helps LLMs overcome limitations like outdated training data, reduces "hallucinations," and enables domain-specific knowledge integration.  
* RAG allows for attributable answers, as the LLM's response is grounded in retrieved sources.  
* GraphRAG leverages a knowledge graph to understand the relationships between different pieces of information, allowing it to answer complex questions that require synthesizing data from multiple sources.  
* Agentic RAG moves beyond simple information retrieval by using an intelligent agent to actively reason about, validate, and refine external knowledge, ensuring a more accurate and reliable answer.  
* Practical applications span enterprise search, customer support, legal research, and personalized recommendations.

> * 知识检索（RAG）通过让 LLM 访问外部的、最新的、具体的信息来增强其能力。  
> * 流程包括检索（在知识库中搜索相关片段）与增强（将这些片段加入 LLM 提示）。  
> * RAG 帮助 LLM 克服训练数据过时等局限，减少「幻觉」，并整合领域知识。  
> * RAG 支持可归因的回答，因为回应锚定在检索来源上。  
> * GraphRAG 利用知识图谱理解信息之间的关系，从而回答需要综合多源数据的复杂问题。  
> * Agentic RAG 超越简单检索：用智能体主动推理、校验并精炼外部知识，使回答更准确可靠。  
> * 实际应用涵盖企业搜索、客户支持、法律研究与个性化推荐等。

## Conclusion

In conclusion, Retrieval-Augmented Generation (RAG) addresses the core limitation of a Large Language Model's static knowledge by connecting it to external, up-to-date data sources. The process works by first retrieving relevant information snippets and then augmenting the user's prompt, enabling the LLM to generate more accurate and contextually aware responses. This is made possible by foundational technologies like embeddings, semantic search, and vector databases, which find information based on meaning rather than just keywords. By grounding outputs in verifiable data, RAG significantly reduces factual errors and allows for the use of proprietary information, enhancing trust through citations.

> 总之，检索增强生成（RAG）通过将大语言模型的静态知识与外部、最新数据源相连，应对其核心局限。流程先检索相关片段，再增强用户提示，使 LLM 能生成更准确、更具语境意识的回应。嵌入、语义搜索与向量数据库等基础技术使系统能按含义而非仅按关键词找信息。将输出锚定在可核验数据上，RAG 显著减少事实性错误，并支持使用专有信息，通过引用增强信任。

An advanced evolution, Agentic RAG, introduces a reasoning layer that actively validates, reconciles, and synthesizes retrieved knowledge for even greater reliability. Similarly, specialized approaches like GraphRAG leverage knowledge graphs to navigate explicit data relationships, allowing the system to synthesize answers to highly complex, interconnected queries. This agent can resolve conflicting information, perform multi-step queries, and use external tools to find missing data. While these advanced methods add complexity and latency, they drastically improve the depth and trustworthiness of the final response. Practical applications for these patterns are already transforming industries, from enterprise search and customer support to personalized content delivery. Despite the challenges, RAG is a crucial pattern for making AI more knowledgeable, reliable, and useful. Ultimately, it transforms LLMs from closed-book conversationalists into powerful, open-book reasoning tools.

> 高级演进 Agentic RAG 引入推理层，主动校验、协调并综合检索知识，进一步提升可靠性。同样，GraphRAG 等专门方法利用知识图谱导航显式数据关系，使系统能综合回答高度复杂、相互关联的查询。智能体可消解冲突信息、执行多步查询并用外部工具补全缺失数据。这些方法虽增加复杂度与延迟，却能大幅提升最终回应的深度与可信度。这些模式的实际应用已在改变各行业，从企业搜索、客户支持到个性化内容分发。尽管仍有挑战，RAG 仍是使 AI 更博学、可靠、实用的关键模式；最终它将 LLM 从闭卷对话者转变为强大的开卷推理工具。

## References

> 参考文献：以下条目保留英文与原始链接，不作逐条翻译。

1. Lewis, P., et al. (2020). *Retrieval-Augmented Generation for Knowledge-Intensive NLP Tasks*. [https://arxiv.org/abs/2005.11401](https://arxiv.org/abs/2005.11401)
2. Google AI for Developers Documentation.  *Retrieval Augmented Generation - [https://cloud.google.com/vertex-ai/generative-ai/docs/rag-engine/rag-overview](https://cloud.google.com/vertex-ai/generative-ai/docs/rag-engine/rag-overview)*
3. Retrieval-Augmented Generation with Graphs (GraphRAG), [https://arxiv.org/abs/2501.00309](https://arxiv.org/abs/2501.00309)
4. LangChain and LangGraph: Leonie Monigatti, "Retrieval-Augmented Generation (RAG): From Theory to LangChain Implementation,"  [*https://medium.com/data-science/retrieval-augmented-generation-rag-from-theory-to-langchain-implementation-4e9bd5f6a4f2*](https://medium.com/data-science/retrieval-augmented-generation-rag-from-theory-to-langchain-implementation-4e9bd5f6a4f2)
5. Google Cloud Vertex AI RAG Corpus [*https://cloud.google.com/vertex-ai/generative-ai/docs/rag-engine/manage-your-rag-corpus#corpus-management*](https://cloud.google.com/vertex-ai/generative-ai/docs/rag-engine/manage-your-rag-corpus#corpus-management)
