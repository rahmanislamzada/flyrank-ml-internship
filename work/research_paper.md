# Autonomous Search Console Analytics & Positional Action Scoring
**Author:** Rahman Islamzada (ML & Data Engineering Intern)  
**Publication Date:** July 2026  
**Artifact Repository:** [GitHub Repository](https://github.com/rahmanislamzada/flyrank-ml-internship)

---

## Abstract
This research investigates automated position-decay and CTR gap detection using large-scale Search Console dataset aggregations. We formalize a zero-leakage priority scoring model evaluated against 79M+ search impression snapshots. By benchmarking a Random Forest Classifier against a baseline heuristic under a client-grouped holdout split, we measured substantial performance gains in identifying high-impact striking-distance pages. The resulting pipeline exports human-in-the-loop content action playbooks with clear reason codes and strict operational boundaries. All experimental figures, metrics, and data contracts are fully reproducible via committed open-source notebooks.

---

## 1. Introduction & Problem Statement
Search Engine Optimization (SEO) teams frequently struggle to prioritize content updates across thousands of URLs. Traditional workflows rely on static spreadsheet exports and manual sorting, leading to missed opportunities on "striking-distance" pages (positions 5–12). This paper presents an autonomous analytics framework leveraging DuckDB for zero-leakage feature calculation and dynamic priority score generation.

---

## 2. Data & Feature Engineering
* **Data Source:** FlyRank ML Internship Dataset (~79M rows of GSC daily search performance metrics).
* **Exclusions:** Excluded low-volume queries with $< 500$ total impressions to eliminate statistical noise.
* **Features:** 
  * `feat_hist_impressions`: Historical 30-day aggregated impression volume.
  * `feat_avg_position`: Mean organic SERP position.
  * `feat_hist_ctr`: Click-through rate calculated using `NULLIF(impressions, 0)`.
  * `feat_days_stale`: Days elapsed since the last content update.

---

## 3. Methodology & Validation Design
* **Baseline Heuristic:** Naive thresholding based solely on position $\le 10$.
* **ML Model:** Random Forest Classifier ($n\_estimators=100, max\_depth=5$).
* **Validation Strategy:** Client-Grouped K-Fold Cross-Validation (`GroupKFold`) ensuring zero data leakage between training and evaluation client domains.

---

## 4. Results & Performance Benchmarking
Under an honest client-grouped validation split, the Random Forest model demonstrated consistent decision-support gains over the naive baseline:

| Metric | Baseline Heuristic (Week 4) | Grouped ML Model (Week 6 Audit) | Measured Gain |
|---|---|---|---|
| **Accuracy** | 0.8120 | 0.9240 | +11.20% |
| **Precision** | 0.6540 | 0.8850 | +23.10% |
| **Recall** | 0.5820 | 0.8410 | +25.90% |
| **F1-Score** | 0.6158 | 0.8623 | +24.65% |

---

## 5. Limitations & Honest Claim Framing
* **Decision Support Only:** Model outputs serve as directional recommendations for human editors; they do not auto-publish content.
* **Domain Volatility:** Performance is subject to sudden SERP position shifts caused by core Google search algorithm updates.

---

## 6. Ranked Content Recommendations
Outputs are mapped directly to human-audited **Reason Codes**:
* `RC_HIGH_IMP_LOW_CTR`: High impressions, position $\le 8.0$, CTR $< 2\%$. (Action: Update meta title/intent).
* `RC_STRIKING_DISTANCE`: Position 8.1 to 15.0. (Action: Add internal links and header refresh).
* **No-Go List:** Direct automated URL redirects, page deletions, or unreviewed AI content publishing are strictly prohibited.

---

## 7. Reproducibility & Artifact Receipts
All experimental results trace back directly to executable repository receipts:
* Data Contract & Schema: `work/notebooks/w03_data_contract.ipynb`
* Baseline Score: `work/notebooks/w04_baseline_score.ipynb`
* Grouped Validation Audit: `work/notebooks/w06_validation_audit.ipynb`
* Action Playbook & Exports: `work/notebooks/w07_action_playbook.ipynb`

---

## 8. Acknowledgments & Data Credit
This research artifact and its underlying experimental pipelines were **Built on the [FlyRank ML Internship](https://flyrank.ai)** dataset.
