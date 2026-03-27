# Zero-Shot Cell Annotation and State Prediction in Cancer Single-Cell RNA-seq

This repository hosts the GitHub Pages site for my MSc research project on zero-shot cell annotation and malignant state prediction in cancer single-cell RNA sequencing data.

The project explores whether large pre-trained foundation models can generalise to biologically meaningful prediction tasks without task-specific retraining, with a focus on challenging cancer settings where heterogeneity, domain shift, and limited labelled data make annotation difficult.

## Project Overview

Single-cell RNA sequencing has become a powerful tool for studying tumour composition, cell identity, and disease progression. However, accurate cell type annotation and state prediction often depend on supervised pipelines that require labelled reference data and may not generalise well across datasets.

This project investigates zero-shot approaches using pre-trained biological foundation models to test whether they can:

- distinguish malignant from non-malignant cells
- identify finer malignant cell states
- generalise across cancer datasets without full retraining

The broader aim is to understand both the promise and the limitations of zero-shot transfer in cancer single-cell analysis.

## Models Explored

This work evaluates multiple pre-trained models designed for biological representation learning, including:

- **Geneformer-V1**
- **Geneformer-V2-Cancer**
- **LangCell**

These models were compared on their ability to transfer to downstream cancer annotation tasks under a zero-shot setting.

## Research Questions

The project was guided by questions such as:

1. Can pre-trained foundation models separate malignant from non-malignant cells in unseen cancer datasets?
2. Can these models capture more fine-grained malignant cell states beyond broad class separation?
3. How robust are their learned representations under dataset shift and biological heterogeneity?
4. What are the practical limitations of zero-shot annotation in cancer single-cell genomics?

## Key Findings

Some of the main takeaways from the project include:

- Zero-shot foundation models can provide useful biological signal for broad classification tasks
- Performance is stronger for coarse-grained discrimination than for subtle malignant state prediction
- Generalisation remains challenging across datasets, especially where tumour state definitions are noisy or biologically overlapping
- Representation quality varies across models, showing that domain-specific pretraining matters

Overall, the results suggest that zero-shot approaches are promising, but not yet sufficient as a standalone solution for difficult cancer annotation tasks.

## Repository Contents

```text
docs/
├── _config.yml
├── index.md
├── about.md
├── _posts/
│   └── 2026-03-27-zero-shot-cell-annotation-cancer-single-cell.md
└── assets/