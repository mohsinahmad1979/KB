Based on Marina Wyss's guide *"How to Build Production AI Agents on Google Cloud"*, the core **theoretical concepts** focus on moving beyond basic LLM prototypes ("model + tools") to build reliable, enterprise-ready systems.

Here are the primary theoretical concepts extracted from the article:

### 1. Ephemeral vs. Persistent State (Session Memory vs. Long-Term Memory)

- **Session Context (Ephemeral):** Temporary state bound to a single continuous interaction. It holds immediate conversational history, but resets when a new session starts.
- **Long-Term Memory (Persistent):** Cross-conversational state that survives session boundaries. It requires a structured extraction mechanism to distill permanent facts/preferences (e.g., "preferred contact method") from transient dialogue and store them in a durable memory bank for future retrieval.

### 2. Defense-in-Depth & Non-Deterministic Security

- **Deterministic vs. Probabilistic Controls:** Large Language Models are inherently probabilistic—you cannot guarantee compliance solely through natural language instructions (e.g., instructing an LLM "Never show User B's data").
- **Code-Enforced Authorization:** Security boundaries and access checks (such as tenant isolation or ownership checks) must be enforced deterministically inside application code (the tool layer) rather than delegated to the LLM's system prompt.
- **Boundary Filtering (Gateway & Armor):** Enterprise agent security requires layered defensive perimeters—network filtering (Agent Gateway) to restrict communication targets, and content inspection (Model Armor) to detect prompt injections and prevent data exfiltration (PII leaks).

### 3. Identity and Least-Privilege Execution (IAM)

- **Agent Identity:** Treating an autonomous AI agent as an independent security principal (service account) rather than using shared master API keys or user credentials.
- **Principle of Least Privilege:** Restricting an agent's runtime capabilities via fine-grained infrastructure-as-code (Terraform) to only the explicit operations required for its task (e.g., invoking a model, writing logs, executing specific database reads), preventing system-wide compromise if the agent is hijacked.

### 4. Continuous Evaluation & Regression Testing (Evals)

- **Deterministic Test Suites for Non-Deterministic Models:** Because LLM outputs fluctuate, quality assurance relies on structured evaluation sets ("golden datasets") featuring known inputs, missing-data scenarios, and boundary conditions.
- **Automated Scoring:** Running automated test suites before and after code or prompt modifications to detect accuracy regressions or hallucinated responses before deployment to end users.

### 5. Distributed Observability & Root-Cause Tracing

- **Execution Waterfall (Tracing):** Multi-step agent workflows (LLM call → tool execution → context retrieval → response generation) introduce multiple failure points and latency bottlenecks.
- **Step-Level Attribution:** Distributed tracing (e.g., Cloud Trace) isolates whether an incorrect final answer stems from model reasoning failure, stale context returned by a tool, or API performance latency.

### 6. Context Engineering & Tool Abstraction

- **Context Quality:** An agent's operational capability is strictly bounded by the quality and freshness of information injected into its context window (e.g., ensuring retrieval tools pull active policies rather than deprecated documents).
- **Tool Contract Design:** Structuring functions so that the LLM acts purely as a decision-maker (choosing parameters) while the tool executes business logic and data validation safely behind a fixed interface.