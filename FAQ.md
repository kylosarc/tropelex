# Tropelex Technical & Governance FAQ

Welcome to the **Tropelex Technical & Governance FAQ**. This comprehensive, deep-dive reference provides answers to architectural, operational, safety, research, multi-agent, and troubleshooting questions for software engineers, systems architects, and engineering teams building and pairing with AI coding agents.

---

## Table of Contents

### 1. Fundamentals & Storage Architecture
- [What is Tropelex and what problem does it solve?](#what-is-tropelex-and-what-problem-does-it-solve)
- [What is the difference between Tropelex, Tropebook, and the Web Dashboard?](#what-is-the-difference-between-tropelex-tropebook-and-the-web-dashboard)
- [Where is memory, research, and governance data stored on disk?](#where-is-memory-research-and-governance-data-stored-on-disk)
- [How does the Local-First Storage Architecture guarantee 100% data privacy?](#how-does-the-local-first-storage-architecture-guarantee-100-data-privacy)
- [How does project isolation work, and how does soft-delete/trash retention work?](#how-does-project-isolation-work-and-how-does-soft-deletetrash-retention-work)
- [How does Tropelex handle concurrent writes and race conditions across multiple agents?](#how-does-tropelex-handle-concurrent-writes-and-race-conditions-across-multiple-agents)
- [What are the hardware and runtime requirements for self-hosting Tropelex?](#what-are-the-hardware-and-runtime-requirements-for-self-hosting-tropelex)
- [What do I do if I am not seeing any results for the active page?](#what-do-i-do-if-i-am-not-seeing-any-results-for-the-active-page)

### 2. AI Performance, Context & Token Optimization
- [How can I improve my general AI coding workflows?](#how-can-i-improve-my-general-ai-coding-workflows)
- [What makes the AI's job easier and potentially reduces token consumption?](#what-makes-the-ais-job-easier-and-potentially-reduces-token-consumption)
- [What is the exact anatomy of an injected Tropelex context packet in an LLM prompt?](#what-is-the-exact-anatomy-of-an-injected-tropelex-context-packet-in-an-llm-prompt)
- [How does Tropelex prevent "Lost-in-the-Middle" degradation across 128k+ context windows?](#how-does-tropelex-prevent-lost-in-the-middle-degradation-across-128k-context-windows)
- [What is context compression and how does it work?](#what-is-context-compression-and-how-does-it-work)
- [How does Context Prefetch select the optimal subset of decisions for a prompt?](#how-does-context-prefetch-select-the-optimal-subset-of-decisions-for-a-prompt)
- [How does Semantic Search work when API keys or vector embeddings are absent?](#how-does-semantic-search-work-when-api-keys-or-vector-embeddings-are-absent)
- [What is Prompt Lab and how does Prompt Genealogy track win rates?](#what-is-prompt-lab-and-how-does-prompt-genealogy-track-win-rates)
- [What is the Goals & Intent Engine and how does it prevent agent goal drift?](#what-is-the-goals--intent-engine-and-how-does-it-prevent-agent-goal-drift)

### 3. Decisions, Memory & Rationale
- [What is an Architecture Decision Record (ADR)?](#what-is-an-architecture-decision-record-adr)
- [What is the difference between a static ADR and a Living ADR?](#what-is-the-difference-between-a-static-adr-and-a-living-adr)
- [What are Ghost Decisions and why do they matter?](#what-are-ghost-decisions-and-why-do-they-matter)
- [What is the Knowledge Graph and how are decisions connected?](#what-is-the-knowledge-graph-and-how-are-decisions-connected)
- [How does Decision Tree Cycle Detection prevent circular logic in complex DAGs?](#how-does-decision-tree-cycle-detection-prevent-circular-logic-in-complex-dags)
- [How does Tropelex compute Decision Confidence scores and half-life decay?](#how-does-tropelex-compute-decision-confidence-scores-and-half-life-decay)
- [What is the difference between pinning, unpinning, and attesting a decision?](#what-is-the-difference-between-pinning-unpinning-and-attesting-a-decision)
- [How do I backfill or edit the rationale context for an existing decision?](#how-do-i-backfill-or-edit-the-rationale-context-for-an-existing-decision)
- [How does Tropelex track developer friction and frustration signals?](#how-does-tropelex-track-developer-friction-and-frustration-signals)

### 4. Safety, Alignment & Governance
- [What is synthetic data and why should I provide synthetic data details?](#what-is-synthetic-data-and-why-should-i-provide-synthetic-data-details)
- [What is the EU AI Act compliance checker in the Synthetic Data Policy?](#what-is-the-eu-ai-act-compliance-checker-in-the-synthetic-data-policy)
- [How does the Pre-Write Safety Guard evaluate proposed diffs?](#how-does-the-pre-write-safety-guard-evaluate-proposed-diffs)
- [What is the Safety Envelope and how does Tropelex enforce multi-dimensional operational limits?](#what-is-the-safety-envelope-and-how-does-tropelex-enforce-multi-dimensional-operational-limits)
- [How does Alignment Drift detection measure semantic deviation from project baseline values?](#how-does-alignment-drift-detection-measure-semantic-deviation-from-project-baseline-values)
- [What is Corrigibility Testing and how does Tropelex evaluate an agent's receptiveness to corrections?](#what-is-corrigibility-testing-and-how-does-tropelex-evaluate-an-agents-receptiveness-to-corrections)
- [How does the Risk Heatmap quantify decision blast radius and cascade vulnerabilities?](#how-does-the-risk-heatmap-quantify-decision-blast-radius-and-cascade-vulnerabilities)
- [What are Fairness, Accountability, and Robustness audits in Tropelex governance?](#what-are-fairness-accountability-and-robustness-audits-in-tropelex-governance)
- [What is the Per-Agent Safety Budget and how do safety rate limits work?](#what-is-the-per-agent-safety-budget-and-how-do-safety-rate-limits-work)
- [What is the Persona Market and how are Agent Risk Tiers evaluated?](#what-is-the-persona-market-and-how-are-agent-risk-tiers-evaluated)
- [What is the "Needs Attention" queue and how do citation health checks work?](#what-is-the-needs-attention-queue-and-how-do-citation-health-checks-work)
- [How does Tropelex detect memory tampering and verify SHA-256 hash chains?](#how-does-tropelex-detect-memory-tampering-and-verify-sha-256-hash-chains)

### 5. Memory Lifecycle, Time Travel & Compaction
- [How do I rollback memory or time-travel to a previous session?](#how-do-i-rollback-memory-or-time-travel-to-a-previous-session)
- [How does session snapshotting work during active work sessions?](#how-does-session-snapshotting-work-during-active-work-sessions)
- [How does Memory Compaction prevent context bloat over months of use?](#how-does-memory-compaction-prevent-context-bloat-over-months-of-use)
- [How do automated Decay Reviews prompt developers to re-attest stale architectural assumptions?](#how-do-automated-decay-reviews-prompt-developers-to-re-attest-stale-architectural-assumptions)
- [How does 30-Day Trash Retention allow instant recovery of deleted projects?](#how-does-30-day-trash-retention-allow-instant-recovery-of-deleted-projects)

### 6. Research, Ingestion & Feeds (Tropebook)
- [What is the Tropebook citation engine and how does Deep Research work?](#what-is-the-tropebook-citation-engine-and-how-does-deep-research-work)
- [How does Multi-Engine Search Routing prioritize providers (Brave, Exa, Serper, DuckDuckGo) and handle fallbacks?](#how-does-multi-engine-search-routing-prioritize-providers-brave-exa-serper-duckduckgo-and-handle-fallbacks)
- [What are the differences between Quick, Balanced, and Deep research presets?](#what-are-the-differences-between-quick-balanced-and-deep-research-presets)
- [What is Query-Fingerprint Caching and how does it prevent redundant API token burn?](#what-is-query-fingerprint-caching-and-how-does-it-prevent-redundant-api-token-burn)
- [How do Multi-Project Research Feeds and automated background scheduling work?](#how-do-multi-project-research-feeds-and-automated-background-scheduling-work)
- [How does Citation Hygiene detect broken links, 404s, and stale web references?](#how-does-citation-hygiene-detect-broken-links-404s-and-stale-web-references)
- [How does Decision Promotion convert web research into verified architectural decisions?](#how-does-decision-promotion-convert-web-research-into-verified-architectural-decisions)
- [How do Query Rewrite Suggestions improve automated research feed results?](#how-do-query-rewrite-suggestions-improve-automated-research-feed-results)
- [What are Repo Seek, Trending Tech Feeds, and Last30Days queries?](#what-are-repo-seek-trending-tech-feeds-and-last30days-queries)

### 7. Multi-Agent Workflows & Team Collaboration
- [How do multiple different AI agents collaborate on the same project memory?](#how-do-multiple-different-ai-agents-collaborate-on-the-same-project-memory)
- [What is an Agent Handoff Packet and when should I use it?](#what-is-an-agent-handoff-packet-and-when-should-i-use-it)
- [Can Tropelex share rationale and knowledge across different projects (Cross-Pollination)?](#can-tropelex-share-rationale-and-knowledge-across-different-projects-cross-pollination)
- [How does PR Commentary Synthesis generate high-context pull request summaries?](#how-does-pr-commentary-synthesis-generate-high-context-pull-request-summaries)
- [How does the Financial Cost Ledger track token expenditure across models?](#how-does-the-financial-cost-ledger-track-token-expenditure-across-models)

### 8. Integrations, Tools & IDE Plugins
- [How do I configure the Tropelex Model Context Protocol (MCP) Server?](#how-do-i-configure-the-tropelex-model-context-protocol-mcp-server)
- [What slash commands are supported in OpenCode, Claude Code, Devin, Gemini CLI, Zed, Cursor, and Aider?](#what-slash-commands-are-supported-in-opencode-claude-code-devin-gemini-cli-zed-cursor-and-aider)
- [How do I integrate Tropelex with Emacs or VSCode?](#how-do-i-integrate-tropelex-with-emacs-or-vscode)
- [How does the Terminal UI (TUI) work and when should I use it?](#how-does-the-terminal-ui-tui-work-and-when-should-i-use-it)
- [How does Git Sync automatically synchronize repository commits with decision memory?](#how-does-git-sync-automatically-synchronize-repository-commits-with-decision-memory)
- [How does the OpenCode plugin hook into prompt generation via `plugins/tropelex.js`?](#how-does-the-opencode-plugin-hook-into-prompt-generation-via-pluginstropelexjs)

### 9. Troubleshooting, Error Codes & Diagnostics
- [Why am I getting `[Errno 98] address already in use` when starting the server?](#why-am-i-getting-errno-98-address-already-in-use-when-starting-the-server)
- [Why do I see "401 Unauthorized" or "API Key Missing" on certain endpoints?](#why-do-i-see-401-unauthorized-or-api-key-missing-on-certain-endpoints)
- [Why are changes to memory not immediately visible in the dashboard?](#why-are-changes-to-memory-not-immediately-visible-in-the-dashboard)
- [What should I do if an MCP client (Claude, Cursor, Devin, Zed) cannot connect to Tropelex?](#what-should-i-do-if-an-mcp-client-claude-cursor-devin-zed-cannot-connect-to-tropelex)
- [Why is the OpenCode plugin not registering `/tropelex-*` slash commands?](#why-is-the-opencode-plugin-not-registering-tropelex--slash-commands)
- [How do I diagnose and fix a corrupted or malformed `memory/<project>.json` file?](#how-do-i-diagnose-and-fix-a-corrupted-or-malformed-memoryprojectjson-file)
- [How do I run the automated Pytest suite to verify system health?](#how-do-i-run-the-automated-pytest-suite-to-verify-system-health)
- [What do the different HTTP status codes mean in Tropelex?](#what-do-the-different-http-status-codes-mean-in-tropelex)
- [HTTP 400 Bad Request — Root Causes & Solutions](#http-400-bad-request--root-causes--solutions)
- [HTTP 401 Unauthorized & 403 Forbidden — Security Gates & Safety Budgets](#http-401-unauthorized--403-forbidden--security-gates--safety-budgets)
- [HTTP 404 Not Found — Missing Projects, Decisions & Feeds](#http-404-not-found--missing-projects-decisions--feeds)
- [HTTP 409 Conflict — Name Collisions & Integrity Hash Conflicts](#http-409-conflict--name-collisions--integrity-hash-conflicts)
- [HTTP 422 Unprocessable Entity — Schema & Payload Validation Failures](#http-422-unprocessable-entity--schema--payload-validation-failures)
- [HTTP 429 Too Many Requests — Agent Mutation Rates & Provider Throttling](#http-429-too-many-requests--agent-mutation-rates--provider-throttling)
- [HTTP 500 Internal Server Error & 503 Service Unavailable — Server & Provider Failures](#http-500-internal-server-error--503-service-unavailable--server--provider-failures)
- [System & OS Error Codes (Errno 98, Errno 13, Errno 2) & CLI Exit Codes](#system--os-error-codes-errno-98-errno-13-errno-2--cli-exit-codes)

---

## Frequently Asked Questions

---

### <a id="what-is-tropelex-and-what-problem-does-it-solve"></a>What is Tropelex and what problem does it solve?

Tropelex is a persistent memory and rationale engine designed for AI coding agents. It solves the "stateless AI" problem where agents lose architectural context between chat sessions and repeatedly make conflicting decisions.

<details>
<summary>🔍 <b>Expand full answer</b></summary>
<br>

Without Tropelex, every new session requires re-explaining architectural choices, tech stack preferences, and safety boundaries. Tropelex acts as a long-term memory layer that automatically injects relevant project decisions, learned coding patterns, and rationale graphs directly into the AI prompt context, keeping human developers and AI agents perfectly aligned over months of active development.
</details>

---

### <a id="what-is-the-difference-between-tropelex-tropebook-and-the-web-dashboard"></a>What is the difference between Tropelex, Tropebook, and the Web Dashboard?

Tropelex is the overarching persistent memory and governance platform. Tropebook is the citation and web research engine inside Tropelex. The Web Dashboard is the graphical control panel.

<details>
<summary>🔍 <b>Expand full answer</b></summary>
<br>

Here is how the components relate:
* **Tropelex (Core Memory Engine):** The parent framework (`core/`) providing project state storage, living ADRs, decision DAGs, causal Q&A, safety envelopes, and multi-agent coordination.
* **Tropebook (Citation & Research Engine):** The research subsystem (`core/tropebook/`) responsible for deep web search, multi-provider query routing (Brave, Exa, Serper, DuckDuckGo), citation extraction, and research feed scheduling.
* **Web Dashboard (`UI/animated_tropebook_dashboard/code.html`):** The interactive web front-end served at `http://localhost:8766` providing visual management for all memory groups, knowledge graphs, and safety audit logs.
* **MCP Server (`mcp_server/server.py`):** The Model Context Protocol bridge allowing external AI tools (Claude Code, Devin, Cursor, Zed, Gemini CLI) to read and write memory directly.
</details>

---

### <a id="where-is-memory-research-and-governance-data-stored-on-disk"></a>Where is memory, research, and governance data stored on disk?

All memory, research, and governance data is stored in standard local JSON files inside the `memory/` directory of your workspace.

<details>
<summary>🔍 <b>Expand full answer</b></summary>
<br>

Tropelex operates on a 100% local-first architecture:
* **Project Decisions & Governance:** `memory/<project-name>.json` (stores decisions, sessions, safety metrics, and confidence decay parameters).
* **Research & Citations:** `memory/tropebook/citations.json` and `memory/tropebook/research_feeds.json`.
* **Session Diff Snapshots:** `memory/snapshots/` (stores timestamped unified diffs for time-travel and rollback).
* **Soft-Deleted Projects:** `memory/.trash/<project-name>.json` (retained for 30 days before permanent deletion).
* **Security Hash Chains:** Integrated directly into each decision record in `memory/<project-name>.json` as SHA-256 tamper-evident checksums.

No governance metrics or project code files are ever transmitted to third-party cloud servers or external databases.
</details>

---

### <a id="how-does-the-local-first-storage-architecture-guarantee-100-data-privacy"></a>How does the Local-First Storage Architecture guarantee 100% data privacy?

Tropelex requires no external database daemons (e.g. PostgreSQL, Redis, MongoDB) and transmits zero proprietary source code or decision telemetry to remote servers.

<details>
<summary>🔍 <b>Expand full answer</b></summary>
<br>

Key privacy guarantees:
* **Zero Telemetry Collection:** All analytics, friction scores, and audit logs are computed locally on your machine.
* **Plaintext Version-Controllable Files:** Memory files are standard JSON, allowing teams to check architectural memory directly into Git repositories alongside their code.
* **Offline Operation:** The entire memory engine, decision DAG, Living ADR generator, and BM25 search fallback operate with 100% functionality on air-gapped networks.
</details>

---

### <a id="how-does-project-isolation-work-and-how-does-soft-deletetrash-retention-work"></a>How does project isolation work, and how does soft-delete/trash retention work?

Each project in Tropelex is completely isolated in its own dedicated JSON memory file (`memory/<project>.json`), preventing cross-contamination between unrelated codebases.

<details>
<summary>🔍 <b>Expand full answer</b></summary>
<br>

Key project lifecycle features:
1. **Isolated Namespaces:** Decisions, sessions, goals, and agent budgets in project `Alpha` cannot leak into or overwrite project `Beta`.
2. **Soft-Delete Safety:** When a project is deleted via the API (`DELETE /api/memory/{project}`), it is moved into `memory/.trash/<project>.json` rather than immediately unlinked from disk.
3. **30-Day Trash Retention:** Deleted projects in `.trash/` remain restorable for 30 days. Projects older than 30 days are automatically purged during periodic maintenance ticks.
4. **Controlled Cross-Pollination:** To intentionally share architectural patterns between projects, Tropelex uses the explicit Cross-Pollination endpoint (`GET /api/memory/{project}/cross-pollinate`), which searches other projects for matching embeddings without merging raw memory stores.
</details>

---

### <a id="how-does-tropelex-handle-concurrent-writes-and-race-conditions-across-multiple-agents"></a>How does Tropelex handle concurrent writes and race conditions across multiple agents?

Tropelex employs atomic file-write patterns (`write-to-temp + atomic rename`) paired with file locking primitives (`fcntl` on POSIX / `msvcrt` on Windows) to guarantee ACID-like consistency during concurrent agent operations.

<details>
<summary>🔍 <b>Expand full answer</b></summary>
<br>

Concurrency mechanisms:
* **Atomic Replacement:** Changes to `memory/<project>.json` are written to a temporary staging file (`memory/.tmp_<project>_<pid>.json`) and flushed to disk before executing an atomic OS-level rename.
* **Optimistic Concurrency & ETag Verification:** API write endpoints verify `prev_hash` integrity; if two agents mutate the same project memory simultaneously, the second write detects a hash mismatch (HTTP 409) and safely merges using non-destructive DAG append rules.
</details>

---

### <a id="what-are-the-hardware-and-runtime-requirements-for-self-hosting-tropelex"></a>What are the hardware and runtime requirements for self-hosting Tropelex?

Tropelex is designed to be ultra-lightweight and runs effortlessly on developer laptops, edge devices, or cloud CI/CD runners:

<details>
<summary>🔍 <b>Expand full answer</b></summary>
<br>

* **Operating System:** Linux, macOS, or Windows (via WSL2 or native PowerShell).
* **Python Runtime:** Python 3.10, 3.11, or 3.12+.
* **Memory Footprint:** ~80 MB RAM baseline for the FastAPI backend and in-memory DAG index.
* **Storage Requirement:** <50 MB for core installation; memory JSON files consume ~50 KB per 100 recorded decisions.
* **Dependencies:** FastAPI, Uvicorn, Requests, NumPy, Pytest. (Zero required database servers).
</details>

---

### <a id="what-do-i-do-if-i-am-not-seeing-any-results-for-the-active-page"></a>What do I do if I am not seeing any results for the active page?

Try a **hard refresh** first (`Ctrl+Shift+R` / `Cmd+Shift+R`) — this clears the most common cause of "empty" or stuck data before you go looking for a real bug. If a section still displays empty metrics or zero decisions after that, ensure a project is selected in the top-bar dropdown (`#global-project-select`) and click the **Refresh** button on the section panel.

<details>
<summary>🔍 <b>Expand full answer</b></summary>
<br>

Follow these quick diagnostic steps:
1. **Hard refresh the page:** `Ctrl+Shift+R` (Windows/Linux) or `Cmd+Shift+R` (Mac). If the dashboard server was restarted while your tab was open, a normal refresh can still serve stale page state — a hard refresh forces a clean reload and resolves this the vast majority of the time.
2. **Check Global Project Selection:** Look at the top-right header dropdown. If it displays `No project`, click to select your active project (e.g., `Tropelex`).
3. **Run Diagnostic Self-Test:** Navigate to **Getting Started** (`Help Hub`) and click **Re-test All Systems** to verify FastAPI backend connection and Pytest status.
4. **Verify File Memory:** Confirm that `memory/<project-name>.json` exists in your workspace root. If empty, run `/tropelex-show-context` or record a starter decision.
</details>

---

### <a id="how-can-i-improve-my-general-ai-coding-workflows"></a>How can I improve my general AI coding workflows?

To maximize output quality with AI coding agents, establish consistent boundaries: define small modular tasks, record architectural decisions immediately, and maintain living context.

<details>
<summary>🔍 <b>Expand full answer</b></summary>
<br>

Recommended best practices:
1. **Record as You Decide:** When you or your agent makes a choice (e.g., "Use SQLite with WAL mode for local storage"), log it immediately with `/tropelex-record-decision`.
2. **Bundle Context Before Coding:** Prompt the agent with active decisions using `/tropelex-show-context` or context prefetch so the model respects existing constraints.
3. **End Every Session Cleanly:** Use `/tropelex-end-session` with a one-sentence summary of what was accomplished; this updates confidence decay scores and detects friction zones.
4. **Enforce Safety Gates:** Use the Pre-Write Safety Guard on large diffs to catch unintended architectural drift before committing to Git.
</details>

---

### <a id="what-makes-the-ais-job-easier-and-potentially-reduces-token-consumption"></a>What makes the AI's job easier and potentially reduces token consumption?

Providing a focused, structured memory snapshot of 5-10 active decisions is vastly more effective (and token-efficient) than dumping entire multi-megabyte source files into the prompt window.

<details>
<summary>🔍 <b>Expand full answer</b></summary>
<br>

Why focused memory beats raw file dumping:
* **Reduces Attention Distortion:** Large context windows suffer from "lost in the middle" degradation where models ignore constraints buried in thousands of lines of code.
* **Cuts Token Cost by 80%+:** Injecting a 500-token rationale summary costs a fraction of sending 50,000 tokens of raw source code on every request.
* **Eliminates Ambiguity:** Explicit ADRs (e.g., "Do not use external dependencies for JSON parsing") prevent the AI from guessing or making conflicting assumptions.
</details>

---

### <a id="what-is-the-exact-anatomy-of-an-injected-tropelex-context-packet-in-an-llm-prompt"></a>What is the exact anatomy of an injected Tropelex context packet in an LLM prompt?

When an agent requests context (`/tropelex-show-context` or `POST /api/memory/{project}/rag/context`), Tropelex synthesizes a clean Markdown block designed for the model's system prompt:

<details>
<summary>🔍 <b>Expand full answer</b></summary>
<br>

```markdown
<!-- TROPELEX ARCHITECTURAL CONTEXT (Project: Tropelex) -->
## Active Constraints & Architectural Decisions:
1. [DEC-01] (Confidence: 1.0, PINNED) Using Python 3.10+ & FastAPI for REST API backend.
   - Rationale: Provides high-throughput async processing and native OpenAPI schemas.
2. [DEC-04] (Confidence: 0.95) All memory stored in local-first memory/<project>.json files.
   - Constraint: Zero external database daemons required.
3. [DEC-09] (Confidence: 0.88) SHA-256 Merkle hash chain maintained across all records.

## Active Engineering Goals:
- [Goal #1] Implement multi-project research feed subscriptions (Status: IN_PROGRESS).
- [Goal #2] Zero-warning Pytest execution across all 2,600+ unit tests.

## Negative Constraints (Past Rejected Approaches):
- DO NOT use Celery/Redis for background workers (Rejected in DEC-03: Use BackgroundScheduler).
```
</details>

---

### <a id="how-does-tropelex-prevent-lost-in-the-middle-degradation-across-128k-context-windows"></a>How does Tropelex prevent "Lost-in-the-Middle" degradation across 128k+ context windows?

Research shows that LLMs accurately retrieve information from the beginning and end of long context windows, but suffer steep accuracy drops on information placed in the middle.

<details>
<summary>🔍 <b>Expand full answer</b></summary>
<br>

Tropelex mitigates this by:
1. **Dynamic Context Chunking:** Ordering high-priority pinned constraints at the very top of the system prompt.
2. **Context Compression:** Stripping out redundant discussion and preserving only the distilled rule statements.
3. **Targeted Subgraph Extraction:** Supplying only the 5-10 decisions directly connected to the active module rather than dumping the entire historical ledger.
</details>

---

### <a id="what-is-context-compression-and-how-does-it-work"></a>What is context compression and how does it work?

Context compression (`core/compression.py` / `POST /api/compress`) uses intelligent summarization and deduplication algorithms to condense long decision histories into compact token-efficient summaries without losing architectural intent.

<details>
<summary>🔍 <b>Expand full answer</b></summary>
<br>

Tropelex provides dual compression pathways:
1. **Deterministic / Heuristic Compression (No LLM Required):** Clusters decisions by tag/component, merges superseded choices, and prunes stale historical iterations.
2. **LLM-Refined Compaction (`OPENAI_API_KEY` configured):** Uses `gpt-4o-mini` to synthesize multi-paragraph rationale into dense, bulleted constraint rules.
</details>

---

### <a id="how-does-context-prefetch-select-the-optimal-subset-of-decisions-for-a-prompt"></a>How does Context Prefetch select the optimal subset of decisions for a prompt?

Context Prefetch (`core/rag.py` / `POST /api/memory/{project}/rag/context`) analyzes the developer's active task prompt or target filename and uses hybrid retrieval to extract only the decisions directly relevant to the current edit.

<details>
<summary>🔍 <b>Expand full answer</b></summary>
<br>

The prefetch algorithm performs:
1. **Component / Keyword Matching:** Extracts filenames, function names, and library tokens from the prompt.
2. **Semantic Cosine Similarity:** Computes vector similarity against the decision embedding index.
3. **Graph Neighborhood Expansion:** Follows `caused_by` and `supersedes` edges in the Decision Tree to include critical dependency constraints.
4. **Confidence Weighting:** Prioritizes pinned and high-confidence decisions over decayed or stale entries.
</details>

---

### <a id="how-does-semantic-search-work-when-api-keys-or-vector-embeddings-are-absent"></a>How does Semantic Search work when API keys or vector embeddings are absent?

Tropelex features an automatic zero-dependency fallback: if `OPENAI_API_KEY` is not set or embeddings cannot be computed, Tropelex falls back to a fast, local BM25/keyword ngram similarity engine.

<details>
<summary>🔍 <b>Expand full answer</b></summary>
<br>

* **With OpenAI Key:** Uses `text-embedding-3-small` (1536 dimensions) with cosine distance computed via local NumPy routines.
* **Without OpenAI Key (Offline / Local):** Tokenizes text into word-frequency term vectors with Jaccard/TF-IDF scoring. Search continues to function seamlessly with zero network dependencies.
</details>

---

### <a id="what-is-prompt-lab-and-how-does-prompt-genealogy-track-win-rates"></a>What is Prompt Lab and how does Prompt Genealogy track win rates?

Prompt Lab (`Engine Core` -> `Prompt Lab`) is an experimentation environment for drafting, testing, and tracking the evolutionary lineage of AI prompts across multiple model backends.

<details>
<summary>🔍 <b>Expand full answer</b></summary>
<br>

Key capabilities:
* **Prompt Genealogy (`core/prompt_genealogy.py`):** Tracks parent/child versions of prompts, recording modifications made across iterations.
* **Win-Rate Rankings:** Records binary or scored outcomes (e.g., test passed, build succeeded, code accepted) for each prompt variant.
* **Outcome Correlation:** Calculates which prompt phrasing correlates with higher first-attempt code accuracy, helping teams standardize on high-performing system prompts.
</details>

---

### <a id="what-is-the-goals--intent-engine-and-how-does-it-prevent-agent-goal-drift"></a>What is the Goals & Intent Engine and how does it prevent agent goal drift?

The Goals & Intent Engine (`Engine Core` -> `Goals & Intent` / `core/goals.py`) tracks active engineering objectives and scores whether ongoing code modifications remain aligned with the project's original intent.

<details>
<summary>🔍 <b>Expand full answer</b></summary>
<br>

Features of the Goals Engine:
* **Automatic Goal Detection:** Infers active goals from Git commit messages and session diff summaries.
* **Goal Status Tracking:** Monitors milestones across `Active`, `Blocked`, `In Review`, and `Completed`.
* **Alignment Scoring:** Evaluates whether newly added decisions conflict with or advance active goal statements, alerting developers when an agent wanders off-track.
</details>

---

### <a id="what-is-an-architecture-decision-record-adr"></a>What is an Architecture Decision Record (ADR)?

An **ADR (Architecture Decision Record)** is a short text document that captures an important architectural choice made in a project, along with its context, rationale, and consequences.

<details>
<summary>🔍 <b>Expand full answer</b></summary>
<br>

Tropelex introduces **Living ADRs** (`core/adr_generator.py`), which automatically compile your recorded project decisions into standardized industry formats:
- **Nygard Format:** Concise Title, Context, Decision, and Status.
- **MADR (Markdown Architectural Decision Records):** Standardized rationale, options considered, and pros/cons.
- **Tropelex Enhanced:** Enriched with live decision tree relationships (supersedes, caused_by, reverts) and real-time confidence scores.
</details>

---

### <a id="what-is-the-difference-between-a-static-adr-and-a-living-adr"></a>What is the difference between a static ADR and a Living ADR?

Traditional ADRs are static Markdown files written manually that quickly become outdated. A **Living ADR** in Tropelex is dynamically generated from real-time project memory, automatically updating confidence scores and lineage graph connections.

<details>
<summary>🔍 <b>Expand full answer</b></summary>
<br>

Unlike static files:
- Living ADRs track **Downstream Impact** (which subsequent decisions were caused by this choice).
- Living ADRs incorporate **Time-Based Knowledge Decay** scores.
- Living ADRs automatically update when a decision is superseded or reverted in Git.
</details>

---

### <a id="what-are-ghost-decisions-and-why-do-they-matter"></a>What are Ghost Decisions and why do they matter?

Ghost decisions occur when developers or AI agents write new code features or change architectures without logging the underlying rationale in project memory.

<details>
<summary>🔍 <b>Expand full answer</b></summary>
<br>

Ghost decisions create "silent drift," where future AI agents misunderstand the codebase structure and unintentionally break or revert unrecorded choices. Tropelex's **Ghost Decision Scanner** (`Quality & Integrity`) scans your repository diffs against active memory to surface uncaptured decisions before technical debt accumulates.
</details>

---

### <a id="what-is-the-knowledge-graph-and-how-are-decisions-connected"></a>What is the Knowledge Graph and how are decisions connected?

The Knowledge Graph (`Engine Core` -> `Decision Graph` / `core/decision_tree.py`) is a D3.js visualization that auto-detects relationships between architectural choices.

<details>
<summary>🔍 <b>Expand full answer</b></summary>
<br>

The graph automatically links decisions using 4 key relationship types:
1. `supersedes`: A newer decision replaces an older strategy.
2. `caused_by`: A decision was required due to a previous technical choice.
3. `related_to`: Shared component or tag context.
4. `reverts`: Undoes a previous decision.
</details>

---

### <a id="how-does-decision-tree-cycle-detection-prevent-circular-logic-in-complex-dags"></a>How does Decision Tree Cycle Detection prevent circular logic in complex DAGs?

The Decision Tree engine (`core/decision_tree.py`) runs Tarjan's strongly connected components algorithm to guarantee that architectural dependency links form a strict Directed Acyclic Graph (DAG).

<details>
<summary>🔍 <b>Expand full answer</b></summary>
<br>

If an agent attempts to link decision `A -> caused_by -> B` when `B` already depends on `A` (a circular dependency loop), Tropelex intercepts the mutation, rejects the invalid link, and issues an advisory error report.
</details>

---

### <a id="how-does-tropelex-compute-decision-confidence-scores-and-half-life-decay"></a>How does Tropelex compute Decision Confidence scores and half-life decay?

Tropelex assigns every decision a **Confidence Score** (0.0 to 1.0) based on citation diversity, human verification, and temporal age.

<details>
<summary>🔍 <b>Expand full answer</b></summary>
<br>

Confidence Calculation Mechanics:
* **Base Score:** Derived from citation richness and rationale detail.
* **Attestation Boost:** When a human developer or tech lead reviews and attests a decision, its confidence resets to 1.0.
* **Half-Life Decay:** Decisions that have not been reinforced, referenced, or attested over 30+ days gradually decay in confidence. Decayed decisions are flagged during **Decay Reviews** (`Quality & Integrity`) for re-validation or retirement.
</details>

---

### <a id="what-is-the-difference-between-pinning-unpinning-and-attesting-a-decision"></a>What is the difference between pinning, unpinning, and attesting a decision?

Tropelex provides three explicit governance controls for managing the lifecycle of critical decisions:

<details>
<summary>🔍 <b>Expand full answer</b></summary>
<br>

* **Pinning (`POST .../pin`):** Locks the decision into active context forever. Pinned decisions are immune to temporal decay and are guaranteed to appear in all context prefetch bundles.
* **Unpinning (`POST .../unpin`):** Returns the decision to standard decay scoring.
* **Attesting (`POST .../attest`):** Human sign-off confirming that the decision remains valid and compliant with current architecture, resetting its decay clock.
</details>

---

### <a id="how-do-i-backfill-or-edit-the-rationale-context-for-an-existing-decision"></a>How do I backfill or edit the rationale context for an existing decision?

You can update the rationale context of any recorded decision without deleting it or breaking graph relationships using the context patch endpoint.

<details>
<summary>🔍 <b>Expand full answer</b></summary>
<br>

Execute a `PATCH` request against `/api/memory/{project}/decisions/{decision_id}/context`:

```bash
curl -X PATCH http://localhost:8766/api/memory/Tropelex/decisions/dec-123/context \
  -H "Content-Type: application/json" \
  -d '{"context": "Updated benchmark data confirms FastAPI out-performs Flask by 3.2x under async load."}'
```
</details>

---

### <a id="how-does-tropelex-track-developer-friction-and-frustration-signals"></a>How does Tropelex track developer friction and frustration signals?

Friction Mining (`Quality & Integrity`) scans session transcripts and editor behavior for implicit frustration signals (such as rapid repeated file saves, failed compilation loops, or repeated prompts).

<details>
<summary>🔍 <b>Expand full answer</b></summary>
<br>

When 5+ rapid saves occur in 5 seconds or a build command fails twice, Tropelex flags a **Friction Zone**. This alerts team leads and AI agents to clarify underspecified requirements before developer fatigue sets in.
</details>

---

### <a id="what-is-synthetic-data-and-why-should-i-provide-synthetic-data-details"></a>What is synthetic data and why should I provide synthetic data details?

Synthetic data refers to artificially generated training datasets, test suites, or mock payloads created by LLMs rather than collected from direct human activity.

<details>
<summary>🔍 <b>Expand full answer</b></summary>
<br>

Providing synthetic data details is vital for AI safety and legal compliance:
1. **Prevents Model Collapse:** Over-reliance on synthetic outputs without ground-truth validation causes generational quality degradation.
2. **Auditability:** Recording prompt provenance, generation seeds, and filtering thresholds ensures full reproducibility for enterprise security audits.
</details>

---

### <a id="what-is-the-eu-ai-act-compliance-checker-in-the-synthetic-data-policy"></a>What is the EU AI Act compliance checker in the Synthetic Data Policy?

The Synthetic Data Policy engine (`Safety & Alignment` -> `Synthetic Data Policies`) validates project datasets against EU AI Act Article 10 and Article 13 transparency mandates.

<details>
<summary>🔍 <b>Expand full answer</b></summary>
<br>

Compliance checks include:
* **High-Risk AI Screening:** Flags datasets used in safety-critical automated pipelines.
* **Watermarking & Provenance:** Verifies that synthetic outputs contain cryptographic watermarks or metadata tags.
* **Bias & Representation Checks:** Evaluates data diversity scores to mitigate automated demographic or technical bias.
</details>

---

### <a id="how-does-the-pre-write-safety-guard-evaluate-proposed-diffs"></a>How does the Pre-Write Safety Guard evaluate proposed diffs?

The Pre-Write Safety Guard (`Quality & Integrity`) lets you paste a proposed code diff or function change *before* applying it to test if it violates active decisions or security rules.

<details>
<summary>🔍 <b>Expand full answer</b></summary>
<br>

When you click **Check for Ghosts / Pre-Write Check**, Tropelex parses the AST and diff signature, comparing it against the project decision graph. If the proposed code introduces an unrecorded architecture change or breaks a safety constraint, Tropelex issues a warning report with recommended mitigations.
</details>

---

### <a id="what-is-the-safety-envelope-and-how-does-tropelex-enforce-multi-dimensional-operational-limits"></a>What is the Safety Envelope and how does Tropelex enforce multi-dimensional operational limits?

The Safety Envelope (`Safety & Alignment` -> `Safety Envelope` / `core/safety_envelope.py`) establishes dynamic operational boundaries beyond which an AI agent cannot execute changes without explicit human intervention.

<details>
<summary>🔍 <b>Expand full answer</b></summary>
<br>

The Safety Envelope monitors four simultaneous operational vectors:
1. **Token Velocity Cap:** Limits maximum tokens consumed per minute to prevent runaway loops.
2. **Blast Radius Threshold:** Evaluates the number of downstream dependent files affected by a proposed edit; changes exceeding the threshold trigger a containment warning.
3. **Protected Module Boundaries:** Core kernel and security paths (e.g., `core/governance.py`, `auth/`, crypto routines) are marked immutable to unauthorized agents.
4. **Privilege Escalation Barriers:** Prevents agents from assigning themselves elevated permissions or disabling test validation flags.

Query current safety envelope status:
```bash
curl -s http://localhost:8766/api/memory/Tropelex/safety-envelope
```
</details>

---

### <a id="how-does-alignment-drift-detection-measure-semantic-deviation-from-project-baseline-values"></a>How does Alignment Drift detection measure semantic deviation from project baseline values?

Alignment Drift (`Safety & Alignment` -> `Alignment Drift` / `core/alignment_drift.py`) calculates the semantic vector distance between newly proposed architectural decisions and the project's foundational value charter.

<details>
<summary>🔍 <b>Expand full answer</b></summary>
<br>

Mechanics:
* **Baseline Value Anchor:** When a project is initialized, foundational goals and non-negotiable architectural principles (e.g., "offline-first", "zero-telemetry", "deterministic verification") form the baseline embedding vector.
* **Rolling Semantic Cosine Distance:** Every new decision is embedded and scored against the baseline.
* **Drift Velocity Alerting:** If recent decisions drift more than 25% from the anchor (indicating subtle architectural erosion or reward hacking), Tropelex flags an **Alignment Drift Warning** on the governance dashboard (`GET /api/memory/{project}/alignment/drift`).
</details>

---

### <a id="what-is-corrigibility-testing-and-how-does-tropelex-evaluate-an-agents-receptiveness-to-corrections"></a>What is Corrigibility Testing and how does Tropelex evaluate an agent's receptiveness to corrections?

Corrigibility Testing (`Safety & Alignment` -> `Corrigibility` / `core/corrigibility.py`) measures how reliably an AI agent accepts, retains, and respects human architectural interventions without reverting to discarded approaches.

<details>
<summary>🔍 <b>Expand full answer</b></summary>
<br>

Features:
* **Rejection Memory:** When a developer rejects an agent's proposed decision or code diff, Tropelex records the rejection rationale into the project negative-constraint ledger.
* **Corrigibility Score (0.0 to 1.0):** If an agent repeatedly attempts rejected strategies across subsequent sessions, its Corrigibility Score drops, and its risk tier in the Persona Market is downgraded.
* **Reversion Detection:** Flags instances where an agent silently reintroduces code patterns previously vetoed by human review (`GET /api/memory/{project}/corrigibility`).
</details>

---

### <a id="how-does-the-risk-heatmap-quantify-decision-blast-radius-and-cascade-vulnerabilities"></a>How does the Risk Heatmap quantify decision blast radius and cascade vulnerabilities?

The Risk Heatmap (`Safety & Alignment` -> `Risk Heatmap` / `core/risk_heatmap.py`) analyzes the Decision DAG to identify high-centrality decisions whose failure or modification would cause widespread architectural disruption.

<details>
<summary>🔍 <b>Expand full answer</b></summary>
<br>

Risk Classification:
* **Critical Root Nodes (Red):** Decisions with 5+ downstream `caused_by` dependents (e.g., primary database choice, authentication framework). Modifications require multi-agent consensus and human attestation.
* **Intermediate Nodes (Amber):** Decisions with 2-4 dependents.
* **Leaf Nodes (Green):** Isolated decisions with zero dependents (low blast radius; safe for autonomous agent refactoring).

Inspect risk metrics via REST API:
```bash
curl -s http://localhost:8766/api/memory/Tropelex/risk-heatmap
```
</details>

---

### <a id="what-are-fairness-accountability-and-robustness-audits-in-tropelex-governance"></a>What are Fairness, Accountability, and Robustness audits in Tropelex governance?

Tropelex provides three automated audit engines (`core/fairness.py`, `core/accountability.py`, `core/robustness.py`) for enterprise governance compliance:

<details>
<summary>🔍 <b>Expand full answer</b></summary>
<br>

1. **Fairness Audit (`GET /api/memory/{project}/fairness/audit`):** Scans synthetic datasets and agent decisions for demographic, statistical, or category imbalance.
2. **Accountability Report (`GET /api/memory/{project}/accountability/report`):** Generates an auditable chain of custody linking every line of generated code to the exact prompt, agent persona, and human reviewer who authorized it.
3. **Robustness Test (`GET /api/memory/{project}/robustness/test`):** Injects adversarial edge-case inputs into prompt templates to verify that safety constraints remain intact under jailbreak pressure.
</details>

---

### <a id="what-is-the-per-agent-safety-budget-and-how-do-safety-rate-limits-work"></a>What is the Per-Agent Safety Budget and how do safety rate limits work?

The Safety Budget system (`Safety & Alignment` -> `Agent Safety Budget`) assigns hourly or daily mutation limits to individual AI agents (e.g., Devin, Claude, Cursor, Gemini).

<details>
<summary>🔍 <b>Expand full answer</b></summary>
<br>

How Safety Budgets protect codebases:
* **Mutation Limits:** Caps the number of decisions an agent can record or modify within a 1-hour window.
* **Risk Threshold Escalation:** High-risk decisions (e.g., security, database schema changes) consume more budget than documentation updates.
* **Human-in-the-Loop Escalation:** When an agent exhausts its safety budget, subsequent write actions are halted and routed to the **Needs Attention** queue for human approval.
</details>

---

### <a id="what-is-the-persona-market-and-how-are-agent-risk-tiers-evaluated"></a>What is the Persona Market and how are Agent Risk Tiers evaluated?

The Persona Market (`Safety & Alignment` -> `Persona Leaderboard`) tracks the behavioral reliability, test passing rate, and safety violation frequency of different AI personas and models.

<details>
<summary>🔍 <b>Expand full answer</b></summary>
<br>

Personas are classified into 3 Risk Tiers:
* **Tier 1 (Low Risk - Trusted):** Models with >95% verification rates and zero security policy violations. Authorized with autonomous decision-logging privileges.
* **Tier 2 (Moderate Risk - Monitored):** Models with occasional test regressions. Requires automated Pre-Write Guard validation.
* **Tier 3 (High Risk - Supervised):** Experimental models or untrusted external scripts. All decisions are placed in `Pending Review` until confirmed by a human developer.
</details>

---

### <a id="what-is-the-needs-attention-queue-and-how-do-citation-health-checks-work"></a>What is the "Needs Attention" queue and how do citation health checks work?

The Needs Attention panel (`Safety & Alignment` -> `Needs Attention`) aggregates actionable governance flags that require developer intervention.

<details>
<summary>🔍 <b>Expand full answer</b></summary>
<br>

Flags include:
1. **Broken / Stale Citations:** Decisions citing URLs or research feeds that return HTTP 404/500 errors.
2. **Escalated Safety Reviews:** Decisions flagged by the Pre-Write Guard or budget exhaustion.
3. **Ghost Decision Alerts:** Code modifications detected without corresponding memory records.
</details>

---

### <a id="how-does-tropelex-detect-memory-tampering-and-verify-sha-256-hash-chains"></a>How does Tropelex detect memory tampering and verify SHA-256 hash chains?

Tropelex maintains a cryptographic Merkle-like hash chain across all recorded decisions in `memory/<project>.json`.

<details>
<summary>🔍 <b>Expand full answer</b></summary>
<br>

Every decision contains a `hash` computed from its timestamp, text, rationale, and the `hash` of the preceding decision (`prev_hash`). Running the integrity verification tool (`GET /api/memory/{project}/integrity/verify`) recalculates the entire chain; if any historical decision was modified or deleted outside of Tropelex, the tamper detection engine identifies the exact corrupted record.
</details>

---

### <a id="how-do-i-rollback-memory-or-time-travel-to-a-previous-session"></a>How do I rollback memory or time-travel to a previous session?

Session Replay (`Memory Lifecycle` -> `Session Replay`) snapshots memory state at the start and end of every session, allowing you to view structured diffs or rollback project memory.

<details>
<summary>🔍 <b>Expand full answer</b></summary>
<br>

If an experimental session introduced unwanted or incorrect decisions into project memory:
1. Navigate to **Memory Lifecycle** -> **Session Replay**.
2. Click **diff** to inspect exact memory changes made during that session.
3. Click **Rollback** (`POST /api/memory/{project}/sessions/{session_id}/rollback`) to restore project memory to the exact state before that session began.
</details>

---

### <a id="how-does-session-snapshotting-work-during-active-work-sessions"></a>How does session snapshotting work during active work sessions?

When you call `/tropelex-end-session` or invoke the session endpoint, Tropelex records a session object containing:
* Start and End timestamps.
* List of decisions added, updated, or superseded during the session.
* Git commit hash and unified diff snapshot saved in `memory/snapshots/`.
* Developer friction metrics and test outcomes.
</details>

---

### <a id="how-does-memory-compaction-prevent-context-bloat-over-months-of-use"></a>How does Memory Compaction prevent context bloat over months of use?

Over long projects, logging hundreds of decisions could bloat the memory store. Memory Compaction (`POST /api/compress`) runs hierarchical pruning to maintain high signal-to-noise ratio.

<details>
<summary>🔍 <b>Expand full answer</b></summary>
<br>

Compaction actions:
1. Merges intermediate iterative decisions into final architectural rules.
2. Archives superseded historical iterations into deep storage.
3. Preserves all pinned, attested, and active Living ADRs with 100% fidelity.
</details>

---

### <a id="how-do-automated-decay-reviews-prompt-developers-to-re-attest-stale-architectural-assumptions"></a>How do automated Decay Reviews prompt developers to re-attest stale architectural assumptions?

Decay Reviews (`Quality & Integrity` -> `Decay Reviews` / `core/decay.py`) run automated periodic audits that flag decisions that have not been reinforced in 30, 60, or 90 days.

<details>
<summary>🔍 <b>Expand full answer</b></summary>
<br>

When a decision reaches its decay threshold:
* It is placed on the **Decay Review Queue**.
* Developers can choose:
  1. **Attest:** Resets the confidence clock to 1.0 for another 30 days.
  2. **Supersede:** Log a newer decision that replaces the outdated strategy.
  3. **Deprecate:** Archive the decision into inactive history.
</details>

---

### <a id="how-does-30-day-trash-retention-allow-instant-recovery-of-deleted-projects"></a>How does 30-Day Trash Retention allow instant recovery of deleted projects?

When a project is deleted via `DELETE /api/memory/{project}`, Tropelex moves the file to `memory/.trash/<project>.json` instead of executing an unrecoverable unlink.

<details>
<summary>🔍 <b>Expand full answer</b></summary>
<br>

To restore a deleted project:
```bash
# Move the file back from .trash to active memory
mv memory/.trash/MyProject.json memory/MyProject.json
```
After moving the file back, execute a refresh on the dashboard or call `GET /api/projects` to resume work immediately.
</details>

---

### <a id="what-is-the-tropebook-citation-engine-and-how-does-deep-research-work"></a>What is the Tropebook citation engine and how does Deep Research work?

Tropebook is Tropelex's deep research engine (`core/tropebook/`) that performs verified web research and automatically extracts citation-grade documentation.

<details>
<summary>🔍 <b>Expand full answer</b></summary>
<br>

Deep Research Workflow (`POST /api/research/auto`):
1. **Multi-Engine Search Routing:** Queries primary search engines (Brave Search -> Exa -> Serper -> DuckDuckGo fallback).
2. **Page Content Extraction & Markdown Conversion:** Downloads full HTML, strips ads/cruft, and parses technical documentation into clean Markdown.
3. **Citation Ledger:** Saves source URLs, snippets, and publication dates into `memory/tropebook/citations.json`.
</details>

---

### <a id="how-does-multi-engine-search-routing-prioritize-providers-brave-exa-serper-duckduckgo-and-handle-fallbacks"></a>How does Multi-Engine Search Routing prioritize providers (Brave, Exa, Serper, DuckDuckGo) and handle fallbacks?

Tropebook uses an intelligent cascading provider architecture (`core/tropebook/deep_research.py`) that prioritizes citation-rich search engines and automatically fails over if a provider is unavailable or rate-limited.

<details>
<summary>🔍 <b>Expand full answer</b></summary>
<br>

Cascading Resolution Order:
1. **Brave Search API (`BRAVE_SEARCH_API_KEY`):** Primary provider. Delivers structured technical citations, publication timestamps, and raw text snippets.
2. **Exa Neural Search (`EXA_API_KEY`):** Secondary semantic fallback. Excellent for finding obscure code patterns and developer blog discussions.
3. **Serper Google API (`SERPER_API_KEY`):** High-volume fallback for broad technical queries.
4. **DuckDuckGo (Zero-Key Local Fallback):** Guaranteed fallback requiring zero API keys and zero configuration.

If a primary provider returns HTTP 429 or 503, Tropebook seamlessly switches to the next provider without failing the parent research task.
</details>

---

### <a id="what-are-the-differences-between-quick-balanced-and-deep-research-presets"></a>What are the differences between Quick, Balanced, and Deep research presets?

Tropebook provides 3 research presets tailored for different latency and depth requirements:

<details>
<summary>🔍 <b>Expand full answer</b></summary>
<br>

* **Quick (Fastest):** Executes 1 targeted search query against the top provider. Returns immediate 3-5 citation summaries in <2 seconds.
* **Balanced (Default):** Runs 3 diversified queries across multiple search providers. Extracts full body markdown from the top 3 results.
* **Deep (Comprehensive):** Executes 5+ recursive queries with query-fingerprint caching. Analyzes multiple sources for consensus, contradiction detection, and citation diversity scoring.
</details>

---

### <a id="what-is-query-fingerprint-caching-and-how-does-it-prevent-redundant-api-token-burn"></a>What is Query-Fingerprint Caching and how does it prevent redundant API token burn?

Query-Fingerprint Caching (`core/tropebook/deep_research.py`) computes a deterministic SHA-256 hash of normalized search queries to prevent duplicate external API calls.

<details>
<summary>🔍 <b>Expand full answer</b></summary>
<br>

Mechanics:
* **Query Normalization:** Strips punctuation, sorts keyword tokens, and lowercases text.
* **Cache TTL:** Search results and parsed markdown extracts are cached locally in `memory/tropebook/cache/` for 24 hours (configurable).
* **Token Savings:** If multiple coding agents or research feeds ask identical questions (e.g., `"FastAPI async background tasks"`), cached citation bundles are returned in <5ms with zero external API token burn.
</details>

---

### <a id="how-do-multi-project-research-feeds-and-automated-background-scheduling-work"></a>How do Multi-Project Research Feeds and automated background scheduling work?

Research Feeds (`Research & Ingestion` -> `Research Feeds` / `core/research_feeds.py`) allow you to subscribe to ongoing topics (e.g., `"FastAPI security advisories"`, `"PyTorch 2.x migration guides"`).

<details>
<summary>🔍 <b>Expand full answer</b></summary>
<br>

Features:
* **Automated Background Polling:** Tropelex's background scheduler checks active feeds periodically.
* **Multi-Project Sharing:** Feeds can be shared across multiple projects without duplicating research runs.
* **Citation Notifications:** Discovered updates appear directly in your dashboard telemetry stream.
</details>

---

### <a id="how-does-citation-hygiene-detect-broken-links-404s-and-stale-web-references"></a>How does Citation Hygiene detect broken links, 404s, and stale web references?

Citation Hygiene (`core/tropebook/stale_detector.py` / `GET /api/research/stale`) runs periodic lightweight HTTP `HEAD` checks on all recorded research URLs to ensure documentation links remain alive and trustworthy.

<details>
<summary>🔍 <b>Expand full answer</b></summary>
<br>

Hygiene checks:
* **Dead Link Detection:** Identifies URLs returning HTTP 404 Not Found, 410 Gone, or DNS failures.
* **Redirect Tracking:** Detects migrated documentation URLs (HTTP 301/308) and automatically updates citation targets.
* **Needs Attention Integration:** Stale or broken citations are flagged in the **Needs Attention** queue (`Safety & Alignment`), alerting developers before an agent references defunct API docs.
</details>

---

### <a id="how-does-decision-promotion-convert-web-research-into-verified-architectural-decisions"></a>How does Decision Promotion convert web research into verified architectural decisions?

Decision Promotion (`POST /api/memory/{project}/decisions/promote`) allows you to convert a research finding directly into an official project decision with attached source citations in a single click.

<details>
<summary>🔍 <b>Expand full answer</b></summary>
<br>

When a research run produces a validated architectural solution:
1. In the Research UI, click **Promote to Decision**.
2. Tropelex copies the finding into `memory/<project>.json`, attaches the citation IDs, and links the decision into the Decision Tree.
</details>

---

### <a id="how-do-query-rewrite-suggestions-improve-automated-research-feed-results"></a>How do Query Rewrite Suggestions improve automated research feed results?

Query Rewrite (`POST /api/research-feeds/{feed_id}/suggest-query-rewrite`) uses LLM analysis to refine search terms when an automated research feed returns too few results or excessive off-topic noise.

<details>
<summary>🔍 <b>Expand full answer</b></summary>
<br>

When you trigger a query rewrite:
* **Broadening:** Expands overly restrictive queries (e.g., converting `"Python 3.12 GIL removal deadlock in multiprocessing"` to broader semantic concepts).
* **Narrowing:** Adds negative keyword exclusions when generic search terms return consumer marketing articles instead of technical developer documentation.
</details>

---

### <a id="what-are-repo-seek-trending-tech-feeds-and-last30days-queries"></a>What are Repo Seek, Trending Tech Feeds, and Last30Days queries?

Tropelex includes specialized research tools for open-source discovery:
* **Repo Seek:** Searches GitHub repositories for code patterns and verified implementation examples.
* **Trending Tech Feed:** Monitors real-time developer trends and library releases.
* **Last30Days Research (`/api/last30days/query`):** Executes time-bounded web searches constrained to the past 30 days to ensure recent library compatibility.
</details>

---

### <a id="how-do-multiple-different-ai-agents-collaborate-on-the-same-project-memory"></a>How do multiple different AI agents collaborate on the same project memory?

Tropelex acts as a universal coordination bus across diverse AI models and coding assistants (e.g., Claude Code, Cursor, Devin, Gemini CLI, Zed, Aider).

<details>
<summary>🔍 <b>Expand full answer</b></summary>
<br>

Collaboration mechanics:
* **Unified State Ledger:** When Claude Code records an architectural decision, Cursor and Devin immediately see that decision in their context prefetch bundle on the next edit.
* **Attribution Metadata:** Every decision and session record logs the `agent` (e.g., `claude-3-5-sonnet`, `gemini-1.5-pro`, `devin`) and persona role responsible for the change.
* **Conflict Prevention:** When Agent A is working on module `auth/`, Tropelex flags active work in progress to prevent Agent B from applying colliding diffs.
</details>

---

### <a id="what-is-an-agent-handoff-packet-and-when-should-i-use-it"></a>What is an Agent Handoff Packet and when should I use it?

An Agent Handoff Packet (`Team & Collaboration` -> `Agent Handoff`) is a role-tailored context bundle designed to transfer work from one specialized agent role to another (e.g., from `Architect` to `CoderAgent` or `TestEngineer`).

<details>
<summary>🔍 <b>Expand full answer</b></summary>
<br>

Instead of dumping raw context, the packet builder (`core/handoff/packet_builder.py`) filters decisions and requirements to match the receiving agent's role profile:
- **`CoderAgent`**: Receives function signatures, active API tasks, and structural guidelines.
- **`TestEngineer`**: Receives boundary conditions, failure cases, and assertion targets.
- **`DevOpsSpecialist`**: Receives deployment constraints, environment variables, and safety envelope limits.
</details>

---

### <a id="can-tropelex-share-rationale-and-knowledge-across-different-projects-cross-pollination"></a>Can Tropelex share rationale and knowledge across different projects (Cross-Pollination)?

Yes. Tropelex includes a **Cross-Pollination Engine** (`core/rag.py`) that searches across multiple project memories to suggest proven architectural solutions and patterns from other repositories.

<details>
<summary>🔍 <b>Expand full answer</b></summary>
<br>

If you encounter a problem in project B (e.g., `"implement JWT auth with refresh tokens"`), Tropelex's semantic RAG engine checks project A's decision ledger and suggests identical, verified solutions that succeeded in past sessions.
</details>

---

### <a id="how-does-pr-commentary-synthesis-generate-high-context-pull-request-summaries"></a>How does PR Commentary Synthesis generate high-context pull request summaries?

PR Commentary Synthesis (`core/pr_synthesis.py` / `POST /api/memory/{project}/pr-summary`) analyzes session diffs and recorded decisions to generate complete, high-quality GitHub/GitLab PR descriptions.

<details>
<summary>🔍 <b>Expand full answer</b></summary>
<br>

Generated PR descriptions include:
1. **Summary of Changes:** Grouped by architectural component.
2. **Linked Decisions & ADRs:** Explicitly documents *why* each change was made with links to active decision records.
3. **Safety & Test Verification:** Summarizes Pytest outcomes, lint validations, and Pre-Write Safety Guard checks.
</details>

---

### <a id="how-does-the-financial-cost-ledger-track-token-expenditure-across-models"></a>How does the Financial Cost Ledger track token expenditure across models?

The Financial Cost Ledger (`Integrations & Ops` -> `Cost Ledger` / `GET /api/memory/{project}/cost/report`) computes real-time dollar estimates for all LLM calls, embeddings, and research queries.

<details>
<summary>🔍 <b>Expand full answer</b></summary>
<br>

Cost tracking features:
* **Model Pricing Breakdown:** Tracks token costs across Claude 3.5 Sonnet, GPT-4o, GPT-4o-mini, Gemini 1.5 Pro, and DeepSeek.
* **Per-Agent Attribution:** Identifies which agent or persona consumed the highest token volume.
* **Savings from Context Compaction:** Quantifies total dollars saved by injecting compacted memory over raw full-file context.
</details>

---

### <a id="how-do-i-configure-the-tropelex-model-context-protocol-mcp-server"></a>How do I configure the Tropelex Model Context Protocol (MCP) Server?

Tropelex provides a standard MCP server in `mcp_server/server.py` exposing 11 tools and 4 interactive prompts.

<details>
<summary>🔍 <b>Expand full answer</b></summary>
<br>

Add Tropelex to your client's MCP configuration (e.g., `~/.claude/claude_desktop_config.json` or `.mcp.json`):

```json
{
  "mcpServers": {
    "tropelex": {
      "command": "python3",
      "args": ["-m", "mcp_server.server"],
      "env": {
        "TROPELEX_URL": "http://127.0.0.1:8766"
      }
    }
  }
}
```
</details>

---

### <a id="what-slash-commands-are-supported-in-opencode-claude-code-devin-gemini-cli-zed-cursor-and-aider"></a>What slash commands are supported in OpenCode, Claude Code, Devin, Gemini CLI, Zed, Cursor, and Aider?

Tropelex provides full slash command parity across all major AI coding environments:

<details>
<summary>🔍 <b>Expand full answer</b></summary>
<br>

| Slash Command | Supported AI Tools | Usage & Description |
| :--- | :--- | :--- |
| `/tropelex-record-decision` *(or `/record_decision`)* | OpenCode, Claude Code, Devin, Gemini CLI, Zed, Cursor, Aider | Records architectural decision: `/tropelex-record-decision Using FastAPI` |
| `/tropelex-end-session` *(or `/end_session`)* | OpenCode, Claude Code, Devin, Gemini CLI, Zed, Cursor, Aider | Summarizes work session: `/tropelex-end-session Completed auth module` |
| `/tropelex-show-context` *(or `/show_context`)* | OpenCode, Claude Code, Devin, Gemini CLI, Zed, Cursor | Displays active task context bundle |
| `/tropelex-context` *(or `/explain_why`)* | OpenCode, Claude Code, Devin, Gemini CLI, Zed, Cursor | Asks causal question: `/explain_why Why did we choose SQLite?` |
| `/tropelex-up` | OpenCode, Claude Code | Initializes or updates project details |
</details>

---

### <a id="how-do-i-integrate-tropelex-with-emacs-or-vscode"></a>How do I integrate Tropelex with Emacs or VSCode?

Tropelex includes native integrations for Emacs (`emacs/tropelex-capture.el`) and VSCode extensions (`vscode-tropelex/`).

<details>
<summary>🔍 <b>Expand full answer</b></summary>
<br>

In Emacs:
- `C-c t c`: Capture active buffer / function as a decision.
- `C-c t r`: Capture selected region as decision context.
- `C-c t f`: Scan buffer for friction signals.
- `C-c t g`: Capture current git HEAD commit as a decision.
- `C-c t s`: Check server connectivity.
</details>

---

### <a id="how-does-the-terminal-ui-tui-work-and-when-should-i-use-it"></a>How does the Terminal UI (TUI) work and when should I use it?

Tropelex includes a standalone curses-based Terminal UI (`core/tropebook/tui.py`) designed for lightweight SSH sessions, remote headless servers, or developers who prefer working purely inside the terminal.

<details>
<summary>🔍 <b>Expand full answer</b></summary>
<br>

Launch the TUI from the repository root:
```bash
python3 -m core.tropebook.tui
```
Use the arrow keys or `j`/`k` to navigate decisions, view active citations, search research feeds, and trigger compaction without opening a browser.
</details>

---

### <a id="how-does-git-sync-automatically-synchronize-repository-commits-with-decision-memory"></a>How does Git Sync automatically synchronize repository commits with decision memory?

Git Sync (`Integrations & Ops` -> `Git Sync` / `POST /api/git/sync`) connects your Git commit history with Tropelex's architectural decision ledger.

<details>
<summary>🔍 <b>Expand full answer</b></summary>
<br>

Git Sync capabilities:
* **Commit-to-Decision Linking:** Matches Git commit hashes with decisions made in corresponding work sessions.
* **Auto-Commit Memory:** Automatically stages and commits updated `memory/<project>.json` files when milestone sessions are completed.
* **Deep Git Summary:** Analyzes recent repository commit logs to detect potential unrecorded architectural changes.
</details>

---

### <a id="how-does-the-opencode-plugin-hook-into-prompt-generation-via-pluginstropelexjs"></a>How does the OpenCode plugin hook into prompt generation via `plugins/tropelex.js`?

The OpenCode plugin (`plugins/tropelex.js`) registers custom tool handlers and slash commands directly with the OpenCode runtime.

<details>
<summary>🔍 <b>Expand full answer</b></summary>
<br>

When you execute `/tropelex-show-context` inside OpenCode:
1. `plugins/tropelex.js` queries `http://127.0.0.1:8766/api/memory/{project}/rag/context`.
2. The endpoint returns the structured context block.
3. The plugin injects the block directly into the ongoing agent conversation as a high-priority system context message.
</details>

---

### <a id="why-am-i-getting-errno-98-address-already-in-use-when-starting-the-server"></a>Why am I getting `[Errno 98] address already in use` when starting the server?

This error occurs when a previous instance of the Tropelex FastAPI server (or another service) is already running and bound to port `8766`.

<details>
<summary>🔍 <b>Expand full answer</b></summary>
<br>

To resolve:
1. Find the running process PID:
   ```bash
   pgrep -f "core.tropebook.web.server"
   ```
2. Terminate the existing process:
   ```bash
   kill -9 $(pgrep -f "core.tropebook.web.server")
   ```
3. Restart the server:
   ```bash
   python3 -m core.tropebook.web.server
   ```
</details>

---

### <a id="why-do-i-see-401-unauthorized-or-api-key-missing-on-certain-endpoints"></a>Why do I see "401 Unauthorized" or "API Key Missing" on certain endpoints?

Tropelex runs core memory features locally without requiring API keys. However, certain advanced external features require third-party provider keys:

<details>
<summary>🔍 <b>Expand full answer</b></summary>
<br>

* **Web Deep Research (`/api/research/auto`):** Requires `BRAVE_SEARCH_API_KEY`, `EXA_API_KEY`, or `SERPER_API_KEY`. (DuckDuckGo fallback runs if none are provided).
* **Vector Embeddings (`/api/semantic-search`):** Uses `OPENAI_API_KEY`. If absent, Tropelex automatically switches to the offline TF-IDF keyword similarity fallback.
* Set keys in your environment or workspace `.env` file:
  ```bash
  export BRAVE_SEARCH_API_KEY="your_brave_key"
  export OPENAI_API_KEY="your_openai_key"
  ```
</details>

---

### <a id="why-are-changes-to-memory-not-immediately-visible-in-the-dashboard"></a>Why are changes to memory not immediately visible in the dashboard?

If newly recorded decisions do not appear on the web UI immediately, it is typically due to browser caching or project mismatch in the dashboard header.

<details>
<summary>🔍 <b>Expand full answer</b></summary>
<br>

Resolution steps:
1. **Hard Refresh:** Press `Ctrl+Shift+R` (Windows/Linux) or `Cmd+Shift+R` (Mac) to bypass stale browser cache.
2. **Verify Active Project:** Check the project dropdown in the top-right header and ensure the correct project is active.
3. **Check Server WebSocket Telemetry:** Ensure the backend server is running and transmitting telemetry events.
</details>

---

### <a id="what-should-i-do-if-an-mcp-client-claude-cursor-devin-zed-cannot-connect-to-tropelex"></a>What should I do if an MCP client (Claude, Cursor, Devin, Zed) cannot connect to Tropelex?

If your MCP client reports that the Tropelex server is unreachable or tools are missing:

<details>
<summary>🔍 <b>Expand full answer</b></summary>
<br>

1. **Verify Server is Running:** Confirm `http://127.0.0.1:8766/api/health` returns `{"status": "ok"}`.
2. **Verify Python Path in MCP Config:** Ensure the `command` in `.mcp.json` points to the correct virtualenv or system `python3` binary with Tropelex dependencies installed.
3. **Test MCP Server Directly:**
   ```bash
   python3 -m mcp_server.server
   ```
   The process should start in stdio mode without throwing ImportError or syntax errors.
</details>

---

### <a id="why-is-the-opencode-plugin-not-registering-tropelex--slash-commands"></a>Why is the OpenCode plugin not registering `/tropelex-*` slash commands?

If `/tropelex-*` commands do not autocomplete in OpenCode:

<details>
<summary>🔍 <b>Expand full answer</b></summary>
<br>

1. **Confirm Plugin Installation:** Ensure `plugins/tropelex.js` is copied to your OpenCode plugins directory:
   ```bash
   cp plugins/tropelex.js ~/.config/opencode/plugins/tropelex.js
   ```
2. **Check `opencode.json`:** Confirm `"tropelex"` is listed in the `"plugin"` array inside `~/.config/opencode/opencode.json`.
3. **Restart OpenCode:** Fully restart your OpenCode session to reload plugins.
</details>

---

### <a id="how-do-i-diagnose-and-fix-a-corrupted-or-malformed-memoryprojectjson-file"></a>How do I diagnose and fix a corrupted or malformed `memory/<project>.json` file?

If a memory JSON file becomes corrupted due to an interrupted write or manual edit error:

<details>
<summary>🔍 <b>Expand full answer</b></summary>
<br>

1. **Validate JSON Syntax:**
   ```bash
   python3 -m json.tool memory/<project>.json > /dev/null
   ```
2. **Restore from Snapshot:** Check `memory/snapshots/` for the most recent session backup.
3. **Check Soft-Delete Trash:** If the file was inadvertently deleted, check `memory/.trash/<project>.json`.
4. **Repair Hashes:** If the file is valid JSON but fails integrity checks, run the hash backfill endpoint:
   ```bash
   curl -X POST http://localhost:8766/api/memory/<project>/security/backfill-hashes
   ```
</details>

---

### <a id="how-do-i-run-the-automated-pytest-suite-to-verify-system-health"></a>How do I run the automated Pytest suite to verify system health?

Per the Tropelex testing mandate, run `pytest` directly in your Linux/WSL terminal:

```bash
pytest tests/ -x -q
```

<details>
<summary>🔍 <b>Expand full answer</b></summary>
<br>

All unit tests must pass before declaring features or bug fixes complete. Note: Last30Days engine tests consume external API tokens and are excluded by default; to run them explicitly, run `pytest -m last30days`.
</details>

---

### <a id="what-do-the-different-http-status-codes-mean-in-tropelex"></a>What do the different HTTP status codes mean in Tropelex?

Tropelex follows standard REST API conventions with predictable HTTP status codes for success, client errors, security gating, and server anomalies:

<details>
<summary>🔍 <b>Expand full answer</b></summary>
<br>

| Status Code | Meaning | Primary Trigger in Tropelex |
| :--- | :--- | :--- |
| **`200 OK`** | Success | Request succeeded and payload returned. |
| **`302 Found`** | Redirect | Automatic redirect (e.g. root `/` routing to dashboard). |
| **`400 Bad Request`** | Malformed Request | Missing required payload parameters or invalid timeline filters. |
| **`401 Unauthorized`** | Authentication Required | Endpoint requires an API token or security key. |
| **`403 Forbidden`** | Action Blocked | Pre-Write Safety Guard violation or Safety Budget exhausted. |
| **`404 Not Found`** | Resource Missing | Project container, Decision ID, Session ID, or Feed ID not found. |
| **`409 Conflict`** | State Conflict | Project already exists or SHA-256 hash chain mismatch. |
| **`422 Unprocessable Entity`** | Schema Validation Failure | Pydantic model validation error (invalid types, missing nested keys). |
| **`429 Too Many Requests`** | Rate Limit Exceeded | Agent hourly mutation cap hit or search provider rate limit. |
| **`500 Internal Error`** | Server Exception | Unhandled Python exception or corrupted disk JSON file. |
| **`503 Service Unavailable`** | Service Degraded | External search provider down or background worker initializing. |
</details>

---

### <a id="http-400-bad-request--root-causes--solutions"></a>HTTP 400 Bad Request — Root Causes & Solutions

An `HTTP 400 Bad Request` indicates that the request syntax or payload structure was invalid.

<details>
<summary>🔍 <b>Expand full answer</b></summary>
<br>

**Common Triggers:**
* Sending empty or whitespace-only decision text in `POST /api/memory/{project}/decisions`.
* Providing an invalid ISO 8601 timestamp range for timeline queries.
* Submitting malformed citation promotion requests missing required `citation_id` or `target_project`.

**How to Fix:**
1. Inspect the JSON error response: `{"detail": "<specific validation error>"}`.
2. Ensure `Content-Type: application/json` is sent in the request header.
3. Validate that required string fields contain at least 1 non-whitespace character.
</details>

---

### <a id="http-401-unauthorized--403-forbidden--security-gates--safety-budgets"></a>HTTP 401 Unauthorized & 403 Forbidden — Security Gates & Safety Budgets

`HTTP 401` occurs when credentials are missing. `HTTP 403` occurs when credentials are valid, but the action is blocked by governance rules or safety limits.

<details>
<summary>🔍 <b>Expand full answer</b></summary>
<br>

**Common Triggers for 401 Unauthorized:**
* Attempting to call protected management endpoints without a bearer token when authentication is active.

**Common Triggers for 403 Forbidden:**
* **Pre-Write Safety Violation:** Proposed diff or action triggers a high-severity security rule.
* **Safety Budget Exhaustion:** An automated agent exceeded its hourly decision creation quota (see `Agent Safety Budget`).
* **Locked Decision Mutation:** Attempting to modify or delete a pinned/attested decision without explicit tech lead attestation.

**How to Fix:**
* If blocked by a safety budget, approve the pending action in the **Needs Attention** dashboard queue or escalate via `POST /api/memory/{project}/agents/{agent}/safety-budget/escalate`.
* If authentication failed, ensure your client passes the configured API key header.
</details>

---

### <a id="http-404-not-found--missing-projects-decisions--feeds"></a>HTTP 404 Not Found — Missing Projects, Decisions & Feeds

An `HTTP 404 Not Found` indicates that the server cannot locate the requested project, decision, session, or research feed.

<details>
<summary>🔍 <b>Expand full answer</b></summary>
<br>

**Common Triggers:**
* `GET /api/memory/MyProject`: The file `memory/MyProject.json` does not exist.
* `PATCH .../decisions/dec-999/context`: Decision `dec-999` does not exist in the specified project.
* `GET /api/research-feeds/feed-123`: The feed ID is invalid or was deleted.

**How to Fix:**
1. Check the list of active projects via `GET /api/projects`.
2. If the project was recently deleted, restore it from `memory/.trash/<project>.json`.
3. Check decision IDs using `GET /api/memory/{project}` before executing `PATCH` or `DELETE` requests.
</details>

---

### <a id="http-409-conflict--name-collisions--integrity-hash-conflicts"></a>HTTP 409 Conflict — Name Collisions & Integrity Hash Conflicts

An `HTTP 409 Conflict` occurs when a request attempts to create a duplicate entity or creates a cryptographic integrity discrepancy.

<details>
<summary>🔍 <b>Expand full answer</b></summary>
<br>

**Common Triggers:**
* **Duplicate Project:** Calling `POST /api/memory` with a project name that already exists.
* **Hash Chain Conflict:** Direct manual edits to `memory/<project>.json` that broke SHA-256 `prev_hash` links.
* **Session Rollback Collision:** Attempting to rollback a session that was already reverted.

**How to Fix:**
* For duplicate project names, choose a unique project identifier.
* For hash conflicts, run the automatic repair endpoint:
  ```bash
  curl -X POST http://localhost:8766/api/memory/<project>/security/backfill-hashes
  ```
</details>

---

### <a id="http-422-unprocessable-entity--schema--payload-validation-failures"></a>HTTP 422 Unprocessable Entity — Schema & Payload Validation Failures

An `HTTP 422 Unprocessable Entity` is returned by FastAPI when request payload fields fail Pydantic model validation.

<details>
<summary>🔍 <b>Expand full answer</b></summary>
<br>

**Common Triggers:**
* Sending a string where an integer is expected (e.g., `"limit": "ten"` instead of `"limit": 10`).
* Missing a required field in nested objects (e.g. omitting `"status"` in goal updates).
* Submitting confidence threshold values outside the valid `0.0` to `1.0` range.

**How to Fix:**
Inspect the FastAPI validation error payload:
```json
{
  "detail": [
    {
      "loc": ["body", "confidence"],
      "msg": "Input should be less than or equal to 1.0",
      "type": "less_than_equal"
    }
  ]
}
```
Update your client request payload to match the OpenAPI specification at `/openapi.json`.
</details>

---

### <a id="http-429-too-many-requests--agent-mutation-rates--provider-throttling"></a>HTTP 429 Too Many Requests — Agent Mutation Rates & Provider Throttling

An `HTTP 429 Too Many Requests` indicates that request frequency has exceeded allowable thresholds.

<details>
<summary>🔍 <b>Expand full answer</b></summary>
<br>

**Common Triggers:**
* **Agent Mutation Cap:** An agent in an infinite coding loop dispatched too many decision requests in a 60-second window.
* **Search Engine Rate Limit:** Brave Search or Exa API returned 429 due to query quota limits.

**How to Fix:**
1. For agent limits: Throttle agent execution rate or increase the agent's hourly budget in `Agent Safety Budget`.
2. For research limits: Tropelex automatically falls back to DuckDuckGo when primary search keys encounter 429 errors.
</details>

---

### <a id="http-500-internal-server-error--503-service-unavailable--server--provider-failures"></a>HTTP 500 Internal Server Error & 503 Service Unavailable — Server & Provider Failures

`HTTP 500` indicates an unexpected internal server crash. `HTTP 503` indicates a temporary downstream service outage.

<details>
<summary>🔍 <b>Expand full answer</b></summary>
<br>

**Common Triggers for 500:**
* Corrupted JSON syntax on disk in `memory/<project>.json`.
* Disk full or file lock contention during high-concurrency writes.

**Common Triggers for 503:**
* Background scheduler initializing or stopped.
* All web search providers (Brave, Exa, Serper, DuckDuckGo) unreachable due to network outage.

**How to Fix:**
1. Check the server console log output for python tracebacks.
2. Validate JSON files with `python3 -m json.tool memory/<project>.json`.
3. Check internet connectivity if running deep research queries.
</details>

---

### <a id="system--os-error-codes-errno-98-errno-13-errno-2--cli-exit-codes"></a>System & OS Error Codes (Errno 98, Errno 13, Errno 2) & CLI Exit Codes

When running Tropelex from the command line, POSIX OS error numbers and CLI return codes communicate underlying runtime conditions:

<details>
<summary>🔍 <b>Expand full answer</b></summary>
<br>

#### Operating System Error Codes
* **`[Errno 98] Address already in use` (EADDRINUSE):** Another process is listening on port `8766`. Kill existing PID via `kill -9 $(pgrep -f "core.tropebook.web.server")`.
* **`[Errno 13] Permission denied` (EACCES):** Current user lacks read/write permissions for `memory/` or static UI directories. Run `chmod -R u+rw memory/`.
* **`[Errno 2] No such file or directory` (ENOENT):** Required folder `memory/` does not exist. Run `mkdir -p memory/snapshots memory/tropebook memory/.trash`.

#### CLI & Pytest Exit Codes
* **Exit Code `0`:** Clean termination / all Pytest tests passed.
* **Exit Code `1`:** One or more Pytest tests failed, or fatal CLI argument error.
* **Exit Code `2`:** Process interrupted by user (`SIGINT` / `Ctrl+C`).
* **Exit Code `4`:** Pytest command-line usage syntax error.
* **Exit Code `5`:** No tests were collected by Pytest.
</details>

---

## Need Further Help?
Launch the interactive web dashboard at `http://localhost:8766` and click **Documentation** or **API Reference** for live endpoint testing and one-click CLI command copiers.
