# Task 2 — Define and Review QC Metrics (with Tiering)

> **Goal:** Create a **tiered QC metric list** that balances comprehensiveness with practical adoption.

This task focuses on reviewing, refining, and organizing QC metrics for proteomics into a structured, tiered system aligned with the **PSI-MS controlled vocabulary (CV)**.
You'll ensure that the metrics used by pMultiQC and mzQC are both standardized and relevant across diverse workflows — from DDA to DIA and phosphoproteomics.

---

## Objectives

By the end of this task, you should have:
- [x] A finalized **tiered QC metric list** (Tier 1 = core, Tier 2 = extended, Tier 3 = specialized).
- [x] A clear mapping between each metric and its **PSI-MS CV accession** (MS:4000xxx).
- [x] A summary document (`metrics_tiering.tsv` or `.md`) describing metric tiers, categories, and applicable workflows.
- [x] Proposed new CV terms for missing metrics, following PSI-MS categorization.
- [x] Integration notes to support other tasks (Task 1 – mzQC export, Task 4 – SDRF integration).

---

## Background

### Why this matters

The mzQC format references metrics via **controlled vocabulary (CV) accessions** from the **PSI-MS ontology**.
These accessions (e.g. `MS:4000059` = *number of MS1 spectra*) ensure unambiguous communication of QC metrics across tools and datasets.
However, hundreds of potential QC measures exist — defining a practical tiering scheme makes adoption easier and more consistent.

### Inputs for this task

1. **The PSI-MS controlled vocabulary (CV):**
   - Source file → [`psi-ms.obo`](https://github.com/HUPO-PSI/psi-ms-CV/blob/master/psi-ms.obo)
   - Interactive browser → [Ontology Lookup Service (OLS)](https://www.ebi.ac.uk/ols/ontologies/ms)
     - Tip: search for terms in the **MS:4000000–MS:4999999** range (these correspond to QC metrics).
     - Inspect hierarchies to see how existing QC metrics are categorized.
2. **Curated literature-based metric list:**
   👉 [`docs/assets/curated_qc_metrics.tsv`](../assets/curated_qc_metrics.tsv)
   This file aggregates QC metrics reported across major studies.
3. **Example pMultiQC metrics** extracted from existing modules.

You'll integrate these sources into a harmonized, tiered QC ontology.

---

## Implementation Steps

1. **Review existing PSI-MS QC terms**
   - Use the [OLS browser](https://www.ebi.ac.uk/ols/ontologies/ms) or the raw [`psi-ms.obo`](https://github.com/HUPO-PSI/psi-ms-CV/blob/master/psi-ms.obo).
   - Search for QC metrics (`MS:4000xxx` terms) and note their definitions, parents, and units.
   - Identify overlapping or redundant entries.

2. **Review the curated literature-based list**
   - Check `curated_qc_metrics.tsv` for frequently used or experimentally validated metrics.
   - For each metric, determine:
     - If a matching PSI-MS CV term already exists.
     - Determine its category (e.g. part of the MS workflow).
     - The metric's level of general applicability (universal / specific).
     - Its preferred measurement unit.

3. **Assign tier levels**
   - **Tier 1 — Core metrics**: universally applicable across workflows.
     Examples: total ion current stability, MS2 scan count, precursor mass accuracy, identification rate.
   - **Tier 2 — Extended metrics**: valuable for deeper inspection or workflow-specific contexts.
     Examples: retention time reproducibility, chromatographic peak width, charge-state distribution.
   - **Tier 3 — Specialized metrics**: limited to niche applications.
     Examples: DIA precursor isolation purity, phosphopeptide localization rate, reporter ion interference.

4. **Apply categorization**
   - Assign each metric to one of the **existing PSI-MS QC categories** or propose a new one if justified.
   - Categories can be inferred from the PSI-MS "has_metric_category" relationships.
   - Ensure the chosen category reflects the metric's biological or technical context.

5. **Propose new metrics where gaps exist**
   - Identify missing or undefined metrics (e.g. DIA-specific signal completeness).
   - Add proposals to `ontology_extensions.tsv` with columns:
     | Name | Definition | Category | Applies To | Unit | Tier | Proposed CV ID |
     |------|------------|----------|------------|------|------|----------------|

6. **Document and summarize**
   - Write `metrics_tiering.md` summarizing:
     - Each Tier's purpose and scope.
     - Example metrics with PSI-MS accessions and categories.
     - Links to relevant OLS entries.

7. **Coordinate with other tasks**
   - **Task 1:** confirm metric names and CV IDs match those used in mzQC export.
   - **Task 4:** note which metrics benefit from SDRF metadata context (e.g. per instrument or condition).

---

## Tips & Pointers

- Focus on **clarity and reuse** — a compact, well-defined core set is most useful.
- Use OLS's **"children"** and **"is-a"** relationships to group similar metrics.
- Keep track of **units and value types** – they're critical for mzQC consistency.
- Discuss uncertain or ambiguous metrics with the group on Slack.
- If possible, include OLS permalinks in your final tiering table.

---

## Example Tiering Table

| Tier | Metric name | PSI-MS accession | Description | Applies to | Unit |
|------|--------------|------------------|--------------|-------------|------|
| 1 | total ion currents | [MS:4000104](https://www.ebi.ac.uk/ols/ontologies/ms/terms?iri=http://purl.obolibrary.org/obo/MS_4000104) | Tabular representation of the total ion current detected in each of a series of mass spectra. | All workflows | a.u. |
| 1 | number of MS2 spectra | [MS:4000060](https://www.ebi.ac.uk/ols/ontologies/ms/terms?iri=http://purl.obolibrary.org/obo/MS_4000060) | The number of MS2 events in the run. | DDA, DIA | count |
| 2 | Retention time stability | (proposed) | Std. dev. of RT across replicates | All workflows | min |
| 3 | DIA isolation purity | (proposed) | Average precursor isolation purity | DIA only | % |

---

## Definition of Done

- [ ] `metrics_tiering.tsv` (or `.md`) summarizing the tiered QC metric list created.
- [ ] Existing PSI-MS QC terms (`MS:4000xxx`) reviewed and mapped to tiers.
- [ ] Missing metrics proposed in `ontology_extensions.tsv`.
- [ ] Tier definitions and rationale documented in Markdown.
- [ ] Cross-checked consistency with Task 1 (export) and Task 4 (metadata).
- [ ] Pull Request opened and reviewed.
