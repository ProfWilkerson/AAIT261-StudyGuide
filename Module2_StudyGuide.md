# Module 2 Study Guide
## AAIT261 | AWS Certified AI Practitioner (AIF-C01)

This study guide covers Module 2 content: the remainder of Task Statement 1.2 (AWS AI Services and practical use cases) and Task Statement 1.3 (the ML development lifecycle). These two areas together give you the vocabulary and framework to understand how AI systems are built and deployed in real AWS environments.

---

## Part 1: Task Statement 1.2 — AWS AI Services

### Overview

AWS offers a range of managed AI services that allow businesses to add AI capabilities to their applications without building or training custom models. The exam tests your ability to match a described use case to the correct service.

### Core AWS AI Services

| Service | What It Does | Primary Use Case |
|---------|-------------|-----------------|
| **Amazon Rekognition** | Analyzes images and video to detect objects, people, text, scenes, and activities. Can compare faces and detect unsafe content. | Security camera analysis; content moderation; identity verification |
| **Amazon Comprehend** | Natural language processing service that identifies sentiment, entities, key phrases, and language in text. | Analyzing customer reviews; categorizing support tickets; detecting entities in documents |
| **Amazon Transcribe** | Converts audio speech to text (automatic speech recognition). | Meeting transcriptions; call center analytics; subtitle generation |
| **Amazon Polly** | Converts text to lifelike speech using deep learning. | Voice-enabled applications; accessibility tools; audiobook generation |
| **Amazon Translate** | Neural machine translation service for translating text between languages. | Multilingual customer support; translating product catalogs; localizing applications |
| **Amazon Forecast** | Time-series forecasting using ML. Predicts future values based on historical data. | Demand planning; inventory management; energy consumption forecasting |
| **Amazon Personalize** | Builds real-time personalization and recommendation systems. | Product recommendations; content suggestions; personalized search results |
| **Amazon Lex** | Builds conversational interfaces (chatbots) using voice and text. Powers Amazon Alexa's conversational capabilities. | Customer service chatbots; virtual assistants; FAQ automation |
| **Amazon Textract** | Extracts text and structured data (forms, tables) from scanned documents using ML. Goes beyond simple OCR. | Document processing; medical record extraction; financial form digitization |
| **Amazon Kendra** | Intelligent enterprise search service powered by ML. Understands natural language queries. | Internal knowledge base search; document retrieval; employee self-service portals |
| **Amazon SageMaker** | End-to-end ML platform for building, training, and deploying custom machine learning models. | Custom model development; MLOps; research and experimentation |

### Choosing the Right Service

A key exam skill is distinguishing when a managed AWS AI service is appropriate versus when a custom model (built with SageMaker) is needed.

**Use a managed AWS AI service when:**
- The use case aligns directly with one of the service's stated capabilities
- Speed to production matters more than custom optimization
- The organization lacks data science expertise or infrastructure
- Cost of a managed service is justified by the reduced development burden

**Use Amazon SageMaker (custom model) when:**
- The use case is domain-specific and not covered by a managed service
- The organization has proprietary data that provides a competitive advantage
- Fine-tuning or custom architectures are required
- Full control over the model, features, and training process is necessary

---

## Part 2: Task Statement 1.3 — The ML Development Lifecycle

### Overview

Building an ML model is not a single step — it is a structured process that moves from raw data to a deployed, monitored system. The exam tests your ability to name each stage, describe its purpose, and recognize common challenges at each step.

### Stages of the ML Development Lifecycle

| Stage | What Happens | Key Considerations |
|-------|-------------|-------------------|
| **1. Business Problem Framing** | Define the problem the model should solve. Translate a business question into an ML objective. | Is this actually an ML problem? What does success look like? What are the constraints? |
| **2. Data Collection** | Gather the raw data needed to train the model. Data may come from databases, logs, APIs, sensors, or third-party providers. | Is there enough data? Is it representative of the real population? Is it ethically sourced? |
| **3. Data Preparation** | Clean, transform, and format data for model training. Includes handling missing values, removing duplicates, and encoding categorical variables. | Data quality is the most important factor in model quality. Garbage in, garbage out. |
| **4. Feature Engineering** | Select, transform, or create input variables (features) that will be used by the model. Features are the inputs the model learns from. | Which features have predictive power? Are there features that introduce bias? |
| **5. Model Selection** | Choose the appropriate algorithm or model architecture for the problem type (regression, classification, clustering, etc.). | Is this a supervised or unsupervised problem? What are the complexity and interpretability requirements? |
| **6. Model Training** | Feed the prepared dataset into the chosen algorithm to produce a trained model. The algorithm adjusts the model's parameters to minimize prediction error. | Training data split, compute resources, training time, and hyperparameters |
| **7. Model Evaluation** | Assess the model's performance on data it was not trained on (a held-out test set). | Common metrics: accuracy, precision, recall, F1 score, AUC-ROC. Watch for overfitting. |
| **8. Model Tuning (Hyperparameter Optimization)** | Adjust model settings (hyperparameters) to improve performance. Hyperparameters control how the model learns and are set before training. | Balancing model complexity with the risk of overfitting |
| **9. Model Deployment** | Move the trained model to a production environment where it can receive real-world inputs and produce outputs. | Deployment options: real-time endpoint, batch transform, serverless inference |
| **10. Model Monitoring** | Track the model's performance in production over time. Detect drift, degradation, or unexpected behavior. | Data drift, concept drift, and performance degradation require ongoing vigilance |

---

### Key Vocabulary for Task Statement 1.3

| Term | Definition |
|------|------------|
| **Feature** | An individual measurable property or characteristic used as an input to a model. In a housing price model, features might include square footage, number of bedrooms, and zip code. |
| **Label / Target Variable** | The output or outcome a supervised learning model is trained to predict. In a spam detection model, the label is "spam" or "not spam." |
| **Training Data** | The portion of the dataset used to train a model. The model learns patterns from this data. |
| **Validation Data** | A held-out portion of data used during training to tune hyperparameters and detect overfitting. |
| **Test Data** | A held-out portion of data used only after training to evaluate final model performance on unseen data. |
| **Hyperparameter** | A setting that controls how a model learns. Set before training begins and not updated during training. Examples: learning rate, number of trees in a random forest, number of layers in a neural network. |
| **Accuracy** | The percentage of predictions the model got correct. Can be misleading when class distributions are imbalanced. |
| **Precision** | Of all the positive predictions the model made, what fraction were actually positive? Measures how often the model's positive calls are correct. |
| **Recall** | Of all actual positives in the data, what fraction did the model correctly identify? Measures how many true positives the model captured. |
| **F1 Score** | The harmonic mean of precision and recall. Useful when both false positives and false negatives carry significant cost. |
| **Data Drift** | When the statistical properties of the model's input data change over time, potentially degrading model performance. |
| **Concept Drift** | When the relationship between the input features and the target variable changes over time, making the model's learned patterns less accurate. |
| **Confusion Matrix** | A table that compares a model's predicted classifications against the true classifications. Used to calculate precision, recall, and F1. |

---

### The Train / Validation / Test Split

A critical concept for the exam is understanding why data is divided into three sets and what each is used for.

**Training set (typically 60–80% of data):** Used to train the model. The model sees this data and learns from it.

**Validation set (typically 10–20%):** Used during the development process to tune hyperparameters and detect overfitting. The model does not train on this data, but its performance here influences decisions made during development.

**Test set (typically 10–20%):** Used only once — after the model is finalized — to produce an unbiased estimate of its real-world performance. Evaluating on the test set too early contaminates results.

---

### Model Monitoring: Drift and Degradation

Once deployed, a model's performance can degrade without any change to the model itself. Two types of drift explain why:

**Data drift** occurs when the distribution of incoming data changes. For example, a fraud detection model trained on pre-pandemic transaction patterns may perform poorly post-pandemic because spending behaviors have shifted.

**Concept drift** occurs when the underlying relationship between inputs and the target changes. For example, a model that predicts customer churn based on usage patterns may become less accurate if the reasons customers churn change over time.

AWS SageMaker Model Monitor provides automated monitoring capabilities to detect data drift, model quality degradation, and bias drift in production.
