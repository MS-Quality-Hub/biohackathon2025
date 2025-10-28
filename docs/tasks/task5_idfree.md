# Task 5 — Explore Identification-Free QC Modules

> **Goal:** Develop **identification-free (ID-free) QC workflows** that assess data quality directly from raw MS data, without relying on peptide identifications.

---

## Objectives

By the end of this task, you should have:
- [ ] A prototype **Python-based module or script** that computes one or more ID-free QC metrics from raw data files.
- [ ] Example test datasets and example output in **mzQC format**.
- [ ] Documentation showing how these metrics can complement identification-based QC (Task 1).
- [ ] Optional: integration hooks for pMultiQC or repository pipelines.

---

## Background

### Why ID-free QC matters

A large portion of public mass spectrometry datasets lack full peptide identifications.
However, raw data itself contains valuable information about acquisition stability, noise, and chromatographic quality.

**ID-free QC** focuses on signal- and acquisition-level features such as:
- Total ion current (TIC) and base peak intensity over time
- Scan rate and acquisition frequency
- MS1 signal stability and chromatographic consistency
- Retention time reproducibility and gradient integrity
- MS1/MS2 balance and dropout detection

These metrics can be computed *directly* from vendor or converted **mzML** files.

---

## Implementation Steps

### 1. Choose a development toolkit

Use any open library that can read **mzML** or **mzXML** files:

| Library | Description | Installation |
|----------|--------------|---------------|
| **Pyteomics** | Lightweight parser for mzML/mzXML with NumPy-based spectrum access. | `pip install pyteomics` |
| **pyOpenMS** | Python bindings for OpenMS; robust access to spectra and chromatograms. | `pip install pyopenms` |

### 2. Compute one or more ID-free QC metrics

Start with a few basic ones; build up modularly.

| Metric                  | Description                                          | Example implementation                         |
| ----------------------- | ---------------------------------------------------- | ---------------------------------------------- |
| **MS1 TIC stability**   | Variation in total ion current per scan or over time | compute TIC series → rolling mean / CV         |
| **Base peak intensity** | Maximum intensity per spectrum                       | extract base peak → plot or compute statistics |
| **Scan rate**           | Number of MS1/MS2 scans per minute                   | count scans / total runtime                    |
| **MS1/MS2 ratio**       | Quantify acquisition balance                         | count MS1 vs MS2 events                        |
| **RT stability**        | Deviation in chromatographic peak elution            | compute centroid RT variance                   |
| **Dropout detection**   | Identify acquisition gaps                            | detect intervals with missing scans or low TIC |

### 3. Export results in mzQC format

- Use the [mzQC format](https://hupo-psi.github.io/mzQC/) for standardized QC output.
- mzQC files can be easily produced in Python ([pymzqc](https://github.com/MS-Quality-Hub/pymzqc)), R ([rmzqc](https://github.com/MS-Quality-Hub/rmzqc)), Java ([jmzqc](https://github.com/MS-Quality-Hub/jmzqc)).
* Validate your `.mzQC` file using the [online validator](https://hupo-psi.github.io/mzQC/validator).

### 4. (Optional) Integrate with pMultiQC

If time allows:

- Add your script/module as abn **adapter** to pMultiQC.
- For example, detect raw files in a directory and compute ID-free QC alongside existing metrics.
- Follow pMultiQC's contributing guide:
  [https://github.com/bigbio/pmultiqc/blob/main/CONTRIBUTING.md](https://github.com/bigbio/pmultiqc/blob/main/CONTRIBUTING.md)

### 5. (Optional) Visualize metrics

Generate quick summary plots to demonstrate your results:

```python
import matplotlib.pyplot as plt
plt.plot(rt, tic_series)
plt.title("TIC over time")
plt.xlabel("Retention time (min)")
plt.ylabel("Total ion current")
plt.show()
```

---

## Tips & Pointers

* Work with **mzML**, not proprietary vendor formats. If needed, use **ThermoRawFileParser** or **msconvert** to convert data.
* Choose metrics that are **computationally light** — hackathon-friendly runtime (<1 min per file).
* Leverage NiumPy/SciPy for efficient vector operations.
* If multiple team members compute different metrics, define a shared schema to merge outputs.
* Coordinate with **Task 2** to ensure proposed metrics can be mapped to PSI-MS CV terms.
* Coordinate with **Task 1** for mzQC export integration.

---

## Definition of Done

* [ ] One or more ID-free QC metrics computed directly from raw data.
* [ ] Outputs written in mzQC format and validated successfully.
* [ ] Example mzML file and example output included in `/examples/` or `/tests/resources/`.
* [ ] (Optional) Visual summary or pMultiQC integration.
* [ ] Short Markdown documentation added under `/docs/tasks/`.
* [ ] Pull request opened and reviewed.

