# Module 4 Study Guide
## AAIT261 | AWS Certified AI Practitioner (AIF-C01)

This study guide covers Module 4 content: Task Statement 2.3 (AWS Infrastructure and Technologies for Generative AI) and Task Statement 3.1 (Design Considerations for Foundation Model Applications). Together, these topics connect the conceptual understanding of generative AI from Module 3 to the practical AWS services and architectural patterns used to build real applications.

---

## Part 1: Task Statement 2.3 — AWS Infrastructure for Generative AI

### Amazon Bedrock

**Amazon Bedrock** is the primary AWS service for building generative AI applications. It is a fully managed service that provides access to a curated selection of high-performing foundation models from AWS and leading AI providers through a single API.

Key characteristics of Amazon Bedrock:
- **Serverless:** No infrastructure to provision or manage. You pay only for the tokens you process.
- **Multi-model access:** Access models from Amazon (Titan), Anthropic (Claude), Meta (Llama), Cohere, AI21 Labs, Mistral, and others through a unified API.
- **Privacy by default:** Your data is not used to train the underlying foundation models. Inputs and outputs are not shared with model providers.
- **Integrated tooling:** Bedrock includes Knowledge Bases (RAG), Agents, Guardrails, and Model Evaluation as built-in features.

**What to remember for the exam:** When a scenario describes an organization that wants to build a GenAI application without managing infrastructure, and wants to choose from multiple foundation models, Amazon Bedrock is the answer.

---

### Amazon SageMaker in the GenAI Context

Amazon SageMaker supports generative AI workloads in several ways:

- **SageMaker JumpStart:** A hub of pre-trained models including open-source LLMs (like Llama and Falcon) that can be deployed and fine-tuned within SageMaker.
- **Custom training and fine-tuning:** Organizations that want to fine-tune a foundation model on proprietary data with full control over the training process can do so through SageMaker.
- **MLOps:** SageMaker's pipelines, model registry, and monitoring tools support the deployment and ongoing management of both traditional ML and generative AI models.

**Bedrock vs. SageMaker — when to choose which:**

| Choose Amazon Bedrock when... | Choose Amazon SageMaker when... |
|------------------------------|--------------------------------|
| You want managed access to multiple foundation models with no infrastructure | You need full control over training, fine-tuning, or deployment configuration |
| Speed to production matters and infrastructure management is a burden | You are working with open-source models or custom architectures |
| You want built-in RAG, agents, and guardrails | You need to run your own training jobs or custom ML pipelines |

---

### AWS AI Accelerators: Trainium and Inferentia

AWS has developed its own silicon chips to optimize AI workloads at lower cost and higher efficiency than general-purpose CPUs or even standard GPUs.

| Chip | Primary Use | Description |
|------|------------|-------------|
| **AWS Trainium** | Model **training** | Custom AWS chip designed for the high-compute demands of training large deep learning models. Offers significant cost savings compared to equivalent GPU-based training. Available via Amazon EC2 Trn instances. |
| **AWS Inferentia** | Model **inferencing** | Custom AWS chip optimized for running trained models at low latency and low cost. Designed for high-throughput inferencing workloads. Available via Amazon EC2 Inf instances. |

**Memory aid:** Trainium = **Tr**aining. Inferentia = **Inf**erencing.

---

### Amazon Q

**Amazon Q** is AWS's AI-powered assistant for business and developer use cases. It is built on Amazon Bedrock's foundation models and is available in two primary versions:

| Version | Use Case |
|---------|----------|
| **Amazon Q Business** | An intelligent AI assistant for enterprise employees. Connects to company data sources (SharePoint, S3, Salesforce, etc.) to answer questions using organizational knowledge. Supports role-based access controls. |
| **Amazon Q Developer** | An AI coding assistant for developers. Integrates with IDEs to provide code suggestions, explain code, identify security vulnerabilities, and generate tests. Previously known in part as Amazon CodeWhisperer. |

**What to remember for the exam:** Amazon Q Business is the answer when a scenario describes an organization wanting to give employees a conversational interface to internal company data. Amazon Q Developer is the answer for developer productivity and AI-assisted coding.

---

## Part 2: Task Statement 3.1 — Design Considerations for Foundation Model Applications

### Retrieval-Augmented Generation (RAG)

**RAG** is the most important architectural pattern in Domain 3 and one of the highest-tested topics on the AIF-C01 exam.

**The problem RAG solves:**
Foundation models have a knowledge cutoff and no access to your organization's private or current data. Without augmentation, a model answering questions about your company's policies, products, or recent events will hallucinate or simply admit ignorance.

**How RAG works:**

1. **Index your knowledge base.** Documents (PDFs, web pages, support articles, policies) are chunked into smaller segments, converted into embeddings, and stored in a vector database.
2. **Receive a user query.** When a user asks a question, that query is also converted into an embedding.
3. **Retrieve relevant content.** The vector database finds the document chunks whose embeddings are most similar to the query embedding.
4. **Augment the prompt.** The retrieved content is inserted into the prompt alongside the user's question.
5. **Generate a grounded response.** The foundation model uses the retrieved content as context to generate its answer, reducing hallucination and providing up-to-date information.

**RAG in one sentence:** Give the model a relevant reference document at the moment it needs to answer, so it can generate a grounded response rather than guess.

**AWS implementation:** Knowledge Bases for Amazon Bedrock handles the full RAG pipeline — document ingestion, embedding, vector storage (using Amazon OpenSearch Serverless or other vector stores), retrieval, and augmentation — with minimal configuration.

---

### When to Use RAG vs. Fine-Tuning

This is a common exam comparison. Both RAG and fine-tuning adapt a foundation model to specific content, but they work differently.

| Characteristic | RAG | Fine-Tuning |
|---------------|-----|------------|
| **What it does** | Gives the model access to current documents at inference time | Adjusts the model's weights by training it on specific data |
| **Best for** | Frequently changing information; private/proprietary documents; reducing hallucination on factual questions | Teaching the model a specific style, format, or domain-specific vocabulary |
| **Knowledge updating** | Easy — update the knowledge base without retraining | Hard — requires retraining when information changes |
| **Cost** | Per-query retrieval costs | One-time (but significant) training cost |
| **When info is current** | Always — retrieval happens at query time | Frozen at training time |

**Key exam rule:** If the scenario describes needing up-to-date or frequently changing information, RAG is preferred over fine-tuning.

---

### Guardrails for Amazon Bedrock

**Guardrails** are configurable safety controls for foundation model applications built on Amazon Bedrock.

What Guardrails can do:
- **Topic blocking:** Prevent the model from discussing specified topics (e.g., competitors, political content).
- **Content filtering:** Block harmful content categories — hate speech, violence, sexual content, insults.
- **PII redaction:** Automatically detect and redact personally identifiable information (names, phone numbers, SSNs) from model inputs and outputs.
- **Grounding checks:** Detect and filter responses that are not grounded in the provided source documents (hallucination detection).
- **Word and phrase blocking:** Prevent specific words or phrases from appearing in outputs.

**Why Guardrails matter for the exam:** Guardrails are the answer when a scenario asks how to prevent an LLM application from generating harmful content, discussing prohibited topics, or exposing PII.

---

### Agents for Amazon Bedrock

**Agents for Amazon Bedrock** enable foundation models to take actions in the real world — not just generate text, but plan and execute multi-step tasks.

How Agents work:
1. A user provides a goal in natural language.
2. The agent uses the foundation model to break the goal into steps.
3. For each step, the agent can call external APIs, query databases, retrieve information, or invoke AWS Lambda functions.
4. The agent synthesizes results and continues until the goal is complete.
5. The final response is returned to the user.

**Example:** A user asks an HR chatbot, "What is my remaining vacation balance and can I request time off for the week of December 20?" An agent can: (1) query the HR system for the user's leave balance, (2) check the calendar for the requested week, (3) submit the leave request, and (4) confirm the action to the user — all from a single natural language request.

**What distinguishes agents from standard LLM responses:** Agents can take actions with real-world consequences, not just generate text. This is the defining feature of agentic AI.
