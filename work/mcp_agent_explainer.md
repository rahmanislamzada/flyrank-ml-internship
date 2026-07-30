# Phase: Build (Core) — Agent Concepts and Model Context Protocol (FL-05)

---

## 1. Workflows vs. Agents: The Fundamental Distinction

In modern AI engineering, the terms "workflow" and "agent" describe two fundamentally different execution patterns along a spectrum of autonomy:

* **Workflows:** Orchestrated systems where Large Language Models (LLMs) and code step through predefined, deterministic paths. Control flow is hardcoded via logic branches, sequential chaining, or conditional loops. The system follows a fixed recipe created by a human developer.
* **Agents:** Dynamic systems where an LLM acts as an autonomous decision-making engine. Given a goal, environment context, and a set of tools, the agent dynamically decides which actions to take, evaluates the feedback from those actions, and adjusts its loop iteratively until the objective is completed.

### Classification of the FL-04 Pipeline
The **FL-04 pipeline** created in the previous task is strictly a **Workflow**. It follows a static 4-step sequence: *Gather & Synthesize $\to$ Draft & Structure $\to$ Critique & Adversarial Audit $\to$ Format & Export*. At no point does Step 2 dynamically decide to skip Step 3, nor can the system autonomously query a live database to fetch additional data when a critique fails. It is a deterministic, high-efficiency prompt chain—not an agent.

---

## 2. Model Context Protocol (MCP) & Core Primitives

The **Model Context Protocol (MCP)** serves as an open standard—often called the *"USB-C port for AI applications"*—that enables AI models to securely interface with external host applications, local file systems, databases, and third-party APIs.

MCP establishes three primary architecture primitives:

1. **Tools:** Executable functions exposed by the server that allow the model to perform side-effects or fetch dynamic data (e.g., executing a DuckDB SQL query, writing a local Markdown file, or invoking a web search endpoint).
2. **Resources:** Read-only data sources exposed to the model as context (e.g., local database schemas, file contents, log files, or API documentation).
3. **Prompts:** Pre-configured template prompts hosted on the server that guide the model in structuring its interaction with specific tools and resources effectively.

---

## 3. Practical MCP Connector Execution & Proof

To demonstrate tool-use capabilities beyond standalone chat interfaces, an MCP Filesystem/Database Connector was initialized to execute three specific local tasks:

1. **Task 1: Local File Inspection & Schema Validation**  
   * *Tool Invoked:* `read_file(path="work/outputs/baseline_action_score.csv")`  
   * *Output:* Inspected local data contract output structure, verifying column headers (`client_hash_id`, `priority_score`, `reason_code`) directly from disk.
2. **Task 2: In-Memory DuckDB Query Execution**  
   * *Tool Invoked:* `execute_duckdb_sql(query="SELECT COUNT(*), AVG(gsc_clicks) FROM fact_daily")`  
   * *Output:* Direct execution against local memory space to return deterministic row counts and statistical distribution without manual user copy-pasting.
3. **Task 3: Automated File Output Writing**  
   * *Tool Invoked:* `write_file(path="work/outputs/mcp_run_log.json")`  
   * *Output:* Generated and saved execution metadata JSON directly to local repository path `work/outputs/`.

---

## 4. Upgrading the FL-04 Workflow to an Autonomous Agent

To upgrade the static FL-04 workflow into a true **Autonomous Agent**, the system requires three architectural enhancements:

1. **Dynamic Tool Integration via MCP:** Replace static prompt inputs with real-time MCP tool bindings (`read_duckdb`, `fetch_gsc_api`, `run_python_script`).
2. **Evaluator-Optimizer Loop:** Instead of passing text down a linear chain, the agent will inspect the output of its own draft, run DuckDB verification queries via MCP, evaluate whether accuracy thresholds (e.g., $R^2 > 0.85$) are met, and autonomously decide whether to re-query data or finalize output.
3. **Autonomous Error Recovery:** If a SQL query fails or returns zero rows during execution, the agent autonomously inspects the error traceback, adjusts its query parameter bounds, and re-executes without requiring human intervention.
