# Level 3 Submission - Aditi Mehta

### Agent Description
Instead of a basic chatbot, I built the **SMILE Gap Analyzer (The Critic Agent)**. It acts as a Senior Architect that audits a user's digital twin concept against the SMILE framework to find physical, human, and architectural blind spots. I chose to build this using raw Python to understand MCP communication under the hood. I built a **stateless IPC bridge** using `subprocess.communicate()` to handle tool calls, which solved the `BrokenPipeError` and terminal freezing issues found in persistent streams.

### LPI Tools Referenced
1. `smile_overview` — Audits high-level architecture phases.
2. `query_knowledge` — Retrieves domain-specific constraints.
3. `get_case_studies` — Finds real-world failure risks and metrics.
4. `smile_phase_detail` — Deep-dives into implementation gaps.

### Setup Instructions
You'll need Ollama (running `qwen2.5:1.5b`) and the LPI MCP Server built and ready.

1. **Clone it:** `git clone https://github.com/Dynamic-ctrl/lpi-smile-agent`
2. **Setup Path:** Update `LPI_SERVER_PATH` in `agent.py` to point to your local `index.js`.
3. **Run a query:** `python3 agent.py "I want to build a digital twin of a smart grid"`

### Explainability Evidence
Explainability is a core requirement of this agent. It uses **Few-Shot Template Forcing** to ensure the LLM justifies every critique with retrieved LPI data. It doesn't just give advice; it explains the "Why" behind every recommendation.

**Actual Agent Output Evidence:**
> `[SOURCE: LPI/get_case_studies] Critique: You must implement a dedicated backup power supply for your sensors.`
> `Why I recommend this: According to the case studies tool, historical data shows that power outages frequently lead to sensor calibration loss. This evidence-based recommendation mitigates a specific real-world failure risk.`

The agent also prints a **Provenance Log** tracing every decision to its source:
```text
PROVENANCE - Every critique traced to its LPI source:
[1] Tool: smile_overview     -> Sourced baseline safety hazards.
[2] Tool: query_knowledge    -> Sourced manual override constraints.
[3] Tool: get_case_studies   -> Sourced past failure metrics.
[4] Tool: smile_phase_detail -> Sourced sensor implementation gaps.
```

### Security Awareness
I implemented a **regex-based sanitization layer** that sanitizes the terminal input for special characters and command injections before the data ever goes to the LLM or the MCP server. Additionally, **stateless subprocess bridge** provides a security boundary; because each tool call is a fresh process, it prevents memory leaks or state-injection attacks that can stop persistent `stdio` streams.