# Module 6 Study Guide
## AAIT261 | AWS Certified AI Practitioner (AIF-C01)

This study guide covers Module 6 content: Task Statement 3.4 (Evaluating Foundation Model Performance) and Task Statement 4.1 (Responsible AI Development). Both topics require you to apply concepts, not just recall them — expect exam questions that present a scenario and ask you to identify the appropriate evaluation approach or identify a responsible AI principle at stake.

---

## Part 1: Task Statement 3.4 — Evaluating Foundation Model Performance

### Why Evaluation Matters

Deploying a foundation model without rigorous evaluation is a significant risk. A model may perform impressively in a demo but fail in production when it encounters the full diversity of real user inputs. Evaluation provides the evidence needed to make deployment decisions confidently.

Foundation models are evaluated differently from traditional ML models because:
- Their outputs are often open-ended text, not a fixed label or number.
- There is often more than one "correct" answer.
- Quality may depend on style, tone, fluency, and factual accuracy simultaneously.

---

### Automated Evaluation Metrics

These metrics compare a model's output to one or more reference (human-written) answers and produce a numerical score.

| Metric | What It Measures | How It Works | Typical Use |
|--------|-----------------|-------------|------------|
| **ROUGE** (Recall-Oriented Understudy for Gisting Evaluation) | Overlap between the model's output and a reference text. Focuses on recall — how much of the reference is captured in the output. | Counts shared n-grams (word sequences) between the output and the reference. Variants: ROUGE-1 (unigrams), ROUGE-2 (bigrams), ROUGE-L (longest common subsequence). | Summarization tasks |
| **BLEU** (Bilingual Evaluation Understudy) | Overlap between the model's output and the reference. Focuses on precision — how much of the output matches the reference. | Counts n-gram matches, penalizing outputs that are much shorter than the reference (brevity penalty). | Machine translation; text generation |
| **BERTScore** | Semantic similarity between output and reference, not just exact word overlap. | Uses BERT embeddings to compare the meaning of sentences rather than counting shared words. Better at capturing paraphrases. | Tasks where meaning matters more than exact wording |

**Memory aid:**
- ROUGE = recall-oriented → used for summarization (did the summary capture the key ideas?)
- BLEU = precision-oriented → used for translation (how much of what was generated was correct?)
- BERTScore = meaning-based → useful when word choice varies but meaning is the same

**Important limitation of automated metrics:** These metrics compare outputs to human-written references. They cannot capture whether the output is factually correct, helpful, safe, or appropriate — only whether it resembles the reference. A model can score well on ROUGE by repeating the reference text verbatim, and score poorly while still producing an excellent response.

---

### Human Evaluation

**Human evaluation** involves trained raters (or end users) assessing model outputs on defined quality dimensions.

Common evaluation dimensions for generative AI:
- **Fluency:** Is the text grammatically correct and readable?
- **Coherence:** Does the text make logical sense throughout?
- **Relevance:** Does the output actually address the question or task?
- **Factual accuracy:** Is the information correct and grounded?
- **Helpfulness:** Would a real user find this useful?
- **Safety:** Does the output avoid harmful, biased, or offensive content?

**Advantages of human evaluation:**
- Can assess qualities that automated metrics miss (helpfulness, safety, appropriateness)
- Is the gold standard for evaluating open-ended text

**Limitations of human evaluation:**
- Expensive and time-consuming
- Subject to inter-rater variability (different raters may reach different conclusions)
- Does not scale easily to continuous production monitoring

---

### Benchmark Datasets

**Benchmark datasets** are standardized evaluation sets used to compare model performance across the AI research community.

| Benchmark | What It Tests |
|-----------|--------------|
| **MMLU** (Massive Multitask Language Understanding) | Knowledge and reasoning across 57 academic subjects including math, law, medicine, and science |
| **HellaSwag** | Commonsense reasoning and sentence completion |
| **TruthfulQA** | Tendency to produce truthful answers rather than plausible-sounding falsehoods |
| **HumanEval** | Code generation ability, evaluated by running the generated code against test cases |

**Why benchmarks matter for the exam:** Benchmarks allow fair, standardized comparisons between models. When AWS or a third-party provider publishes model comparison tables, benchmark scores are typically the basis.

---

### Amazon Bedrock Model Evaluation

**Amazon Bedrock Model Evaluation** is a built-in tool that allows organizations to evaluate and compare foundation models available in Bedrock using their own prompts and use cases.

Capabilities:
- **Automatic evaluation:** Uses built-in metrics to score model outputs on accuracy, robustness, toxicity, and other dimensions.
- **Human evaluation:** Routes model outputs to human reviewers (internal or via Amazon Mechanical Turk) for subjective quality ratings.
- **Custom evaluation datasets:** Organizations can upload their own prompt-response pairs to evaluate models against their specific use case.
- **Model comparison:** Evaluate multiple models side by side on the same dataset to identify which performs best for the task.

---

## Part 2: Task Statement 4.1 — Responsible AI Development

### What Is Responsible AI?

**Responsible AI** refers to the principles, practices, and processes that ensure AI systems are developed and deployed in ways that are safe, ethical, fair, and aligned with human values. It is not optional — it is a professional and, increasingly, a legal requirement.

AWS identifies seven dimensions of responsible AI:

| Dimension | Definition |
|-----------|-----------|
| **Fairness** | AI systems should treat all individuals and groups equitably, without discriminating based on protected characteristics such as race, gender, age, or disability. |
| **Explainability** | AI systems should be able to provide understandable reasons for their outputs, decisions, or recommendations. |
| **Privacy and security** | AI systems should protect the personal data used to train and operate them, and defend against misuse and unauthorized access. |
| **Safety** | AI systems should operate as intended and avoid causing physical, psychological, financial, or reputational harm. |
| **Controllability** | Humans should be able to monitor, adjust, correct, override, or shut down AI systems. |
| **Veracity and robustness** | AI systems should perform reliably and consistently under a variety of conditions, including adversarial inputs. |
| **Governance** | Organizations should have clear policies, processes, and accountability structures for how AI systems are developed and deployed. |

---

### Bias in AI Systems

**Bias** occurs when an AI system produces systematically unfair or discriminatory outputs. Bias can enter at multiple stages:

| Source of Bias | Description | Example |
|----------------|-------------|---------|
| **Training data bias** | The training data over-represents or under-represents certain groups, reflecting historical inequities. | A hiring model trained on historical hiring decisions inherits past discrimination against certain demographics. |
| **Label bias** | The labels or ground truth used in supervised learning reflect human biases. | Medical imaging datasets labeled by providers from specific regions may not generalize across populations. |
| **Measurement bias** | Certain groups are measured differently or with lower quality data. | A facial recognition model performs well on lighter skin tones because training photos were predominantly of those groups. |
| **Aggregation bias** | A single model is applied to diverse groups whose patterns differ significantly. | A health risk model trained on a general population may perform poorly for underrepresented subgroups. |

**Mitigation approaches:**
- Auditing training data for representational gaps
- Using bias detection tools (Amazon SageMaker Clarify)
- Testing model outputs across demographic groups
- Incorporating diverse perspectives in model development and evaluation

---

### Privacy in AI

AI systems consume data — and in doing so, they create significant privacy risks.

| Privacy Risk | Description |
|-------------|-------------|
| **Training data exposure** | A model may memorize and reproduce sensitive details from its training data (e.g., names, addresses, medical information). |
| **PII in inference data** | Users may input personal information when interacting with an AI system, which could be logged or retained. |
| **Re-identification** | Combining anonymized data with other datasets can re-identify individuals. |
| **Unauthorized data use** | Training on data without proper consent or in violation of data use agreements. |

**Privacy protections relevant to the exam:**
- Differential privacy: Adds statistical noise to training data to prevent individual records from being memorized.
- Data minimization: Collect and use only the data necessary for the task.
- PII detection and redaction (Amazon Comprehend, Amazon Bedrock Guardrails).
- Access controls on training data and model outputs.

---

### Human Oversight

Responsible AI is not a fully autonomous endeavor. Human oversight remains essential, especially for high-stakes decisions.

**Why human oversight matters:**
- AI systems can fail in unexpected ways, particularly in edge cases.
- Some decisions carry consequences too significant to be made by a model alone (medical diagnoses, legal determinations, financial decisions).
- Models do not carry moral or legal responsibility — humans and organizations do.

**The concept of "human in the loop":** Design patterns that keep a human in the decision-making process for high-stakes or uncertain outputs. Examples: AI surfaces top three recommendations for a human to review; AI flags suspicious activity for human investigation; AI drafts a document that a human must approve before it is sent.

---

### Shared Responsibility for AI

Responsible AI is not the responsibility of any single party. The AIF-C01 exam recognizes three layers of responsibility:

| Party | Responsibility |
|-------|---------------|
| **AI developers** (labs that create foundation models) | Ensure models are trained responsibly, evaluate for bias and safety, provide documentation (model cards), and communicate known limitations. |
| **AWS (as a platform provider)** | Provide services, tools, and controls (Guardrails, SageMaker Clarify, Bedrock Governance) that help customers deploy AI responsibly. |
| **Organizations (builders and deployers)** | Configure applications appropriately, apply guardrails, audit outputs, obtain proper consent, monitor for harm, and ensure compliance with applicable laws. |
