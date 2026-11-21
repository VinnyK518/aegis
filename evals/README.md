# evals

The eval harness. It runs the agent against the scenarios in `../scenarios`, compares the output with the ground truth and reports triage accuracy, root-cause accuracy, hallucination rate, latency and cost per incident.

The harness does not depend on LangGraph. Results are versioned so changes can be compared over time.
