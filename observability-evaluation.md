# Observability

### Understanding Observability in the Context of AI Agents

In the realm of artificial intelligence, observability is the practice of gaining deep, real-time insights into the internal state and behavior of an AI agent based on the data it generates. It's about moving beyond simply knowing *if* an agent succeeded or failed and understanding *why* it behaved the way it did. This is crucial for debugging, optimizing, and ensuring the reliability of these complex and often unpredictable systems.

Think of it as having a comprehensive toolkit to ask any question about your AI agent's performance and getting a clear, data-backed answer. For AI agents, which can be highly autonomous and non-deterministic, this level of insight is not just beneficial—it's essential for building trust and ensuring they operate safely and effectively.

### Why Standard Monitoring Isn't Enough

Traditional monitoring often focuses on predefined metrics, like CPU usage or error rates. This approach is effective for predictable systems but falls short for AI agents. The key difference lies in the nature of the systems:

*   **Predictable Systems (Traditional Software):** You know the likely points of failure and can set up alerts for them. For example, "Alert me if API response time exceeds 500ms."
*   **Unpredictable Systems (AI Agents):** The potential failure modes are vast and often unknown beforehand. An AI agent's decision-making process can be opaque, and its interactions with other systems, tools, and users can lead to unexpected outcomes. You don't always know what you need to look for until a problem occurs.

This is where observability shines. It provides the granular data needed to explore the unknown and diagnose novel issues as they arise.

### The Three Pillars of Observability for AI Agents

Observability is typically built on three core types of data that, when combined, provide a complete picture of the agent's operations:

1.  **Traces:** Traces are the cornerstone of AI agent observability. They provide a detailed, step-by-step record of an entire workflow or task execution. For an AI agent, a single trace might capture:
    *   The initial prompt or user request.
    *   Each thought or reasoning step the agent took.
    *   Any tools or APIs the agent decided to use (e.g., calling a search engine, accessing a database).
    *   The inputs and outputs of each tool call.
    *   The final response generated for the user.
    By examining these detailed traces, developers can pinpoint the exact moment a failure occurred or where the agent went off track.

2.  **Logs:** Logs provide discrete, timestamped records of specific events. In the context of AI agents, logs can capture important information such as:
    *   Errors encountered during an API call.
    *   Moderation flags for generated content (e.g., identifying toxic or inappropriate language).
    *   Latency measurements for specific operations.
    *   User feedback events (e.g., a user clicking "thumbs up" or "thumbs down" on a response).

3.  **Metrics:** Metrics are numerical representations of data aggregated over a period of time. They offer a high-level overview of the agent's health and performance. Key metrics for AI agents include:
    *   **Task Success Rate:** The percentage of tasks the agent completes successfully.
    *   **Cost Per Run:** The computational cost (e.g., tokens used) for each task.
    *   **Tool Usage Frequency:** How often specific tools are being utilized by the agent.
    *   **Latency:** The average time it takes for the agent to complete a task.
    *   **User Satisfaction Scores:** Aggregated feedback from users.

### What Does Observability Enable for AI Agents?

By implementing robust observability, teams building and deploying AI agents can:

*   **Rapidly Debug Failures:** When an agent produces an incorrect or nonsensical result, developers can follow the trace to understand its reasoning process and identify the root cause, whether it was a flawed prompt, a malfunctioning tool, or a "hallucination" by the language model.
*   **Optimize Performance and Cost:** By analyzing metrics on latency and token usage, developers can identify inefficiencies in the agent's workflow and optimize prompts or tool interactions to make the agent faster and more cost-effective.
*   **Evaluate and Improve Quality:** Observability platforms allow for the evaluation of agent responses against predefined criteria, such as relevance, coherence, and helpfulness. This is often done using a combination of human feedback and "LLM-as-a-judge" techniques where another AI scores the agent's output.
*   **Ensure Safety and Compliance:** By logging and monitoring the agent's outputs, teams can detect and prevent harmful or biased behavior, ensuring the agent adheres to safety guidelines and ethical principles.
*   **Enhance User Experience:** Understanding how users interact with the agent and analyzing their feedback helps in refining the agent's behavior to better meet user needs and expectations.

In essence, observability transforms the "black box" of an AI agent's decision-making process into a more transparent and manageable system. As AI agents become more integrated into our daily lives and critical business operations, this ability to observe, understand, and guide their behavior is fundamental to harnessing their full potential responsibly.


# Evaluation

### Evaluating AI Agents: A Deep Dive into Ensuring Performance and Trustworthiness

In the rapidly advancing field of artificial intelligence, AI agents are emerging as powerful tools capable of autonomously performing complex tasks, making decisions, and interacting with users and systems. From customer service chatbots to sophisticated systems managing critical infrastructure, the reliability and effectiveness of these agents are paramount. This has led to the crucial practice of AI agent evaluation, a systematic process of assessing how well an autonomous agent performs its designated functions.

At its core, the evaluation of AI agents is about understanding their behavior, capabilities, and limitations in various contexts. This process is essential for several reasons: it verifies that agents are meeting their intended goals, identifies areas for improvement, and ensures they operate safely, ethically, and in alignment with user expectations. Without rigorous evaluation, deploying AI agents into real-world scenarios would be a shot in the dark, potentially leading to inefficiencies, errors, and even harmful outcomes.

### Key Metrics for a Thorough Evaluation

To comprehensively assess an AI agent's performance, a variety of metrics are employed, often categorized into several key areas:

**1. Performance and Efficiency:** These metrics quantify how effectively and efficiently an agent completes its tasks.
*   **Success/Task Completion Rate:** This fundamental metric measures the percentage of tasks an agent successfully completes.
*   **Accuracy:** This assesses how closely the agent's output aligns with the desired or correct result.
*   **Error Rate:** The percentage of incorrect outputs or failed operations provides insight into the agent's reliability.
*   **Latency and Response Time:** These metrics measure the speed of the agent, from the time it takes to process a request to delivering a final response. Low latency is critical for a positive user experience.
*   **Cost and Resource Utilization:** In the context of large language models (LLMs), this often refers to the computational expense, such as the number of tokens used or API calls made.

**2. Quality of Interaction and Response:** For agents that interact with users, the quality of that interaction is crucial.
*   **Relevance and Coherence:** This evaluates whether the agent's responses are logical, on-topic, and contextually appropriate.
*   **Hallucinations:** A significant concern with LLM-based agents, this metric checks for instances where the agent generates information not based on provided data or factual reality.
*   **Toxicity:** This metric identifies any inappropriate, offensive, or harmful content generated by the agent.
*   **Sentiment Analysis:** This gauges the emotional tone of the agent's responses to ensure they are appropriate for the context of the interaction.

**3. Robustness and Reliability:** These metrics assess the agent's stability and consistency.
*   **Robustness:** This measures how well the agent performs under unexpected or challenging conditions, including edge cases and adversarial inputs.
*   **Reliability:** This refers to the consistency of the agent's performance across multiple runs and over time.

**4. Ethical Considerations:** As AI agents become more autonomous, ensuring they adhere to ethical principles is vital.
*   **Fairness and Bias:** This evaluates whether the agent exhibits any unfair biases in its decisions and outputs across different user groups.
*   **Safety and Policy Compliance:** This ensures the agent avoids harmful behaviors and adheres to predefined operational policies and safety guidelines.

### Diverse Methods for Comprehensive Evaluation

A multi-faceted approach to evaluation is necessary to capture the complexity of AI agent behavior. Key methods include:

*   **Automated Benchmarks:** Standardized test suites, known as benchmarks, provide a consistent and scalable way to evaluate agents. These benchmarks often consist of a set of tasks and datasets designed to test specific capabilities in a reproducible manner. Popular examples include AgentBench for reasoning and decision-making, WebArena for web-based tasks, and GAIA for general AI assistants.

*   **LLM-as-a-Judge:** This emerging technique uses a powerful large language model to automatically assess the performance of another AI agent. By providing the "judge" LLM with predefined criteria and metrics, it can score an agent's responses for qualities like coherence, relevance, and accuracy. This method offers a scalable alternative to manual human evaluation.

*   **Human-in-the-Loop (HITL) Evaluation:** Despite advancements in automated methods, human judgment remains the gold standard for evaluating nuanced aspects of agent performance, such as the quality of user experience and the appropriateness of responses. HITL involves incorporating human feedback directly into the evaluation process to refine and correct the AI's behavior. This can involve humans rating the quality of agent outputs, identifying errors, and providing corrective feedback.

*   **Real-World Simulations:** Creating high-fidelity simulations of the environments where the AI agent will operate allows for testing its performance in a controlled yet realistic setting. This is particularly important for agents designed for high-stakes domains like healthcare, where real-world deployment carries significant risks.

### The Challenges of Evaluating Autonomous Systems

The evaluation of AI agents is not without its difficulties. Their autonomy and the complexity of their interactions with dynamic environments pose unique challenges.

*   **The Evolving Nature of Agents:** Unlike traditional software, AI agents can learn and adapt over time, making it difficult to establish a fixed performance baseline. Their behavior can be non-deterministic, meaning they may not produce the same output for the same input every time.
*   **Defining "Success":** For complex, open-ended tasks, defining a clear and measurable definition of success can be challenging.
*   **The Cost and Effort of Evaluation:** Rigorous evaluation, especially involving human assessors, can be time-consuming and expensive.
*   **Real-World Complexity:** It is difficult to create evaluation scenarios that fully capture the unpredictability and diversity of real-world situations.

### The Practical Steps of AI Agent Evaluation

A structured approach to evaluation is crucial for obtaining meaningful results. The process typically involves:

1.  **Defining Clear Goals:** The first step is to establish specific, measurable goals for the agent that align with business or user objectives.
2.  **Selecting Relevant Metrics:** Based on the defined goals, appropriate metrics are chosen to measure the agent's performance against those objectives.
3.  **Preparing Test Data:** Representative datasets and test scenarios are created to reflect real-world conditions and potential user interactions.
4.  **Choosing the Right Tools and Methods:** The appropriate evaluation methods, whether automated benchmarks, LLM-as-a-judge, or human evaluation, are selected.
5.  **Analyzing Results and Iterating:** The collected data is analyzed to identify areas for improvement. This analysis then informs the next cycle of development and refinement.

### The Future of AI Agent Evaluation

The field of AI agent evaluation is continuously evolving to keep pace with the advancements in AI technology. Future trends include:

*   **Standardized Benchmarks:** Efforts are underway to develop more comprehensive and standardized benchmarks to allow for fairer and more consistent comparisons between different agents.
*   **Continuous Evaluation:** Moving beyond one-off assessments, the focus is shifting towards continuous evaluation pipelines that monitor agent performance in real-time and trigger retraining or adjustments as needed.
*   **Focus on Safety and Trustworthiness:** As agents become more autonomous, there is a growing emphasis on developing robust methods for evaluating their safety, reliability, and ethical compliance.

In conclusion, the evaluation of AI agents is a critical and multifaceted process that is essential for building trustworthy and effective AI systems. By employing a combination of rigorous metrics and diverse evaluation methods, developers and researchers can ensure that these powerful new technologies are deployed responsibly and deliver on their promise to augment human capabilities and solve real-world problems.


### Agent Evaluation != Model Evaluation

|Language Model Evaluation  |   Agent Evaluation    |
|---------------------------|-----------------------|
|Evaluation consists of input and output strings | Evaluation consists of agents taking action on some environment |
|Cost limited to the i/p and o/p token length of LLM | Cost can be unbounded |
|A single language model can be evaluated on multiple benchmarks | Task-specific agents are purpose built for a single type of task and benchmark |

# Tool Comparison

| Feature / Attribute                | **LangSmith**                                                                                                                                                                                          | **Arize**                                                                                                                                                                          | **Langtrace**                                                                                                                                                                  |
| ---------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **Platform Type**                  | Commercial SaaS (by LangChain), with hybrid & self‑host deployment options ([LangChain][1])                                                                                                            | Commercial ML observability platform (ML & LLM), SaaS plus open-source offerings ([Walturn][2], [Langfuse][3])                                                                     | Fully open-source (MIT‑style) observability tool with hosted version optional ([Langtrace][4], [Reddit][5])                                                                    |
| **Tracing / Observability**        | Deep tracing of LangChain agent workflows; step‑by‑step trace viewer & root cause debugging ([LangChain][1], [LangChain Blog][6])                                                                      | Supports interactive performance tracing for embeddings & prediction; drift and performance tracking ([Walturn][2])                                                                | OTEL‑based tracing that surfaces deep traces across the LLM pipeline (model, frameworks, vectorDB) ([Langtrace][4], [Reddit][7])                                               |
| **Evaluation & Feedback**          | Built‑in LLM‑as‑Judge automated evaluations plus human‑in‑the‑loop scoring; Playground UI for prompt comparisons ([LangChain][1], [Walturn][2])                                                        | Strong evaluation tooling: embedding drift, classification feedback loops, bias detection, curated data support ([Walturn][2], [Langfuse][3])                                      | Enables annotation queues and dataset creation from traced interactions; Playground support for prompt testing ([Langtrace][4], [Reddit][8])                                   |
| **Monitoring & Metrics**           | Live monitoring dashboards for latency, cost, error rate, feedback scores; custom alerting via webhooks/PagerDuty ([LangChain Blog][9], [LangChain Blog][6])                                           | Rich monitoring: drift detection for embeddings/features, performance over time, alerting on anomalies ([Walturn][2])                                                              | Basic metrics tracking (token usage, latency, etc.) surfaced via OTEL; relies on integration with external dashboards for metrics visualization ([Reddit][10], [Langtrace][4]) |
| **Custom Alerts & Automations**    | Alerts on key metrics (error/latency/feedback), advanced filters, aggregations, and custom automations; sampling automations to dataset or annotation queue ([LangChain Blog][9], [LangChain Blog][6]) | Offers drift-based alerts, embedding anomalies, and rule-based performance alerting ([Walturn][2])                                                                                 | Doesn’t ship built-in alert frameworks—depends on external observability infrastructure to generate alerts from OTEL traces ([Langtrace][4], [Reddit][11])                     |
| **Prompt Management / Playground** | Prompt Canvas & Playground to build, test, and iterate prompts across models with team collaboration ([LangChain][1], [Walturn][2])                                                                    | Offers experiment tracking and prompt comparison within model evaluation workflows ([Walturn][2])                                                                                  | Provides a prompt playground for side‑by‑side testing across models/settings ([Reddit][8], [Langtrace][4])                                                                     |
| **Deployment Model**               | Fully managed or self‑hosted (enterprise plan); works with or without LangChain; supports OTEL SDKs ([LangChain][1], [IBM][12])                                                                        | Cloud‑hosted SaaS plus open‑source "Arize Phoenix" for self‑hosted use (depending on license) ([Walturn][2], [Langfuse][3])                                                        | Fully open‑source and self‑hosted; hosted free tier currently available; no vendor lock‑in ([Reddit][5], [Langtrace][4])                                                       |
| **Data Ownership & Security**      | Customer owns data; no training on data; supports SOC 2 Type II; GCP‑based regions for storage ([LangChain][1], [IBM][12])                                                                             | Enterprise‑grade compliance available; suitable for regulated industries ([Walturn][2])                                                                                            | SOC 2 Type II certified on hosted offering; self‑hosting puts all data in your own environment ([Langtrace][4])                                                                |
| **Ideal Use Cases**                | Teams building LangChain/agent workflows; need unified tracing, evaluation, prompt experimentation, and alerts in one package ([Walturn][2], [LangChain][1])                                           | Organizations operating both traditional ML and LLM workloads that require embedding drift detection, bias mitigation, and strong evaluation tooling ([Walturn][2], [Langfuse][3]) | Open‑source adopters who desire full transparency, flexible custom tooling, and deep OTEL‑based observability at minimal cost ([Langtrace][4], [Reddit][5])                    |
| **Pros**                           | ✅ Comprehensive end‑to‑end LLM workflow observability<br>✅ Team‑friendly collaboration via prompts and feedback<br>✅ Alerting & automation built‑in                                                    | ✅ Broad model support beyond LLMs<br>✅ Advanced drift detection, bias/embedding evaluation<br>✅ Scalable enterprise usage                                                          | ✅ Fully open‑source and extensible<br>✅ Deep OTEL compliance and integration<br>✅ Very easy 2‑line setup, minimal vendor lock‑in                                               |
| **Cons**                           | ❌ Biz‑tier pricing at scale<br>❌ Focus mostly on LangChain-based workflows (<i>less generic stack support</i>)                                                                                         | ❌ Commercial pricing may be high<br>❌ Some features more focused on non-agent ML workflows                                                                                         | ❌ No built‑in alerting/dashboarding (requires external infra)<br>❌ Self‑hosted monitoring requires ops investment                                                              |

[1]: https://www.langchain.com/langsmith?utm_source=chatgpt.com "LangSmith"
[2]: https://www.walturn.com/insights/ai-observability-stack-for-monitoring-and-debugging-llms?utm_source=chatgpt.com "AI Observability Stack for Monitoring and Debugging LLMs"
[3]: https://langfuse.com/faq/all/ai-research-assistant-monitoring?utm_source=chatgpt.com "Monitoring AI Research Assistants - Ensuring Accuracy and Reliability - Langfuse"
[4]: https://langtrace.ai/?utm_source=chatgpt.com "Langtrace AI"
[5]: https://www.reddit.com/r/LangChain/comments/1bv4nzb?utm_source=chatgpt.com "Update: Langtrace Launch: Opensource LLM monitoring tool - achieving better cardinality compared to Langsmith."
[6]: https://blog.langchain.com/langsmith-production-logging-automations?utm_source=chatgpt.com "LangSmith: Production Monitoring & Automations"
[7]: https://www.reddit.com/r/LangChain/comments/1eh0ly3?utm_source=chatgpt.com "Spoke to 22 LangGraph devs and here's what we found"
[8]: https://www.reddit.com/r/LangChain/comments/1cmk0dn?utm_source=chatgpt.com "Langtrace - Added support for Prompt Playground"
[9]: https://blog.langchain.com/langsmith-alerts?utm_source=chatgpt.com "Catch production failures early with LangSmith Alerts"
[10]: https://www.reddit.com/r/ChatGPTCoding/comments/1bwm2tj?utm_source=chatgpt.com "I built an open source LLM monitoring & evaluation tool. It helps with monitoring token usage and latency. You can also evaluate responses to measure accuracy and improve it."
[11]: https://www.reddit.com/r/LLMDevs/comments/1feb51m?utm_source=chatgpt.com "How do you monitor your LLM models in prod?"
[12]: https://www.ibm.com/think/topics/langsmith?utm_source=chatgpt.com "What is LangSmith? | IBM"


As an AI Expert, here is a detailed comparison of LangSmith, Arize AI, and Langfuse, focusing on the aspects most critical for developers and teams building with large language models.

### Detailed Comparison: LangSmith vs. Arize AI vs. Langfuse

| Feature | LangSmith | Arize AI | Langfuse |
| :--- | :--- | :--- | :--- |
| **Primary Focus** | A unified, developer-first platform for the entire LLM application lifecycle: debugging, testing, evaluating, and monitoring, with deep roots in the LangChain ecosystem. | An enterprise-grade ML observability platform for both traditional machine learning models and modern LLM/GenAI applications, with a strong focus on production monitoring and troubleshooting at scale. | An open-source LLM engineering platform designed for collaborative development, providing deep insights into traces, evaluations, and prompt management to improve application quality. |
| **Ideal User** | Developers and teams of all sizes, especially those heavily invested in the LangChain or LangGraph frameworks, who need a seamless, end-to-end development and observability solution. | Data scientists, ML engineers, and large enterprises that need a robust, scalable solution to monitor and manage a diverse portfolio of AI models (including LLMs) in high-stakes production environments. | Developers and teams looking for a flexible, open-source, and self-hostable solution that offers granular control and a collaborative environment for building and refining complex LLM applications. |
| **Core Strength** | **Seamless Integration & Developer Experience.** Its tight coupling with LangChain makes instrumenting and debugging incredibly fast and intuitive. The platform is designed to mirror the developer's workflow from prototype to production. | **Production-Grade Observability & Troubleshooting.** Excels at real-time performance monitoring, drift detection, and root cause analysis in production. Its analytics and dashboards are built for large-scale, critical deployments. | **Open-Source Flexibility & Granular Control.** Being fully open-source provides maximum flexibility and avoids vendor lock-in. It offers detailed tracing and a collaborative UI designed for engineering teams to work together on prompt and model improvements. |
| **Tracing & Debugging** | Provides highly detailed, hierarchical traces that visualize the full execution path of chains and agents. Allows developers to see every step, input, output, and tool call, making it easy to pinpoint errors. | Offers powerful tracing and analytics for production issues. Enables troubleshooting by filtering on model performance, data drift, or user segments. Its open-source library, **Phoenix**, is a powerful tool for tracing and evaluation in development environments. | Delivers granular tracing with detailed insights into latency, token usage, and costs for each step of an LLM call. The user interface is explicitly designed for collaborative debugging among team members. |
| **Evaluation & Testing** | Features a comprehensive and user-friendly evaluation suite. Supports creating datasets, running evaluators (including custom ones and "LLM-as-a-Judge"), and comparing results over time. Fully integrated with tracing for easy failure analysis. | Provides a robust evaluation framework for both offline (pre-production) and online (production) testing. Supports programmatic evaluations and LLM-as-a-judge for metrics like hallucination detection and RAG quality. Strong focus on tracking evaluation metrics over time. | Offers a flexible evaluation module where users can score traces manually or programmatically. Allows for creating and managing datasets for running batch evaluations. The results are tied directly to traces for easy analysis. |
| **Monitoring** | Includes dashboards for monitoring key operational metrics like latency, cost per trace, and error rates. Users can also track custom business metrics and user feedback signals (e.g., thumbs up/down). | This is its primary strength. Offers real-time monitoring of model performance, data quality, and drift with highly customizable dashboards and automated alerting. Essential for managing models in production. | Provides dashboards to track key metrics like token usage, cost, latency, and quality scores over time. This helps teams monitor trends and make data-driven decisions about their applications. |
| **Prompt & Model Management** | Includes the "LangSmith Hub" (formerly Prompt Hub), a central place to discover, version, and share prompts. The "Playground" allows for rapid, collaborative iteration on prompts and models. | Offers prompt management capabilities within its broader platform, allowing teams to version prompts and analyze their performance in production. The focus is on linking prompt versions to production outcomes. | Features a dedicated prompt management system to version control, manage, and deploy prompts. Allows for easy comparison of different prompt versions and rolling back if performance degrades. |
| **Open Source Model** | **Closed-source product.** While it integrates with open-source LangChain, the LangSmith platform itself is a proprietary, hosted service. A self-hosted option is available for enterprise plans. | **Hybrid model.** The core Arize AI platform is a commercial product. However, its powerful **Phoenix** library for tracing, evaluation, and data analysis is fully open-source and can be used independently. | **Fully open-source.** The entire Langfuse platform is open-source (MIT License), allowing for self-hosting, customization, and community contributions. This is a key differentiator for teams wanting to avoid vendor lock-in. |
| **Integrations** | Deepest possible integration with **LangChain** and **LangGraph**. Also supports any LLM framework through its SDKs and is compatible with OpenTelemetry for broader observability. | Extensive integrations with the entire MLOps stack, including cloud platforms (Vertex AI, SageMaker, AzureML), data warehouses, and major LLM frameworks like LangChain, LlamaIndex, and OpenAI SDKs. | Broad compatibility with major LLM providers (OpenAI, Anthropic, etc.), frameworks (LangChain, LlamaIndex, LiteLLM), and vector databases. It is built on top of OpenTelemetry, making it interoperable with other observability tools. |
| **Pricing Structure** | Offers a generous free "Developer" plan for individuals. Paid "Plus" plan is priced per seat with usage-based costs for traces. Custom "Enterprise" plan is available. | Offers a free tier for individual developers and the open-source Phoenix library. Paid plans ("Pro" and "Enterprise") are designed for teams and large-scale production use, with pricing based on volume and features. | The open-source version is free when self-hosted. They also offer a managed cloud service with a generous free tier for getting started, followed by usage-based pricing for larger teams. |

## Retrieval Augemented Generation (RAG) Evaluation

- Metrics for Retrieval
    - faithfulness : Answers should be grounded in the context. The LLM should not answer if the answer is not in the context. This helps reduce hallucinations. **Answer -> Context**
    - context_precision : **Question -> Context**
    - context_relevancy : The context supplied should be focused, and contain as little irrelevant information as possible. If contexts are too long, LLMs tend to be less effective in general
    - context_recall : **Ground Truth -> Context**


- Format


|Question   | Answer    | Context   | Ground Truth  |
|-----------|-----------|-----------|---------------|

- Metrics for Generation
    - faithfulness
    - answer_relevancy : Answers should address the question that was provided. **Question -> Answer**
    - answer_similarity
    - answer_correctness


## Evaluation Techniques

### LLM-as-a-Judge

Key considerations when using LLM as a Judge

- Will not be 100% correct
- Only the best models align closely with human judgement
- Tuning your LLM judge prompt can help close this gap
- Always use discrete classification labels, never an undefined score
    - Incorrect vs correct, not 1%-100% accuracy


### Code Evals

Code run on the outputs of the application. Examples of code evaluators

- Matches regex
    - e.g., response only contains numbers
- JSON parseable
- Contains Keyword(s)
    - e.g., response contains competitor name
- Output matches the expected one
    - Either a direct match or a semantic match
- Check if the generated code is runnable

### Human Annotations

Add human evaluation labels to your traces:

- Using annotation queues and human labelers
- Using :+1: :-1: response from users


### Advanced Evals: Agent as a Judge

Framework components for a coding agent

- Graph : Constructs a graph of the project
- Locate : Identifies the folders and files specified by requirements
- Read : reads files and understands data
- Search : find relevant code snippets
- Retrieve : extracts info from long texts
- Ask : decides whether requirements are satisfied
- Memory : store historical judgement information
- Planning : plans the agent's path



### Advanced Evals: Trajectory, Planning, Reflection

|Eval Type      | Purpose       | Technique(s)      |
|---------------|---------------|-------------------|
|Planning       | Evaluate the plan generated by an agent before calling | LLM as a judge |
|Reflection     | Decide whether to repeat the previous step | LLM as a judge, code based |
|Trajectory     | Determine whether the optimal path was taken by the agent overall | LLM as a judge, Comparison against human labels |