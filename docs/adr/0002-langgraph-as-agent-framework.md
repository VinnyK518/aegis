# 0002 – LangGraph as agent framework

- Status: Accepted
- Date: 2026-11-21

## Context

The two candidates were LangGraph and Google's Agent Development Kit (ADK). ADK comes with evaluation and deployment tooling and was originally attractive as a signal for a specific employer. The deciding criterion became general relevance on the job market rather than a single company.

With multi-agent orchestration out of scope, the agent is a single graph, so the frameworks' differences in multi-agent support matter little here.

## Decision

The agent is built with LangGraph. Claude is the default model. The eval harness does not depend on LangGraph and talks to the agent through a narrow interface.

## Consequences

- LangGraph is widely used in production and in job requirements.
- The agent stays model-agnostic, which keeps a later model comparison cheap.
- Tracing to Langfuse uses its LangChain/LangGraph integration.
- Because the harness is framework-independent, a framework switch or a comparison against a plain agent loop on the Claude API remains possible without rebuilding the evals.
