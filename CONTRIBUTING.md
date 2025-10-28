# Contributing Guidelines

Welcome to the *Repository-Scale QC in Proteomics* BioHackathon project!
This guide explains how to collaborate effectively, follow good coding practices, and make sure your contributions integrate smoothly.

---

## Quick Overview

1. **Open an Issue before you start.**
   - Describe your feature, idea, or bug fix clearly.
   - Tag everyone involved so others know what's happening.
   - Include: motivation, what you plan to implement, data/tools you'll use, expected outputs.
   - Use checklists to track progress.

2. **Branch naming convention**
```
feature/<task-or-idea-name>
fix/<short-description>
docs/<section-updated>
````

3. **Commit messages**
- Be clear and concise: `Add mzQC export to pMultiQC` or `Fix SDRF parser mapping`.
- Reference the related issue (`Fixes #12`).

4. **Pull requests**
- PRs should be small and focused — one feature or fix at a time.
- Describe what you did, why, and how to test it.
- Reference issues (`Implements #12`).
- Assign reviewers or tag teammates.
- PRs will be discussed and merged during **daily hackathon syncs**.

---

## Collaboration Rules of Thumb

- **Communicate early.** Post your plans and partial progress in issues.
- **Avoid duplication.** Check existing issues before starting something new.
- **Pair up.** Joint efforts speed up debugging and idea generation.
- **Document everything.** Even short notes help others continue where you left off.
- **Reuse existing outputs.** Build on the results from Tasks 1–5 when possible.

---

## Code Layout and Style

- Follow the structure and conventions of the existing `pmultiqc` code.
- Use **Python 3.10+** and follow **PEP8** coding style.
- Indent with **4 spaces**, use **snake_case** for variables and functions.
- Add docstrings (`"""Short summary."""`) to all functions and classes.
- Keep modules lightweight — avoid adding large dependencies.
- Place small test or demo data under `tests/resources/<tool_name>/`.

---

## Testing & Validation

- Test locally using example data or small public datasets.
- Validate mzQC outputs using the [online validator](https://hupo-psi.github.io/mzQC/validator).
- For new adapters, run:
```bash
cd tests
multiqc resources/<tool> -o ./out
````
- Check that your metrics appear in:
  - The HTML report
  - The `.mzQC` output (if integrated)

---

## Documentation

- Add concise Markdown pages under `/docs/tasks/` or `/docs/ideas/`.
- Include:
  - A brief description of your code or analysis.
  - Example commands or data used.
  - References to relevant CV terms, tools, or standards.
* Add screenshots or plots where possible — visuals are great for the final presentation!

---

## Hackathon Best Practices

- Push your code frequently to avoid merge conflicts.
- Sync daily and communicate blockers early.
- Prefer **working prototypes** over polished perfection — small wins add up fast.
- If you create something novel (e.g. new QC metrics, visualization, or workflow), summarize it for the **final presentation slides**.

---

## Summary

| Step | Action                  | Purpose                                   |
| ---- | ----------------------- | ----------------------------------------- |
| 1    | Open an Issue           | Describe your idea and tag collaborators  |
| 2    | Create a feature branch | Keep work isolated and organized          |
| 3    | Code, test, document    | Follow style, add examples                |
| 4    | Open a PR               | Get review and merge                      |
| 5    | Present results         | Share during daily sync and final session |

Thank you for contributing to repository-scale QC for proteomics!
