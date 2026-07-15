# Module 5 Study Guide
## AAIT261 | AWS Certified AI Practitioner (AIF-C01)

This study guide covers Module 5 content: Task Statement 3.2 (Prompt Engineering) and Task Statement 3.3 (Training and Fine-Tuning Foundation Models). Both topics are heavily represented on the AIF-C01 exam. Expect scenario questions that ask you to choose between prompting approaches or to decide whether prompt engineering, RAG, or fine-tuning is most appropriate for a given situation.

---

## Part 1: Task Statement 3.2 — Prompt Engineering

### What Is Prompt Engineering?

**Prompt engineering** is the practice of designing and refining the inputs given to a foundation model to achieve better, more accurate, or more appropriate outputs. It requires no changes to the model itself — only to the text (or other input) the model receives.

Prompt engineering is the first strategy to try when working with a foundation model. It is fast, cheap, and often sufficient for many use cases.

---

### Prompting Techniques

#### Zero-Shot Prompting
The model is given a task with no examples. It relies entirely on its pre-trained knowledge to complete the task.

- **Use when:** The task is well-defined and the model has likely encountered it in training.
- **Example:** *"Summarize the following customer review in one sentence: [review text]"*
- **Limitation:** Performance can be inconsistent on complex or unusual tasks.

#### One-Shot Prompting
The model is given one example of the task before being asked to complete a new instance.

- **Use when:** The output format or style needs to be demonstrated, but only one example is available.
- **Example:** *"Summarize a customer review in one sentence. Review: 'Arrived late, packaging was damaged, but the product worked fine.' Summary: 'Order arrived late with damaged packaging but the product functioned correctly.' Now summarize: [new review]"*

#### Few-Shot Prompting
The model is given several examples (typically 3–10) before being asked to complete the task.

- **Use when:** The task has a specific format, style, or classification scheme that benefits from demonstration.
- **Best practice:** Examples should be representative of the range of inputs the model will encounter.
- **Limitation:** Examples consume tokens in the context window. Too many examples can crowd out the actual input.

---

#### Chain-of-Thought (CoT) Prompting
Instead of asking the model directly for an answer, you prompt it to show its reasoning step by step before arriving at a conclusion.

- **Use when:** The task requires multi-step reasoning — math problems, logical deductions, complex decisions.
- **Standard approach:** *"Let's think through this step by step..."* or include reasoning steps in few-shot examples.
- **Why it works:** By generating intermediate reasoning steps, the model is less likely to skip logical steps or arrive at incorrect conclusions.
- **Limitation:** Produces longer, more token-expensive outputs.

---

### Anatomy of a Prompt

Effective prompts for complex tasks often include several components:

| Component | Purpose | Example |
|-----------|---------|---------|
| **System prompt** | Sets the model's role, persona, and constraints. Applied before the user turn. | *"You are a professional legal document reviewer. Respond in formal language. Do not provide legal advice."* |
| **Context / Background** | Provides relevant information the model needs to complete the task. | *"The following is a customer complaint email received on June 15, 2026."* |
| **Instruction** | The specific task you are asking the model to perform. | *"Classify the complaint as billing, shipping, product quality, or other."* |
| **Input data** | The actual content for the model to work on. | *[The customer email text]* |
| **Output format specification** | Describes the expected format of the response. | *"Respond with a single category label and a one-sentence justification."* |
| **Examples (few-shot)** | Demonstrates the expected input-output pattern. | Pairs of example complaints and their correct classifications. |

---

### Inference Parameters

These parameters control how the model generates output and are often tested on the exam.

| Parameter | What It Controls | Low Setting | High Setting |
|-----------|-----------------|-------------|-------------|
| **Temperature** | Randomness of output | More deterministic and predictable | More random and creative |
| **Top-P (nucleus sampling)** | Considers only the most probable tokens that together make up P% of the probability mass | Tighter, more focused outputs | More diverse outputs |
| **Top-K** | Limits generation to the top K most probable next tokens | Very constrained output | More varied output |
| **Max Tokens** | Maximum number of tokens in the response | Shorter, more concise responses | Allows longer responses |

**For the exam:** The most commonly tested parameters are temperature and max tokens. Temperature low → consistent/factual. Temperature high → creative/varied.

---

## Part 2: Task Statement 3.3 — Training and Fine-Tuning Foundation Models

### The Training Progression

Understanding how a foundation model goes from raw pre-training to a helpful, safe assistant requires knowing the sequence of training stages.

```
Pre-Training → (Optional) Continued Pre-Training → Instruction Tuning → RLHF → Deployed Model
```

---

### Pre-Training

**Pre-training** is the initial, large-scale training process that creates a foundation model.

- The model is trained on a massive corpus of text (and possibly other data types) from the internet, books, code, and other sources.
- The training objective is typically to predict the next token in a sequence.
- Pre-training is extremely compute-intensive and expensive — it is done by AI labs (AWS, Anthropic, Meta, etc.), not by individual organizations.
- The result is a **base model** that has broad language understanding but is not yet optimized for following instructions or being helpful.

---

### Continued Pre-Training (Domain Adaptation)

**Continued pre-training** takes a base model and continues training it on a specialized corpus — medical literature, legal documents, financial reports, software code — to give the model deeper knowledge in that domain.

- **Use case:** When the domain is highly specialized and the model needs to internalize domain-specific vocabulary, facts, and reasoning patterns.
- **Example:** A healthcare company continues pre-training a base LLM on clinical notes and medical research papers to create a healthcare-specific model.
- **Distinction from fine-tuning:** Continued pre-training deepens the model's knowledge in a domain. Fine-tuning adjusts how the model behaves or what tasks it performs.

---

### Instruction Tuning (Supervised Fine-Tuning)

**Instruction tuning** trains the model on pairs of instructions and ideal responses. The goal is to teach the model to follow instructions rather than just predict the next token.

- After pre-training, a base model is good at text completion but poor at following commands.
- Instruction tuning provides examples like: *[Instruction: "Summarize this article."] → [Response: "Here is a summary: ..."]*.
- The result is a model that is far more useful for real-world task completion.
- This stage is also called **supervised fine-tuning (SFT)**.

---

### Reinforcement Learning from Human Feedback (RLHF)

**RLHF** is a training technique that aligns model behavior with human preferences by using human judgments as a reward signal.

How it works:
1. The instruction-tuned model generates multiple responses to the same prompt.
2. Human raters rank those responses by quality, helpfulness, and safety.
3. A **reward model** is trained to predict which responses humans would prefer.
4. The main model is further trained using reinforcement learning, with the reward model providing feedback to optimize toward human-preferred outputs.

**Why RLHF matters:**
- It reduces harmful, biased, or unhelpful outputs.
- It makes models more aligned with user expectations.
- It is the primary technique behind the helpfulness and safety improvements in models like Claude and ChatGPT.

---

### Choosing the Right Adaptation Strategy

This comparison is one of the most tested topics in Domain 3.

| Strategy | What It Does | Best For | Limitation |
|----------|-------------|---------|-----------|
| **Prompt engineering** | Guides the model through carefully crafted inputs | Quick, low-cost improvements; format and style control; initial experiments | Cannot add new knowledge; limited by context window |
| **RAG** | Gives the model access to current external documents at inference time | Frequently changing information; factual Q&A on proprietary content; reducing hallucination | Requires document infrastructure; adds latency |
| **Fine-tuning** | Adjusts model weights through additional training | Teaching a specific style, tone, or format; domain-specific language; tasks where prompt engineering fails | Costly and time-consuming; knowledge frozen at training time |
| **Continued pre-training** | Extends model knowledge in a specialized domain | Highly specialized domains with unique vocabulary and concepts | Most expensive option; requires large domain corpus |

**Decision rule for the exam:**
- Start with prompt engineering.
- If current/private information is needed → RAG.
- If the model needs to behave differently (style, format, domain tasks) → fine-tuning.
- If the model lacks fundamental knowledge of a specialized domain → continued pre-training.
