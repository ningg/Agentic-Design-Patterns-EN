# Chapter 14: Knowledge Retrieval (RAG)

LLMs exhibit substantial capabilities in generating human-like text. However, their knowledge base is typically confined to the data on which they were trained, limiting their access to real-time information, specific company data, or highly specialized details. Knowledge Retrieval (RAG, or  Retrieval Augmented Generation), addresses this limitation. RAG enables LLMs to access and integrate external, current, and context-specific information, thereby enhancing the accuracy, relevance, and factual basis of their outputs.

> 大语言模型写起「像人说的话」来很强，但知识边界基本锁在训练语料里，难以及时拿到最新情报、内部资料或极专领域细节。检索增强生成（RAG，Retrieval Augmented Generation）正是为补上这块短板：让 LLM 在作答前拉取外部、时效强、与当下语境相关的材料，再把回答锚在可查证的依据上，提升准确性与相关性。

For AI agents, this is crucial as it allows them to ground their actions and responses in real-time, verifiable data beyond their static training. This capability enables them to perform complex tasks accurately, such as accessing the latest company policies to answer a specific question or checking current inventory before placing an order. By integrating external knowledge, RAG transforms agents from simple conversationalists into effective, data-driven tools capable of executing meaningful work.

> 对智能体来说，这一点尤其关键：行动与答复要能站在「可核验、可更新」的数据之上，而不是只靠静态权重里的模糊记忆。于是它们能更稳地干复杂活——比如按最新制度答员工问、下单前对一下实时库存。RAG 把外部知识接进来，智能体就从「会聊」进阶为「能办事」的数据驱动助手。

## Knowledge Retrieval (RAG) Pattern Overview

The Knowledge Retrieval (RAG) pattern significantly enhances the capabilities of LLMs by granting them access to external knowledge bases before generating a response. Instead of relying solely on their internal, pre-trained knowledge, RAG allows LLMs to "look up" information, much like a human might consult a book or search the internet. This process empowers LLMs to provide more accurate, up-to-date, and verifiable answers.

> 「知识检索（RAG）」在模型开口前先让它访问外部知识库，能力边界因此被整体抬高。模型不必只靠预训练权重里的「闭卷记忆」，还能像人查资料一样「翻库」，从而给出更贴题、更新、且便于核对出处的答案。

When a user poses a question or gives a prompt to an AI system using RAG, the query isn't sent directly to the LLM. Instead, the system first scours a vast external knowledge base—a highly organized library of documents, databases, or web pages—for relevant information. This search is not a simple keyword match; it's a "semantic search" that understands the user's intent and the meaning behind their words. This initial search pulls out the most pertinent snippets or "chunks" of information. These extracted pieces are then "augmented," or added, to the original prompt, creating a richer, more informed query. Finally, this enhanced prompt is sent to the LLM. With this additional context, the LLM can generate a response that is not only fluent and natural but also factually grounded in the retrieved data.

> 用户把问题丢给带 RAG 的系统时，请求不会裸送进 LLM。流水线会先在庞大的外部语料——规整好的文档库、业务库或网页索引——里找相关内容；这里用的往往不是纯关键词命中，而是吃透意图的语义检索。系统捞出最相关的若干文本「块」（chunk），把它们拼回原始提示里做上下文增强，再把这份「加料」提示交给模型。多了一层可引用的证据，回答既顺口，也更不容易飘在空泛训练记忆上。

The RAG framework provides several significant benefits. It allows LLMs to access up-to-date information, thereby overcoming the constraints of their static training data. This approach also reduces the risk of "hallucination"—the generation of false information—by grounding responses in verifiable data. Moreover, LLMs can utilize specialized knowledge found in internal company documents or wikis. A vital advantage of this process is the capability to offer "citations," which pinpoint the exact source of information, thereby enhancing the trustworthiness and verifiability of the AI's responses..

> RAG 带来的好处很实在：模型能吃到训练截止之后的新事实；把答案拴在检索片段上，可明显压低胡编概率；还能接入内网 wiki、制度库这类私域知识。另一个加分项是「可引用」——段落级溯源让读者自己点回去验，可信度与可审计性一起上来。

To fully appreciate how RAG functions, it's essential to understand a few core concepts (see Fig.1):

> 想搞懂 RAG 怎么转起来，先抓住下面几块拼图（见图 1）：

### Embeddings

In the context of LLMs, embeddings are numerical representations of text, such as words, phrases, or entire documents. These representations are in the form of a vector, which is a list of numbers. The key idea is to capture the semantic meaning and the relationships between different pieces of text in a mathematical space. Words or phrases with similar meanings will have embeddings that are closer to each other in this vector space. For instance, imagine a simple 2D graph. The word "cat" might be represented by the coordinates (2, 3), while "kitten" would be very close at (2.1, 3.1). In contrast, the word "car" would have a distant coordinate like (8, 1), reflecting its different meaning. In reality, these embeddings are in a much higher-dimensional space with hundreds or even thousands of dimensions, allowing for a very nuanced understanding of language.

> 在 LLM 体系里，嵌入（embedding）就是把词、句、篇文本压成一串数字——也就是向量——好让机器在几何空间里「比划」语义远近：意思像的，向量就挨得近。教材里爱用二维举例：「cat」可能在 (2,3)，「kitten」贴着 (2.1,3.1)，而「car」跑到 (8,1) 一类远角。真系统里维度动辄几百上千，才能装下细颗粒度的语义差别。

### Text Similarity

Text similarity refers to the measure of how alike two pieces of text are. This can be at a surface level, looking at the overlap of words (lexical similarity), or at a deeper, meaning-based level. In the context of RAG, text similarity is crucial for finding the most relevant information in the knowledge base that corresponds to a user's query. For instance, consider the sentences: "What is the capital of France?" and "Which city is the capital of France?". While the wording is different, they are asking the same question. A good text similarity model would recognize this and assign a high similarity score to these two sentences, even though they only share a few words. This is often calculated using the embeddings of the texts.

> 文本相似度问的是「两段话有多像」：可以看成词面重合（词汇相似），也可以看成语义是否同一题。RAG 检索吃的就是这一层——要在库里捞出和用户问题最对路的片段。比如 *What is the capital of France?* 与 *Which city is the capital of France?* 字面差不少，好模型仍会给高分；实务上多半用双方 embedding 的距离/相似度来算。

### Semantic Similarity and Distance

Semantic similarity is a more advanced form of text similarity that focuses purely on the meaning and context of the text, rather than just the words used. It aims to understand if two pieces of text convey the same concept or idea. Semantic distance is the inverse of this; a high semantic similarity implies a low semantic distance, and vice versa. In RAG, semantic search relies on finding documents with the smallest semantic distance to the user's query. For instance, the phrases "a furry feline companion" and "a domestic cat" have no words in common besides "a". However, a model that understands semantic similarity would recognize that they refer to the same thing and would consider them to be highly similar. This is because their embeddings would be very close in the vector space, indicating a small semantic distance. This is the "smart search" that allows RAG to find relevant information even when the user's wording doesn't exactly match the text in the knowledge base.

> 语义相似度再往前走一步：比的是「说的是不是一回事」，而不是「有没有同款词」。语义距离是它的反面——越像，距离越小。RAG 里的向量检索，本质上就是在找与 query embedding 最近的文档块。像 *a furry feline companion* 与 *a domestic cat* 几乎不共享实词，但语义模型会把它们钉在邻近向量上。靠这种「懂意思的搜索」，用户换种说法也能捞到库里的相关段落。

![RAG Core Concept: Chunking, Embeddings, and Vector Database](../assets-new/RAG_Core_Concepts_Chunking_Embeddings_and_Vector_Database.png)

Fig.1: RAG Core Concepts: Chunking, Embeddings, and Vector Database

> 图 1：RAG 核心概念——分块、嵌入与向量数据库

### Chunking of Documents

Chunking is the process of breaking down large documents into smaller, more manageable pieces, or "chunks." For a RAG system to work efficiently, it cannot feed entire large documents into the LLM. Instead, it processes these smaller chunks. The way documents are chunked is important for preserving the context and meaning of the information. For instance, instead of treating a 50-page user manual as a single block of text, a chunking strategy might break it down into sections, paragraphs, or even sentences. For instance, a section on "Troubleshooting" would be a separate chunk from the "Installation Guide." When a user asks a question about a specific problem, the RAG system can then retrieve the most relevant troubleshooting chunk, rather than the entire manual. This makes the retrieval process faster and the information provided to the LLM more focused and relevant to the user's immediate need. Once documents are chunked, the RAG system must employ a retrieval technique to find the most relevant pieces for a given query. The primary method is vector search, which uses embeddings and semantic distance to find chunks that are conceptually similar to the user's question. An older, but still valuable, technique is BM25, a keyword-based algorithm that ranks chunks based on term frequency without understanding semantic meaning. To get the best of both worlds, hybrid search approaches are often used, combining the keyword precision of BM25 with the contextual understanding of semantic search. This fusion allows for more robust and accurate retrieval, capturing both literal matches and conceptual relevance.

> 分块（chunking）就是把长文档切成小块再入库——整本 50 页手册若当一块塞给模型，又贵又容易噪声爆表，按章节/段落甚至句子切开，「安装」与「排障」各归各的桶，用户问具体故障时只捞排障段，又快又准。块建好以后，检索主路径通常是向量搜索：用 embedding 找与用户问题语义最近的片段；BM25 这类词频排序的老办法仍有用，尤其在专有名词、型号字面命中上。实务里常见「向量 + BM25」混合，兼顾字面咬死与语义泛化。

### Vector Databases

A vector database is a specialized type of database designed to store and query embeddings efficiently. After documents are chunked and converted into embeddings, these high-dimensional vectors are stored in a vector database. Traditional retrieval techniques, like keyword-based search, are excellent at finding documents containing exact words from a query but lack a deep understanding of language. They wouldn't recognize that "furry feline companion" means "cat." This is where vector databases excel. They are built specifically for semantic search. By storing text as numerical vectors, they can find results based on conceptual meaning, not just keyword overlap. When a user's query is also converted into a vector, the database uses highly optimized algorithms (like HNSW \- Hierarchical Navigable Small World) to rapidly search through millions of vectors and find the ones that are "closest" in meaning. This approach is far superior for RAG because it uncovers relevant context even if the user's phrasing is completely different from the source documents. In essence, while other techniques search for words, vector databases search for meaning. This technology is implemented in various forms, from managed databases like Pinecone and Weaviate to open-source solutions such as Chroma DB, Milvus, and Qdrant. Even existing databases can be augmented with vector search capabilities, as seen with Redis, Elasticsearch, and Postgres (using the pgvector extension). The core retrieval mechanisms are often powered by libraries like Meta AI's FAISS or Google Research's ScaNN, which are fundamental to the efficiency of these systems.

> 向量库就是为存 embedding、做近邻检索而生的。关键词检索擅长「词对词」，却难以理解 *furry feline companion* 其实在说猫；向量检索则按「意思近不近」找人。查询也向量化之后，库用 HNSW 这类索引在百万级向量里秒级捞出语义邻居——用户换说法也能撞上正确段落。一句话：传统搜字，向量搜意。落地形态从 Pinecone、Weaviate 等托管服务，到 Milvus、Qdrant、Chroma 等开源方案，再到给 Redis、ES、Postgres（pgvector）加向量能力；底层也常借 FAISS、ScaNN 等库榨性能。

### RAG's Challenges

Despite its power, the RAG pattern is not without its challenges. A primary issue arises when the information needed to answer a query is not confined to a single chunk but is spread across multiple parts of a document or even several documents. In such cases, the retriever might fail to gather all the necessary context, leading to an incomplete or inaccurate answer. The system's effectiveness is also highly dependent on the quality of the chunking and retrieval process; if irrelevant chunks are retrieved, it can introduce noise and confuse the LLM. Furthermore, effectively synthesizing information from potentially contradictory sources remains a significant hurdle for these systems.  Besides that, another challenge is that RAG requires the entire knowledge base to be pre-processed and stored in specialized databases, such as vector or graph databases, which is a considerable undertaking. Consequently, this knowledge requires periodic reconciliation to remain up-to-date, a crucial task when dealing with evolving sources like company wikis. This entire process can have a noticeable impact on performance, increasing latency, operational costs, and the number of tokens used in the final prompt.

> RAG 很强，但坑也不少：答案所需证据往往跨段、跨文档，Retriever 若只吐一两块，模型就容易答半拉子。效果还极度吃分块策略与排序质量——噪声块一多，LLM 反而被带偏。多源信息彼此打架时，如何合成仍是开放题。工程侧要先把全库切分、向量化、灌进专用存储，后续还要持续同步变更（尤其是活文档/wiki），否则知识陈旧。整条链路也会推高延迟、账单与 prompt token。

In summary,  the Retrieval-Augmented Generation (RAG) pattern represents a significant leap forward in making AI more knowledgeable and reliable. By seamlessly integrating an external knowledge retrieval step into the generation process, RAG addresses some of the core limitations of standalone LLMs. The foundational concepts of embeddings and semantic similarity, combined with retrieval techniques like keyword and hybrid search, allow the system to intelligently find relevant information, which is made manageable through strategic chunking. This entire retrieval process is powered by specialized vector databases designed to store and efficiently query millions of embeddings at scale. While challenges in retrieving fragmented or contradictory information persist, RAG empowers LLMs to produce answers that are not only contextually appropriate but also anchored in verifiable facts, fostering greater trust and utility in AI.  

> 总之，RAG 让模型从「只背训练集」进化到「边查边答」，是提升可靠性与可用性的一大步：生成前插入检索，把静态 LLM 的短板补上；embedding、语义相似度、关键词/混合检索与合理的 chunk 策略一起决定「找得准不准」；向量库则负责在规模上扛住近邻搜索。碎片化证据与矛盾来源仍是硬骨头，但把好检索与引用，回答就能既贴语境又可核对，信任感自然上去。

### Graph RAG

GraphRAG is an advanced form of Retrieval-Augmented Generation that utilizes a knowledge graph instead of a simple vector database for information retrieval. It answers complex queries by navigating the explicit relationships (edges) between data entities (nodes) within this structured knowledge base. A key advantage is its ability to synthesize answers from information fragmented across multiple documents, a common failing of traditional RAG. By understanding these connections, GraphRAG provides more contextually accurate and nuanced responses.

> GraphRAG 把「图」请进检索管线：不只量向量近邻，还在实体（节点）与关系（边）上走路由，专啃需要多跳推理的问题。传统 RAG 常输在信息碎在多篇文档里拼不起来，图结构恰好擅长把散落事实串成一张网，回答会更连贯、语境更饱满。

Use cases include complex financial analysis, connecting companies to market events, and scientific research for discovering relationships between genes and diseases. The primary drawback, however, is the significant complexity, cost, and expertise required to build and maintain a high-quality knowledge graph. This setup is also less flexible and can introduce higher latency compared to simpler vector search systems. The system's effectiveness is entirely dependent on the quality and completeness of the underlying graph structure. Consequently, GraphRAG offers superior contextual reasoning for intricate questions but at a much higher implementation and maintenance cost. In summary, it excels where deep, interconnected insights are more critical than the speed and simplicity of standard RAG.

> 典型场景如金融里把公司—事件—指标织成网，科研里挖基因—疾病—通路关联。代价是建图、对齐、增量更新都贵且吃专家；相比纯向量方案，架构更重、链路更长，效果又几乎完全绑在图的质量与覆盖率上。适合「多跳、强关系」题；若只要快糙猛的段落检索，标准 RAG 往往更划算。

### Agentic RAG

An evolution of this pattern, known as **Agentic RAG** (see Fig.2), introduces a reasoning and decision-making layer to significantly enhance the reliability of information extraction. Instead of just retrieving and augmenting, an "agent"—a specialized AI component—acts as a critical gatekeeper and refiner of knowledge. Rather than passively accepting the initially retrieved data, this agent actively interrogates its quality, relevance, and completeness, as illustrated by the following scenarios.

> **Agentic RAG**（图 2）在标准 RAG 上再叠一层「会想的」编排：不只检索+拼 prompt，还让智能体充当质检与精炼角色——主动质疑首轮召回是否够新、够准、够全，下面四个情景就是写照。

First, an agent excels at reflection and source validation. If a user asks, "What is our company's policy on remote work?" a standard RAG might pull up a 2020 blog post alongside the official 2025 policy document. The agent, however, would analyze the documents' metadata, recognize the 2025 policy as the most current and authoritative source, and discard the outdated blog post before sending the correct context to the LLM for a precise answer.

> 其一，反思与信源排序。用户问「我司远程办公政策？」朴素 RAG 可能把 2020 年旧博文和 2025 年制度一起捞上来；智能体可读元数据、版本与发布渠道，优先保留现行权威版，把过期噪音挡在模型门外。

![Agentic RAG Introduces Reasoning Agent](../assets-new/Agentic_RAG_Introduces_Reasoning_Agent.png)

Fig.2: Agentic RAG introduces a reasoning agent that actively evaluates, reconciles, and refines retrieved information to ensure a more accurate and trustworthy final response.

> 图 2：Agentic RAG 引入推理型智能体，对检索结果做评估、对齐与精炼，以提升最终答复的准确性与可信度。

Second, an agent is adept at reconciling knowledge conflicts. Imagine a financial analyst asks, "What was Project Alpha's Q1 budget?" The system retrieves two documents: an initial proposal stating a €50,000 budget and a finalized financial report listing it as €65,000. An Agentic RAG would identify this contradiction, prioritize the financial report as the more reliable source, and provide the LLM with the verified figure, ensuring the final answer is based on the most accurate data.

> 其二，冲突消解。分析师问「Alpha 项目 Q1 预算？」若一份是早期草案写 5 万欧，另一份是定稿财报写 6.5 万欧，智能体应识别矛盾、按文档类型与时间戳倾向更可信的一路，把「该信哪条」写清楚再交给模型总结。

Third, an agent can perform multi-step reasoning to synthesize complex answers. If a user asks, "How do our product's features and pricing compare to Competitor X's?" the agent would decompose this into separate sub-queries. It would initiate distinct searches for its own product's features, its pricing, Competitor X's features, and Competitor X's pricing. After gathering these individual pieces of information, the agent would synthesize them into a structured, comparative context before feeding it to the LLM, enabling a comprehensive response that a simple retrieval could not have produced.

> 其三，多步拆解再综合。对比题如「我们相对 X 竞品的功能与定价？」可拆成四次检索（我方功能/定价，对方功能/定价），智能体先把材料整理成对照表式上下文，再让模型输出结构化结论，单次向量召回往往够不着这种覆盖面。

Fourth, an agent can identify knowledge gaps and use external tools. Suppose a user asks, "What was the market's immediate reaction to our new product launched yesterday?" The agent searches the internal knowledge base, which is updated weekly, and finds no relevant information. Recognizing this gap, it can then activate a tool—such as a live web-search API—to find recent news articles and social media sentiment. The agent then uses this freshly gathered external information to provide an up-to-the-minute answer, overcoming the limitations of its static internal database.

> 其四，缺口感知与工具外延。问「昨天新品上市，市场即时反馈？」若内库一周才同步一次，智能体应意识到语料不够新，转而调用实时搜索/舆情 API 补证据，再组织答案，而不是硬编。

### Challenges of Agentic RAG

While powerful, the agentic layer introduces its own set of challenges. The primary drawback is a significant increase in complexity and cost. Designing, implementing, and maintaining the agent's decision-making logic and tool integrations requires substantial engineering effort and adds to computational expenses. This complexity can also lead to increased latency, as the agent's cycles of reflection, tool use, and multi-step reasoning take more time than a standard, direct retrieval process. Furthermore, the agent itself can become a new source of error; a flawed reasoning process could cause it to get stuck in useless loops, misinterpret a task, or improperly discard relevant information, ultimately degrading the quality of the final response.

> 智能体层并非免费午餐：决策逻辑、工具权限与失败重试都要工程化，算力与延迟通常明显高于「一检索一生成」。更糟的是，蹩脚推理会引入新故障模式——死循环、误删相关片段、读错任务——反而把答案带沟里。

### In Summary

Agentic RAG represents a sophisticated evolution of the standard retrieval pattern, transforming it from a passive data pipeline into an active, problem-solving framework. By embedding a reasoning layer that can evaluate sources, reconcile conflicts, decompose complex questions, and use external tools, agents dramatically improve the reliability and depth of the generated answers. This advancement makes the AI more trustworthy and capable, though it comes with important trade-offs in system complexity, latency, and cost that must be carefully managed.

> 小结：Agentic RAG 把流水线升级成「会规划、会质疑、会补洞」的主动系统，靠推理层做信源评估、冲突仲裁、子问题拆解与工具调用，换来更高可靠性与分析深度；代价是架构更重、时延更长、账单更厚，需要刻意治理。

## Practical Applications & Use Cases

Knowledge Retrieval (RAG) is changing how Large Language Models (LLMs) are utilized across various industries, enhancing their ability to provide more accurate and contextually relevant responses.

> RAG 正在改写各行业落地 LLM 的姿势：让回答更准、更懂当下语境，而不是泛泛背稿。

Applications include:

> 常见落点包括：

* **Enterprise Search and Q\&A:** Organizations can develop internal chatbots that respond to employee inquiries using internal documentation such as HR policies, technical manuals, and product specifications. The RAG system extracts relevant sections from these documents to inform the LLM's response.  
* **Customer Support and Helpdesks:** RAG-based systems can offer precise and consistent responses to customer queries by accessing information from product manuals, frequently asked questions (FAQs), and support tickets. This can reduce the need for direct human intervention for routine issues.  
* **Personalized Content Recommendation:** Instead of basic keyword matching, RAG can identify and retrieve content (articles, products) that is semantically related to a user's preferences or previous interactions, leading to more relevant recommendations.  
* **News and Current Events Summarization:** LLMs can be integrated with real-time news feeds. When prompted about a current event, the RAG system retrieves recent articles, allowing the LLM to produce an up-to-date summary.

> * **企业搜索 / 内部问答：** 用制度、手册、规格书喂库，员工问 HR/IT/产品问题先检索再答，减少「模型瞎编内部规章」。  
> * **客服与工单：** 手册、FAQ、历史工单入库，常见问法直接引用证据回答，降低一线重复劳动。  
> * **个性化推荐：** 不只关键词命中，可按用户兴趣 embedding 找语义相近的内容或商品。  
> * **新闻与时事：** 接实时 feed，先拉最新稿件再摘要，避免模型活在训练截止日期之前。

By incorporating external knowledge, RAG extends the capabilities of LLMs beyond simple communication to function as knowledge processing systems.

> 接上外部知识后，LLM 不只是聊天窗口，而是可审计的知识加工与分发接口。

## Hands-On Code Example (ADK)

To illustrate the Knowledge Retrieval (RAG) pattern,  let's see three examples.

> 下面用三个例子串起 RAG 从「搜」到「答」的链路。

First, is how to use Google Search to do RAG and ground LLMs to search results. Since RAG involves accessing external information, the Google Search tool is a direct example of a built-in retrieval mechanism that can augment an LLM's knowledge.

> 第一个例子用 Google 搜索当检索器，把模型输出拴在实时 SERP 上——RAG 的本质就是「先取外证，再生成」，内置搜索工具是最直观的实现之一。

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

> 第二段演示在 ADK 里接 Vertex AI RAG：`VertexAiRagMemoryService` 指向云端语料资源，`SIMILARITY_TOP_K` 控制召回条数，`VECTOR_DISTANCE_THRESHOLD` 过滤语义上太远的片段。配好即可让智能体对托管语料做持久化向量检索，把 GCP 侧的 RAG 能力嵌进 ADK 智能体流水线，方便做有证据支撑的答复。

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

> 第三个例子用 LangChain + LangGraph 把端到端 RAG 跑通。

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

> 这段 Python 把 RAG 拆成「建库 → 检索 → 生成」：`CharacterTextSplitter` 切块，`OpenAIEmbeddings` + Weaviate 落库；`StateGraph` 串起 `retrieve_documents_node`（按问题取向量近邻）与 `generate_response_node`（把上下文塞进模板再走 ChatOpenAI）。`app.stream` 便于观察多步状态，演示如何产出带检索证据的回答。

## At Glance

**What:** LLMs possess impressive text generation abilities but are fundamentally limited by their training data. This knowledge is static, meaning it doesn't include real-time information or private, domain-specific data. Consequently, their responses can be outdated, inaccurate, or lack the specific context required for specialized tasks. This gap restricts their reliability for applications demanding current and factual answers.

> **是什么：** LLM 很会写，但知识冻结在训练快照里：没有实时世界、没有你家私有库，回答就容易过期、含糊或缺领域语境，在要「最新 + 可核对」的场景里可靠性打折。

**Why:** The Retrieval-Augmented Generation (RAG) pattern provides a standardized solution by connecting LLMs to external knowledge sources. When a query is received, the system first retrieves relevant information snippets from a specified knowledge base. These snippets are then appended to the original prompt, enriching it with timely and specific context. This augmented prompt is then sent to the LLM, enabling it to generate a response that is accurate, verifiable, and grounded in external data. This process effectively transforms the LLM from a closed-book reasoner into an open-book one, significantly enhancing its utility and trustworthiness.

> **为什么：** RAG 给出一套固定套路：先查库，再把命中的段落拼进 prompt，相当于让模型开卷考试——证据在场，回答就更可核对、也更贴业务事实，整体可信度与可用性一起抬升。

**Rule of Thumb:** Use this pattern when you need an LLM to answer questions or generate content based on specific, up-to-date, or proprietary information that was not part of its original training data. It is ideal for building Q\&A systems over internal documents, customer support bots, and applications requiring verifiable, fact-based responses with citations.

> **经验法则：** 只要答案必须依赖「训练集外的特定/实时/保密」材料，就该考虑 RAG——内部文档问答、合规客服、需要脚注或溯源的写作场景都是典型。

**Visual Summary:**

> **可视化摘要：**

![Knowledge Retrieval Pattern Database](../assets-new/Knowledge_Retrieval_Pattern_Database.png)

Knowledge Retrieval pattern: an AI agent to query and retrieve information from structured databases

> 知识检索模式：智能体向结构化库发起查询并取回记录

![Knowledge Retrieval Pattern Search](../assets-new/Knowledge_Retrieval_Pattern_Search.png)

Fig. 3: Knowledge Retrieval pattern: an AI agent to find and synthesize information from the public internet in response to user queries.

> 图 3：知识检索模式——智能体应用户问句从公网检索并综合信息

## Key Takeaways

* Knowledge Retrieval (RAG) enhances LLMs by allowing them to access external, up-to-date, and specific information.  
* The process involves Retrieval (searching a knowledge base for relevant snippets) and Augmentation (adding these snippets to the LLM's prompt).  
* RAG helps LLMs overcome limitations like outdated training data, reduces "hallucinations," and enables domain-specific knowledge integration.  
* RAG allows for attributable answers, as the LLM's response is grounded in retrieved sources.  
* GraphRAG leverages a knowledge graph to understand the relationships between different pieces of information, allowing it to answer complex questions that require synthesizing data from multiple sources.  
* Agentic RAG moves beyond simple information retrieval by using an intelligent agent to actively reason about, validate, and refine external knowledge, ensuring a more accurate and reliable answer.  
* Practical applications span enterprise search, customer support, legal research, and personalized recommendations.

> * RAG = 先检索外部片段，再把片段塞进提示，让模型「带着证据说话」。  
> * 能缓解训练截止日期、私域盲区，并压低胡编概率。  
> * 片段级引用让答案可追溯、可审计。  
> * GraphRAG 用图结构补多跳、多文档综合短板。  
> * Agentic RAG 用智能体做质检、消歧、多步查询与工具补洞，换更高可靠性。  
> * 企业搜索、客服、法务检索、个性化推荐等场景已大量采用。

## Conclusion

In conclusion, Retrieval-Augmented Generation (RAG) addresses the core limitation of a Large Language Model's static knowledge by connecting it to external, up-to-date data sources. The process works by first retrieving relevant information snippets and then augmenting the user's prompt, enabling the LLM to generate more accurate and contextually aware responses. This is made possible by foundational technologies like embeddings, semantic search, and vector databases, which find information based on meaning rather than just keywords. By grounding outputs in verifiable data, RAG significantly reduces factual errors and allows for the use of proprietary information, enhancing trust through citations.

> 收束一句：RAG 用「外接知识源」补齐 LLM 的静态记忆短板——先搜后写，提示里带着证据；embedding、语义检索与向量库负责按意思找材料；答案拴在可验证片段上，事实错误与私域盲区同时被压缩，引用则把信任成本打下来。

An advanced evolution, Agentic RAG, introduces a reasoning layer that actively validates, reconciles, and synthesizes retrieved knowledge for even greater reliability. Similarly, specialized approaches like GraphRAG leverage knowledge graphs to navigate explicit data relationships, allowing the system to synthesize answers to highly complex, interconnected queries. This agent can resolve conflicting information, perform multi-step queries, and use external tools to find missing data. While these advanced methods add complexity and latency, they drastically improve the depth and trustworthiness of the final response. Practical applications for these patterns are already transforming industries, from enterprise search and customer support to personalized content delivery. Despite the challenges, RAG is a crucial pattern for making AI more knowledgeable, reliable, and useful. Ultimately, it transforms LLMs from closed-book conversationalists into powerful, open-book reasoning tools.

> Agentic RAG 再叠推理层，专门处理信源打架、任务拆解与工具补数；GraphRAG 则借图谱显式关系啃多跳综合题。二者都更吃工程与延迟，换的是答案深度与可信度。落地已渗透搜索、客服、内容分发等垂直场景。挑战仍在，但 RAG 家族仍是把 LLM 从「闭卷聊天」推向「开卷办事」的主干道之一。

## References

> 参考文献：以下条目保留英文与原始链接，不作逐条翻译。

1. Lewis, P., et al. (2020). *Retrieval-Augmented Generation for Knowledge-Intensive NLP Tasks*. [https://arxiv.org/abs/2005.11401](https://arxiv.org/abs/2005.11401)
2. Google AI for Developers Documentation.  *Retrieval Augmented Generation - [https://cloud.google.com/vertex-ai/generative-ai/docs/rag-engine/rag-overview](https://cloud.google.com/vertex-ai/generative-ai/docs/rag-engine/rag-overview)*
3. Retrieval-Augmented Generation with Graphs (GraphRAG), [https://arxiv.org/abs/2501.00309](https://arxiv.org/abs/2501.00309)
4. LangChain and LangGraph: Leonie Monigatti, "Retrieval-Augmented Generation (RAG): From Theory to LangChain Implementation,"  [*https://medium.com/data-science/retrieval-augmented-generation-rag-from-theory-to-langchain-implementation-4e9bd5f6a4f2*](https://medium.com/data-science/retrieval-augmented-generation-rag-from-theory-to-langchain-implementation-4e9bd5f6a4f2)
5. Google Cloud Vertex AI RAG Corpus [*https://cloud.google.com/vertex-ai/generative-ai/docs/rag-engine/manage-your-rag-corpus#corpus-management*](https://cloud.google.com/vertex-ai/generative-ai/docs/rag-engine/manage-your-rag-corpus#corpus-management)
