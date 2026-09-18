<div align="center">

# Joyful Jaw

### An Auditable Clinical Reasoning and Explainability Resource for Temporomandibular Disorder Large Language Models

*Running title: Auditable TMD LLM Resource*

[![Manuscript](https://img.shields.io/badge/Manuscript-Under%20Review-blueviolet)](#paper-status)
[![Code](https://img.shields.io/badge/Code-Coming%20Soon-lightgrey)](#code-availability)
[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](#license)
[![Domain](https://img.shields.io/badge/Domain-Temporomandibular%20Disorders-1f6feb)](#overview)

</div>

---

## Overview

Joyful Jaw is a research resource for evaluating and developing **specialist large language models (LLMs) for temporomandibular disorders (TMDs)**. It was built around a single organising principle — **end-to-end explainability (E2E-XAI)** — which asks that every model output be traceable from the evidence it draws on, through the clinical pathway it activates, to the recommendation it produces.

Reusable benchmarks for medical LLMs rarely assess whether a model's answers are grounded in **inspectable clinical reasoning** and **traceable evidence**. Most existing evaluations report answer accuracy, semantic similarity, or output-level citations, but do not expose how evidence was selected, how patient features were mapped to diagnostic pathways, or how competing diagnoses were compared. Joyful Jaw addresses this gap by combining an evidence-graded knowledge base, explicit diagnostic pathways, a bilingual specialist benchmark, blinded human rating instruments, and a retrospective case-based assessment within a single framework.

The resource is intended for **pre-deployment benchmarking and model development**. It is not a clinical decision-support product, and the reported results do not establish clinical effectiveness, safety, or readiness for autonomous use.

---

## Research Objectives

1. **Make clinical reasoning auditable.** Build and operationalise a framework in which evidence provenance, knowledge organisation, patient-feature matching, pathway activation, and response generation are all inspectable rather than implicit.
2. **Separate knowledge accuracy from explainability.** Evaluate specialist models across complementary dimensions — knowledge, reasoning, explainability, and usability — instead of ranking them by answer accuracy alone.
3. **Test whether the framework discriminates between models.** Compare a purpose-built TMD model against general-purpose models across task types and evaluator groups.
4. **Provide a reusable, extensible reference implementation.** Supply a schema, benchmark, and evaluation protocol that can be adapted to other clinical domains.

---

## Core Methodology

The resource comprises four integrated components.

| Component | Description |
|---|---|
| **Evidence-graded Knowledge Forest** | A structured representation of the global evidence topology. Sources are screened for relevance, assigned one of five evidence grades (**A+** to **D**), mapped to the smallest clinically meaningful node, checked for semantic consistency and clinical plausibility, and versioned. A separate layer of **subtype logical trees** represents local diagnostic reasoning units. |
| **E2E-XAI operationalisation** | End-to-end explainability links evidence acquisition, knowledge organisation, patient-feature standardisation, pathway-level reasoning, evidence-constrained response generation, and knowledge updating. Patient features activate **supporting, weakening, or coexisting** pathways, and outputs are linked to identifiable nodes and source records. |
| **Pathway-based retrieval with an LLM** | Retrieved evidence is organised within explicit clinical pathways rather than being passed to the model as an unstructured context. Evidence Confidence Scoring combines semantic relevance (0.4), evidence grade (0.4), and a time factor (0.2); responses are rejected when the maximum confidence score falls below 0.6. A TMD-specific model (**Joyful Jaw**) was adapted from a 7B open base model using low-rank adaptation on 1,842 instruction–response pairs derived from 326 de-identified clinical records, kept strictly separate from the evaluation set. |
| **Multi-level evaluation** | A bilingual (Chinese/English) benchmark spanning multiple-choice, noun-explanation, and short-answer tasks across anatomy and physiology, pathogenesis, and clinical diagnosis; blinded ratings by five TMD experts and five non-expert clinicians using a prespecified rubric; and a retrospective case-based diagnostic comparison against three dentists with less than three years of practice across 36 cases. |

Evaluation used accuracy for multiple-choice items and BERTScore-F1 for generative answers. Inter-rater reliability was assessed with two-way random-effects intraclass correlation coefficients, and model comparisons used Friedman tests followed by paired Wilcoxon signed-rank tests with Bonferroni correction.

---

## Key Features

- **Evidence-graded knowledge representation** — five evidence tiers (A+ to D) with provenance, scope, grade, and update status retained for every source.
- **Inspectable pathway reasoning** — explicit subtype pathways that show how patient features support, weaken, or coexist across candidate diagnoses.
- **Evidence-constrained generation** — retrieval results are mapped into clinical pathways, and outputs are traced back to identifiable knowledge nodes and sources.
- **Confidence-gated responses** — an evidence confidence score with a rejection threshold for weakly supported generations.
- **Bilingual specialist benchmark** — parallel Chinese and English task sets covering knowledge, pathogenesis, and clinical diagnosis.
- **Dual-evaluator rating framework** — blinded instruments administered independently to TMD specialists and non-specialist clinicians.
- **Case-based diagnostic comparison** — retrospective assessment against reference diagnoses and practising clinicians.
- **Ablation-ready architecture** — component-level ablation supports attribution of performance to the complete system.
- **Domain-adaptable schema** — the Knowledge Forest schema, evaluation protocol, and rating instruments are designed to be reused in other specialties.

---

## Main Contributions

- An **integrated evaluation resource** that links evidence provenance, structured diagnostic pathways, bilingual benchmarking, blinded specialist and non-specialist ratings, and case-based diagnostic comparison within a single framework.
- A **knowledge resource** containing 6,950 entity nodes (6,550 of them evidence nodes) and 6,944 semantic relationships, with 60.9% of evidence nodes at the two highest evidence grades.
- Evidence that **model rankings depend on both task type and evaluator group** — a purpose-built TMD model led expert-rated and non-expert-rated case analysis and expert-rated extended questions, whereas a general-purpose model led non-expert-rated extended questions. This supports reporting task-specific and user-specific outcomes rather than a single aggregate score.
- A **reproducible protocol and schema** for domains in which evidence traceability and clinical reasoning, rather than answer accuracy alone, are the evaluation targets.

---

## Results at a Glance

| Evaluation | Outcome |
|---|---|
| Multiple-choice accuracy (bilingual) | 92.5% overall (19/20 Chinese, 18/20 English) |
| Noun-explanation BERTScore-F1 | 0.721 (Chinese) / 0.863 (English) |
| Short-answer BERTScore-F1 (pooled) | 0.797 |
| Case analysis, mean score | 96.2% (TMD experts) / 89.6% (non-experts) |
| Extended questions, mean score | 89.2% among experts (rank 1); 88.9% among non-experts (rank 2) |
| Retrospective diagnostic agreement | 32/36 cases (88.9%) matched the reference diagnosis, versus 72.2%, 77.8%, and 66.7% for three junior dentists |

> Comparative rankings are **time-specific**, as model versions and commercial systems change. These retrospective results are descriptive and were not a prospective test of clinical effectiveness.

---

## Paper Status

**Status: manuscript under review.**

This repository accompanies a research paper currently under submission to a peer-reviewed journal. The study is a multicentre retrospective technical-development and validation study; it was reviewed and approved by the Ethics Committee of Jiangsu Provincial Stomatological Hospital (PJ2025-026-01), which waived informed consent for the use of de-identified retrospective records.

**Authors:** Jinyi Zhu; Siying Zhu; Hengjia Zhang; Lei Mei; Yining Hu; Yang Liu; Lizhe Xie\*

\* Corresponding author.

**Keywords:** temporomandibular disorders; large language models; clinical reasoning; explainability; Knowledge Forest; benchmark.

---

## Code Availability

> **Code coming soon.**

To preserve the integrity of the peer-review process, the implementation is not released at this stage. Upon acceptance of the manuscript, the following will be made available through a stable repository with a citable DOI:

- Analysis code and evaluation scripts
- Prompt templates and prespecified decoding settings
- The releasable portion of the bilingual benchmark
- Knowledge Forest schema and non-patient metadata
- Figure source data and documentation

The code will be released under the **Apache License 2.0**, subject to third-party software licences. Model weights or adapters will be released only where permitted by the base-model licence, institutional intellectual-property review, benchmark licences, and patient-privacy safeguards, and will be accompanied by a model card describing intended use, excluded uses, training-data provenance at an aggregate level, performance boundaries, and safety limitations.

Patient-level data cannot be released publicly: the ethics approval and consent waiver do not permit unrestricted redistribution of individual records. Requests for a minimum de-identified dataset and data dictionary may be submitted to the corresponding author and will be reviewed by the institutional Data Access Committee. Approved data may be used only for the agreed non-commercial research purpose in a secure environment, and may not be redistributed or used for re-identification.

---

## Repository Contents

This repository is being prepared for the release described above. The structure below will be populated when the code becomes available.

```
Joyful-Jaw/
├── knowledge-forest/      # Knowledge Forest schema and non-patient metadata
├── pathways/              # Subtype reasoning pathway definitions
├── benchmark/             # Releasable bilingual evaluation tasks
├── evaluation/            # Scoring, rating, and statistical analysis scripts
├── prompts/               # Prompt templates and decoding settings
├── docs/                  # Documentation and model card
└── README.md
```

---

## Citation

A full citation will be provided once the manuscript is published. In the meantime, please cite the paper as:

```bibtex
@article{joyfuljaw_tmd_llm,
  title  = {An auditable clinical reasoning and explainability resource for
            temporomandibular disorder large language models},
  author = {Zhu, Jinyi and Zhu, Siying and Zhang, Hengjia and Mei, Lei and
            Hu, Yining and Liu, Yang and Xie, Lizhe},
  note   = {Manuscript under review},
  year   = {2026}
}
```

---

## Contact

For questions about the study, the evaluation protocol, or data access requests, please contact the corresponding author:

**Prof. Lizhe Xie, PhD**
The Affiliated Stomatological Hospital of Nanjing Medical University, Nanjing, China
Jiangsu Provincial Stomatological Hospital
Email: [xielizhe@njmu.edu.cn](mailto:xielizhe@njmu.edu.cn)

For questions specifically about this repository, please open an issue.

---

## Acknowledgments

This study was supported by the National Natural Science Foundation of China (grant 82571165), the National Key Research and Development Program of China (grant SQ2023YFC2400025), and the Key Research and Development Program of Jiangsu Province (grant BE2023836). The funders had no role in study design; data collection, analysis, or interpretation; writing of the report; or the decision to submit the paper for publication.

## License

This project is licensed under the **Apache License 2.0**. See the [LICENSE](LICENSE) file for the full license text.

The licence applies to the released implementation, benchmark, schema, and documentation, subject to the terms of any bundled third-party software.

Copyright 2026 The Joyful Jaw Authors.

## Disclaimer

This repository and the accompanying resource are provided for **research and evaluation purposes only**. They are not intended for clinical diagnosis, treatment decisions, or any other clinical use. The reported performance is retrospective and does not establish clinical effectiveness, safety, or readiness for autonomous use.
