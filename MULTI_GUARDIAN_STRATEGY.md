# Multi-Guardian Orchestration Strategy (Portfolio-Level)

## Scope

This document defines a portfolio-level strategy for coordinating multiple governance guardians under a deterministic orchestrator.

It is written to be:
- deterministic (no ambiguity in terms)
- composable (works across many MCPs)
- contract-safe (V1 frozen semantics; V2 changes explicitly versioned)

This strategy intentionally distinguishes three planes:
- Execution
- Policy
- Safety posture (fail-closed)

Do not conflate them.

---

## The Three Planes

### Plane A — Execution (Orchestrator wrapper)
Question: did the orchestrator run deterministically and produce an output object?

This plane answers operational questions:
- did the run complete?
- did it remain network-free/read-only as promised?
- did it emit a canonical output artifact?

Execution semantics MUST NOT be interpreted as policy approval.

### Plane B — Policy (Guardian outcomes)
Question: do the guardians approve the target with ok == true?

This plane is authoritative for compliance / gating decisions.

Policy success is computed from guardian results, not from orchestrator wrapper ok.

### Plane C — Safety posture (Fail-closed)
Question: when a guardian cannot evaluate reliably, do we stop the world?

Fail-closed means:
- uncertainty results in a failing outcome (not a permissive outcome)
- downstream automation should treat fail-closed as a hard stop

Fail-closed posture is authoritative at the guardian level for policy decisions.

---

## Canonical Consumer-Side Aggregation (V1)

Assume the orchestrator emits:
- wrapper fields: ok, fail_closed
- guardian list entries with: ok, fail_closed, invoked, details, output

Define the following derived values for consumers (CI/CD, agents, humans):

- execution_ok = orchestrator.ok
- execution_fail_closed = orchestrator.fail_closed

- policy_ok = ALL(guardian.ok == true) across invoked guardians
- policy_fail_closed = ANY(guardian.fail_closed == true) across invoked guardians

---

## Tier 2 Proof (Reference Evidence)

Authoritative reference implementation: mcp-governance-orchestrator (tag v0.2.5).

Evidence:
- Tier 2 two-guardian composition proof captured in docs/EXAMPLE_OUTPUTS.md
- Clean-room reproducibility verified; canonical JSON output confirmed byte-identical across runs
- No schema changes; no behavioral changes; V1 contract remains frozen

This milestone demonstrates composable governance under deterministic aggregation using the consumer-side formulas above.


Important:
- orchestrator.ok MUST NOT be treated as policy_ok
- orchestrator.fail_closed MUST NOT be treated as policy_fail_closed unless the orchestrator itself cannot operate deterministically

If a guardian is not invoked due to import failure:
- treat policy_ok as false
- treat policy_fail_closed as true
- capture evidence in details (e.g., guardian_import_failed)

---

## Guardian ID and Versioning Convention

Guardian IDs should be stable and explicit:
- name:v1 indicates a contract-stable output surface and stable interpretation semantics
- name:v2 indicates an intentional breaking/expanding change with migration notes

Meaning of "v1":
- deterministic output shape
- documented semantics
- reproducible E2E
- no silent drift

---

## Maturity Tiers (Lightweight Governance)

Tier 0:
- deterministic, read-only, network-free, fail-closed

Tier 1:
- Tier 0 + documented V1 contract + reproducible E2E example output

Tier 2:
- Tier 1 + multi-guardian composition checklist satisfied + documented aggregation semantics

Tier 3:
- Tier 2 + release-gating integration guidance + versioned change-control playbook

Portfolio goal:
- every guardian reaches Tier 1
- the orchestrator + representative guardian sets reach Tier 2

---

## Composition Invariants (What Must Always Hold)

1) Determinism:
- identical inputs produce identical canonical JSON output

2) Independence:
- a failing guardian must not corrupt other guardians' outputs

3) Fail-closed integrity:
- inability to evaluate reliably results in failing outcomes with explicit details

4) Semantics stability:
- execution semantics and policy semantics are never conflated
- consumer-side aggregation rules remain stable within a major version

---

## V2 Change Policy (If Behavior Must Change)

If a behavior change is desired (e.g., wrapper ok reflecting policy_ok):
- propose it as V2
- publish migration notes
- provide dual interpretation guidance during transition
- do not silently change semantics under a V1 label
