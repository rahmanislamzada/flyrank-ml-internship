# Phase: Build+ — Explain It Like You Built It (Week 6)

---

## 1. The Real Piece I Built
**Feature Focus:** The DuckDB Search Console Query Pipeline & Dynamic Priority Scoring Logic (`baseline_action_score.csv`).

---

## 2. Plain-Words Explanation (Teaching a Friend)

Imagine you run a massive online library, but you have no idea which books people are looking for versus which books they actually end up reading. That’s exactly what Google Search Console (GSC) data looks like—millions of rows of query impressions (how many people saw your page in Google results) and clicks (how many people clicked it).

If you try to process this in a traditional spreadsheet like Excel, it crashes. If you process it in a basic SQL database, it gets slow. In my build, I used **DuckDB**, which is like an in-memory sports car for data processing.

Here is how the piece I built actually works in plain English:

1. **Filtering the Noise:** First, my code looks at pages that get a lot of eyeballs (high impressions, e.g., $>500$) but sit on "Position 5 to 12" on Google. Why? Because if a page is on page 50, nobody sees it anyway. But if it's on page 1, position 8, a tiny tweak can jump it to position 3 and double the traffic.
2. **Preventing the 'Division by Zero' Disaster:** When calculating Click-Through Rate ($CTR = Clicks / Impressions$), new pages often have $0$ clicks and $0$ impressions. If a computer tries to divide by zero, the whole pipeline breaks. I built a guardrail using `NULLIF(impressions, 0)` so the system safely outputs zero instead of crashing.
3. **The Priority Score:** Instead of just guessing which page to fix first, I created a single metric called `priority_score`. It multiplies how visible a page is by how badly its CTR is underperforming compared to its position.
4. **Zero Leakage:** I made sure the code only looks at past data to score today's actions. It never accidentally sneaks future performance data into the calculation—ensuring the ML model learns honestly.

Now, instead of manually digging through 10,000 rows of spreadsheets every Monday, this query runs in less than 2 seconds and exports a clean top-10 list of exact pages to optimize.

---

## 3. Why This Matters
Building this taught me that ML engineering isn't just about training complex neural networks—it’s 90% about building bulletproof, leak-free data pipelines that turn messy raw logs into clean, honest signals a model (and a business) can trust.
