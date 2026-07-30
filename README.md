# Personal SEO & Content Optimization Agent (FL-09)

An autonomous decision-support agent designed for SEO analysts and content teams to evaluate Google Search Console performance metrics, isolate striking-distance opportunities, and generate human-in-the-loop action playbooks with strict safety guardrails.

---

## 1. Overview & Key Capabilities

* **Target Audience:** SEO Managers, Content Strategists, and Editorial Teams.
* **Core Problem:** Eliminates hundreds of hours of manual Search Console spreadsheet analysis by prioritizing high-impression, low-CTR pages (positions 5–12).
* **Zero-Leakage Pipeline:** Computes temporal partition metrics using DuckDB to ensure historical features do not leak target signals.

---

## 2. Quickstart & Setup Guide

### Prerequisites
* Python 3.10 or higher
* DuckDB (`pip install duckdb pandas numpy matplotlib`)

### Installation & Execution
```bash
# 1. Clone the repository
git clone [https://github.com/rahmanislamzada/flyrank-ml-internship.git](https://github.com/rahmanislamzada/flyrank-ml-internship.git)
cd flyrank-ml-internship

# 2. Run the Action Playbook Notebook
jupyter notebook work/notebooks/w07_action_playbook.ipynb
