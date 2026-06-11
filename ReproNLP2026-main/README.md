# ReproNLP 2026: A Third Replication of the Human Evaluation of a QAG System for Children's Storybooks

[![ACL Anthology](https://img.shields.io/badge/ACL-Anthology-red)](https://aclanthology.org/)

## Overview

This repository contains all data, code, and supplementary materials for the paper:

> **ReproNLP 2026: A Third Replication of the Human Evaluation of a QAG System for Children's Storybooks**
> Marcel Mroczek, Chiara Albarello, Paul-Emmanuel Floch, Maciej Gawinecki
> *Proceedings of the 5th Workshop on Generation, Evaluation and Metrics (GEM 2026), July 2026, San Diego, CA, USA*

This paper presents a third independent replication of the human evaluation originally conducted by [Yao et al. (2022)](https://aclanthology.org/2022.acl-long.54/), which assessed an automated Question-Answer Generation (QAG) system for children's storybooks. The QAG system was evaluated against a baseline and human-authored ground truth across three criteria — Readability, Question Relevance, and Answer Relevance — using five Natural Language Processing (NLP)-literate annotators. Our replication confirms the main findings of the original study: the QAG system outperforms the baseline on Readability and Question Relevance, and the Ground Truth (GT) ranks highest across all criteria. System rankings are preserved across all three criteria, with the exception of a statistically non-significant difference in Answer Relevance. We additionally document several methodological concerns, including data quality issues and evaluation design limitations identified during our pilot study, some of which were unreported in prior replications.

This work is a submission to the [ReproNLP](https://repronlp.github.io/) 2026 shared task, part of the ongoing [ReproHum](https://reprohum.github.io/) research programme.

## Repository Structure

```
.
├── annotations/             # Raw annotation data from all four studies
├── images/                  # Figures generated for the paper and poster
├── qra/                     # Input/output files for the QRA3 reproducibility tool
├── datacard.json            # Human Evaluation Datasheet (HEDS) for this study
├── replication_study.ipynb  # Main analysis notebook
└── requirements.txt         # Python dependencies
```


## Annotation Data

The `annotations/` folder contains item-level human annotations from all four studies analysed in this paper. Each CSV file provides one row per annotated question-answer (QA) pair, with columns for `labeller_id`, `story_name`, `qa_id`, `section_id`, `System` (one of `QAG`, `PAQ`, `GT`), and the three quality criteria scores.

| File | Description |
|---|---|
| `mroczek2026.csv` | Annotations collected for **this** replication study |
| `yao2022.csv` | Annotations from the original study by [Yao et al. (2022)](https://aclanthology.org/2022.acl-long.54/) |
| `florescu2024.csv` | Annotations from the first replication by [Florescu et al. (2024)](https://aclanthology.org/2024.humeval-1.10/) |
| `braun2025.csv` | Annotations from the second replication by [Braun (2025)](https://aclanthology.org/2025.gem-1.52/) |

> **Note:** The notebook downloads the `yao2022`, `florescu2024`, and `braun2025` annotation files automatically from their original public repositories on demand if they are not already present locally.

The evaluation was conducted on a subset of the [FairytaleQA dataset](https://aclanthology.org/2022.acl-long.34/) ([Xu et al., 2022](https://aclanthology.org/2022.acl-long.34/)), which comprises approximately 10,000 expert-annotated QA pairs from 278 children's storybooks spanning kindergarten to eighth-grade reading level.


## Analysis Notebook

`replication_study.ipynb` is a Jupyter Notebook that reproduces all tables and in-text statistics reported in the paper, as well as additional visualisations for the conference poster.

| Section | Content |
|---|---|
| Table 1 | Mean scores and standard deviations across all studies |
| Table 2 | Inter-annotator agreement (Krippendorff's α) |
| Table 3 | Pairwise system comparisons (this study) |
| Table 4 | QAG vs. PAQ *t*-test comparison across all studies |
| Table 5 | Pairwise CV\* reproducibility across studies |
| Tables 6 & 7 | QRA3 input files (consumed by the external QRA3 tool) |
| §Discussion: `val` impact | Pairwise comparisons on `val`-placeholder-filtered data |
| §Discussion: Item-level correlation | Pearson/Spearman/Kendall correlations between the original study and this replication |
| Poster | Additional visualisations (QAG output examples, IAA collapse heatmap, full vs. cleaned data comparison) |

### Setup

Requires Python 3.12. Install all dependencies via:

```bash
pip install -r requirements.txt
```

Then launch the notebook:

```bash
jupyter notebook replication_study.ipynb
```


## Quantitative Reproducibility Assessment (QRA3)

We report reproducibility using the [QRA3 framework](https://direct.mit.edu/coli/article/doi/10.1162/COLI.a.625/136454/Quantified-Reproducibility-Assessment-for-Four) ([Belz & Thomson, 2026](https://direct.mit.edu/coli/article/doi/10.1162/COLI.a.625/136454/Quantified-Reproducibility-Assessment-for-Four)), which provides quantitative reproducibility assessments at three levels of granularity using measures comparable across studies.

The notebook computes aggregated system-level means and saves them as QRA3-format input files in the `qra/` folder. These are then consumed by the external [QRA3 command-line tool](https://github.com/DCU-NLG/qra).

**For *n* = 3 studies (all three criteria — Readability, Question Relevance, Answer Relevance):**

```bash
qra \
    --input "qra/metrics-3-studies.csv" \
    --config "qra/config-3-studies.json" \
    --krippendorff-alpha-mode ordinal \
    --out-dir "qra/output-3-studies" \
    --force
```

**For *n* = 4 studies (Readability only, including [Braun, 2025](https://aclanthology.org/2025.gem-1.52/) who evaluated only this criterion):**

```bash
qra \
    --input "qra/metrics-4-studies.csv" \
    --config "qra/config-4-studies.json" \
    --krippendorff-alpha-mode ordinal \
    --out-dir "qra/output-4-studies" \
    --force
```



## Human Evaluation Datasheet (HEDS)

`datacard.json` is the Human Evaluation Datasheet (HEDS) ([Belz & Thomson, 2022](https://aclanthology.org/2025.gem-1.6/)) for this study. A separate HEDS record is also available at: https://github.com/nlp-heds/repronlp2026


## Images

The `images/` directory contains all figures generated by the notebook for use in the paper and poster, including:

- Inter-annotator agreement (IAA) heatmaps
- Answer Relevance comparison: full data vs. `val`-artifact-cleaned data


## How to Cite

If you use the data, code, or findings from this paper, please cite:

```bibtex
@inproceedings{mroczek-etal-2026-repronlp,
  author    = {Mroczek, Marcel and Albarello, Chiara and Floch, Paul-Emmanuel and Gawinecki, Maciej},
  title     = {ReproNLP 2026: A Third Replication of the Human Evaluation of a QAG System for Children's Storybooks},
  booktitle = {Proceedings of the 5th Workshop on Generation, Evaluation and Metrics (GEM 2026)},
  month     = {July},
  year      = {2026},
  address   = {San Diego, CA, USA},
  publisher = {Association for Computational Linguistics}
}
```

### Related Works

Please also consider citing the original study and prior replications that this work builds upon:

- **Original study:** [Yao et al. (2022)](https://aclanthology.org/2022.acl-long.54/) — *It is AI's Turn to Ask Humans a Question: Question-Answer Pair Generation for Children's Story Books*
- **First replication:** [Florescu et al. (2024)](https://aclanthology.org/2024.humeval-1.10/) — *Once Upon a Replication: It is Humans’ Turn to Evaluate AI’s Understanding of Children’s Stories for QA Generation*
- **Second replication:** [Braun (2025)](https://aclanthology.org/2025.gem-1.52/) — *ReproHum #0031-01: Reproducing the Human Evaluation of Readability from “It is AI’s Turn to Ask Humans a Question”*
- **FairytaleQA dataset:** [Xu et al. (2022)](https://aclanthology.org/2022.acl-long.34/)
- **QRA3 framework:** [Belz & Thomson (2026)](https://direct.mit.edu/coli/article/doi/10.1162/COLI.a.625/136454/Quantified-Reproducibility-Assessment-for-Four)
- **ReproNLP shared task series:** [Belz & Thomson (2023)](https://aclanthology.org/2023.humeval-1.4/), [Belz & Thomson (2024)](https://aclanthology.org/2024.humeval-1.9/), [Belz et al. (2025)](https://aclanthology.org/2025.gem-1.78/), Belz et al. (2026)



## Acknowledgements

We thank Katarzyna Basista for her participation in the pilot study, the anonymous annotators who participated in the human evaluation, the ReproNLP shared task organisers (especially Craig Thomson), and the original authors for providing additional information to the ReproHum team.
