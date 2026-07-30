# Phase: Submit — Tell the Story & Showcase Preparation (ML-12)

---

## 1. Five-Minute Showcase Demo Outline

* **Minute 1: The Problem (The Question):**  
  SEO and editorial teams waste hundreds of hours manually auditing Search Console logs, missing high-traffic opportunity windows on "striking-distance" pages (positions 5–12). How can we automate position-decay metrics to generate actionable, zero-leakage priority queues?
* **Minute 2: The Methodology (The System):**  
  Built an autonomous analytical pipeline using DuckDB and a Random Forest Classifier trained on 79M+ impression snapshot records. Enforced strict group-based client validation splits (`GroupKFold`) to eliminate cross-domain data leakage.
* **Minute 3: The Key Artifact (One Chart):**  
  *Present Figure: `work/figures/priority_score_distribution.png`*  
  Demonstrate how the metric dynamically isolates high-impression, low-CTR targets into a clear long-tail distribution ready for editorial triage.
* **Minute 4: Honest Results (Before vs. After):**  
  Under an honest grouped client split, the model achieved a measured **+24.65% F1-score improvement** over naive threshold heuristics (0.8623 vs 0.6158), proving robust decision support on unseen client domains.
* **Minute 5: Actionable Recommendation (The Playbook):**  
  Outputs map directly to human-in-the-loop Reason Codes (e.g., `RC_HIGH_IMP_LOW_CTR`) with strict no-go rules blocking unreviewed automated site changes or page deletions.

---

## 2. Shareable Cut 1: Technical Social Post (Methodology-Focused)

> 🚀 Just completed an ML research paper analyzing 79M+ Search Console performance snapshots to automate keyword prioritization!
>
> 💡 Key Challenge: Standard models often overfit due to temporal and cross-domain data leakage.
> ⚙️ Solution: Built an in-memory DuckDB analytical pipeline combined with a Random Forest model evaluated using strict Client-Grouped K-Fold validation.
> 📊 Result: Achieved a measured 0.8623 F1-score (+24.65% over naive heuristics), outputting a human-in-the-loop action playbook with strict guardrails.
>
> 🔍 Full open-source paper & reproducible notebooks: https://rahmanislamzada.github.io/flyrank-ml-internship/
>
> Built on the FlyRank ML Internship dataset. #MachineLearning #DataEngineering #DuckDB #Python #SEOAnalytics

---

## 3. Shareable Cut 2: Employer-Facing Summary (3 Sentences)

1. **What I Built:** I engineered an autonomous Search Console analytics pipeline and Random Forest scoring model that detects CTR underperformance on high-impression striking-distance pages.
2. **On What Data:** Built and validated on a 79M+ row Search Console performance dataset using DuckDB and zero-leakage group-based client evaluation splits.
3. **What It Showed:** Measured a 24.65% F1-score improvement over standard heuristics, exporting an automated decision-support playbook with clear reason codes and strict editorial safety guardrails.
