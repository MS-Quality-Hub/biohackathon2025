# Tasks Overview

This page lists all hackathon tasks and their goals so you can quickly find where your skills fit best.
Each task can be tackled independently, but collaboration across teams is highly encouraged.

---

## How the Tasks Fit Together

All tasks contribute to building a **repository-scale quality control (QC) framework** that connects:
- **pMultiQC** → extracts and aggregates QC metrics.
- **mzQC** → provides the standardized QC output format.
- **SDRF-Proteomics** → supplies metadata to guide and interpret QC analyses.

By the end of the week, we aim to have a working prototype generating standardized QC outputs at repository scale.

---

## Task List

Each task has its own Markdown page with detailed goals, background, and "definition of done."

| #     | Title                                   | Focus                                                                                                    | Skills / Tools                                 | Link                               |
| ----- | --------------------------------------- | -------------------------------------------------------------------------------------------------------- | ---------------------------------------------- | ---------------------------------- |
| **1** | Implement mzQC Export in pMultiQC       | Map pMultiQC's internal QC data to the mzQC schema and generate valid `.mzQC` outputs.                   | Python, JSON, proteomics QC                    | [Task 1](./task1_mzqc_export.md) |
| **2** | Define and Review QC Metrics            | Curate a tiered QC metric ontology (core, extended, specialized) and align with mzQC CV terms.           | QC expertise, controlled vocabularies          | [Task 2](./task2_metrics.md)     |
| **3** | Build Adapters for Additional Workflows | Extend pMultiQC to parse outputs from new tools (e.g. MSFragger, Comet, OpenMS workflows).               | Python, data parsing, proteomics tools         | [Task 3](./task3_adapters.md)    |
| **4** | Strengthen SDRF Integration             | Use SDRF-Proteomics metadata to contextualize QC and group results by experiment, sample, or condition.  | Python, SDRF schema, FAIR metadata             | [Task 4](./task4_sdrf.md)        |
| **5** | Explore ID-Free QC Modules              | Develop QC metrics directly from raw data (mzML) without identifications.                                | Python, pyOpenMS / Pyteomics, MS data analysis | [Task 5](./task5_idfree.md)      |
| **6** | Optional Extensions                     | Build complementary prototypes such as dashboards, benchmark datasets, or ML-based QC anomaly detection. | Open-ended, web/app development, ML            | [Task 6](./task6_optional.md)    |

---

## Choosing a Task

- If you like coding: Tasks 1, 3, and 5 involve the most Python development.
- If you like metadata or data standards: Task 2 and Task 4 focus on controlled vocabularies and SDRF integration.
- If you're creative or visual: Task 6 is open for dashboard design or visualization ideas.

All contributions, from bug fixes to documentation, are valuable!

---

## Common Definition of Done

Each task page contains its own detailed "definition of done," but all contributions should meet these general criteria:
- Produce valid mzQC outputs or contribute toward that goal.
- Use official CV terms (or propose new ones via PR).
- Include example data and reproducible steps.
- Document work clearly in Markdown under `/docs/tasks/`.
- Open a Pull Request referencing your issue (e.g. "Fixes #12").

---

## Related Documentation

| Topic                  | Link                                                                                           |
|----------------------- | -----------------------------------------------------------------------------------------------|
| Background & Resources | [../resources.md](../resources.md)                                                             |
| mzQC specification     | [https://hupo-psi.github.io/mzQC/](https://hupo-psi.github.io/mzQC/)                           |
| pMultiQC documentation | [https://pmultiqc.quantms.org/](https://pmultiqc.quantms.org/)                                 |
| SDRF-Proteomics schema | [https://www.ebi.ac.uk/pride/markdownpage/sdrf](https://www.ebi.ac.uk/pride/markdownpage/sdrf) |

---

## Collaboration Tips

- Use the Slack channel `#29-towards-repository-scale-quality-control` to coordinate in real time.
- Open GitHub Issues to discuss ideas or blockers.
- Pair up with others — each task connects to the rest, so cross-talk is key.
- Share partial results early! Even prototypes and notes are valuable for integration.

---

## Final Integration

On the last hackathon day, we'll merge all task outputs into a single demonstrator pipeline:
1. Run pMultiQC on example datasets.
2. Export results in standardized mzQC.
3. Link with SDRF metadata.
4. Visualize repository-scale QC summaries.

This will serve as the foundation for future integration into public repositories such as PRIDE.

---

**Next step:**
Pick a task that interests you and open its corresponding page to get started!
