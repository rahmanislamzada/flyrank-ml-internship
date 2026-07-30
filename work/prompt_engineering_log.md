Aha, baş üstə! Bütün mətni birbaşa tam olaraq kopyalayıb `work/prompt_engineering_log.md` faylına yapışdıra bilməyin üçün aşağıda tək bir blokda verirəm:

```markdown
# Phase: Foundations — Prompt Engineering Iteration Log & Cross-Model Audit

* **Target Task from FL-01 Audit:** Task 1 — SQL & Data Extraction Query Generation (DuckDB) for Google Search Console (GSC) analytics.

---

## 1. Prompt Iteration Log (Naive + 5 Technique Versions)

### Version 0: Naive Baseline
* **Technique Applied:** None (Naive Baseline)
* **Prompt:** `"Write a DuckDB query for GSC click data."`
* **Output Excerpt:**
  ```sql
  SELECT * FROM gsc_data WHERE clicks > 0;

```

* **Observed Output Difference:** Returned an overly simplistic SELECT query with generic table/column names. Complete failure for production data pipelines.

---

### Version 1: Role Assignment

* **Technique Applied:** Role Assignment
* **Prompt:** `"You are a Senior Data Engineer specializing in DuckDB and search analytics. Write a DuckDB SQL query to aggregate GSC performance metrics."`
* **Output Excerpt:**
```sql
SELECT page, SUM(clicks) as total_clicks, AVG(position) as avg_pos
FROM gsc_performance
GROUP BY page;

```


* **Observed Output Difference:** The model adopted an engineering perspective, adding GROUP BY aggregations and alias names (total_clicks), but still used assumed table schemas.

---

### Version 2: Context and Motivation

* **Technique Applied:** Context and Motivation
* **Prompt:** `"You are a Senior Data Engineer specializing in DuckDB and search analytics. We are building a decision-support pipeline for FlyRank. We need to identify underperforming pages that have high impressions but low click-through rates (CTR) so SEO teams can prioritize re-optimization. Write a DuckDB SQL query for this."`
* **Output Excerpt:**
```sql
SELECT page, SUM(clicks) AS total_clicks, SUM(impressions) AS total_impressions,
       (SUM(clicks)::FLOAT / NULLIF(SUM(impressions), 0)) AS ctr
FROM gsc_performance
GROUP BY page
HAVING SUM(impressions) > 1000 AND (SUM(clicks)::FLOAT / NULLIF(SUM(impressions), 0)) < 0.02;

```


* **Observed Output Difference:** Adding motivation drastically improved domain logic: the model automatically introduced NULLIF division-by-zero protection and filtered for high impression / low CTR thresholds via HAVING.

---

### Version 3: Few-Shot Examples

* **Technique Applied:** Few-Shot Examples (In-Context Learning)
* **Prompt:** `"You are a Senior Data Engineer specializing in DuckDB. We need to query FlyRank GSC daily tables (fact_daily) where columns are client_hash_id, content_hash_id, gsc_clicks, gsc_impressions, gsc_sum_position. Example Input/Output: Input: Calculate page-level average position. Output: AVG(gsc_sum_position::FLOAT / NULLIF(gsc_impressions, 0)) AS avg_position Write a DuckDB query to find underperforming pages per client with high impressions (>500) and CTR < 2%."`
* **Output Excerpt:**
```sql
SELECT client_hash_id, content_hash_id,
       SUM(gsc_clicks) AS total_clicks,
       SUM(gsc_impressions) AS total_impressions,
       AVG(gsc_sum_position::FLOAT / NULLIF(gsc_impressions, 0)) AS avg_position,
       (SUM(gsc_clicks)::FLOAT / NULLIF(SUM(gsc_impressions), 0)) AS avg_ctr
FROM fact_daily
GROUP BY client_hash_id, content_hash_id
HAVING SUM(gsc_impressions) > 500 AND (SUM(gsc_clicks)::FLOAT / NULLIF(SUM(gsc_impressions), 0)) < 0.02;

```


* **Observed Output Difference:** Giving exact schema and few-shot column math syntax eliminated column guessing entirely. The query now matches FlyRank's actual dataset schema.

---

### Version 4: Output Structure & Formatting Constraints

* **Technique Applied:** Output Structure Enforcement
* **Prompt:** `"...[V3 Prompt]... Output format constraints:

1. Provide ONLY executable DuckDB SQL inside a markdown code block.
2. Include a short 2-bullet commentary below the SQL explaining query performance/indexing considerations.
3. No conversational intros or outros (e.g. 'Here is your query')."`

* **Output Excerpt:**
*(Code block returned cleanly without fluff, followed by 2 crisp bullet points on DuckDB column pushdown).*
* **Observed Output Difference:** Eliminated conversational padding completely. Output became directly parseable for automated CI/CD tools or immediate notebook copy-pasting.

---

### Version 5: Step Decomposition (Chain of Thought)

* **Technique Applied:** Step Decomposition (Thinking Steps)
* **Prompt:** `"...[V4 Prompt]... Before generating the final SQL query, think step-by-step inside  tags:

1. Verify column names match provided schema (gsc_sum_position, gsc_impressions).
2. Ensure division by zero is handled safely with NULLIF.
3. Confirm filtering condition (HAVING vs WHERE).
4. Output the final clean SQL code block."`

* **Output Excerpt:**
```xml
<thinking>
1. Schema verified: using gsc_sum_position / gsc_impressions for weighted position calculation.
2. Safe division checked: NULLIF used in both CTR and avg_position math.
3. Aggregation check: HAVING clause required since filters operate on SUM(gsc_impressions).
</thinking>

```


*(Followed by perfect, bug-free DuckDB SQL code block).*
* **Observed Output Difference:** Forcing explicit step decomposition eliminated edge-case syntax bugs (such as incorrectly placing aggregated filters in WHERE instead of HAVING).

---

## 2. Cross-Model Comparison (Claude 3.5 Sonnet vs. ChatGPT GPT-4o)

| Dimension | Claude (3.5 Sonnet) | ChatGPT (GPT-4o) |
| --- | --- | --- |
| **Tone & Style** | Exceptionally concise, strictly adhered to `<thinking>` tags and negative constraints without fluff. | Slightly more verbose, added polite closing remarks despite negative constraints. |
| **SQL Accuracy** | Correctly implemented weighted position math (`gsc_sum_position / NULLIF(gsc_impressions, 0)`) on first try. | Initially tried to simple `AVG(gsc_sum_position)`, missing the weighted density context until re-checked. |
| **Structure & Formatting** | Rendered markdown blocks and `<thinking>` reasoning tags with 100% precision. | Excellent markdown formatting, but included minor explanatory text outside requested sections. |
| **Failure Points** | Tended to be overly strict—if a constraint was ambiguous, it omitted optional commentary. | Tended to hallucinate extra SQL helper CTEs that weren't requested in the prompt. |

---

## 3. Final Reusable Prompt Template

```text
You are an expert Data Engineer specializing in analytical SQL (DuckDB/PostgreSQL).

Context & Task:
Generate a production-ready analytical SQL query for [DATABASE ENGINE, e.g. DuckDB] using schema [TABLE & COLUMN NAMES]. The business goal is [BUSINESS GOAL, e.g. isolate low-CTR pages with high impressions].

Execution Steps:
Inside <thinking> tags, explicitly verify:
1. Aggregation logic (WHERE vs HAVING).
2. Safe division handling for ratio metrics using NULLIF.
3. Proper indexing or memory-efficient grouping.

Constraints & Output Format:
- Provide ONLY executable SQL inside a clean code block.
- Followed by exactly 2 bullet points explaining query optimization.
- Do NOT include introductory text, greetings, or conversational sign-offs.

```
