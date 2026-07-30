# Phase: Build (Core) — Automation Workflow v2 Walkthrough (FL-04)

---

## 1. Workflow Architecture & Step Diagram

**Pipeline Objective:** "Draft, Critique, and Format" — Transforming raw DuckDB/GSC query analysis into publication-ready technical SEO & ML case studies.

[Step 1: Gather & Synthesize]
        │  (NotebookLM / DuckDB Query Logs)
        ▼
[Step 2: Draft & Structure]
        │  (Claude Project / Prompt v5 Template)
        ▼
[Step 3: Critique & Adversarial Audit]
        │  (Custom Audit System Prompt)
        ▼
[Step 4: Format & CI-Ready Export]
        │  (Final Clean Markdown & Output Metadata)

---

## 2. System Configuration & Prompts Used

### Step 1 Prompt (Synthesis)
> *"Extract core empirical metrics from DuckDB query execution logs: sample size (n), position buckets, average CTR, and top low-performing URLs."*

### Step 2 Prompt (Drafting - 3-Beat Shape)
> *"Using the extracted metrics, draft a 3-beat technical case study: Beat 1 (Problem), Beat 2 (What I Did & Decided), Beat 3 (What Came of It)."*

### Step 3 Prompt (Adversarial Critique)
> *"Act as a skeptical Senior Staff Data Engineer. Audit the draft for: 1. Label leakage or future-window bias, 2. Over-claimed statistical significance, 3. Missing NULLIF division guards."*

### Step 4 Prompt (Final Formatting)
> *"Format the approved copy strictly into executable Markdown with zero conversational intros or outros."*

---

## 3. Five Real Execution Runs

| Run # | Input Dataset / Query Focus | Step 1 Output | Step 3 Critique Result | Final Output Status |
|---|---|---|---|---|
| **Run 1** | GSC Daily Clicks (2026-03) | n=1,000 rows extracted | Flagged missing NULLIF guard | **PASSED** (Guards added) |
| **Run 2** | Position vs CTR Gap Analysis | Top 10 pos filtered | Approved without revision | **PASSED** (Clean output) |
| **Run 3** | Content Staleness (>90d) | 120 stale pages identified | Suggested adding bounce rate context | **PASSED** (Updated) |
| **Run 4** | Priority Score CSV Generation | baseline_action_score.csv | Approved ranking logic | **PASSED** (Verified) |
| **Run 5** | FlyRank Internship Schema Test | fact_daily join verified | Flagged column name mismatch | **PASSED** (Fixed schema) |

---

## 4. Honest Time-Saved Accounting

* **Manual Pipeline Execution Time (5 runs):** ≈ 150 minutes (30 mins per document).
* **Automated Workflow Execution Time (5 runs):** ≈ 25 minutes (5 mins per run).
* **One-Time Workflow Setup Cost:** 45 minutes.
* **Net Time Saved:** **80 minutes saved** on the first 5 runs (time savings compound on future runs).

---

## 5. Known Failure Points & Required Human Review

1. **Schema Evolution:** If DuckDB column names change upstream (e.g., `gsc_clicks` renamed to `clicks`), Step 1 synthesis requires manual prompt alignment.
2. **Adversarial False Positives:** Step 3 critique occasionally flags legitimate domain-specific metrics as anomalies; a human engineer must make the final decision on technical trade-offs.
