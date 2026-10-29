# Fabric DAX Analyzer

A planned Microsoft Fabric app for understanding DAX query performance: how much time is spent in the Storage Engine (SE) and Formula Engine (FE), where the bottlenecks are, and what changes could improve execution.

## Intended capabilities

- Inspect a DAX query alongside captured server timings and query-plan evidence.
- Compare overall duration, FE duration, SE duration, SE CPU, and SE request counts when supported by the capture source.
- Explore expensive SE requests, materialization, and FE-heavy execution patterns.
- Explain likely bottlenecks and suggest specific query or model changes, with evidence and confidence.
- Compare before-and-after runs while keeping cache state and execution context visible.

## Analysis principles

- DAX text alone cannot provide measured SE/FE timings. Real breakdowns require a supported trace or server-timings capture.
- Distinguish measured values from derived estimates and static-analysis suggestions. Missing timing data must remain unavailable, not zero.
- Do not sum overlapping SE requests or confuse SE CPU with elapsed time. Define the timing method and account for parallel execution.
- Do not claim exact DAX-line attribution unless the available execution evidence supports it.
- Validate optimization recommendations with repeatable before-and-after measurements and equivalent query results.
- Keep query text, model metadata, and traces private by default; never commit customer captures, credentials, or tokens.

## Initial implementation decisions

The application has not been implemented yet. First establish:

1. The Fabric integration surface and its authentication and permission requirements.
2. Which supported capture sources can supply server timings and query plans, including whether live capture is feasible in the chosen hosting environment.
3. An analysis data contract that preserves capture provenance, units, cache state, and execution context.
4. An initial workflow for inspecting a query, reviewing the SE/FE breakdown, investigating expensive operations, and comparing an optimization.

An offline import workflow is a possible starting point if live tracing is not available. Neither tracing access nor a particular Fabric extension capability is assumed.
