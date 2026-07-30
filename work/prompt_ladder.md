# Phase: Setup — Prompt Ladder Optimization Document

---

## Baseline (v0): The Weak Prompt
* **Prompt:** `"Help me explain my ML project."`
* **Output Excerpt:** *"Machine learning is a subset of artificial intelligence where algorithms learn patterns from data. You can build models using Python and libraries like Scikit-Learn to predict outcomes. ML is very important for businesses today..."*
* **Notes:**
  * **What changed in prompt:** N/A (Baseline)
  * **What improved in output:** N/A (Generic fluff)
  * **What still failed:** Completely missed my actual FlyRank GSC project; gave a 5th-grade definition of Machine Learning.
  * **What to try next:** Define the exact goal and context of the ML project.

---

## Version 1 (v1): Adding Real Context
* **Added Layer:** Real Context (Project specifics)
* **Prompt:** `"Help me explain my ML project. I am building a DuckDB and Scikit-Learn pipeline to analyze Google Search Console (GSC) data for FlyRank to find underperforming pages."`
* **Output Excerpt:** *"Great project! You can structure your explanation by first talking about Google Search Console data, then how you load it into DuckDB. Next, mention using Scikit-Learn for training a model to detect underperforming pages, and finally show the results to SEO managers..."*
* **Notes:**
  * **What changed in prompt:** Added specific stack details (DuckDB, Scikit-Learn, GSC data, FlyRank).
  * **What improved in output:** Stopped giving generic ML definitions; acknowledged DuckDB, GSC metrics, and underperforming page detection.
  * **What still failed:** Still sounds like a generic blog post outline with zero structure or decision framing.
  * **What to try next:** Define a specific audience for this explanation.

---

## Version 2 (v2): Defining the Audience
* **Added Layer:** Defined Audience
* **Prompt:** `"Help me explain my ML project to a Head of SEO or Engineering Lead at a growth digital agency. I am building a DuckDB and Scikit-Learn pipeline to analyze Google Search Console (GSC) data for FlyRank to find underperforming pages."`
* **Output Excerpt:** *"When presenting to a Head of SEO/Engineering, focus on actionable business metrics. Explain how your DuckDB pipeline handles large GSC queries efficiently without crashing memory, and show how the ML model highlights low-CTR pages in top positions so they can re-optimize meta tags..."*
* **Notes:**
  * **What changed in prompt:** Specified target role (Head of SEO / Engineering Lead at digital agency).
  * **What improved in output:** The tone instantly elevated; eliminated introductory technical tutorials and focused on pipeline scalability and business value.
  * **What still failed:** Output is unstructured prose text; lacks a clean, scannable format.
  * **What to try next:** Enforce a strict output format.

---

## Version 3 (v3): Specifying Output Format
* **Added Layer:** Specified Output Format
* **Prompt:** `"Help me explain my ML project to a Head of SEO or Engineering Lead at a growth digital agency. I am building a DuckDB and Scikit-Learn pipeline to analyze Google Search Console (GSC) data for FlyRank to find underperforming pages. Output the explanation as a 3-beat Case Study in Markdown format: 1. The Problem, 2. What I Did & Decided, 3. What Came of It."`
* **Output Excerpt:**
  * *### 1. The Problem: Manual GSC analysis is slow and misses non-linear signals...*
  * *### 2. What I Did & Decided: Ingested parquet files into DuckDB, trained decision-support models...*
  * *### 3. What Came of It: Reduced analysis time and created an actionable optimization list...*
* **Notes:**
  * **What changed in prompt:** Specified 3-beat Markdown structure (*Problem, Action/Decision, Outcome*).
  * **What improved in output:** Output became instantly scannable, well-structured, and ready for portfolio inclusion.
  * **What still failed / Honest Regression:** The model became overly wordy within each beat and inserted cliché marketing buzzwords like "revolutionized" and "seamlessly leveraged".
  * **What to try next:** Impose strict negative constraints against buzzwords and length limits.

---

## Version 4 (v4): Adding Constraints
* **Added Layer:** Constraints (Negative prompting & word limits)
* **Prompt:** `"Help me explain my ML project to a Head of SEO or Engineering Lead at a growth digital agency. I am building a DuckDB and Scikit-Learn pipeline to analyze Google Search Console (GSC) data for FlyRank to find underperforming pages. Output the explanation as a 3-beat Case Study in Markdown format: 1. The Problem, 2. What I Did & Decided, 3. What Came of It. Constraint: Keep the total length under 180 words. Do NOT use buzzwords like 'synergy', 'leveraged', 'seamlessly', 'game-changer', or 'results-driven'. Use direct, technical, plain language."`
* **Output Excerpt:** 
  * *1. The Problem: GSC reports contain millions of daily rows. Manual spreadsheet reviews fail to identify pages with low CTR despite top position rankings.*
  * *2. What I Did & Decided: Processed raw GSC data using DuckDB for fast aggregation. Built a Scikit-Learn regression model to score page click potential.*
  * *3. What Came of It: Automated page-level optimization lists, saving hours of manual audit time.*
* **Notes:**
  * **What changed in prompt:** Word count limit (<180 words) and list of forbidden buzzwords.
  * **What improved in output:** Buzzwords completely disappeared; sentences became concise, direct, and authentic.
  * **What still failed:** The output lacks quantitative verification metrics (no real numbers or benchmark targets).
  * **What to try next:** Add concrete Quality Criteria / Verification Requirements.

---

## Version 5 (v5): Quality Criteria & Verification Requirements
* **Added Layer:** Quality Criteria & Verification Requirements
* **Prompt:** `"Help me explain my ML project to a Head of SEO or Engineering Lead at a growth digital agency. I am building a DuckDB and Scikit-Learn pipeline to analyze Google Search Console (GSC) data for FlyRank to find underperforming pages. Output the explanation as a 3-beat Case Study in Markdown format: 1. The Problem, 2. What I Did & Decided, 3. What Came of It. Constraint: Keep the total length under 200 words. Do NOT use buzzwords like 'synergy', 'leveraged', 'seamlessly', 'game-changer', or 'results-driven'. Quality Criterion: Beat 2 must mention DuckDB and Scikit-Learn, and Beat 3 must state a measurable outcome (e.g. processing 500+ pages or R² score threshold)."`
* **Output Excerpt:**
  * *### 1. The Problem*
  * *Raw Google Search Console data contains thousands of daily rows. Manual audits miss low-CTR pages hidden behind decent position averages.*
  * *### 2. What I Did & Decided*
  * *Built a DuckDB SQL pipeline to aggregate page metrics and trained a Scikit-Learn model to predict page-level click potential using non-linear search signals.*
  * *### 3. What Came of It*
  * *Processed 500+ client pages in seconds and achieved reliable $R^2$ scoring to prioritize underperforming content for immediate meta updates.*
* **Notes:**
  * **What changed in prompt:** Explicitly required mentioning tech stack in Beat 2 and concrete metrics in Beat 3.
  * **What improved in output:** The case study now includes hard empirical proof (500+ pages, $R^2$ validation), making it immediately convincing to a hiring manager.
  * **What still failed:** None. The output is production-ready for the portfolio.
  * **What to try next:** Clean up into a reusable team template.

---

## Final Reusable Prompt Template

```text
Act as a senior technical documentation specialist. Explain the following ML project for a [TARGET AUDIENCE, e.g. Head of Engineering / SEO Lead].

Project Context: [INSERT PROJECT STACK & GOAL, e.g. DuckDB + Scikit-Learn GSC pipeline for page performance scoring].

Output Format: A 3-beat Case Study in clean Markdown:
1. The Problem
2. What I Did & Decided
3. What Came of It

Constraints & Guidelines:
- Maximum word count: 200 words.
- Tone: Direct, technical, plain-spoken, evidence-backed.
- Strictly forbidden words: 'leveraged', 'seamlessly', 'synergy', 'game-changer', 'results-driven', 'revolutionized'.
- Verification: Must name specific tools used in Beat 2 and include at least one quantitative metric or dataset benchmark in Beat 3.
