# MCP Factory Specification (V1)

Status: Governance-plane doctrine  
Scope: Deterministic guardian scaffolding for Tier 1 eligibility  
Version discipline: Immutable under V1 unless explicitly versioned

---

## 1. Purpose

Define the minimum deterministic structure required for a new MCP guardian
to qualify for Tier 1 under the governance model.

This specification enables safe, repeatable guardian creation by automated
executors (e.g., Claude Code) while preserving governance authority.

This document governs structure — not features.

---

## 2. Required Structural Elements (Tier 1 Eligible Guardian)

A guardian MUST satisfy all of the following:

### 2.1 Determinism

- Canonical JSON output (`json.dumps(..., sort_keys=True, separators=(",", ":"), ensure_ascii=False)`)
- No timestamps
- No randomness
- No network calls
- No nondeterministic filesystem traversal
- Stable ordering of checks

### 2.2 Fail-Closed Behavior

- `fail_closed = true` only on execution/internal error
- Policy failure MUST NOT be conflated with execution failure
- Unknown configuration MUST fail-closed

### 2.3 Output Contract (V1)

Top-level fields:

- guardian (string, versioned identifier)
- ok (bool)
- fail_closed (bool)
- checks (array)
- optional error (object; only when fail_closed=true)

No additional top-level fields permitted under V1.

### 2.4 Read-Only Operation

- No mutation of repository
- No writes
- No external state modification

### 2.5 Example Output

Repository MUST include:

- Deterministic example JSON
- Captured from real run
- Byte-identical reproducibility verified

### 2.6 Explicit Contract Freeze Section

README MUST include:

- V1 contract freeze declaration
- No schema expansion under v0.x
- Clear V2 migration rule

### 2.7 Pinned "Start Here" Issue

Repository MUST contain:

- A pinned issue explaining scope and non-goals
- Explicit Tier level declaration

---

## 3. Orchestrator Integration Protocol

Guardian is not considered composable until:

1. Guardian is installed
2. Guardian is added to GUARDIAN_ROUTING_TABLE
3. Deterministic Tier 2 composition output is captured
4. Documentation updated with canonical JSON + SHA256

Routing table modification is a code change and MUST be versioned.

---

## 4. Tier Qualification Model

Tier 0 — Concept  
Tier 1 — Deterministic standalone guardian  
Tier 2 — Composable deterministic orchestration proof  
Tier 3 — Operational release gating

Promotion between tiers MUST be documented and version-tagged.

---

## 5. Change Control Doctrine

Under V1:

- No schema changes
- No output field additions
- No aggregation changes
- No nondeterminism introduction

Any of the above requires:

- V2 designation
- Migration notes
- Explicit diff documentation

---

## 6. Executor Boundary (Claude Code Role)

Executor MAY:

- Scaffold guardian structure
- Implement deterministic checks
- Produce example output
- Prepare documentation drafts

Executor MAY NOT:

- Change schema
- Modify orchestrator aggregation
- Declare tier promotion
- Override governance freeze

Governance authority remains human-controlled.

---

## 7. Non-Goals

This specification does NOT define:

- Feature roadmap
- Business positioning
- Vulnerability scanning
- External compliance standards

It defines deterministic governance structure only.

---

End of Specification (V1)
