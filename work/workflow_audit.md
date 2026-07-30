# Phase: Setup — Workflow Audit & AI Integration

## 1. Weekly Task Classification Matrix (12 Tasks)

| # | Task | Classification | Rationale |
|---|---|---|---|
| 1 | Designing overall system architecture for ML pipelines | Just me | Requires high-level decision-making and context that AI cannot fully grasp without human intuition. |
| 2 | Final code review and approving pull requests | Just me | Security and quality standards require human accountability before merging into main branches. |
| 3 | Writing Python boilerplate and SQL queries (e.g. DuckDB) | Delegate to AI with review | AI generates syntax accurately for structured queries, requiring only my quick syntax check. |
| 4 | Debugging obscure library/environment errors | Collaborate with AI | AI helps narrow down stack traces faster, but hands-on debugging is needed to fix environment issues. |
| 5 | Writing technical documentation and READMEs | Delegate to AI with review | AI structures markdown files cleanly based on my rough notes and code comments. |
| 6 | Summarizing long research papers/documentation | Delegate to AI with review | AI extracts core findings rapidly, saving time before deep-dive manual reading. |
| 7 | Refactoring messy Jupyter Notebook code into modular Python scripts | Collaborate with AI | AI suggests clean modular code, while I ensure state management and execution order remain valid. |
| 8 | Formatting daily/weekly progress updates | Fully automate | Automated templates convert notebook outputs into markdown reports without manual formatting. |
| 9 | Preprocessing raw GSC performance datasets | Collaborate with AI | AI suggests feature engineering formulas, but domain validation requires human check. |
| 10 | Brainstorming research questions for ML experiments | Collaborate with AI | AI expands idea trees, while I narrow down to realistic, executable project scopes. |
| 11 | Organizing repository directory structures and file naming | Fully automate | Pre-commit hooks and script templates automatically enforce folder structure standards. |
| 12 | Writing unit tests for data cleaning pipelines | Delegate to AI with review | AI generates edge-case test cases quickly, which I inspect for coverage correctness. |

---

## 2. Target Tasks for FL-02 through FL-04 & Success Definitions

### Task 1: SQL & Data Extraction Query Generation (DuckDB)
* **Goal:** Generating complex analytical SQL queries for GSC/Clickstream data.
* **Definition of "Done Well":** The query runs error-free in DuckDB without schema mismatches, accurately handles NULLs/div-by-zero, and returns expected feature columns in under 3 seconds.

### Task 2: Machine Learning Code Refactoring & Optimization
* **Goal:** Converting messy notebook exploratory code into modular functions.
* **Definition of "Done Well":** Code passes PEP8 standards, has zero redundant variables, includes docstrings, and runs top-to-bottom deterministically without breaking notebook state.

### Task 3: Research Question Framing & Executive Summaries
* **Goal:** Drafting technical research framing and project summaries for stakeholders.
* **Definition of "Done Well":** The document covers decision, action, cost of wrong calls, avoids ungrounded causal claims, and stays under 300 words with clear bullet points.

---

## 3. Tool Setup & Claude Project Configuration

* **Anthropic Academy Enrollment:** Enrolled in *AI Fluency: Framework & Foundations*.
* **Claude Project Instructions configured with:**
  * **Role:** Computer Graphics & Machine Learning Engineering Intern at FlyRank.
  * **Tone:** Direct, technical, precise, concise, no unnecessary fluff.
  * **Goals:** Build production-ready ML capstone models and scalable GSC analytics pipelines.
