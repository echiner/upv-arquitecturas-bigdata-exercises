# Exercise 2: Evaluating RAG Pipelines with Ragas

## 🏆 Project Objective
Learn how to use **Ragas** (Retrieval Augmented Generation Assessment), a leading framework for evaluating RAG applications. You will set up an evaluation dataset, compute the core Ragas metrics, and analyze the performance of a pipeline to diagnose whether the retriever or the generator is the bottleneck.

---

## 📊 Core Ragas Metrics Explained

Ragas uses an "LLM-as-a-judge" approach to calculate scores between `0` and `1`. The framework evaluates your system along two main axes: **Generation** (how well the LLM answered) and **Retrieval** (how well the vector search retrieved relevant info).

```
          ┌──────────────────────────────────────────┐
          │                 Question                 │
          └─────┬──────────────────────────────┬─────┘
                │                              │
        (Answer Relevance)             (Context Recall)
                │                              │
                ▼                              ▼
  ┌──────────────────────────┐   ┌──────────────────────────┐
  │     Generated Answer     ├───┼─────────► Context        │
  └──────────────────────────┘   │     (Faithfulness)       │
                                 └──────────────────────────┘
```

1.  **Faithfulness (Generation)**
    *   *What it measures*: Groundedness. It checks if all claims in the generated answer are supported *only* by the retrieved context (detects hallucinations).
    *   *Example*:
        *   **Context**: *"Paris is the capital of France and has 2 million residents."*
        *   **Answer**: *"The capital of France is Paris, which has a population of 5 million."*
        *   **Result**: Low Faithfulness (the population claim is not in the context).
2.  **Answer Relevance (Generation)**
    *   *What it measures*: Answer quality. It checks if the answer addresses the actual user question rather than drifting or being redundant.
    *   *Example*:
        *   **Question**: *"How do I install python?"*
        *   **Answer**: *"Python is a popular programming language created in 1991 by Guido van Rossum."*
        *   **Result**: Low Answer Relevance (while true, it does not answer the installation instructions query).
3.  **Context Recall (Retrieval)**
    *   *What it measures*: Completeness. It checks if the retrieved context contains all the necessary information required to construct the ground-truth answer.
    *   *Example*:
        *   **Ground Truth**: *"The company was founded in 2015 by Jane Doe and John Smith."*
        *   **Retrieved Context**: *"Jane Doe founded the company in 2015."*
        *   **Result**: Low Context Recall (missing John Smith).
4.  **Context Precision (Retrieval)**
    *   *What it measures*: Signal-to-noise ratio and ranking. It checks if the most relevant retrieved chunks are ranked at the top of the context list.

---

## ⚙️ Step-by-Step Implementation

### Step 1: Install Dependencies
Create a Python virtual environment and install `ragas` along with Hugging Face `datasets` and `pandas` for handling table outputs:
```bash
pip install ragas datasets pandas
```

### Step 2: Set Up Environment Variables
Ragas requires an LLM to evaluate the outputs. By default, it uses OpenAI, but you can configure it for any gateway (e.g., LiteLLM). Set your OpenAI key:
```bash
export OPENAI_API_KEY="your-api-key"
```

### Step 3: Prepare the Evaluation Dataset
Ragas expects a dataset containing four fields:
*   `question`: The input query.
*   `contexts`: The retrieved text chunks (represented as a list of strings).
*   `answer`: The generated answer.
*   `ground_truth`: The ideal, reference answer.

Create a Python script `evaluate_rag.py` and set up a sample dataset:

```python
import os
import pandas as pd
from datasets import Dataset
from ragas import evaluate
from ragas.metrics import (
    faithfulness,
    answer_relevance,
    context_recall,
    context_precision,
)

# 1. Sample dataset mimicking RAG outputs
data = {
    "question": [
        "What is the company policy on remote work?",
        "When was the company founded and by whom?",
    ],
    "contexts": [
        [
            "Employees are allowed to work remotely up to 3 days a week. Core hours are 10 AM to 4 PM."
        ],
        [
            "The company was incorporated in October 2018.",
            "Our founder, Alice Johnson, started the firm in her garage."
        ],
    ],
    "answer": [
        "You can work from home up to three days per week, as long as you are available during core hours.",
        "The company was founded in October 2018.",
    ],
    "ground_truth": [
        "Employees can work remotely up to 3 days per week with core hours between 10 AM and 4 PM.",
        "The company was founded in October 2018 by Alice Johnson.",
    ],
}

dataset = Dataset.from_dict(data)
```

### Step 4: Run the Evaluation
Append the evaluation call and print the output in `evaluate_rag.py`:

```python
# 2. Run the evaluation
print("Running Ragas evaluation...")
result = evaluate(
    dataset=dataset,
    metrics=[
        faithfulness,
        answer_relevance,
        context_precision,
        context_recall,
    ],
)

# 3. Inspect results
df = result.to_pandas()
print("\n--- Evaluation Scores Per Query ---")
print(df[["question", "faithfulness", "answer_relevance", "context_precision", "context_recall"]])

print("\n--- Average Scores ---")
print(result)
```

Run the evaluation:
```bash
python evaluate_rag.py
```

---

## 📤 Project Deliverables

1.  **Deliverable 1: Code Repository**
    *   The complete `evaluate_rag.py` script.
2.  **Deliverable 2: Evaluation Results Table**
    *   The printed output table containing the scores for all 4 metrics on the sample dataset.
3.  **Deliverable 3: Performance Analysis**
    *   Write a short analysis based on the output scores. If `faithfulness` is low, what changes should you make to your system? If `context_recall` is low, how would you address it?

---
[⬅ Back to Module 5 README](./README.md)
