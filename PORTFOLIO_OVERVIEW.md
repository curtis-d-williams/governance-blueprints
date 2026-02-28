# Deterministic Governance Infrastructure — Portfolio Overview

## Executive Summary

This portfolio demonstrates a deterministic, composable governance primitive for MCP-based systems.

The core objective is not feature expansion.
The objective is verifiable, reproducible, fail-closed automation with explicit semantic boundaries.

All components operate under frozen V1 contracts unless explicitly versioned otherwise.

---

## Architectural Thesis

Modern automation systems frequently conflate:
- execution success
- policy approval
- safety posture

This portfolio separates those concerns into explicit planes:

1. Execution — Did the orchestrator run deterministically?
2. Policy — Do guardians approve (ok == true)?
3. Safety posture — Did any guardian fail-closed?

Aggregation is deterministic and documented.
Consumer-side formulas are explicit and version-stable.

---

## Core Components

### 1. mcp-governance-orchestrator

Implements:
- Deterministic multi-guardian coordination
- Canonical JSON output (stable ordering, no timestamps)
- Explicit separation of execution vs policy semantics
- Documented aggregation formulas
- Clean-room reproducibility validation

Status:
- V1 schema frozen
- Tier 2 deterministic composition proof complete (v0.2.5)

Repository:
https://github.com/curtis-d-williams/mcp-governance-orchestrator

---

### 2. mcp-release-guardian

Implements:
- Release-safety validation
- Fail-closed policy posture
- Deterministic evaluation surface

Status:
- Tier 1 contract stable
- Participated in Tier 2 proof

---

### 3. mcp-repo-sanity-guardian

Implements:
- Minimal deterministic, read-only guardian
- No network calls
- Fail-closed evaluation

Status:
- V1 contract stable
- Used in Tier 2 deterministic composition proof
- Public reference implementation
- Not published to PyPI (reference-grade)

Repository:
https://github.com/curtis-d-williams/mcp-repo-sanity-guardian

---

## Maturity Model

Tier 0:
Deterministic, read-only, network-free, fail-closed.

Tier 1:
Tier 0 + documented V1 contract + reproducible E2E output example.

Tier 2:
Tier 1 + multi-guardian composition proof + documented aggregation semantics.

Tier 3:
Tier 2 + formal release-gating operationalization + evidence retention + explicit change-control playbook.

Current portfolio status:
- Orchestrator + guardians: Tier 2 proven
- Governance doctrine: Tier 3 operational guidance defined

---

## Determinism Guarantees

The system enforces:

- Canonical JSON output
- Stable key ordering
- No timestamps or nondeterministic fields
- Byte-identical reproducibility across clean-room runs
- Fail-closed posture on evaluation uncertainty
- No silent schema drift under V1

Any change to:
- output schema
- aggregation semantics
- determinism guarantees

requires V2 designation and explicit migration notes.

---

## Intended Use

This infrastructure is designed to:

- Provide reproducible release gating
- Serve as governance primitives for AI-driven automation
- Enable composable guardian architectures
- Support portfolio-level policy enforcement

It is not:
- a feature product
- an opinionated CI/CD framework
- an anti-automation ideology

It is structured automation with explicit contracts.

---

## Design Constraints

- No behavioral expansion under v0.x without migration notes
- No schema mutation under V1
- Aggregation semantics remain stable within major versions
- Determinism is non-negotiable

---

## Strategic Position

This portfolio establishes:

- A deterministic governance primitive
- A composable multi-guardian architecture
- A documented maturity ladder
- A reproducible release-gating model

It is infrastructure, not experimentation.

