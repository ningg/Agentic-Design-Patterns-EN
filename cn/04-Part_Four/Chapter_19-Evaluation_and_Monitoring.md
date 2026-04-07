# Chapter 19: Evaluation and Monitoring

> 第十九章：评估与监控（Evaluation and Monitoring）

This chapter examines methodologies that allow intelligent agents to systematically assess their performance, monitor progress toward goals, and detect operational anomalies. While Chapter 11 outlines goal setting and monitoring, and Chapter 17 addresses Reasoning mechanisms, this chapter focuses on the continuous, often external, measurement of an agent's effectiveness, efficiency, and compliance with requirements. This includes defining metrics, establishing feedback loops, and implementing reporting systems to ensure agent performance aligns with expectations in operational environments (see Fig.1)

> 本章讨论使智能体能够系统评估自身表现、监控向目标的进展并检测运行异常的方法。第十一章阐述目标设定与监控，第十七章讨论推理机制；本章则聚焦对智能体有效性、效率及是否符合要求的持续性、常为外部的度量，包括定义指标、建立反馈回路与实施报告制度，以使智能体表现与运营环境中的期望一致（见图 1）。

![Monitoring and Evaluating Agent Performance](../assets-new/Monitoring_and_Evaluating_Agent_Performance.png)

Fig:1. Best practices for evaluation and monitoring

> 图 1：评估与监控的最佳实践

## Practical Applications & Use Cases

> ## 实际应用与用例

Most Common Applications and Use Cases:

> 最常见应用与用例：

* **Performance Tracking in Live Systems:** Continuously monitoring the accuracy, latency, and resource consumption of an agent deployed in a production environment (e.g., a customer service chatbot's resolution rate, response time).  
* **A/B Testing for Agent Improvements:** Systematically comparing the performance of different agent versions or strategies in parallel to identify optimal approaches (e.g., trying two different planning algorithms for a logistics agent).  
* **Compliance and Safety Audits:** Generate automated audit reports that track an agent's compliance with ethical guidelines, regulatory requirements, and safety protocols over time. These reports can be verified by a human-in-the-loop or another agent, and can generate KPIs or trigger alerts upon identifying issues.  
* **Enterprise systems:** To govern Agentic AI in corporate systems, a new control instrument, the AI "Contract," is needed. This dynamic agreement codifies the objectives, rules, and controls for AI-delegated tasks.  
* **Drift Detection:** Monitoring the relevance or accuracy of an agent's outputs over time, detecting when its performance degrades due to changes in input data distribution (concept drift) or environmental shifts.  
* **Anomaly Detection in Agent Behavior:** Identifying unusual or unexpected actions taken by an agent that might indicate an error, a malicious attack, or an emergent un-desired behavior.  
* **Learning Progress Assessment:** For agents designed to learn, tracking their learning curve, improvement in specific skills, or generalization capabilities over different tasks or data sets.

> * **线上系统性能跟踪：** 持续监控生产环境中部署的智能体的准确率、延迟与资源消耗（如客服机器人的解决率、响应时间）。  
> * **智能体改进的 A/B 测试：** 并行比较不同智能体版本或策略的表现，以识别最优方案（如对物流智能体尝试两种规划算法）。  
> * **合规与安全审计：** 生成自动化审计报告，跟踪智能体对伦理准则、法规要求与安全规程的长期遵守情况；报告可由人在回路或其他智能体验证，并可在发现问题时生成 KPI 或触发告警。  
> * **企业系统：** 要在企业系统中治理智能体 AI，需要新的控制工具——AI「合约（Contract）」；该动态协议将 AI 委派任务的目标、规则与控制措施成文化。  
> * **漂移检测：** 监控智能体输出随时间的相关性或准确性，检测因输入分布变化（概念漂移）或环境变化导致的表现下滑。  
> * **智能体行为异常检测：** 识别不寻常或出乎意料的行动，可能预示错误、恶意攻击或涌现的不期望行为。  
> * **学习进度评估：** 对具备学习能力的智能体，跟踪其学习曲线、特定技能提升或跨任务/数据集的泛化能力。

## Hands-On Code Example

> ## 动手代码示例

Developing a comprehensive evaluation framework for AI agents is a challenging endeavor, comparable to an academic discipline or a substantial publication in its complexity. This difficulty stems from the multitude of factors to consider, such as model performance, user interaction, ethical implications, and broader societal impact. Nevertheless, for practical implementation, the focus can be narrowed to critical use cases essential for the efficient and effective functioning of AI agents.

> 为 AI 智能体构建全面评估框架是一项艰巨工作，其复杂程度可比拟一门学科或一部重要专著；难点在于需同时考虑模型表现、用户交互、伦理影响及更广泛的社会影响等。尽管如此，在实际落地时，可将焦点收窄到对智能体高效、有效运行至关重要的关键用例。

**Agent Response Assessment:** This core process is essential for evaluating the quality and accuracy of an agent's outputs. It involves determining if the agent delivers pertinent, correct,  logical, unbiased, and accurate information in response to given inputs. Assessment metrics may include factual correctness, fluency, grammatical precision, and adherence to the user's intended purpose.

> **智能体回复评估：** 该核心流程用于评估智能体输出的质量与准确性，判断其是否针对给定输入提供相关、正确、合乎逻辑、无偏见且准确的信息；指标可包括事实正确性、流畅度、语法精确度及是否符合用户意图。

```python
def evaluate_response_accuracy(agent_output: str, expected_output: str) -> float:
    """Calculates a simple accuracy score for agent responses."""
    # This is a very basic exact match; real-world would use more sophisticated metrics
    return 1.0 if agent_output.strip().lower() == expected_output.strip().lower() else 0.0


# Example usage
agent_response = "The capital of France is Paris."
ground_truth = "Paris is the capital of France."
score = evaluate_response_accuracy(agent_response, ground_truth)
print(f"Response accuracy: {score}")
```

The Python function `evaluate_response_accuracy` calculates a basic accuracy score for an AI agent's response by performing an exact, case-insensitive comparison between the agent's output and the expected output, after removing leading or trailing whitespace. It returns a score of 1.0 for an exact match and 0.0 otherwise, representing a binary correct or incorrect evaluation. This method, while straightforward for simple checks, does not account for variations like paraphrasing or semantic equivalence.

> Python 函数 `evaluate_response_accuracy` 在去除首尾空白后，对智能体输出与期望输出做不区分大小写的逐字符精确比较，计算基础准确率：完全匹配返回 1.0，否则 0.0，即二元对错。该方法对简单检查直观，但不考虑改写或语义等价等情况。

The problem lies in its method of comparison. The function performs a strict, character-for-character comparison of the two strings. In the example provided:

* `agent_response`: "The capital of France is Paris."  
* `ground_truth`: "Paris is the capital of France."

Even after removing whitespace and converting to lowercase, these two strings are not identical. As a result, the function will incorrectly return an accuracy score of `0.0`, even though both sentences convey the same meaning.

> 问题在于比较方式：函数对两串做严格逐字比较。示例中：  
> * `agent_response`：「The capital of France is Paris.」  
> * `ground_truth`：「Paris is the capital of France.」  
> 即便去空白并转小写，两串仍不相同，函数会错误返回 `0.0`，尽管语义相同。

A straightforward comparison falls short in assessing semantic similarity, only succeeding if an agent's response exactly matches the expected output. A more effective evaluation necessitates advanced Natural Language Processing (NLP) techniques to discern the meaning between sentences. For thorough AI agent evaluation in real-world scenarios, more sophisticated metrics are often indispensable. These metrics can encompass String Similarity Measures like Levenshtein distance and Jaccard similarity, Keyword Analysis for the presence or absence of specific keywords, Semantic Similarity using cosine similarity with embedding models, LLM-as-a-Judge Evaluations (discussed later for assessing nuanced correctness and helpfulness), and RAG-specific Metrics such as faithfulness and relevance.

> 简单字符串比较不足以衡量语义相似度，仅当回复与期望输出完全一致时才「成功」。更有效评估需要先进自然语言处理（NLP）技术以辨别句间含义。面向真实场景的 AI 智能体评估往往离不开更复杂指标，例如：编辑距离、Jaccard 等字符串相似度；关键词有无分析；基于嵌入的余弦语义相似度；LLM-as-a-Judge 评估（后文讨论，用于细粒度正确性与有用性）；以及 RAG 场景下的忠实度、相关性等指标。

**Latency Monitoring:** Latency Monitoring for Agent Actions is crucial in applications where the speed of an AI agent's response or action is a critical factor. This process measures the duration required for an agent to process requests and generate outputs. Elevated latency can adversely affect user experience and the agent's overall effectiveness, particularly in real-time or interactive environments. In practical applications, simply printing latency data to the console is insufficient. Logging this information to a persistent storage system is recommended. Options include structured log files (e.g., JSON), time-series databases (e.g., InfluxDB, Prometheus), data warehouses (e.g., Snowflake, BigQuery, PostgreSQL), or observability platforms (e.g., Datadog, Splunk, Grafana Cloud).

> **延迟监控：** 在响应或行动速度至关重要的应用中，对智能体行动的延迟监控十分关键；它度量处理请求与生成输出所需时间。高延迟会损害用户体验与智能体整体效果，尤其在实时或交互场景。实务上仅打印到控制台往往不够，建议写入持久化存储：结构化日志（如 JSON）、时序库（如 InfluxDB、Prometheus）、数据仓库（如 Snowflake、BigQuery、PostgreSQL）或可观测平台（如 Datadog、Splunk、Grafana Cloud）。

**Tracking Token Usage for LLM Interactions:** For LLM-powered agents, tracking token usage is crucial for managing costs and optimizing resource allocation. Billing for LLM interactions often depends on the number of tokens processed (input and output). Therefore, efficient token usage directly reduces operational expenses. Additionally, monitoring token counts helps identify potential areas for improvement in prompt engineering or response generation processes.

> **跟踪 LLM 交互的 token 用量：** 对由 LLM 驱动的智能体，跟踪 token 用量对成本管理与资源优化至关重要；计费常按处理 token 数（输入与输出）。高效用 token 直接降低运营成本；监控 token 还有助于发现提示工程或回复生成环节的改进空间。

```python
# This is conceptual as actual token counting depends on the LLM API
class LLMInteractionMonitor:
    def __init__(self):
        self.total_input_tokens = 0
        self.total_output_tokens = 0

    def record_interaction(self, prompt: str, response: str):
        # In a real scenario, use LLM API's token counter or a tokenizer
        input_tokens = len(prompt.split())  # Placeholder
        output_tokens = len(response.split())  # Placeholder
        self.total_input_tokens += input_tokens
        self.total_output_tokens += output_tokens
        print(f"Recorded interaction: Input tokens={input_tokens}, Output tokens={output_tokens}")

    def get_total_tokens(self):
        return self.total_input_tokens, self.total_output_tokens


# Example usage
monitor = LLMInteractionMonitor()
monitor.record_interaction("What is the capital of France?", "The capital of France is Paris.")
monitor.record_interaction("Tell me a joke.", "Why don't scientists trust atoms? Because they make up everything!")
input_t, output_t = monitor.get_total_tokens()
print(f"Total input tokens: {input_t}, Total output tokens: {output_t}")
```

This section introduces a conceptual Python class, `LLMInteractionMonitor`, developed to track token usage in large language model interactions. The class incorporates counters for both input and output tokens. Its `record_interaction` method simulates token counting by splitting the prompt and response strings. In a practical implementation, specific LLM API tokenizers would be employed for precise token counts. As interactions occur, the monitor accumulates the total input and output token counts. The `get_total_tokens` method provides access to these cumulative totals, essential for cost management and optimization of LLM usage.

> 本节介绍概念性 Python 类 `LLMInteractionMonitor`，用于跟踪大语言模型交互中的 token 用量；含输入与输出计数器。`record_interaction` 通过分词模拟计数，实际部署应使用具体 LLM API 的分词器。交互发生时累加总量，`get_total_tokens` 返回累计值，供成本管理与用量优化。

**Custom Metric for "Helpfulness" using LLM-as-a-Judge:** Evaluating subjective qualities like an AI agent's "helpfulness" presents challenges beyond standard objective metrics. A potential framework involves using an LLM as an evaluator. This LLM-as-a-Judge approach assesses another AI agent's output based on predefined criteria for "helpfulness." Leveraging the advanced linguistic capabilities of LLMs, this method offers nuanced, human-like evaluations of subjective qualities, surpassing simple keyword matching or rule-based assessments. Though in development, this technique shows promise for automating and scaling qualitative evaluations.

> **用 LLM-as-a-Judge 度量「有用性」：** 评估「有用性」等主观品质超出常规客观指标。可行框架是让 LLM 担任评判者，按预设「有用性」标准评估另一智能体的输出；借助 LLM 的语言能力，可对主观品质做接近人类的细粒度评价，优于简单关键词或规则。该技术仍在发展，但在自动化、规模化质性评估方面前景可期。

```python
import os
import json
import logging
from typing import Optional

import google.generativeai as genai

# --- Configuration ---
logging.basicConfig(level=logging.INFO, format='%(asctime)s - %(levelname)s - %(message)s')

# Set your API key as an environment variable to run this script
# For example, in your terminal: export GOOGLE_API_KEY='your_key_here'
try:
    genai.configure(api_key=os.environ["GOOGLE_API_KEY"])
except KeyError:
    logging.error("Error: GOOGLE_API_KEY environment variable not set.")
    exit(1)

# --- LLM-as-a-Judge Rubric for Legal Survey Quality ---
LEGAL_SURVEY_RUBRIC = """
 You are an expert legal survey methodologist and a critical legal reviewer. Your task is to evaluate the quality of a given legal survey question. Provide a score from 1 to 5 for overall quality, along with a detailed rationale and specific feedback.

 Focus on the following criteria:

 1.  **Clarity & Precision (Score 1-5):**
    * 1: Extremely vague, highly ambiguous, or confusing.
    * 3: Moderately clear, but could be more precise.
    * 5: Perfectly clear, unambiguous, and precise in its legal terminology (if applicable) and intent.

 2.  **Neutrality & Bias (Score 1-5):**
    * 1: Highly leading or biased, clearly influencing the respondent towards a specific answer.
    * 3: Slightly suggestive or could be interpreted as leading.
    * 5: Completely neutral, objective, and free from any leading language or loaded terms.

 3.  **Relevance & Focus (Score 1-5):**
    * 1: Irrelevant to the stated survey topic or out of scope.
    * 3: Loosely related but could be more focused.
    * 5: Directly relevant to the survey's objectives and well-focused on a single concept.

 4.  **Completeness (Score 1-5):**
    * 1: Omits critical information needed to answer accurately or provides insufficient context.
    * 3: Mostly complete, but minor details are missing.
    * 5: Provides all necessary context and information for the respondent to answer thoroughly.

 5.  **Appropriateness for Audience (Score 1-5):**
    * 1: Uses jargon inaccessible to the target audience or is overly simplistic for experts.
    * 3: Generally appropriate, but some terms might be challenging or oversimplified.
    * 5: Perfectly tailored to the assumed legal knowledge and background of the target survey audience.

 **Output Format:**
 Your response MUST be a JSON object with the following keys:
 * `overall_score`: An integer from 1 to 5 (average of criterion scores, or your holistic judgment).
 * `rationale`: A concise summary of why this score was given, highlighting major strengths and weaknesses.
 * `detailed_feedback`: A bullet-point list detailing feedback for each criterion (Clarity, Neutrality, Relevance, Completeness, Audience Appropriateness). Suggest specific improvements.
 * `concerns`: A list of any specific legal, ethical, or methodological concerns.
 * `recommended_action`: A brief recommendation (e.g., "Revise for neutrality", "Approve as is", "Clarify scope").
"""

class LLMJudgeForLegalSurvey:
    """A class to evaluate legal survey questions using a generative AI model."""

    def __init__(self, model_name: str = 'gemini-1.5-flash-latest', temperature: float = 0.2):
        """
        Initializes the LLM Judge.

        Args:
            model_name (str): The name of the Gemini model to use.
                              'gemini-1.5-flash-latest' is recommended for speed and cost.
                              'gemini-1.5-pro-latest' offers the highest quality.
            temperature (float): The generation temperature. Lower is better for deterministic evaluation.
        """
        self.model = genai.GenerativeModel(model_name)
        self.temperature = temperature

    def _generate_prompt(self, survey_question: str) -> str:
        """Constructs the full prompt for the LLM judge."""
        return f"{LEGAL_SURVEY_RUBRIC}\n\n---\n**LEGAL SURVEY QUESTION TO EVALUATE:**\n{survey_question}\n---"

    def judge_survey_question(self, survey_question: str) -> Optional[dict]:
        """
        Judges the quality of a single legal survey question using the LLM.

        Args:
            survey_question (str): The legal survey question to be evaluated.

        Returns:
            Optional[dict]: A dictionary containing the LLM's judgment, or None if an error occurs.
        """
        full_prompt = self._generate_prompt(survey_question)

        try:
            logging.info(f"Sending request to '{self.model.model_name}' for judgment...")
            response = self.model.generate_content(
                full_prompt,
                generation_config=genai.types.GenerationConfig(
                    temperature=self.temperature,
                    response_mime_type="application/json"
                )
            )

            # Check for content moderation or other reasons for an empty response.
            if not response.parts:
                safety_ratings = response.prompt_feedback.safety_ratings
                logging.error(f"LLM response was empty or blocked. Safety Ratings: {safety_ratings}")
                return None

            return json.loads(response.text)
        except json.JSONDecodeError:
            logging.error(f"Failed to decode LLM response as JSON. Raw response: {response.text}")
            return None
        except Exception as e:
            logging.error(f"An unexpected error occurred during LLM judgment: {e}")
            return None


# --- Example Usage ---
if __name__ == "__main__":
    judge = LLMJudgeForLegalSurvey()

    # --- Good Example ---
    good_legal_survey_question = """
    To what extent do you agree or disagree that current intellectual property laws in Switzerland adequately protect emerging AI-generated content, assuming the content meets the originality criteria established by the Federal Supreme Court?
    (Select one: Strongly Disagree, Disagree, Neutral, Agree, Strongly Agree)
    """
    print("\n--- Evaluating Good Legal Survey Question ---")
    judgment_good = judge.judge_survey_question(good_legal_survey_question)
    if judgment_good:
        print(json.dumps(judgment_good, indent=2))

    # --- Biased/Poor Example ---
    biased_legal_survey_question = """
    Don't you agree that overly restrictive data privacy laws like the FADP are hindering essential technological innovation and economic growth in Switzerland?
    (Select one: Yes, No)
    """
    print("\n--- Evaluating Biased Legal Survey Question ---")
    judgment_biased = judge.judge_survey_question(biased_legal_survey_question)
    if judgment_biased:
        print(json.dumps(judgment_biased, indent=2))

    # --- Ambiguous/Vague Example ---
    vague_legal_survey_question = """
    What are your thoughts on legal tech?
    """
    print("\n--- Evaluating Vague Legal Survey Question ---")
    judgment_vague = judge.judge_survey_question(vague_legal_survey_question)
    if judgment_vague:
        print(json.dumps(judgment_vague, indent=2))
```

The Python code defines a class LLMJudgeForLegalSurvey designed to evaluate the quality of legal survey questions using a generative AI model. It utilizes the google.`generativeai` library to interact with Gemini models.

> 该 Python 代码定义 `LLMJudgeForLegalSurvey` 类，用生成式 AI 模型评估法律调查问题的质量；通过 google.`generativeai` 库与 Gemini 模型交互。

The core functionality involves sending a survey question to the model along with a detailed rubric for evaluation. The rubric specifies five criteria for judging survey questions: Clarity & Precision, Neutrality & Bias, Relevance & Focus, Completeness, and Appropriateness for Audience. For each criterion, a score from 1 to 5 is assigned, and a detailed rationale and feedback are required in the output. The code constructs a prompt that includes the rubric and the survey question to be evaluated.

> 核心流程是将调查问题与详细评分细则一并送入模型。细则规定五项评判标准：清晰度与精确性、中立性与偏见、相关性与聚焦、完整性、以及对受众的适宜性；每项 1–5 分，并要求给出理由与反馈。代码构建的提示包含细则与待评估问题。

The `judge_survey_question` method sends this prompt to the configured Gemini model, requesting a JSON response formatted according to the defined structure. The expected output JSON includes an overall score, a summary rationale, detailed feedback for each criterion, a list of concerns, and a recommended action. The class handles potential errors during the AI model interaction, such as JSON decoding issues or empty responses. The script demonstrates its operation by evaluating examples of legal survey questions, illustrating how the AI assesses quality based on the predefined criteria.

> `judge_survey_question` 将提示发给所配置的 Gemini 模型，请求按约定结构返回 JSON：总分、简要理由、各准则详细反馈、关切列表与建议行动。类还处理交互中的潜在错误（如 JSON 解析失败或空响应）。脚本用若干法律调查问题示例演示评估流程。

Before we conclude, let's examine various evaluation methods, considering their strengths and weaknesses.

> 在结束之前，我们比较几种评估方法及其优劣。

| Evaluation Method | Strengths | Weaknesses |
| :---- | :---- | :---- |
| Human Evaluation  | Captures subtle behavior | Difficult to scale, expensive, and time-consuming, as it considers subjective human factors. |
| LLM-as-a-Judge | Consistent, efficient, and scalable.  | Intermediate steps may be overlooked. Limited by LLM capabilities. |
| Automated Metrics  | Scalable, efficient, and objective | Potential limitation in capturing complete capabilities. |

> 上表含义（中文对照）：人工评估能捕捉细微行为，但难扩展、昂贵、耗时且含主观因素；LLM 评判一致、高效、可扩展，但可能忽略中间步骤且受 LLM 能力限制；自动化指标可扩展、高效、客观，但可能无法完整刻画能力。

## Agents trajectories

> ## 智能体轨迹（Agents trajectories）

Evaluating agents' trajectories is essential, as traditional software tests are insufficient. Standard code yields predictable pass/fail results, whereas agents operate probabilistically, necessitating qualitative assessment of both the final output and the agent's trajectory—the sequence of steps taken to reach a solution. Evaluating multi-agent systems is challenging because they are constantly in flux. This requires developing sophisticated metrics that go beyond individual performance to measure the effectiveness of communication and teamwork. Moreover, the environments themselves are not static, demanding that evaluation methods, including test cases, adapt over time.

> 评估智能体轨迹至关重要，传统软件测试并不足够：常规代码有确定的通过/失败，而智能体概率化运行，需要对最终输出与到达解的步骤序列（轨迹）做质性评估。多智能体系统持续变化，评估更难，需要超越个体表现的复杂指标来衡量沟通与协作成效；环境亦非静态，评估方法与测试用例需随时间演进。

This involves examining the quality of decisions, the reasoning process, and the overall outcome. Implementing automated evaluations is valuable, particularly for development beyond the prototype stage. Analyzing trajectory and tool use includes evaluating the steps an agent employs to achieve a goal, such as tool selection, strategies, and task efficiency. For example, an agent addressing a customer's product query might ideally follow a trajectory involving intent determination, database search tool use, result review, and report generation. The agent's actual actions are compared to this expected, or ground truth, trajectory to identify errors and inefficiencies. Comparison methods include exact match (requiring a perfect match to the ideal sequence), in-order match (correct actions in order, allowing extra steps), any-order match (correct actions in any order, allowing extra steps), precision (measuring the relevance of predicted actions), recall (measuring how many essential actions are captured), and single-tool use (checking for a specific action). Metric selection depends on specific agent requirements, with high-stakes scenarios potentially demanding an exact match, while more flexible situations might use an in-order or any-order match.

> 这包括考察决策质量、推理过程与总体结果。自动化评估在超越原型的开发中很有价值。轨迹与工具使用分析涵盖工具选择、策略与任务效率等步骤。例如处理客户产品咨询时，理想轨迹可能包含：判定意图、调用数据库检索、审阅结果、生成报告。将实际行为与期望（真值）轨迹对比以发现错误与低效。比较方式包括：精确匹配、保序匹配（允许多余步骤）、任意序匹配（允许多余步骤）、精确率、召回率、单工具检查等。指标选择依场景而定：高风险可能要求精确匹配，较灵活场景可用保序或任意序匹配。

Evaluation of AI agents involves two primary approaches: using test files and using evalset files. Test files, in JSON format, represent single, simple agent-model interactions or sessions and are ideal for unit testing during active development, focusing on rapid execution and simple session complexity. Each test file contains a single session with multiple turns, where a turn is a user-agent interaction including the user’s query, expected tool use trajectory, intermediate agent responses, and final response. For example, a test file might detail a user request to “Turn off `device_2` in the Bedroom,” specifying the agent’s use of a `set_device_info` tool with parameters like location: Bedroom, `device_id: device_2`, and status: OFF, and an expected final response of “I have set the `device_2` status to off.” Test files can be organized into folders and may include a `test_config`.json file to define evaluation criteria. Evalset files utilize a dataset called an “evalset” to evaluate interactions, containing multiple potentially lengthy sessions suited for simulating complex, multi-turn conversations and integration tests. An evalset file comprises multiple “evals,” each representing a distinct session with one or more “turns” that include user queries, expected tool use, intermediate responses, and a reference final response. An example evalset might include a session where the user first asks “What can you do?” and then says “Roll a 10 sided dice twice and then check if 9 is a prime or not,” defining expected `roll_die` tool calls and a `check_prime` tool call, along with the final response summarizing the dice rolls and the prime check.

> AI 智能体评估主要有两类：**测试文件（test files）**与 **evalset 文件**。测试文件为 JSON，表示单次、较简单的智能体—模型交互或会话，适合活跃开发期的单元测试，强调快速执行与会话结构简单。每个测试文件含一个多轮会话；一轮包含用户查询、期望工具使用轨迹、中间回复与最终回复。例如用户要求「关闭卧室里的 `device_2`」，期望调用 `set_device_info`（如 location: Bedroom、`device_id: device_2`、status: OFF），最终回复「我已将 `device_2` 设为关闭」。测试文件可分层组织，并可含 `test_config`.json 定义评估准则。**Evalset** 用名为 evalset 的数据集评估交互，可含多个较长会话，适合模拟复杂多轮对话与集成测试；evalset 文件含多个 eval，每个 eval 为一个或多个 turn 的会话，含查询、期望工具使用、中间回复与参考最终回复。示例：用户先问「你能做什么？」再说「掷两次十面骰并判断 9 是否为质数」，并定义期望的 `roll_die` 与 `check_prime` 调用及总结骰子与质数判断的最终回复。

**Multi-agents**: Evaluating a complex AI system with multiple agents is much like assessing a team project. Because there are many steps and handoffs, its complexity is an advantage, allowing you to check the quality of work at each stage. You can examine how well each individual "agent" performs its specific job, but you must also evaluate how the entire system is performing as a whole.

> **多智能体：** 评估含多个智能体的复杂系统类似评估团队项目：步骤与交接多，复杂度反而便于分阶段检查质量；既要考察每个智能体是否做好本职，也要评估整体系统表现。

To do this, you ask key questions about the team's dynamics, supported by concrete examples:

> 为此可围绕团队动态提出关键问题，并辅以具体例子：

* Are the agents cooperating effectively? For instance, after a 'Flight-Booking Agent' secures a flight, does it successfully pass the correct dates and destination to the 'Hotel-Booking Agent'? A failure in cooperation could lead to a hotel being booked for the wrong week.  
* Did they create a good plan and stick to it? Imagine the plan is to first book a flight, then a hotel. If the 'Hotel Agent' tries to book a room before the flight is confirmed, it has deviated from the plan. You also check if an agent gets stuck, for example, endlessly searching for a "perfect" rental car and never moving on to the next step.  
* Is the right agent being chosen for the right task? If a user asks about the weather for their trip, the system should use a specialized 'Weather Agent' that provides live data. If it instead uses a 'General Knowledge Agent' that gives a generic answer like "it's usually warm in summer," it has chosen the wrong tool for the job.  
* Finally, does adding more agents improve performance? If you add a new 'Restaurant-Reservation Agent' to the team, does it make the overall trip-planning better and more efficient? Or does it create conflicts and slow the system down, indicating a problem with scalability?.

> * 智能体是否有效协作？例如「航班预订智能体」订好票后，是否把正确日期与目的地交给「酒店预订智能体」？协作失败可能导致订错周的酒店。  
> * 是否制定了合理计划并坚持？若计划是先订机票再订酒店，而「酒店智能体」在航班确认前订房，则偏离计划；也要检查是否卡住（如无休止找「完美」租车而不进入下一步）。  
> * 是否为正确任务选对智能体？用户问行程天气时，应使用能提供实时数据的「天气智能体」；若用「通识智能体」只答「夏天通常很热」，则是选错工具。  
> * 增加智能体是否提升表现？加入「餐厅预订智能体」后，整体行程规划是否更好更高效，还是引发冲突、拖慢系统，暴露扩展性问题？

## From Agents to Advanced Contractors

> ## 从智能体到高级「承包商（Contractors）」

 Recently, it has been proposed (Agent Companion, gulli et al.) an evolution from simple AI agents to advanced "contractors", moving from probabilistic, often unreliable systems to more deterministic and accountable ones designed for complex, high-stakes environments (see Fig.2)

> 近期（Agent Companion，gulli 等）提出从简单 AI 智能体演进为高级「承包商」：由概率化、常不可靠的系统，走向面向复杂高风险场景、更确定且可问责的设计（见图 2）。

 Today's common AI agents operate on brief, underspecified instructions, which makes them suitable for simple demonstrations but brittle in production, where ambiguity leads to failure. The "contractor" model addresses this by establishing a rigorous, formalized relationship between the user and the AI, built upon a foundation of clearly defined and mutually agreed-upon terms, much like a legal service agreement in the human world. This transformation is supported by four key pillars that collectively ensure clarity, reliability, and robust execution of tasks that were previously beyond the scope of autonomous systems

> 当今常见智能体依赖简短、欠具体说明的指令，适合简单演示却在生产中脆弱——歧义导致失败。「承包商」模型通过在用户与 AI 之间建立严谨、正式的关系来应对，以清晰、双方认可的条件为基础，类似人类世界中的法律服务协议。该转变由四大支柱支撑，共同保证清晰度、可靠性与稳健执行，使此前超出自主系统能力范围的任务得以落地。

First is the pillar of the Formalized Contract, a detailed specification that serves as the single source of truth for a task. It goes far beyond a simple prompt. For example, a contract for a financial analysis task wouldn't just say "analyze last quarter's sales"; it would demand "a 20-page PDF report analyzing European market sales from Q1 2025, including five specific data visualizations, a comparative analysis against Q1 2024, and a risk assessment based on the included dataset of supply chain disruptions." This contract explicitly defines the required deliverables, their precise specifications, the acceptable data sources, the scope of work, and even the expected computational cost and completion time, making the outcome objectively verifiable.

> 第一支柱是**正式化合约（Formalized Contract）**：作为任务的单一事实来源的详细规格，远非一句提示可比。例如金融分析任务不会只说「分析上季度销售」，而会要求「一份 20 页 PDF，分析 2025 年一季度欧洲市场销售，含五类指定可视化、与 2024 年一季度的对比分析，以及基于所附供应链扰动数据集的风险评估」。合约明确交付物、规格、可接受数据源、工作范围乃至预期算力与完成时间，使结果可客观核验。

Second is the pillar of a Dynamic Lifecycle of Negotiation and Feedback. The contract is not a static command but the start of a dialogue. The contractor agent can analyze the initial terms and negotiate. For instance, if a contract demands the use of a specific proprietary data source the agent cannot access, it can return feedback stating, "The specified XYZ database is inaccessible. Please provide credentials or approve the use of an alternative public database, which may slightly alter the data's granularity." This negotiation phase, which also allows the agent to flag ambiguities or potential risks, resolves misunderstandings before execution begins, preventing costly failures and ensuring the final output aligns perfectly with the user's actual intent.

> 第二支柱是**谈判与反馈的动态生命周期**。合约不是静态命令，而是对话起点；承包商智能体可分析初始条款并协商。例如合约要求使用无法访问的专有数据源时，可反馈：「指定的 XYZ 数据库不可达，请提供凭证或批准改用替代公开数据库（可能略微改变数据粒度）。」该谈判阶段也允许标出歧义或风险，在执行前消除误解，避免昂贵失败，并使最终产出与用户真实意图一致。

![Contract Execution Example Among Agents](../assets-new/Contract_Execution_Example_Among_Agents.png)

Fig. 2: Contract execution example among agents

> 图 2：智能体之间的合约执行示例

The third pillar is Quality-Focused Iterative Execution. Unlike agents designed for low-latency responses, a contractor prioritizes correctness and quality. It operates on a principle of self-validation and correction. For a code generation contract, for example, the agent would not just write the code; it would generate multiple algorithmic approaches, compile and run them against a suite of unit tests defined within the contract, score each solution on metrics like performance, security, and readability, and only submit the version that passes all validation criteria. This internal loop of generating, reviewing, and improving its own work until the contract's specifications are met is crucial for building trust in its outputs.

> 第三支柱是**以质量为中心的迭代执行**。不同于追求低延迟回复的智能体，承包商优先正确性与质量，遵循自我校验与修正。以代码生成合约为例：不仅写代码，还会生成多种算法路径，在合约规定的单测集上编译运行，从性能、安全、可读性等维度打分，仅提交通过全部校验的版本。在达到合约规格前持续生成—审阅—改进的内部循环，对建立输出信任至关重要。

Finally, the fourth pillar is Hierarchical Decomposition via Subcontracts. For tasks of significant complexity, a primary contractor agent can act as a project manager, breaking the main goal into smaller, more manageable sub-tasks. It achieves this by generating new, formal "subcontracts." For example, a master contract to "build an e-commerce mobile application" could be decomposed by the primary agent into subcontracts for "designing the UI/UX," "developing the user authentication module," "creating the product database schema," and "integrating a payment gateway." Each of these subcontracts is a complete, independent contract with its own deliverables and specifications, which could be assigned to other specialized agents. This structured decomposition allows the system to tackle immense, multifaceted projects in a highly organized and scalable manner, marking the transition of AI from a simple tool to a truly autonomous and reliable problem-solving engine.

> 第四支柱是**通过子合约的层级分解**。对高度复杂任务，主承包商智能体可扮演项目经理，将总目标拆为更小、可管理的子任务，并生成新的正式「子合约」。例如总合约为「构建电商移动应用」，可分解为 UI/UX 设计、用户认证模块、商品数据库 schema、支付网关集成等子合约；每项都是完整独立合约，含自有交付物与规格，可交由其他专职智能体。结构化分解使系统能以高度可组织、可扩展的方式承担庞大多面项目，标志 AI 从简单工具转向真正自主、可靠的问题求解引擎。

Ultimately, this contractor framework reimagines AI interaction by embedding principles of formal specification, negotiation, and verifiable execution directly into the agent's core logic. This methodical approach elevates artificial intelligence from a promising but often unpredictable assistant into a dependable system capable of autonomously managing complex projects with auditable precision. By solving the critical challenges of ambiguity and reliability, this model paves the way for deploying AI in mission-critical domains where trust and accountability are paramount.

> 归根结底，承包商框架将正式规格、协商与可验证执行的原则嵌入智能体核心逻辑，重塑人机交互；使 AI 从前景可期却常难预测的助手，升级为能以可审计精度自主管理复杂项目的可靠系统。通过应对歧义与可靠性两大挑战，该模型为在强调信任与问责的关键任务领域部署 AI 铺平道路。

## Google's ADK

> ## Google ADK

Before concluding, let's look at a concrete example of a framework that supports evaluation. Agent evaluation with Google's ADK (see Fig.3) can be conducted via three methods: web-based UI (adk web) for interactive evaluation and dataset generation, programmatic integration using pytest for incorporation into testing pipelines, and direct command-line interface (adk eval) for automated evaluations suitable for regular build generation and verification processes.

> 结束前看一个支持评估的框架实例。使用 Google ADK 评估智能体（见图 3）可通过三种方式：基于 Web 的 UI（`adk web`）做交互式评估与数据集生成；用 pytest 做程序化集成以纳入测试流水线；以及命令行（`adk eval`）做适合常规构建与验证流程的自动化评估。

![Evaluation Support for Google ADK](../assets-new/Evaluation_Support_for_Google_ADK.png)

Fig.3: Evaluation Support for Google ADK

> 图 3：Google ADK 的评估支持

The web-based UI enables interactive session creation and saving into existing or new eval sets, displaying evaluation status. Pytest integration allows running test files as part of integration tests by calling AgentEvaluator.evaluate, specifying the agent module and test file path.

> Web UI 支持交互式创建会话并保存到已有或新建 eval 集，并展示评估状态。与 pytest 集成可通过调用 `AgentEvaluator.evaluate`、指定智能体模块与测试文件路径，将测试文件作为集成测试的一部分运行。

The command-line interface facilitates automated evaluation by providing the agent module path and eval set file, with options to specify a configuration file or print detailed results. Specific evals within a larger eval set can be selected for execution by listing them after the eval set filename, separated by commas.

> 命令行通过提供智能体模块路径与 eval 集文件实现自动化评估，可选配置文件或打印详细结果；可在 eval 集文件名后用逗号列出要执行的特定 eval。

## At a Glance

> ## 要点速览

**What:** Agentic systems and LLMs operate in complex, dynamic environments where their performance can degrade over time. Their probabilistic and non-deterministic nature means that traditional software testing is insufficient for ensuring reliability. Evaluating dynamic multi-agent systems is a significant challenge because their constantly changing nature and that of their environments demand the development of adaptive testing methods and sophisticated metrics that can measure collaborative success beyond individual performance. Problems like data drift, unexpected interactions, tool calling, and deviations from intended goals can arise after deployment. Continuous assessment is therefore necessary to measure an agent's effectiveness, efficiency, and adherence to operational and safety requirements.

> **是什么：** 智能体系统与 LLM 运行于复杂动态环境，表现可能随时间下滑；其概率性与非确定性使传统软件测试不足以保证可靠性。评估动态多智能体系统挑战很大：系统与环境持续变化，需要自适应测试与能衡量超越个体表现的协作成效的复杂指标。部署后可能出现数据漂移、意外交互、工具调用与偏离既定目标等问题，因此需要持续评估以度量有效性、效率及对运营与安全要求的遵守。

**Why:** A standardized evaluation and monitoring framework provides a systematic way to assess and ensure the ongoing performance of intelligent agents. This involves defining clear metrics for accuracy, latency, and resource consumption, like token usage for LLMs. It also includes advanced techniques such as analyzing agentic trajectories to understand the reasoning process and employing an LLM-as-a-Judge for nuanced, qualitative assessments. By establishing feedback loops and reporting systems, this framework allows for continuous improvement, A/B testing, and the detection of anomalies or performance drift, ensuring the agent remains aligned with its objectives.

> **为什么：** 标准化的评估与监控框架为衡量并保障智能体持续表现提供系统方法：包括为准确率、延迟与资源消耗（如 LLM 的 token 用量）定义清晰指标；以及分析智能体轨迹以理解推理过程、使用 LLM-as-a-Judge 做细粒度质性评估等高级技术。通过反馈回路与报告制度，支持持续改进、A/B 测试以及异常或性能漂移检测，使智能体与目标保持一致。

**Rule of Thumb:** Use this pattern when deploying agents in live, production environments where real-time performance and reliability are critical. Additionally, use it when needing to systematically compare different versions of an agent or its underlying models to drive improvements, and when operating in regulated or high-stakes domains requiring compliance, safety, and ethical audits. This pattern is also suitable when an agent's performance may degrade over time due to changes in data or the environment (drift), or when evaluating complex agentic behavior, including the sequence of actions (trajectory) and the quality of subjective outputs like helpfulness.

> **经验法则：** 在实时性能与可靠性至关重要的生产环境部署智能体时使用本模式；在需要系统比较不同智能体版本或底层模型以驱动改进时使用；在受监管或高风险、需合规、安全与伦理审计的场景使用；在数据或环境变化可能导致表现下滑（漂移）时，或在评估复杂智能体行为（含行动序列轨迹与主观输出如「有用性」的质量）时使用。

**Visual Summary:**

> **图示摘要：**

![Evaluation and Monitoring Design Pattern](../assets-new/Evaluation_and_Monitoring_Design_Pattern.png)

Fig.4: Evaluation and Monitoring design pattern

> 图 4：评估与监控设计模式

## Key Takeaways

> ## 关键要点

* Evaluating intelligent agents goes beyond traditional tests to continuously measure their effectiveness, efficiency, and adherence to requirements in real-world environments.  
* Practical applications of agent evaluation include performance tracking in live systems, A/B testing for improvements, compliance audits, and detecting drift or anomalies in behavior.  
* Basic agent evaluation involves assessing response accuracy, while real-world scenarios demand more sophisticated metrics like latency monitoring and token usage tracking for LLM-powered agents.  
* Agent trajectories, the sequence of steps an agent takes, are crucial for evaluation, comparing actual actions against an ideal, ground-truth path to identify errors and inefficiencies.  
* The ADK provides structured evaluation methods through individual test files for unit testing and comprehensive evalset files for integration testing, both defining expected agent behavior.  
* Agent evaluations can be executed via a web-based UI for interactive testing, programmatically with pytest for CI/CD integration, or through a command-line interface for automated workflows.  
* In order to make AI reliable for complex, high-stakes tasks, we must move from simple prompts to formal "contracts" that precisely define verifiable deliverables and scope. This structured agreement allows the Agents to negotiate, clarify ambiguities, and iteratively validate its own work, transforming it from an unpredictable tool into an accountable and trustworthy system.

> * 评估智能体超越传统测试，需在真实环境中持续度量有效性、效率与对要求的遵守。  
> * 实际应用包括线上性能跟踪、改进型 A/B 测试、合规审计以及检测行为漂移或异常。  
> * 基础评估可看回复准确性；真实场景常需延迟监控、LLM 智能体的 token 跟踪等更复杂指标。  
> * 智能体轨迹（步骤序列）对评估至关重要：将实际行动与理想真值路径对比以发现错误与低效。  
> * ADK 通过单测用测试文件、集成测用 evalset 文件提供结构化评估，二者均定义期望行为。  
> * 评估可通过 Web UI 交互、pytest 程序化（对接 CI/CD）或命令行自动化执行。  
> * 要使 AI 在复杂高风险任务上可靠，需从简单提示走向精确定义可验证交付物与范围的正式「合约」；结构化协议使智能体能协商、澄清歧义并迭代自证，将不可预测工具变为可问责、可信赖的系统。

## Conclusions

> ## 结论

In conclusion, effectively evaluating AI agents requires moving beyond simple accuracy checks to a continuous, multi-faceted assessment of their performance in dynamic environments. This involves practical monitoring of metrics like latency and resource consumption, as well as sophisticated analysis of an agent's decision-making process through its trajectory. For nuanced qualities like helpfulness, innovative methods such as the LLM-as-a-Judge are becoming essential, while frameworks like Google's ADK provide structured tools for both unit and integration testing. The challenge intensifies with multi-agent systems, where the focus shifts to evaluating collaborative success and effective cooperation.

> 总之，有效评估 AI 智能体需要超越单一准确率检查，在动态环境中对其表现做持续、多维度衡量：既要实务监控延迟与资源消耗，也要通过轨迹深入分析决策过程。对「有用性」等细腻品质，LLM-as-a-Judge 等方法日益重要；Google ADK 等框架则为单元与集成测试提供结构化工具。多智能体系统使挑战加剧，焦点转向协作成效与有效配合。

To ensure reliability in critical applications, the paradigm is shifting from simple, prompt-driven agents to advanced "contractors" bound by formal agreements. These contractor agents operate on explicit, verifiable terms, allowing them to negotiate, decompose tasks, and self-validate their work to meet rigorous quality standards. This structured approach transforms agents from unpredictable tools into accountable systems capable of handling complex, high-stakes tasks. Ultimately, this evolution is crucial for building the trust required to deploy sophisticated agentic AI in mission-critical domains.

> 为在关键应用中保证可靠性，范式正从简单提示驱动智能体转向受正式协议约束的高级「承包商」。承包商在明确、可验证条款下运作，能协商、分解任务并自我校验以满足严格质量标准。该结构化路径将智能体从难预测工具变为可问责系统，足以承担复杂高风险任务；这一演进对建立信任、在关键任务领域部署高阶智能体 AI 至关重要。

## References

Relevant research includes:

1. ADK Web: [https://github.com/google/adk-web](https://github.com/google/adk-web)
2. ADK Evaluate: [https://google.github.io/adk-docs/evaluate/](https://google.github.io/adk-docs/evaluate/)  
3. Survey on Evaluation of LLM-based Agents, [https://arxiv.org/abs/2503.16416](https://arxiv.org/abs/2503.16416)
4. Agent-as-a-Judge: Evaluate Agents with Agents, [https://arxiv.org/abs/2410.10934](https://arxiv.org/abs/2410.10934)
5. Agent Companion, gulli et al: [https://www.kaggle.com/whitepaper-agent-companion](https://www.kaggle.com/whitepaper-agent-companion)

