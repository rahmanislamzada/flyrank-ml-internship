# Phase: Build — Technical Stack Rationale & Pressure-Test

---

## 1. Project Constraints & Display Requirements

* **Budget:** $0 (Strictly Free Tier tools and hosting).
* **Skill Level:** Data / ML Engineering focus (Strong SQL, Python, Markdown, DuckDB; Basic HTML/CSS/JS).
* **Display Needs:** Long-form technical case studies, clean DuckDB code execution blocks, embedded DataFrame outputs, SVG architecture diagrams, and responsive layout.
* **Backend Requirement:** None yet (Static site suffices; dynamic server logic is currently unnecessary for portfolio display).

---

## 2. Evaluation of Three Stack Options

### Option 1: No-Code Builder (Framer / Notion + Super)
* **Build Method:** Visual drag-and-drop or Markdown page syncing.
* **Hosting:** Framer / Notion Free Subdomain.
* **Backend:** No.
* **Trade-off:** Fast initial setup, but severe limitations on code block syntax highlighting, custom data table rendering, and long-term repository ownership.

---

### Option 2: Static HTML5 / CSS3 + GitHub Pages (CHOSEN FRONT-RUNNER)
* **Build Method:** Lightweight, semantic HTML5 structure styled with clean CSS variables (matching the Identity Kit).
* **Hosting:** GitHub Pages (100% Free, native CI/CD from `main` branch).
* **Backend:** No (Pure static site).
* **Trade-off:** Requires writing simple HTML elements manually, but grants 100% control over typography (`Inter`), syntax highlighting, site speed, and complete maintainability.

---

### Option 3: Modern JS Framework (Next.js + Tailwind CSS + Vercel)
* **Build Method:** Component-driven React / Next.js architecture.
* **Hosting:** Vercel Free Tier.
* **Backend:** Optional API routes available.
* **Trade-off:** High engineering overhead; risk of spending build weeks troubleshooting React hydration/build errors instead of polishing data case studies.

---

## 3. Pressure-Testing the Front-Runner (Option 2)

* **What breaks if I pick Option 1 (No-Code)?** Code formatting looks unappealing, and customization to match custom DuckDB output tables becomes difficult.
* **What do I maintain if I pick Option 3 (Next.js)?** Continuous dependency updates (`npm package` vulnerabilities) and complex build configuration steps.
* **Can I finish in two weeks with Option 2?** Yes, completely. HTML/CSS allows instant editing without build pipelines or compilation steps.
* **Does it show my work properly?** Exceptionally well—code blocks, Pandas data tables, and structured case studies render natively with zero bloat.

---

## 4. Final Decision Rationale (In My Own Words)

> I chose **Option 2 (Static HTML5/CSS3 hosted on GitHub Pages)**. 
> 
> **Why I rejected Option 1:** It limits custom styling for SQL and Python code snippets, making real engineering data look like generic marketing pages.  
> **Why I rejected Option 3:** Next.js introduces unnecessary component overhead for a static technical portfolio, risking time lost on framework debugging instead of refining ML model presentation.  
> **Maintainability & Proof:** Option 2 is 100% free, version-controlled directly inside this repository, and simple to maintain over time. It presents DuckDB queries, model accuracy scores, and data contracts cleanly without unnecessary complexity.
