---
layout: post
title: "Zero-Shot Cell Annotation and State Prediction in Cancer Single-Cell Transcriptomics"
date: 2026-03-27 12:00:00 +0000
categories: [research, single-cell, genomics, foundation-models]
---

This post is based on my MSc research project at Secrier Lab at UCL, which explored whether large pretrained single-cell foundation models can be used in a **strict zero-shot setting** for cancer transcriptomics.

The short version is this: I evaluated whether frozen models could help with two practical tasks in cancer single-cell RNA sequencing data without task-specific fine-tuning:

1. **Separate malignant from non-malignant cells**
2. **Predict malignant cell states**, especially states related to proliferation and dormancy

Across the project, I benchmarked three pretrained models:

- **Geneformer-V1** as a general baseline
- **Geneformer-V2-Cancer** as a cancer-specialised model
- **LangCell** as a text-aligned cell annotation framework

## Why this problem matters

Single-cell RNA sequencing gives us cell-level resolution of tumour ecosystems, but annotation is still difficult.

Manual annotation is slow, marker dependent, and often hard to transfer across tissues or datasets. In cancer, this gets even messier because malignant cells can adopt hybrid transcriptional programmes and sit close to stromal or immune populations in expression space.

This makes zero-shot foundation models an appealing idea. If they work well enough, they could become a useful first-pass tool for rapid malignant triage and biologically informed state exploration.

## Research questions

This project focused on three main questions:

- Can frozen foundation models distinguish malignant from non-malignant cells across multiple cancer types?
- Can the same models predict malignant cell states such as **fast-cycling**, **slow-cycling**, and **G0-arrested** cells?
- How consistent are different model families across tissues and tasks in a strict zero-shot setting?

## Data and tasks

I used solid-tumour single-cell RNA-seq datasets from five tissue types:

- breast
- pancreas
- kidney
- ovarian
- prostate

The evaluation had two main stages.

### Task 1: Binary malignant classification

For each tissue, the model predicted whether a cell was **malignant** or **non-malignant**.

### Task 2: Malignant cell-state prediction

After separating the malignant subset, I evaluated whether models could distinguish three biologically meaningful malignant states:

- **fast-cycling**
- **slow-cycling**
- **G0-arrested**

These states matter because dormant or stress-adapted malignant cells can survive treatment and contribute to relapse.

## Model intuition

### Geneformer

Geneformer treats gene expression like a language modelling problem over ranked genes. The idea is that large-scale pretraining can encode useful biological structure that transfers to downstream tasks.

![Geneformer architecture]({{ '/assets/images/geneformer-architecture.png' | relative_url }})

### LangCell

LangCell adds a second ingredient: alignment between cell embeddings and natural-language descriptions. That means labels are not just class IDs. They can be represented as biological text prompts.

![LangCell architecture]({{ '/assets/images/langcell-architecture.png' | relative_url }})

This is especially interesting in cancer because state labels such as *slow-cycling* or *G0-arrested* are semantically meaningful, not just categorical buckets.

## Main findings

### 1) Geneformer-V2-Cancer was the strongest overall model for malignant triage

Across tissues, **Geneformer-V2-Cancer** was the most consistent model in the binary malignant-versus-non-malignant task.

A few representative results:

- In **kidney**, Geneformer-V2-Cancer reached **0.866 accuracy** and **0.866 macro-F1**, with **0.869 balanced accuracy**.
- In **pancreas**, it achieved **0.806 accuracy**.

This suggests that cancer-specialised pretraining helps when the main goal is rapid malignant separation.

![Kidney binary UMAP using Geneformer-V2-Cancer]({{ '/assets/images/kidney-binary-geneformer-v2-umap.png' | relative_url }})

### 2) Multi-cellular annotation was more mixed, and LangCell helped in more complex label spaces

Performance was not uniform across tissues for broader cell-type annotation.

- **Geneformer-V2-Cancer** performed best in **breast**, **pancreas**, and **prostate**, with macro-F1 scores of **0.4643**, **0.3524**, and **0.6506** respectively.
- **LangCell** performed best in **kidney** and **ovarian**, with macro-F1 scores of **0.6789** and **0.5309**.

My interpretation is that text-guided alignment becomes more useful when label spaces are larger or when nearby lineages are harder to separate from expression alone.

### 3) Malignant cell-state prediction was possible, but still clearly challenging

For breast cancer malignant cells, the results showed a split between the best model overall and the best model for specific states.

- **LangCell** achieved the best **overall accuracy: 0.3838**
- It also performed best on **slow-cycling** cells with **F1 = 0.5670**
- **Geneformer-V2-Cancer** performed best on **fast-cycling** cells with **F1 = 0.3768**
- **Geneformer-V2-Cancer** also performed best on **G0-arrested** cells with **F1 = 0.1975**

These are not strong enough numbers to claim the problem is solved, but they do show that frozen foundation models already encode meaningful state information.

![Breast malignant state UMAP with LangCell]({{ '/assets/images/breast-state-langcell-umap.png' | relative_url }})

## What I think this means

A useful practical takeaway from this project is that these models may play **complementary roles**:

- Use a **cancer-specialised unimodal model** such as Geneformer-V2-Cancer for fast malignant triage
- Use a **text-aligned model** such as LangCell when the label space is more complex or when semantically rich state descriptions matter

In other words, zero-shot single-cell modelling may already be good enough to act as a strong research starting point, even when it is not yet good enough to replace downstream validation.

## Limitations

There were several important limitations.

- Malignant state labels were only available for **breast** tissue, so cross-tissue state generalisation was not tested.
- Errors from the binary task can propagate into the state-prediction task.
- LangCell was sensitive to prompt and label design.
- I did not include full calibration or uncertainty analysis, so reliability under distribution shift still needs more work.

## Future directions

Some natural next steps would be:

- extending malignant state labels to more tissues
- testing prompt ablations more systematically for LangCell
- adding confidence estimation and calibration analysis
- comparing hybrid systems that combine cancer-specialised encoders with text-guided scoring

## Final thoughts

This project convinced me that zero-shot foundation models for single-cell biology are already useful, especially when you treat them as **scientific tools for triage, comparison, and hypothesis generation** rather than as final decision-makers.

The most promising direction, in my view, is not choosing between unimodal and multimodal models, but learning how to combine their strengths.

---

### Acknowledgement
Thank you to Dr Maria Secrier and Dr Shi Pan from Secrier Lab (https://secrierlab.github.io/) at UCL Genetics Institute for supervising me.

### Links

- **Dissertation PDF:** `/assets/papers/dissertation.pdf`
- **LinkedIn:** `https://www.linkedin.com/in/ratneshwaran-maheswaran/`

