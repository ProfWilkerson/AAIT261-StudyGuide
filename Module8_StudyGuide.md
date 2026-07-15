# Module 8 Study Guide
## AAIT261 | AWS Certified AI Practitioner (AIF-C01)

This study guide covers Module 8 content: Task Statement 5.2 (Governance and Compliance for AI Systems) and Exam Preparation. This is the final module before the certification exam. Use it to solidify your understanding of governance and compliance — and then use the exam preparation section to consolidate everything you have learned across the entire course.

---

## Part 1: Task Statement 5.2 — Governance and Compliance for AI Systems

### What Is AI Governance?

**AI governance** refers to the organizational structures, policies, processes, and accountability mechanisms that ensure AI systems are developed, deployed, and retired in ways that are legal, ethical, and aligned with organizational values.

Governance is what makes responsible AI sustainable inside an organization. Principles without governance are aspirational but not operational.

Key elements of AI governance:
- Clear policies on how AI may and may not be used
- Defined roles and responsibilities for AI development and oversight
- Processes for risk assessment before deploying AI systems
- Mechanisms for ongoing monitoring, auditing, and reporting
- Procedures for responding to AI-related incidents or harms

---

### The Shared Responsibility Model for AI on AWS

The AWS shared responsibility model extends to AI workloads. Understanding what AWS is responsible for and what the customer is responsible for is a tested concept.

| Responsibility Layer | AWS Manages | Customer Manages |
|--------------------|-------------|----------------|
| **Physical infrastructure** | Data centers, hardware, networking | — |
| **Cloud platform security** | Security of the cloud (hypervisor, storage, network infrastructure) | Security in the cloud (configurations, access, data) |
| **Managed AI services** (e.g., Bedrock) | Underlying model security, infrastructure, service availability | Prompt design, guardrail configuration, access controls, output monitoring, compliance |
| **Foundation model providers** | Training data curation, model development, safety measures during pre-training | Model selection, deployment configuration, use case appropriateness |
| **Customer applications** | — | Application design, user access, data privacy, legal compliance, output review |

**Key principle:** AWS secures the infrastructure. Customers are responsible for how they configure, deploy, and use AI services — including ensuring compliance with applicable laws and regulations.

---

### Data Governance Concepts for AI

| Concept | Definition | Why It Matters for AI |
|---------|-----------|----------------------|
| **Data lineage** | The documented history of where data came from, how it was transformed, and where it was used. | Enables auditors and regulators to trace exactly what data was used to train a model and verify it was collected appropriately. |
| **Data residency** | Requirements about where data must be physically stored — often driven by national or regional law (e.g., EU data must stay in the EU). | AI training data and model outputs may be subject to data residency requirements. AWS Regions allow organizations to control where their data is stored. |
| **Data retention** | Policies governing how long data is kept and when it must be deleted. | Training data, inference logs, and model outputs may be subject to retention requirements under privacy law. |
| **Data provenance** | Documentation of data's origin and chain of custody. | Demonstrates that training data was ethically sourced and that rights to use it were properly obtained. |
| **Data minimization** | Collecting and using only the data necessary for the stated purpose. | Reduces privacy risk and compliance exposure. A model should not be trained on sensitive data it does not need. |

---

### AI Regulation: Emerging Frameworks

AI regulation is evolving rapidly. The exam tests your awareness of the regulatory landscape, not expertise in any specific law.

| Regulation / Framework | Scope | Key Requirements |
|----------------------|-------|-----------------|
| **EU AI Act** | Regulates AI systems in the European Union based on risk level | High-risk AI systems (hiring, credit, biometrics, critical infrastructure) require conformity assessments, transparency, human oversight, and registration |
| **GDPR (General Data Protection Regulation)** | EU data privacy law that applies to AI systems using personal data | Data minimization, purpose limitation, right to explanation for automated decisions, data subject rights |
| **NIST AI Risk Management Framework (AI RMF)** | US voluntary framework for managing AI risk | Structured approach to governing AI: Map, Measure, Manage, Govern |
| **Executive Order on Safe, Secure, and Trustworthy AI** (US, 2023) | US federal guidance on AI safety and governance | Safety testing requirements for high-risk AI systems; standards for watermarking AI-generated content; privacy protections |

**For the exam:** Know that AI regulation is increasing globally, that the EU AI Act is the most comprehensive legislation, and that high-risk AI systems require stronger governance than low-risk applications.

---

### AWS Tools for AI Governance and Compliance

| Service / Feature | Purpose |
|-------------------|---------|
| **Amazon Bedrock Governance** | Provides controls for governing foundation model usage within an organization, including model access policies, usage tracking, and audit capabilities. |
| **AWS Config** | Continuously monitors and records AWS resource configurations. Can be used to detect and alert on misconfigurations in AI infrastructure (e.g., an S3 bucket containing training data with public access enabled). |
| **AWS Audit Manager** | Automates the collection of evidence for compliance audits. Supports frameworks including GDPR and NIST. Can be used to document AI governance practices. |
| **AWS Artifact** | Provides on-demand access to AWS compliance reports and agreements (SOC 2, ISO 27001, etc.) that customers can use to demonstrate that their AWS infrastructure meets regulatory requirements. |
| **AWS CloudTrail** | Logs all AWS API activity. Essential for audit trails — who accessed what AI resource, when, and from where. |

---

## Part 2: Exam Preparation

### AIF-C01 Domain Weights

Allocate your remaining study time proportionally to domain weight:

| Domain | Topic | Exam Weight |
|--------|-------|------------|
| **Domain 1** | Fundamentals of AI and ML | 20% |
| **Domain 2** | Fundamentals of Generative AI | 24% |
| **Domain 3** | Applications of Foundation Models | 28% |
| **Domain 4** | Guidelines for Responsible AI | 14% |
| **Domain 5** | Security, Compliance, and Governance | 14% |

Domain 3 carries the most weight. If you have limited time, prioritize RAG, prompt engineering, fine-tuning comparison, and model evaluation.

---

### Common Exam Question Patterns

**Pattern 1: "Which service is most appropriate?"**
These questions describe a business problem and ask you to choose the right AWS service. Key skill: match the use case to the service without being distracted by partially correct options.

**Pattern 2: "Which adaptation strategy?"**
Prompt engineering vs. RAG vs. fine-tuning vs. continued pre-training. Key skill: know the decision criteria — see the Module 5 study guide table.

**Pattern 3: "Which responsible AI dimension?"**
A scenario describes a problem (unfair outcomes, unexplainable decisions, data exposure). Key skill: match it to the right dimension (fairness, explainability, privacy, safety, controllability).

**Pattern 4: "What is the most likely cause?"**
A model behaves unexpectedly. Key skill: distinguish between hallucination, bias, data drift, concept drift, prompt injection, and context window limits based on the symptoms described.

**Pattern 5: "Which security control?"**
A scenario describes a threat or a compliance requirement. Key skill: map the threat (data poisoning, model inversion, unauthorized access) to the right AWS security service or practice.

---

### Elimination Strategies

- **Eliminate technically impossible answers first.** If an option says Amazon Transcribe can analyze images, eliminate it immediately — Transcribe converts audio to text.
- **Watch for plausible distractors.** The wrong answers on this exam are often services or approaches that are adjacent to the right answer but wrong for the specific use case. Read carefully.
- **"Always" and "never" are almost always wrong.** Real-world AI is full of trade-offs. Absolute language is a red flag.
- **When two answers seem correct, ask which is more specific.** The exam typically rewards the more precise, targeted answer over a general one.

---

### High-Priority Review Topics

These are the most commonly tested concepts across the AIF-C01 exam. If time is limited, focus here:

**From Domain 1:**
- Supervised vs. unsupervised vs. reinforcement learning
- When AI is and is not appropriate
- ML lifecycle stages and terminology (feature, label, training/validation/test split, drift)

**From Domain 2:**
- Foundation models vs. traditional ML models
- Tokens and context windows
- Embeddings and vector stores
- Hallucination, non-determinism, prompt injection, knowledge cutoff

**From Domain 3:**
- RAG — what it solves, how it works, when to use it vs. fine-tuning
- Prompt engineering techniques (zero-shot, one-shot, few-shot, chain-of-thought)
- When to use prompt engineering vs. RAG vs. fine-tuning vs. continued pre-training
- Automated evaluation metrics (ROUGE for summarization, BLEU for translation, BERTScore for semantic similarity)
- Amazon Bedrock: what it is, what it includes (Knowledge Bases, Agents, Guardrails, Model Evaluation)

**From Domain 4:**
- The seven dimensions of responsible AI
- Bias sources and mitigation
- Explainability vs. transparency; model cards
- Deep learning and LLM explainability limitations

**From Domain 5:**
- AI-specific threats: data poisoning, model inversion, adversarial inputs
- AWS security services: IAM, KMS, Macie, CloudTrail, GuardDuty
- Shared responsibility model for AI
- Data governance: lineage, residency, retention
