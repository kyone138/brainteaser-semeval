# Multiple-Choice Question Answering for Riddle-Based Reasoning

## Overview

Question Answering (QA) is a core challenge in Natural Language Processing, requiring models to understand language, reason over meaning, and select correct answers. While recent large language models have shown strong performance, QA—especially **riddle-style multiple-choice questions without context**—remains a difficult and unsolved problem.

In this project, we compare three neural approaches for multiple-choice question answering on **riddle-like puzzles**:

- Attention-based CNN
- GRU-based sequence model
- Fine-tuned BERT Transformer

The task is evaluated on **SemEval Task 9**, which contains two types of puzzles: *word puzzles* and *sentence puzzles*.

---

## Task Description

Given:
- A question
- Four answer choices

Each model:
1. Computes a score for each (question, choice) pair
2. Selects the final answer based on the highest predicted score

Unlike traditional QA tasks:
- **No external context is provided**
- Questions and answers function as riddles
- Solving requires **commonsense reasoning and lateral thinking**

### Example

**Sentence Puzzle**  
> *“A man shaves every day, yet keeps his beard long.”*  
✔ Answer: *He is a barber.*

**Word Puzzle**  
> *“What part of London is in France?”*  
✔ Answer: *The letter N.*

These questions require reasoning that defies surface-level semantic matching, making them particularly challenging for neural models.

---

## Dataset

- **SemEval Task 9**
- ~700 total examples
- Two categories:
  - Word puzzles
  - Sentence puzzles
- Dataset merged and split using an **80/20 train–validation split**

⚠️ Data sparsity is a key challenge in this task and significantly impacts model performance.

---

## Models Compared

### 1. CNN with Attention (Baseline)
- Convolutional encoder with attention mechanism
- Treats QA as pairwise matching between question and choices
- Serves as a baseline for comparison

### 2. GRU-Based Model
- Sequential modeling using GRUs
- Designed to capture temporal dependencies in questions and answers
- Slight architectural improvement over CNN baseline

### 3. Fine-Tuned BERT Transformer
- Pretrained BERT adapted for multiple-choice QA
- Scores each (question, answer) pair
- Minimal architectural modification to standard BERT QA setup

---

## Training Setup

- Batch size: 16
- Learning rate: 0.001
- Dropout: 0.5
- Loss function: Cross-entropy loss
- Epochs: 30

Each training batch contains:
- One question
- Four padded answer choices
- Corresponding label indicating the correct answer

---

## Results

### Performance Summary

| Model | Accuracy |
|-----|----------|
| CNN with Attention | ~36.5% |
| GRU Model | ~36% |
| Fine-Tuned BERT | Low 80% |

### Key Observations

- CNN and GRU models exhibit **decreasing loss but stagnant accuracy**
- Accuracy plateaus early, suggesting **underfitting**
- BERT significantly outperforms baseline models due to pretrained linguistic knowledge
- Even BERT performance is limited by **dataset size and sparsity**

---

## Analysis

- The task requires reasoning beyond surface-level semantic similarity
- Small dataset size (~700 examples) limits the ability of neural models to generalize
- CNN and GRU models struggle with:
  - Commonsense reasoning
  - Lateral thinking required by riddle-style questions
- BERT benefits from large-scale pretraining but still faces:
  - Limited fine-tuning signal
  - Architectural simplicity for this task

---

## Key Takeaways

- Riddle-based QA without context is significantly harder than standard QA tasks
- Pretrained transformers outperform CNN and RNN-based models in low-data regimes
- Data scarcity is a major bottleneck for reasoning-heavy QA tasks
- More sophisticated reasoning modules or data augmentation may improve performance

---

## Future Work

- Incorporate data augmentation or synthetic puzzle generation
- Explore reasoning-enhanced architectures
- Apply contrastive learning between correct and incorrect choices
- Fine-tune larger transformer models with task-specific heads
- Investigate external commonsense knowledge integration

---

## References

- SemEval Task 9
- BERT: Pre-training of Deep Bidirectional Transformers for Language Understanding
- Related work on multiple-choice question answering and commonsense reasoning
