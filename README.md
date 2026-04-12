# Arabic Toxicity Detection and Evaluation Across LLMs

This repository contains the dataset analysis and evaluation setup for Arabic toxicity-related classification using the **MAHED 2025** shared task dataset.

## Dataset Overview

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

## Why MAHED?

MAHED is a recent Arabic benchmark that supports both:
- standard text classification
- structured multitask prediction

It is useful because it covers harmful, prosocial, and affective language in Arabic social media text. The dataset also includes informal writing, dialectal variation, and noisy platform-specific markers such as emojis, mentions, hashtags, and URLs.

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

## Inter-Annotator Agreement

The original MAHED annotation process reports **Cohen's Kappa > 0.85**, indicating high annotation consistency.

As a supplementary check in our work, we manually labeled 20 randomly selected Task 1 samples using 3 annotators. The results showed that disagreement mostly appeared in:

- **implicit hate**
- **political criticism vs hate**
- **hope vs not_applicable** in poetic, emotional, or religious text

This suggests that the main challenge of MAHED is not explicit keyword matching, but contextual interpretation of target, intent, and tone.



---

## Reference

MAHED 2025 Shared Task: Multimodal Detection of Hope and Hate Emotions in Arabic Content.