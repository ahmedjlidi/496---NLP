# Arabic Toxicity Detection and Evaluation Across LLMs

This repository contains the dataset analysis and evaluation setup for Arabic toxicity-related classification using the **MAHED 2025** and **OSACT 5** shared task datasets.

## Dataset Overview

### MAHED 2025
We use the **text-based** parts of the MAHED 2025 dataset:

- **Task 1**: 3-class classification
  - `hate`
  - `hope`
  - `not_applicable`

- **Task 2**: multitask classification
  - **Emotion**: one label from 12 classes  
    `neutral`, `anger`, `anticipation`, `disgust`, `fear`, `joy`, `love`, `optimism`, `pessimism`, `sadness`, `surprise`, `trust`
  - **Offensive**: `yes` / `no`
  - **Hate**: `hate` / `not_hate` for offensive content

The multimodal meme task is excluded in this project.

### OSACT 5
- **Task 1**: binary classification
  - `OFF`
  - `NOT_OFF`
- **Task 2**: binary classification (subset of offensive content)
  - `HS`
  - `NOT_HS`
- **Task 3**: fine-grained hate speech classification
  - `HS1` (Race)
  - `HS2` (Religion)
  - `HS3` (Ideology)
  - `HS4` (Disability)
  - `HS5` (Social Class)
  - `HS6` (Gender)

## Why MAHED?

MAHED is a recent Arabic benchmark that supports both:
- standard text classification
- structured multitask prediction

It is useful because it covers harmful, prosocial, and affective language in Arabic social media text. The dataset also includes informal writing, dialectal variation, and noisy platform-specific markers such as emojis, mentions, hashtags, and URLs.

## Why OSACT?

OSACT 5 is a widely used Arabic benchmark for offensive language and hate speech detection. It complements MAHED by focusing more explicitly on:

- hierarchical toxicity detection
- fine-grained hate target classification

The dataset is built from real Twitter data and captures diverse dialects, conversational interactions, and emoji-driven expressions of toxicity. It also introduces hierarchical labeling, making it suitable for more detailed evaluation of model behavior.

---

## Task 1 Summary

### Split Sizes

| Split      | Samples |
| ---------- | ------: |
| Train      |   6,890 |
| Validation |   1,476 |
| Test       |   1,477 |

### Labels

| Label            | Description                                                                     |
| ---------------- | ------------------------------------------------------------------------------- |
| `hate`           | Harmful or discriminatory language targeting a person or group                  |
| `hope`           | Positive or constructive language such as encouragement, gratitude, or optimism |
| `not_applicable` | Text that does not contain explicit hate or hope                                |

### High-Level Observations

- The dataset is **imbalanced**
- `not_applicable` is the largest class
- `hate` is the smallest class
- The average text length is **22.38 words**
- Social media markers and informal writing patterns are present

### Linguistic Characteristics

| Metric                              | Value |
| ----------------------------------- | ----: |
| Average word count                  | 22.38 |
| Texts with emoji (%)                | 14.02 |
| Texts with hashtag (%)              |  4.91 |
| Texts with mention (%)              | 24.92 |
| Texts with URL (%)                  |  8.49 |
| Texts with repeated punctuation (%) | 15.24 |
| Texts with elongation (%)           | 13.92 |
| Texts with Latin/code-switching (%) | 37.36 |

---

## Task 2 Summary

### Split Sizes

| Split      | Samples |
| ---------- | ------: |
| Train      |   5,960 |
| Validation |   1,277 |
| Test       |   1,278 |

### Task Structure

Each sample in Task 2 has three outputs:

1. **Emotion**
2. **Offensive**
3. **Hate**

### High-Level Observations

- Task 2 is more complex than Task 1 because each sample has multiple related labels
- Emotion classes are clearly imbalanced
- Texts are short on average, similar to Task 1
- Task 2 contains more social media noise and mixed-script content than Task 1

### Linguistic Characteristics

| Metric                              | Value |
| ----------------------------------- | ----: |
| Average word count                  | 21.15 |
| Texts with emoji (%)                | 32.55 |
| Texts with hashtag (%)              | 26.44 |
| Texts with mention (%)              | 50.84 |
| Texts with URL (%)                  | 29.67 |
| Texts with repeated punctuation (%) | 17.51 |
| Texts with elongation (%)           | 22.80 |
| Texts with Latin/code-switching (%) | 84.69 |

---

## OSACT 5 Summary

### Split Sizes

| Split      | Samples |
| ---------- | ------: |
| Train      |   8,557 |
| Validation |   1,266 |
| Test       |   2,541 |
| **Total**      |  **12,364** |

### Dataset Structure

Each sample in OSACT has two labels:

1. `OFF`/ `NOT_OFF`
2. `HS1-6`/ `NOT_HS`

### High-Level Observations

- Offensive and HateSpeech classes are imbalanced
- `NOT_OFF` and `NOT_HS` are the largest classes
- `OFF` represents 35% of the dataset, while `HS` -with its fine-grainded types- represnt 10% of it.
- Texts are short averaging around 13 words
- Emojis is dominantly present (95%) in the texts since its the main method of data collection
- Social Media markers and informal writing patterns are present

### Linguistic Characteristics

| Metric                              | Value |
| ----------------------------------- | ----: |
| Average word count                  | 12.50 |
| Texts with emoji (%)                | 95.08 |
| Texts with hashtag (%)              | 18.42 |
| Texts with mention (%)              | 62.45 |
| Texts with URL (%)                  | 16.54 |
| Texts with repeated punctuation (%) | 11.29 |
| Texts with elongation (%)           | 30.65 |
| Texts with Latin/code-switching (before cleaning) (%) | 83.73 |
| Texts with Latin/code-switching (after cleaning`*`) (%) | 2.69 |

`*The dataset is slightly preprocessed to include ”@USER”, ”RT”, ”URL”, and ”<LF>” which aren’t parts of the main text and context`

---

## Inter-Annotator Agreement

### MAHED 2025
The original MAHED annotation process reports **Cohen's Kappa > 0.85**, indicating high annotation consistency.

As a supplementary check in our work, we manually labeled 20 randomly selected Task 1 samples using 3 annotators. The results showed that disagreement mostly appeared in:

- **implicit hate**
- **political criticism vs hate**
- **hope vs not_applicable** in poetic, emotional, or religious text

This suggests that the main challenge of MAHED is not explicit keyword matching, but contextual interpretation of target, intent, and tone.

### OSACT 5
The OSACT 5 annotation process reports **Cohen’s Kappa ≈ 0.82**, indicating strong agreement among annotators.

- Each tweet was labeled by 3 annotators
- Quality control included hidden test questions and accuracy thresholds
- Disagreements were reviewed by expert linguists
- Around 18% of labels were corrected after expert review

---

## Reference

MAHED 2025 Shared Task: Multimodal Detection of Hope and Hate Emotions in Arabic Content.

OSACT 5 Shared Task: Arabic Offensive Language and Hate Speech Detection.
