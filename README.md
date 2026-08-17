# Personal SEO & Content Optimization Agent (FL-09)

An autonomous decision-support agent designed for SEO analysts and content teams to evaluate Google Search Console performance metrics, isolate striking-distance opportunities, and generate human-in-the-loop action playbooks with strict safety guardrails.

---

## 1. Overview & Key Capabilities

* **Target Audience:** SEO Managers, Content Strategists, and Editorial Teams.
* **Core Problem:** Eliminates manual Search Console spreadsheet analysis by prioritizing high-impression, low-CTR pages (positions 5 to 12).
* **Zero-Leakage Pipeline:** Computes temporal partition metrics using DuckDB to ensure historical features do not leak target signals.

---

## 2. Quickstart & Setup Guide

### Prerequisites
* Python 3.10 or higher
* DuckDB (pip install duckdb pandas numpy matplotlib)

### Installation & Execution
1. Clone repository: git clone https://github.com/rahmanislamzada/flyrank-ml-internship
2. Navigate to project: cd flyrank-ml-internship
3. Launch notebook: jupyter notebook work/notebooks/w07_action_playbook.ipynb

---

## 3. Architecture & Data Flow

1. **Ingestion Stage:** Raw Search Console Partitions (79M+ Rows) are ingested into DuckDB.
2. **Feature Engineering:** Zero-leakage temporal metrics (impressions, positions, CTR gap) are computed.
3. **ML Scoring:** Grouped Random Forest Classifier evaluates client performance metrics.
4. **Action Queue Output:** Human-in-the-loop content recommendations are assigned Reason Codes:
   * RC_HIGH_IMP_LOW_CTR: Meta Title & Intent Triage
   * RC_STRIKING_DISTANCE: Header & Internal Link Refresh
   * RC_MONITOR_ONLY: Stable Baseline

---

## 4. Evaluation Results (v2 Eval)

Evaluated under a strict Client-Grouped K-Fold Cross-Validation (GroupKFold) split to ensure complete domain boundary isolation:

* **Accuracy:** Baseline 0.8120 -> Grouped Agent 0.9240 (+11.20%)
* **Precision:** Baseline 0.6540 -> Grouped Agent 0.8850 (+23.10%)
* **Recall:** Baseline 0.5820 -> Grouped Agent 0.8410 (+25.90%)
* **F1-Score:** Baseline 0.6158 -> Grouped Agent 0.8623 (+24.65%)

---

## 5. Known Limitations & Safety Guardrails (FL-08)

1. **No Automated Publishing:** The agent strictly generates recommendations; it never directly modifies production CMS content or URL redirects.
2. **Algorithm Volatility Limit:** Performance degrades during major Google core search algorithm updates due to unpredictable SERP position reshuffling.
3. **Data Freshness Dependency:** Requires daily/weekly GSC data partition re-ingestion to prevent priority score decay.

---

## 6. AI Transparency & Human Verification
* **AI Assistance:** Architectural boilerplate, LaTeX mathematical formulations, and draft scaffolding were generated with AI assistance.
* **Human Engineering & Verification:** Feature boundaries, SQL aggregation pipelines in DuckDB, `GroupKFold` split validation logic, metric benchmarking, and domain guardrails were verified, written, and executed independently.
