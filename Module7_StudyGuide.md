# Module 7 Study Guide
## AAIT261 | AWS Certified AI Practitioner (AIF-C01)

This study guide covers Module 7 content: Task Statement 4.2 (Transparent and Explainable AI) and Task Statement 5.1 (Methods to Secure AI Systems). These two topics are distinct in content but connected in theme — both are about maintaining trust, accountability, and control over AI systems in the real world.

---

## Part 1: Task Statement 4.2 — Transparent and Explainable AI

### Transparency vs. Explainability

These terms are related but distinct, and the exam may test your ability to differentiate them.

| Concept | Definition | Example |
|---------|-----------|---------|
| **Transparency** | Openness about how an AI system was built, what data it was trained on, what its intended use is, and what its known limitations are. Transparency is about disclosure at the system level. | Publishing a model card that describes training data sources, evaluation results, and known failure modes. |
| **Explainability** | The ability to describe, in human-understandable terms, why a model produced a specific output for a specific input. Explainability is about reasoning at the individual prediction level. | A credit scoring model that tells a loan officer "this application was flagged because of a high debt-to-income ratio and two missed payments in the past 12 months." |

Both transparency and explainability are necessary for responsible AI, but they answer different questions:
- Transparency answers: *What is this system and how was it built?*
- Explainability answers: *Why did it make this specific decision?*

---

### Model Cards

**Model cards** are documentation artifacts that provide structured transparency about an AI model. They are published by the model's creators and intended to help users understand whether the model is appropriate for their use case.

A model card typically includes:

| Section | Contents |
|---------|---------|
| **Model overview** | Model name, version, type, intended use cases, and out-of-scope uses |
| **Training data** | Description of the datasets used, including sources, curation process, and known data limitations |
| **Evaluation results** | Performance metrics across benchmarks and disaggregated results across demographic groups |
| **Ethical considerations** | Known biases, fairness limitations, and mitigation strategies |
| **Limitations** | Edge cases, failure modes, and conditions under which the model should not be used |
| **Usage recommendations** | Guidance on appropriate deployment contexts and human oversight requirements |

**AWS AI Service Cards:** AWS publishes AI Service Cards for its managed AI services (like Rekognition and Comprehend) following a similar format. These provide transparency about the capabilities, limitations, and responsible use of each service.

---

### Explainability Methods

**Feature importance** is the most common category of explainability for traditional ML models. It answers: *Which input features had the most influence on this prediction?*

| Method | How It Works | Notes |
|--------|-------------|-------|
| **SHAP (SHapley Additive exPlanations)** | Assigns each feature a contribution score for a specific prediction, based on cooperative game theory. Shows positive and negative contributors. | Most robust feature importance method; computationally intensive for large models |
| **LIME (Local Interpretable Model-agnostic Explanations)** | Creates a simple, locally accurate approximation of the model's behavior around a specific prediction. | Faster than SHAP but less globally consistent |

**Amazon SageMaker Clarify** provides built-in support for:
- Detecting bias in training data and model outputs (pre-training and post-training bias analysis)
- Generating SHAP-based feature importance explanations for model predictions
- Producing bias and explainability reports that can be shared with stakeholders

---

### Explainability Limitations for Deep Learning and LLMs

A critical exam concept: explainability is fundamentally harder for deep learning models and large language models than for simpler ML models.

| Model Type | Explainability | Reason |
|-----------|---------------|--------|
| **Linear regression** | High — direct | Each feature has a coefficient that directly represents its contribution |
| **Decision tree** | High — traceable | The decision path can be followed and described in plain language |
| **Random forest** | Moderate | Feature importance can be computed, but individual decision paths are harder to trace |
| **Deep learning / neural network** | Low | Thousands or millions of parameters interact in complex, non-linear ways; no single feature "causes" an output |
| **Large language model** | Very low | Billions of parameters; attention patterns are complex; no direct mapping from input tokens to output tokens |

**Why this matters for the exam:** When a scenario describes a regulated industry (banking, healthcare, legal) that requires explainable decisions, deep learning models and LLMs may not be appropriate. Rule-based systems or simpler, interpretable ML models may be preferred even if they sacrifice some accuracy.

---

## Part 2: Task Statement 5.1 — Methods to Secure AI Systems

### The AI Security Attack Surface

AI systems introduce security risks at every stage of their lifecycle. Unlike traditional applications, AI systems can be attacked not just through their interfaces but through their training data and model parameters.

| Stage | Security Risk |
|-------|-------------|
| **Data collection and storage** | Unauthorized access to sensitive training data; data exfiltration; storage misconfigurations |
| **Training** | Data poisoning attacks; unauthorized modification of training pipelines |
| **Model storage** | Theft or unauthorized copying of trained model weights (model IP theft) |
| **Inference / API** | Prompt injection; adversarial inputs; model inversion attacks; excessive API access |
| **Output** | Leakage of sensitive training data in generated outputs; generation of harmful content |

---

### AI-Specific Threat Types

| Threat | Description | Mitigation |
|--------|-------------|-----------|
| **Data poisoning** | An attacker injects malicious examples into the training data to manipulate the model's behavior. A compromised model may, for example, misclassify certain inputs in ways the attacker controls. | Validate and audit training data sources; use data provenance controls; monitor for anomalies in training data |
| **Model inversion / extraction** | An attacker repeatedly queries a model and uses the outputs to reverse-engineer the training data or replicate the model's behavior. | Rate limiting on API calls; output perturbation; monitoring for systematic querying patterns |
| **Adversarial inputs** | Inputs that have been subtly modified (often imperceptibly to humans) to cause the model to produce incorrect outputs. Common in image recognition models. | Adversarial training; input validation; ensemble methods |
| **Prompt injection** | A user crafts inputs designed to override the model's instructions. Particularly dangerous for agentic AI with real-world action capabilities. (Covered in Module 3.) | Input filtering; output validation; least-privilege design for agentic systems |
| **Model weight theft** | Unauthorized access to the stored model artifact (the trained weights) allows an attacker to replicate or repurpose a proprietary model. | Access controls on model artifacts; encryption of model weights; IAM policies on SageMaker model registries and S3 buckets |

---

### AWS Security Services for AI Workloads

| Service | Role in AI Security |
|---------|-------------------|
| **AWS IAM (Identity and Access Management)** | Controls who can access AI resources — SageMaker endpoints, Bedrock models, S3 training data buckets. Enforce least-privilege access. |
| **AWS KMS (Key Management Service)** | Encrypts data at rest and in transit, including training datasets, model artifacts, and inference inputs/outputs. |
| **Amazon Macie** | Uses ML to automatically discover and protect sensitive data (PII, financial records) in Amazon S3. Relevant for training data governance. |
| **AWS CloudTrail** | Logs all API calls to AWS services, providing an audit trail of who accessed AI resources, when, and from where. Essential for compliance and incident investigation. |
| **Amazon GuardDuty** | Threat detection service that identifies unusual activity, including anomalous API call patterns that may indicate model extraction attempts. |
| **AWS PrivateLink / VPC** | Ensures that traffic between AWS services and AI endpoints stays within the AWS network and does not traverse the public internet. |

---

### Access Control Best Practices for AI

**Least privilege:** Grant each user, service, or application only the permissions it needs for its specific task. A data scientist training a model should not have permission to modify production inference endpoints.

**Separation of duties:** Different teams should control different stages of the AI lifecycle — data, training, deployment. No single individual should control the entire pipeline without review.

**Model artifact protection:** Trained model weights are intellectual property and potentially sensitive. Store them in S3 with bucket policies, server-side encryption, and versioning. Restrict access via IAM roles.

**Endpoint security:** Amazon SageMaker endpoints and Amazon Bedrock API access should be restricted to authorized callers using IAM policies, VPC configurations, and resource-based policies.

**Audit logging:** Enable CloudTrail and Amazon SageMaker logging to maintain a record of all access and actions on AI resources. This is required for compliance in most regulated industries.
