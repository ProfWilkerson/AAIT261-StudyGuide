# Module 1 Study Guide
## AAIT261 | AWS Certified AI Practitioner (AIF-C01)

This study guide covers the content for Module 1: Task Statement 1.1 (AI Concepts and Terminology) and the first portion of Task Statement 1.2 (Practical Use Cases for AI). Task Statement 1.1 is a review of foundational concepts from AAIT110. Use it to sharpen your definitions and solidify the relationships between these concepts before moving forward. Task Statement 1.2 builds on that foundation and begins applying it to real-world contexts.

---

## Part 1: Task Statement 1.1 — AI Concepts and Terminology (Review)

### Key Vocabulary

| Term | Definition |
|------|------------|
| **Artificial Intelligence (AI)** | The broad field of computer science focused on building systems that can perform tasks normally requiring human intelligence, such as reasoning, learning, and understanding language. |
| **Machine Learning (ML)** | A subset of AI in which systems learn from data to improve their performance on a task without being explicitly programmed for every possible scenario. |
| **Deep Learning** | A subset of ML that uses neural networks with many layers to learn complex patterns from large amounts of data. Powers many modern AI applications including image recognition and language generation. |
| **Neural Networks** | Computing systems loosely modeled on the structure of the human brain. They consist of layers of connected nodes (neurons) that process and transform data to produce an output. |
| **Computer Vision** | The field of AI that enables machines to interpret and understand visual information, such as images and video. |
| **Natural Language Processing (NLP)** | The field of AI focused on enabling computers to understand, interpret, and generate human language in both written and spoken forms. |
| **Model** | A trained mathematical representation that takes input data and produces an output such as a prediction or classification. A model is the result of training an algorithm on data. |
| **Algorithm** | A set of rules or instructions a machine learning system follows to learn from data and produce predictions or decisions. |
| **Training** | The process of feeding data into a model so it can learn patterns, relationships, and rules. Training adjusts the model's internal parameters to improve accuracy. |
| **Inferencing** | The process of using a trained model to make predictions or decisions on new, previously unseen data. |
| **Bias** | Systematic errors in a model's outputs that result from flawed assumptions or unrepresentative training data. Bias can lead to unfair or inaccurate results. |
| **Fairness** | The principle that a model's outputs should not discriminate against individuals or groups based on protected characteristics and should be equitable across different populations. |
| **Fit** | How well a model has learned the patterns in training data. A model that is underfit has not learned enough; a model that is overfit has learned the training data too specifically and performs poorly on new data. |
| **Large Language Model (LLM)** | A type of AI model trained on massive amounts of text data that can generate, summarize, translate, and answer questions in natural language. Examples include Amazon Titan and GPT-4. |
| **Generative AI (GenAI)** | A category of AI that can generate new content, including text, images, audio, video, and code, based on patterns learned during training. |
| **Agentic AI** | AI systems that can autonomously plan and execute multi-step tasks, make decisions, and use tools or other AI models to accomplish a goal with minimal human intervention. |

---

### How These Concepts Relate

It helps to think of these terms as nested categories rather than separate ideas.

**Artificial Intelligence** is the broadest category. Everything else in this list is a form of AI.

**Machine Learning** is a subset of AI. Rather than being given explicit rules, ML systems learn patterns from data.

**Deep Learning** is a subset of ML. It uses multi-layered neural networks and is particularly effective with large, complex datasets like images and language.

**Generative AI** refers to what a model can do, specifically create new content. Most modern GenAI applications are built on deep learning, often using large language models.

**Agentic AI** refers to how a system operates. An agentic system does not just respond to a single prompt; it plans, takes actions, and completes multi-step tasks autonomously.

A helpful way to visualize this:

```
Artificial Intelligence
  └── Machine Learning
        └── Deep Learning
              └── Neural Networks (the architecture behind deep learning)
                    └── Large Language Models (a type of deep learning model for language)
                          └── Generative AI (what LLMs and similar models can produce)
                                └── Agentic AI (how AI systems can operate autonomously)
```

---

### Types of Inferencing

Once a model is trained, inferencing is how it is used. The type of inferencing chosen depends on the use case's latency requirements, data volume, and cost constraints.

| Inferencing Type | Description | Typical Use Case |
|-----------------|-------------|-----------------|
| **Real-Time** | Processes input data immediately as it arrives, with very low latency. Results are returned in milliseconds. | Fraud detection during a transaction, chatbot responses |
| **Batch** | Processes large volumes of data at scheduled intervals rather than immediately. More cost-efficient for non-urgent workloads. | Generating monthly sales reports, processing overnight data |
| **Asynchronous** | Processing occurs independently of the requesting process. The request is submitted, and results are returned when ready, without requiring the requester to wait. | Document analysis, video processing |
| **Serverless** | Inferencing runs on cloud infrastructure that scales automatically. No server provisioning or management is required. | Infrequent or unpredictable workloads where cost efficiency and scalability matter |

---

### Types of Data in AI Models

The type of data used in training significantly affects which models and techniques are appropriate.

| Data Type | Description | Example |
|-----------|-------------|---------|
| **Labeled** | Data that has been tagged with correct answers or outcomes. Used in supervised learning. | Images tagged as "cat" or "dog"; emails marked "spam" or "not spam" |
| **Unlabeled** | Data without predefined tags or outcomes. Used in unsupervised learning. | A collection of customer purchase records with no categories applied |
| **Tabular** | Data organized in rows and columns, similar to a spreadsheet or database table. | Sales transactions, patient records |
| **Time-Series** | Data points collected at regular intervals over time. Order and sequence matter. | Stock prices, sensor readings, website traffic logs |
| **Image** | Visual data including photographs, medical scans, and video frames. | X-rays for diagnostic AI, photos for computer vision models |
| **Text** | Written or transcribed language data. | Customer reviews, news articles, support tickets |
| **Structured** | Data organized in a predefined, consistent format. Easy for machines to process directly. | Relational databases, CSV files |
| **Unstructured** | Data without a predefined format. Requires additional processing before use in most models. | Emails, social media posts, audio recordings, images |

---

### Types of Machine Learning

| Learning Type | How It Works | Example Use Case |
|--------------|--------------|-----------------|
| **Supervised Learning** | The model learns from labeled training data. Each example includes both an input and a known correct output. The model learns to map inputs to outputs. | Predicting whether a loan applicant will default (labeled historical data with outcomes) |
| **Unsupervised Learning** | The model finds patterns in unlabeled data without being told what to look for. No correct answers are provided. | Grouping customers by purchasing behavior without predefined segments |
| **Reinforcement Learning** | The model learns by taking actions in an environment and receiving rewards or penalties based on the results. It improves over time by maximizing cumulative reward. | Training a robot to navigate a warehouse; game-playing AI |

---

## Part 2: Task Statement 1.2 — Practical Use Cases for AI (Part 1)

### When AI/ML Adds Value

AI and machine learning are most valuable in situations where:

**Human decision-making support is needed at scale.** When decisions involve more data than a human can reasonably process, AI can surface patterns and recommendations that inform better choices. Examples include credit scoring, medical diagnosis support, and content moderation.

**Scalability is a priority.** ML solutions can handle growing volumes of data or users without a proportional increase in cost. A recommendation engine that works for 1,000 users can scale to 1 million with the right infrastructure.

**Automation of repetitive, pattern-based tasks.** Tasks that follow recognizable patterns and do not require nuanced human judgment are strong candidates for automation. Examples include document classification, image tagging, and routine customer service queries.

---

### When AI/ML is Not the Right Choice

AI is not always the appropriate solution. Recognizing when NOT to use it is just as important on the certification exam as knowing when to use it.

| Situation | Why AI/ML May Not Be Appropriate |
|-----------|----------------------------------|
| A specific, deterministic outcome is required | AI models produce predictions, not guaranteed correct answers. If the outcome must be exact and consistent every time, rule-based programming is more appropriate. |
| The cost outweighs the benefit | Building, training, and maintaining an ML model requires time, data, infrastructure, and ongoing monitoring. For simple or low-volume problems, a basic algorithm or human judgment may be more cost-effective. |
| Data is insufficient or unreliable | ML models are only as good as their training data. If the available data is too small, too biased, or too noisy, the model will produce unreliable results. |
| Regulatory or compliance requirements demand full explainability | Some models, particularly deep learning models, function as "black boxes." In regulated industries such as healthcare or finance, a model whose reasoning cannot be clearly explained may not meet compliance requirements. |

---

### Core AI/ML Techniques

| Technique | What It Does | Example |
|-----------|-------------|---------|
| **Regression** | Predicts a continuous numerical value based on input features. | Predicting a house's sale price based on square footage, location, and age |
| **Classification** | Assigns input data to one of several predefined categories. | Determining whether an email is spam or not spam; diagnosing an image as normal or abnormal |
| **Clustering** | Groups similar data points together without predefined categories. The model discovers natural groupings in the data. | Segmenting customers into behavioral groups for targeted marketing |

A quick way to tell them apart: if the output is a number on a continuous scale, think regression. If the output is a category from a predefined list, think classification. If the goal is to discover groups with no predefined labels, think clustering.

---

### Real-World AI Applications

| Application | What It Does | Real-World Example |
|-------------|-------------|-------------------|
| **Computer Vision** | Enables machines to interpret visual information from images and video. | Automated quality inspection on a manufacturing line; detecting anomalies in medical scans |
| **Natural Language Processing (NLP)** | Enables machines to understand and generate human language. | Summarizing legal documents; analyzing customer sentiment from reviews |
| **Speech Recognition** | Converts spoken language into text. | Voice-to-text transcription; voice-activated assistants |
| **Recommendation Systems** | Predicts items a user is likely to want based on behavior and preferences. | Product recommendations on e-commerce platforms; content suggestions on streaming services |
| **Fraud Detection** | Identifies unusual patterns in data that may indicate fraudulent activity. | Flagging suspicious credit card transactions in real time |
| **Forecasting** | Predicts future values based on historical patterns. | Demand planning for inventory; predicting energy consumption |
| **Knowledge Bases** | Organizes and retrieves information intelligently in response to natural language queries. | Enterprise search tools; AI-powered FAQ systems |
| **Agentic AI** | Autonomously plans and executes multi-step tasks using AI tools and models. | An AI assistant that researches, drafts, and schedules a report without step-by-step human instruction |

---

## Practice: Scenario-Based Questions

These questions are written in the format of the AWS Certified AI Practitioner exam. Read each scenario carefully and select the best answer. Review the explanation after each question.

---

**Question 1**

A retail company receives thousands of customer service emails each day. The team wants to automatically route each email to the correct department (billing, shipping, returns, or general inquiry). Which AI/ML technique is most appropriate?

- A. Regression
- B. Clustering
- C. Classification
- D. Reinforcement learning

**Answer: C — Classification**
Classification assigns input data to one of several predefined categories. Because the departments are already defined, this is a classification problem, not a discovery problem.

---

**Question 2**

A hospital has ten years of patient records, including diagnoses and readmission outcomes. They want to build a model that predicts the likelihood a patient will be readmitted within 30 days. What type of machine learning is most appropriate?

- A. Unsupervised learning
- B. Supervised learning
- C. Reinforcement learning
- D. Generative AI

**Answer: B — Supervised learning**
The historical records include labeled outcomes (readmitted or not). Supervised learning trains on labeled data to predict outcomes on new cases.

---

**Question 3**

A fraud detection system must evaluate each bank transaction and flag suspicious activity before the transaction completes. Processing time must be under 200 milliseconds. Which type of inferencing is required?

- A. Batch inferencing
- B. Asynchronous inferencing
- C. Real-time inferencing
- D. Serverless inferencing

**Answer: C — Real-time inferencing**
Real-time inferencing processes input immediately with very low latency. Batch and asynchronous inferencing introduce delays that are incompatible with this use case.

---

**Question 4**

A data scientist trains a model that achieves 99% accuracy on training data but only 61% accuracy on new test data. What problem does this describe?

- A. Underfitting
- B. Bias
- C. Overfitting
- D. Poor fairness

**Answer: C — Overfitting**
Overfitting means the model has memorized the training data rather than learning generalizable patterns. It performs well on data it has seen but poorly on new data.

---

**Question 5**

A marketing team has collected two years of purchase history from 500,000 customers. They want to identify natural groups within their customer base to inform campaign strategy, but they have not defined any categories in advance. Which approach is most appropriate?

- A. Supervised learning using classification
- B. Supervised learning using regression
- C. Unsupervised learning using clustering
- D. Reinforcement learning

**Answer: C — Unsupervised learning using clustering**
Clustering discovers natural groupings in unlabeled data. Because no categories are predefined, supervised learning is not appropriate here.

---

**Question 6**

A company is considering building an ML model to automate approval of expense reports under $50. The current manual process takes 5 minutes per report, and the company processes 10 reports per month. Which factor most strongly suggests AI/ML is NOT the right solution here?

- A. The task involves structured data
- B. The volume is too low to justify the cost of building and maintaining a model
- C. Expense reports contain text, which ML cannot process
- D. Reinforcement learning would be required

**Answer: B — The volume is too low to justify the cost**
Cost-benefit analysis is a key factor in deciding whether to use AI. For 10 reports per month, the time and cost to build, train, and maintain a model far exceed the effort saved.

---

**Question 7**

A company wants to use AI to generate product descriptions for its online catalog based on a list of product attributes. Which category of AI is most applicable?

- A. Computer Vision
- B. Reinforcement Learning
- C. Generative AI
- D. Supervised Learning (regression)

**Answer: C — Generative AI**
Generative AI creates new content, in this case text, based on input. Generating product descriptions from attributes is a text generation task.

---

## Self-Reflection Activity

Before completing the Module 1 Discussion, take a few minutes to consider the following:

Think about a task in your current or previous job that involves repetitive decision-making or pattern recognition. Based on what you reviewed in this module, would AI/ML be an appropriate solution for that task? What type of learning or technique would apply? What data would be needed? Are there any reasons AI/ML would NOT be the right fit?

You do not need to submit this reflection separately. It is intended to prepare you for the Module 1 Discussion, where you will share your experience with the AWS Academy activities and connect it to your own professional context.
