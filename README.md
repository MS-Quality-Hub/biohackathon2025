# 🧬 Project 29: Repository-Scale Quality Control in Proteomics
*ELIXIR BioHackathon 2025*

> **Let's make public proteomics data FAIR and re-usable — at repository scale.**

Mass spectrometry proteomics has generated an enormous global resource:
**>31,000 datasets** in PRIDE alone, representing millions of biological samples.
Yet, much of this treasure trove remains underused because quality information is inconsistent or missing.

This project tackles that head-on.
Together, we'll build an **automated, standardized quality control (QC) framework** that can operate directly on public data repositories — producing **machine-readable QC summaries (mzQC)** linked with rich **experimental metadata (SDRF-Proteomics)**.

By the end of the week, our prototype will:
- Generate mzQC outputs directly from **pMultiQC**.
- Define a **core QC metric ontology** adopted across tools.
- Leverage metadata to **inform and contextualize QC analyses**.
- Pave the way for **FAIR, ML-ready proteomics data reuse**.

If you're excited about open science, reproducible bioinformatics, and hands-on development with real impact on the global proteomics community — **join us!**

[![BioHackathon 2025](https://img.shields.io/badge/ELIXIR-BioHackathon%202025-orange)]()
[![Contributions Welcome](https://img.shields.io/badge/Contributions-Welcome-brightgreen)]()
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)

---

## Project Goals

**Main objective:**
Build an end-to-end framework to enrich public proteomics datasets with **standardized quality control (QC) information**.

**Key components:**
- [**mzQC**](https://github.com/HUPO-PSI/mzQC): HUPO-PSI JSON format for standardized QC reporting.
- [**pMultiQC**](https://github.com/bigbio/pmultiqc): modular, multi-workflow QC tool for proteomics pipelines.
- [**SDRF-Proteomics**](https://www.ebi.ac.uk/pride/markdownpage/sdrf): standardized experimental metadata schema.

**Expected outcomes by the end of the hackathon:**
- pMultiQC extended to export results in **mzQC** format.
- A refined and tiered **QC metric ontology**.
- Broader workflow coverage via **new adapters**.
- Enhanced **SDRF integration** for metadata-driven QC.
- Prototype **ID-free QC** modules for raw-data assessment.
- Documentation and examples for repository integration.

---

## Documentation & Resources

- [Tasks Overview](./docs/tasks/README.md): Summary of all hackathon tasks and roles
- [Task 1 — mzQC Export in pMultiQC](./docs/tasks/task1_mzqc_export.md): Implement mzQC output generation
- [Task 2 — Tiered QC Metrics](./docs/tasks/task2_metrics.md): Curate and define core/extended metrics
- [Task 3 — Workflow Adapters](./docs/tasks/task3_adapters.md): Add support for new tools (e.g., FragPipe, MaxQuant)
- [Task 4 — SDRF Integration](./docs/tasks/task4_sdrf.md): Link sample metadata to QC analyses
- [Task 5 — ID-Free QC](./docs/tasks/task5_idfree.md): Develop raw-level QC modules
- [Optional Extensions](./docs/tasks/task6_optional.md): Dashboards, benchmark datasets, ML exploration
- [Reference Material](./docs/resources.md): Links to mzQC, pMultiQC, and SDRF docs
- [Example Outputs](./examples): Example `.mzQC` files + validation tips

---

## Collaboration & Contribution

- BioHackEU Slack channel: `#29-towards-repository-scale-quality-control`.
- Daily stand-up: 09:00.
- Ideas or questions? Use [Discussions](/discussions).
- Bugs / progress updates? Open [Issues](./issues).
- Code changes: via [Pull Requests](./pulls).

### Contribution Workflow

- Fork the repo and create a branch: `feature/<task-name>`.
- Follow our [coding guidelines](./CONTRIBUTING.md).
- Commit changes and reference your issue (e.g. "Fixes #12").
- Open a PR → review → merge during daily sync.
