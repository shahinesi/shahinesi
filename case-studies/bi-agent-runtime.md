# BI Agent Runtime

> Architecture case study. The production repository is private; this document intentionally excludes confidential data, credentials, and client-specific implementation details.

## Problem

Traditional dashboards answer predefined questions. Business teams increasingly need to ask natural-language questions, resolve ambiguous terminology, explore governed metrics, and receive answers that are supported by traceable evidence rather than plausible text.

## Solution direction

A **definition-driven BI Agent runtime** that treats analytics as a controlled decision process instead of a single LLM prompt.

```mermaid
flowchart LR
    A[User question] --> B[Perception]
    B --> C[Goal & understanding]
    C --> D[Semantic resolution]
    D --> E[Planning]
    E --> F[Tool execution]
    F --> G[Evidence collection]
    G --> H[Evidence evaluation]
    H --> I[Decision]
    I --> J[Response composition]
```

## Core capabilities

- Cognitive states for perception, goal formation, understanding, memory recall, planning, execution, evidence collection, evaluation, reflection, decision, and response composition
- Governed metric and dimension resolution through a semantic catalog and Cube schema alignment
- Tool registry with explicit input/output contracts
- Session memory and retrieval policies that avoid uncontrolled context growth
- Guardrails, audit events, and evidence-backed verification
- Advisory reflection; a dedicated decision state owns transitions
- Manual approval gates after major phases for high-risk changes
- Three-strike circuit breaker to stop repeated autonomous failure loops

## Stack

`LangGraph` · `Cube` · `NestJS` · `Next.js` · `PostgreSQL` · `Vercel AI SDK`

## Engineering principles

1. The semantic layer is the source of truth for analytical meaning.
2. Every material answer should be tied to executed tools and returned evidence.
3. Reflection may advise, but it cannot silently change state transitions.
4. Agent behavior is definition-driven and testable rather than hidden inside prompts.
5. Risky phases stop for validation instead of optimizing purely for autonomy.
