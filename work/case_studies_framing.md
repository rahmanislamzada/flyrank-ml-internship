# Portfolio Voice Card & Case Study Framing

## 1. Voice Card (Standing Instruction)
> **Voice:** *Direct, technical, plain-spoken, evidence-backed, zero buzzwords.*

*(Added to Claude Project Instructions: "Always maintain a direct, technical, plain-spoken tone without fluff or generic buzzwords like 'results-driven' or 'synergy'. Focus purely on problems, technical decisions, and empirical metrics.")*

---

## 2. Case Study: FlyRank GSC Search Analytics ML Pipeline

### Beat 1: The Problem
Google Search Console (GSC) yields millions of daily search impressions and clicks across hundreds of client pages, but raw performance spreadsheets fail to reveal which content updates actually drive search visibility. Content teams waste hundreds of hours manually guessing which pages to re-optimize without understanding non-linear position and CTR signals.

### Beat 2: What I Did & Decided
* **Engineered Data Pipelines:** Built an in-memory SQL extraction engine using **DuckDB** to aggregate page-level CTR, impressions, and position metrics across thousands of daily GSC rows.
* **Formulated ML Task:** Framed search visibility optimization as a decision-support scoring problem, predicting total click potential (`gsc_clicks`) using tree-based regression algorithms rather than rigid heuristic rules.
* **Validated Domain Bounds:** Enforced a `GroupShuffleSplit` validation strategy on unseen client domains to ensure feature importance patterns hold up across different clients without leakage.

### Beat 3: What Came of It
* Created an automated pipeline capable of processing 500+ client pages in seconds and isolating underperforming content with low CTR despite strong search positioning.
* Reduced manual spreadsheet analysis time for SEO managers, replacing arbitrary content edits with empirical model-driven optimization lists.

---

## 3. Bio & Primary CTA Copy

* **Bio:** I am an ML & Data Engineering intern at FlyRank and a student at Holberton. I build reliable, decision-focused Machine Learning pipelines that process large-scale search performance data into actionable growth strategies.
* **CTA Banner:** *"Need automated GSC analytics or custom data pipelines for your search performance? [Book a 15-minute Discovery Call]"*

---

## 4. AI Copy Before / After Comparison

| Type | Text |
|---|---|
| **Generic AI Output (Before)** | *"I leveraged state-of-the-art results-driven Machine Learning algorithms to seamlessly synergize big data metrics and optimize digital marketing touchpoints."* |
| **Edited Authentic Output (After)** | *"I built a DuckDB and ML pipeline to extract GSC page metrics and score content performance, replacing manual spreadsheets with clear page-optimization lists."* |
