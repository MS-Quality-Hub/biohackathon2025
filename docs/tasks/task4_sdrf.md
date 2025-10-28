# Task 4 — Strengthen SDRF Integration

> **Goal:** Use **SDRF-Proteomics metadata** to guide QC generation and dataset annotation.

This task focuses on connecting **sample metadata** (from SDRF files) with **QC metrics** (from pMultiQC / mzQC).
By linking sample- and experiment-level descriptors to QC values, we enable **metadata-driven quality assessment** — letting users explore and compare QC results grouped by experimental factors, instruments, or study design.

---

## Objectives

By the end of this task, you should have:
- [x] Code that can **parse SDRF-Proteomics** metadata files and extract key descriptors.
- [x] Logic that **links each run's QC metrics** (from mzQC or pMultiQC output) to the corresponding SDRF sample row.
- [x] Prototype functionality to **group or summarize QC** by factors such as treatment, replicate, fraction, or instrument.
- [x] Example datasets, documentation, and a clear workflow description.

---

## Background

### What is SDRF-Proteomics?

The **Sample and Data Relationship Format (SDRF)** defines how samples, runs, and data files are linked in proteomics studies.
It's part of the **Investigation/Study/Assay (ISA)** model used across omics and is central to **FAIR data practices**.

- Repository: [https://github.com/bigbio/proteomics-sample-metadata](https://github.com/bigbio/proteomics-sample-metadata)
- Specification: [https://github.com/bigbio/proteomics-sample-metadata/tree/master/sdrf-proteomics](https://github.com/bigbio/proteomics-sample-metadata/tree/master/sdrf-proteomics)
- File format: **tab-delimited text (SDRF.tsv)**, one row per run/file, with columns for sample attributes and data files.

### Why integrate SDRF with QC?

Several public proteomics datasets already provide SDRF files in PRIDE or MassIVE.
By parsing these alongside QC outputs, we can:
- **Annotate QC results** with contextual metadata (sample type, instrument, fraction, etc.).
- **Compare QC metrics** across experimental factors (e.g. replicate reproducibility).
- Enable **repository-level dashboards** that allow filtering or grouping by metadata fields.

---

## Implementation Steps

### 1. Get familiar with SDRF-Proteomics

- Review example SDRF files in the [specification repo](https://github.com/bigbio/proteomics-sample-metadata/tree/master/annotated-projects).
- Typical columns include:
  | Category | Example columns |
  |-----------|----------------|
  | File identification | `comment[data file]`, `comment[file uri]` |
  | Sample description | `characteristics[organism]`, `characteristics[cell type]` |
  | Experimental design | `comment[technical replicate]`, `characteristics[biological replicate]`, `comment[fraction identifier]` |
  | Instrumentation | `comment[instrument]`, `comment[modification parameters]` |

### 2. Parse SDRF files

- Use Python's `pandas` or the official SDRF utilities (in `sdrf-pipelines` package):
  ```bash
  pip install sdrf-pipelines
  ```
- Identify columns that correspond to data files or runs — these will link to QC metrics (usually `comment[data file]`).

### 3. Link SDRF entries to QC results

- An mzQC file or pMultiQC run summary typically represents a **single raw file or assay**.
- Establish the mapping between:

  | SDRF column               | QC metadata field    |
  | ------------------------- | -------------------- |
  | `comment[data file]`      | QC input file name   |
  | `comment[fraction identifier]` | grouping variable    |
  | `comment[instrument]`     | acquisition metadata |

### 4. Group QC metrics by experimental factors

- Once linked, you can group and summarize metrics across sample categories.
- Produce simple plots showing QC variation across factors.

### 5. Output enriched QC summaries

- Write out combined tables, e.g. `qc_grouped_by_factor.mzqc` – aggregated metrics per condition.

### 6. Integrate with pMultiQC

- Optional: Add a hook or plugin that reads SDRF metadata before/after QC aggregation.
- This could enable:
  - Conditional QC visualization by treatment or replicate.
  - Adding SDRF metadata to the report summary tables.
- Follow the [pMultiQC contributing guide](https://github.com/bigbio/pmultiqc/blob/main/CONTRIBUTING.md) for integration style and branch setup.

---

## Tips & Pointers

- The **SDRF-Proteomics validator** (part of `sdrf-pipelines`) can check file consistency.
- Keep your parser tolerant of optional or missing columns.
- Use **FAIR metadata principles** — prefer controlled terms and standard column headers.
- Coordinate with **Task 2** (QC metric tiering) to ensure metadata categories align (e.g. instrument, workflow type).
- Coordinate with **Task 1** to test whether merged QC + SDRF data can be serialized back into `.mzQC`.

---

## Definition of Done

* [ ] SDRF parsing working (columns correctly loaded and mapped).
* [ ] QC metrics successfully joined to SDRF metadata by data file or assay.
* [ ] Grouped QC summaries computed (e.g. per treatment or instrument).
* [ ] Output tables or enriched mzQC created.
* [ ] Short documentation added under `/docs/tasks/`.
* [ ] Pull request opened and reviewed.
