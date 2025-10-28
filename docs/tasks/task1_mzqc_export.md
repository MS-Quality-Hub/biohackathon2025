# Task 1 — Implement mzQC Export in pMultiQC

> **Goal:** Enable pMultiQC to produce fully compliant `.mzQC` outputs for proteomics QC workflows.

This task focuses on extending **pMultiQC** to export standardized, machine-readable QC results using the **mzQC** format.
You'll bridge the gap between pMultiQC's internal data structures and the official mzQC schema — turning QC summaries into reusable, FAIR data objects ready for repository integration.

---

## Objectives

By the end of this task, you should have:
- [x] A new pMultiQC module that writes valid mzQC output.
- [x] Provenance tracking of input files, workflow versions, and software environment.
- [x] Validation of produced files against the official mzQC schema.
- [x] Example outputs under `/examples/mzqc/`.

---

## Background

### What is mzQC?

mzQC is an **open HUPO-PSI standard** for reporting QC metrics in JSON format.
It ensures consistent, structured representation of quality metrics across tools, datasets, and repositories.

Key features:
- JSON-based, both human- and machine-readable.
- Controlled vocabulary (CV) for metric identifiers and units.
- Provenance information (input files, software, parameters).
- Extensible schema for new metrics and community growth.

→ See [mzQC resources](../resources.md#mzqc--standardized-qc-reporting) for details and links.

### What is pMultiQC?

pMultiQC aggregates QC results from multiple proteomics workflows (e.g. quantms, MaxQuant, DIA-NN) and outputs interactive HTML reports.
Internally, it already stores QC data as structured Python objects — the goal here is to **serialize those data into standardized mzQC**.

→ See [pMultiQC resources](../resources.md#pmultiqc--modular-qc-aggregation).

---

## Implementation Steps

### 0. Work in the Hackathon Branch
> [!WARNING]
> All hackathon-related changes to pMultiQC should be made in the dedicated fork:
> [https://github.com/MS-Quality-Hub/pmultiqc](https://github.com/MS-Quality-Hub/pmultiqc)

- Fork this repository and create your feature branch from it, e.g.:
  ```bash
  git clone https://github.com/MS-Quality-Hub/pmultiqc.git
  cd pmultiqc
  git checkout -b feature/mzqc-export
  pip install -e .
- Do not modify the upstream `bigbio/pmultiqc` repository directly — this ensures clean integration of all hackathon contributions.

1. **Explore pMultiQC's internal data structures**
   - Look under `pmultiqc/modules/` and identify where metrics are aggregated.
   - Identify which metadata (tool versions, file paths, timestamps) are available for provenance.

2. **Map internal metrics to the mzQC schema**
   - Use `pymzqc` to construct `MzQcFile`, `RunQuality`, and `QualityMetric` objects.
   - Map pMultiQC metrics to mzQC CV terms.
   - If a metric lacks an existing CV term, note it for **Task 2** (metric ontology extension).

3. **Integrate mzQC export into existing output writing**
   - Add an mzQC serialization step where pMultiQC already writes summary data.
   - Use `pymzqc.to_json()` to serialize the mzQC object.
   - Save the file with a consistent naming convention, e.g. `qc_report.mzQC`, alongside the HTML report.

4. **Add provenance and metadata**
   - Capture software version (`pmultiqc.__version__`), date/time of export, and input file names.
   - Add this information to the `metaData` and `runQualities` fields in mzQC.

5. **Validate output**
   - Use the [online mzQC validator](https://hupo-psi.github.io/mzQC/validator) to ensure your file conforms to the schema.
   - Upload your generated `.mzQC` file and verify that:
     - The schema validation passes successfully.
     - All metric identifiers and units are recognized CV terms.
   - If any warnings or errors appear, document and fix them before submission.

6. **Document and commit**
   - Place example outputs in `/examples/mzqc/`.
   - Add notes to `/docs/tasks/task1_mzqc_export.md` under "Results."
   - Open a pull request referencing your issue.

---

## Tips & Pointers

- **Start small:** Begin with a minimal subset of metrics (e.g. total ion current, MS2 count).
- **Reuse existing tools:** The [`pymzqc`](https://github.com/MS-Quality-hub/pymzqc) package handles object creation and validation.
- **Follow JSON best practices:** Pretty-print for human readability, ensure UTF-8 encoding.
- **Collaborate:** Coordinate with Task 2 (CV metrics) to ensure consistent term usage.

---

## Definition of Done

- [ ] pMultiQC can export a valid `.mzQC` file as part of its output pipeline.
- [ ] All metrics use valid CV terms and units (or proposed new terms).
- [ ] Provenance information (software version, input files, date) is included.
- [ ] Output passes the online validator without errors.
- [ ] Example `.mzQC` file added to `/examples/mzqc/`.
- [ ] Pull Request opened and reviewed.
