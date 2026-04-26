# ReAct (Reason + Act) Loop Architecture

**Tags:** #ai #systems-architecture #python #llm #agentic
**Linked Nodes:** [[Zero-Fail-Debugging]], [[Pandas-Data-Sanitization]]

## The ReAct Paradigm
The ReAct loop is the core orchestration engine of an autonomous AI agent. It forces a Large Language Model (LLM) to slow down, plan its execution and rely on external deterministic tools rather than its own internal hallucinated knowledge.

## The Tri-Node Cycle
An effective inference engine runs on a strict cycle:
1. **Thought:** The model analyzes the user prompt and determines the logical next step.
2. **Action:** The model outputs a strict string (e.g., `Action: check_prereq[CS101]`) requesting a tool execution.
3. **Observation:** The Python backend intercepts the LLM, pauses inference, runs the actual deterministic code and feeds the factual result back into the context window.

## Engineering the Engine
To build a zero-failure engine, you must bridge the probabilistic LLM with deterministic Python. Use strict Regular Expressions (Regex) to parse the `Action` output to prevent parameters from being hallucinated and crashing the local tool registry.
