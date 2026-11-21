# 0001 – Restart from scratch

- Status: Accepted
- Date: 2026-09-16

## Context

A first attempt started in July 2026: a repository, local tooling and a half-finished Hetzner setup. Work stopped in the middle of a setup step and was not fully documented. By September the state was ten weeks old and could not be explained without reconstructing it first.

## Decision

Aegis starts over with a new repository and a new cluster. Nothing from the first attempt is reused or merged. The old repository is archived as a private repository. The project goal, the glossary and the success criteria carry over: thinking is kept, infrastructure is not.

The scope is cut to infrastructure, a single agent, the eval pipeline and a published README. Multi-agent orchestration and production hardening are dropped for now.

## Consequences

- The repository history starts clean and every setup step is reproducible from it.
- A few hours of earlier setup work are redone.
- The reduced scope makes the eval pipeline the clear centre of the project.
