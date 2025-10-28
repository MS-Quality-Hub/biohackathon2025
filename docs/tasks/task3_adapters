# Task 3 — Build Adapters for Additional Workflows and Search Engines

> **Goal:** Extend **pMultiQC** to support additional proteomics workflows and tools, enabling broader adoption and repository-scale quality control.

This task focuses on adding new **adapters (modules)** to pMultiQC for parsing QC-relevant outputs from additional search engines, quantification tools, and workflow systems.
By expanding pMultiQC's coverage, we can automatically compute standardized QC metrics across a larger share of public datasets — and output them as mzQC (see Task 1).

---

## Objectives

By the end of this task, you should have:
- [x] At least one new pMultiQC adapter capable of parsing metrics from a new tool or workflow.
- [x] Extracted relevant QC metrics mapped to PSI-MS CV accessions.
- [x] Example test data and documentation demonstrating correct parsing.
- [x] Integration tested so the new metrics appear in the aggregated QC output (and mzQC export).

---

## Background

### Why this matters

pMultiQC extends the popular MultiQC framework into a **proteomics-centric** QC platform.
It currently supports a limited number of workflows (e.g. MaxQuant, DIA-NN), but thousands of public datasets use many other pipelines.

Adding adapters ensures:
- Broader coverage of repository data.
- Consistent extraction of QC metrics across tools.
- Seamless integration with mzQC for FAIR, machine-readable QC output.

### How adapters work

Each pMultiQC module:
- Defines **file patterns** to detect relevant tool outputs (e.g. `.tsv`, `.log`, `.txt`).
- Implements a **parser** that extracts metrics (e.g. scan counts, ID rates, retention-time spread).
- Adds results to pMultiQC's internal data dictionary for aggregation and visualization.

---

## Implementation Steps

1. **Choose your target tool or workflow**
   - Examples of good candidates: MSFragger, Mascot, MS-GF+, OpenMS.
   - Prefer tools with accessible output or log files (text, TSV, JSON, XML).

2. **Set up a development environment**
   - Clone pMultiQC and follow the official contributing instructions: [pMultiQC Contributing Guidelines](https://github.com/bigbio/pmultiqc/blob/main/CONTRIBUTING.md)
   - Install pMultiQC in editable mode:
     ```bash
     git clone https://github.com/bigbio/pmultiqc.git
     cd pmultiqc
     pip install -e .
     ```
   - Review the pMultiQC developer documentation for architecture, module structure, and examples: [https://pmultiqc.quantms.org/](https://pmultiqc.quantms.org/)
   - Create a new branch for your module (e.g. `feature/msfragger-adapter`).

3. **Add representative outputs for testing**
   - Place 1–2 **small** output files under: `tests/resources/<tool_name>/`.
   - This matches the repo's testing style and makes local / CI tests easy. The README shows a basic smoke test invocation.

4. **Implement a new adapter module**
   - Follow examples under [`pmultiqc/modules/`](https://github.com/bigbio/pmultiqc/tree/main/pmultiqc/modules).
   - Implement logic to:
      - Detect your tool's files (glob patterns / filenames).
      - Parse the fields you need (counts, rates, distributions, TIC time series, etc.).
      - Store metrics in the internal dicts used by the report generator (mirroring existing adapters' keys/structures so plots and tables "just work").
+  - Register your module so MultiQC loads it.

5. **Map metrics to PSI-MS CV terms**
   - Use QC terms in the **MS:4000000–MS:4999999** range.
   - Browse via [OLS](https://www.ebi.ac.uk/ols/ontologies/ms).
   - Example mappings:
     | Metric | PSI-MS accession | Description |
     |--------|------------------|-------------|
     | total ion currents | MS:4000104 | Tabular representation of the total ion current detected in each of a series of mass spectra. |
     | number of MS2 spectra | MS:4000060 | The number of MS2 events in the run. |

6. **Integrate and test**
   - Run pMultiQC on example results containing the new tool's output.
   - Confirm metrics appear in:
     - HTML report
     - Internal data summaries
     - mzQC export (Task 1 integration)
   - Validate mzQC output via the [online validator](https://hupo-psi.github.io/mzQC/validator).

7. **Document your module**
   - Add a short Markdown file in `/docs/tasks/task3_adapters_<tool>.md` or similar.
   - Include:
     - Example command to run pMultiQC on that tool's outputs.
     - List of parsed metrics and CV mappings.
     - Link to sample data.
   - Add your name to the CONTRIBUTORS section.

---

## Tips & Pointers

- Follow the **contributing guide** and code conventions — indentation, naming, docstrings, and test structure.
- Reuse existing MultiQC modules as templates — many share similar parsing logic.
- Keep parsers lightweight; avoid dependencies beyond Python stdlib or existing third-party libraries.
- Validate partial outputs early; it's easier to debug metric parsing in isolation.
- Coordinate with Task 2 for metric naming and CV term consistency.
- Make sure units (counts, %, minutes) are explicitly defined.

---

## Definition of Done

- [ ] New adapter module created under `pmultiqc/modules/<tool_name>/`.
- [ ] At least three QC metrics parsed and mapped to PSI-MS CV accessions.
- [ ] Example data and test run demonstrating successful parsing.
- [ ] Integration tested with mzQC export (Task 1).
- [ ] Short documentation file added under `/docs/tasks/`.
- [ ] Pull request opened and reviewed following [pMultiQC contributing guidelines](https://github.com/bigbio/pmultiqc/blob/main/CONTRIBUTING.md).
