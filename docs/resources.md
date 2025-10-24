# Resources and Background

Welcome to the **Repository-Scale Quality Control** project!
This page collects all background information, standards, and tools relevant to our BioHackathon work.
It's your starting point if you're new to **mzQC**, **pMultiQC**, or **SDRF-Proteomics**, or if you want to understand how these pieces fit together before contributing code.

---

## Overview — How It All Fits Together

Proteomics repositories such as **PRIDE** contain tens of thousands of datasets, yet data reuse is limited because **quality control (QC)** information is inconsistent.
Our project connects three community standards to make QC consistent, automated, and FAIR:
- [**pMultiQC**](https://github.com/bigbio/pmultiqc) computes QC metrics from proteomics workflows.
- [**mzQC**](https://github.com/HUPO-PSI/mzQC) provides a standardized, machine-readable format for those metrics.
- [**SDRF-Proteomics**](https://www.ebi.ac.uk/pride/markdownpage/sdrf) supplies sample and experiment metadata to contextualize QC analyses.

Together, these enable automated, repository-scale QC summaries that can be used for data selection, benchmarking, and machine learning.

---

## Core Standards and Tools

### mzQC — Standardized QC Reporting

- **What it is:** A HUPO-PSI JSON format describing QC metrics in a structured, interoperable way.
- **Why it matters:** Ensures that QC data are comparable across tools, workflows, and repositories.
- **Learn more:**
  - Specification → <https://hupo-psi.github.io/mzQC/>
  - GitHub repository → <https://github.com/HUPO-PSI/mzQC>
  - Controlled vocabulary (CV) → <https://github.com/HUPO-PSI/psi-ms-CV/>
- **Useful tools:**
  - [`pymzqc`](https://github.com/MS-Quality-hub/pymzqc) — Python API for reading and writing mzQC files.
  - Schema validator → <https://hupo-psi.github.io/mzQC/validator/validation/>

---

### pMultiQC — Modular QC Aggregation
- **What it is:** A proteomics-centric extension of MultiQC that aggregates QC results across workflows and tools.
- **Why it matters:** It is the computational backbone of this project — the component we'll extend to export standardized mzQC output.
- **Learn more:**
  - Documentation → <https://pmultiqc.quantms.org/>
  - GitHub → <https://github.com/bigbio/pmultiqc>
- **Typical inputs:** output results from tools such as quantms, MaxQuant, or DIA-NN.
- **Hackathon goal:** add mzQC export and broaden workflow coverage through new adapters.

---

### SDRF-Proteomics — Metadata for Contextualized QC
- **What it is:** A standardized, tab-separated format describing sample, instrument, and experimental design metadata.
- **Why it matters:** Links QC metrics to biological and technical factors — essential for metadata-driven QC analyses.
- **Learn more:**
  - GitHub repository → <https://github.com/bigbio/proteomics-sample-metadata>
  - Documentation → <https://www.ebi.ac.uk/pride/markdownpage/sdrf>
- **Tools:**
  - [`sdrf-pipelines`](https://github.com/bigbio/sdrf-pipelines) — Python parser and validator.
  - [lesSDRF](https://lessdrf.streamlit.app/) — Web app to create SDRF files.
- **Hackathon goal:** integrate SDRF metadata into QC generation and reporting.

---

## Background — QC in Proteomics

**Why QC matters:**
Quality control assesses the performance of an MS experiment and ensures that datasets are reliable, comparable, and suitable for downstream analyses or ML training.

**Common QC metrics:**
- Total ion current (TIC) stability
- MS1/MS2 scan counts
- Precursor mass accuracy
- Retention-time reproducibility
- Identification rate and PSM coverage
- Chromatographic peak width or symmetry
