# Multi-Guardian Composition Checklist

Use this checklist whenever you add a guardian, add a second guardian, or ship an orchestrator change that affects coordination.

## Determinism
- [ ] Network-free behavior verified (no implicit calls)
- [ ] Read-only contract verified (no writes to repo or system)
- [ ] Canonical JSON output verified (stable sorting, deterministic serialization)
- [ ] Clean-room venv run matches documented output

## Failure Modes
- [ ] Missing guardian dependency triggers fail-closed with explicit details (e.g., guardian_import_failed)
- [ ] Guardian internal evaluation uncertainty triggers fail-closed at guardian level
- [ ] Wrapper execution failures are distinguishable from guardian policy failures

## Semantics
- [ ] Execution plane (wrapper ok/fail_closed) is not interpreted as policy approval
- [ ] Policy plane is computed from guardian outcomes (ok/fail_closed)
- [ ] Consumer aggregation rules are stated and stable (see MULTI_GUARDIAN_STRATEGY.md)

## Independence
- [ ] Multiple guardians can run in one orchestrator invocation without cross-contamination
- [ ] One failing guardian does not suppress other guardian outputs
- [ ] Aggregation result is deterministic regardless of guardian ordering (unless explicitly ordered by contract)

## Evidence & Docs
- [ ] docs/EXAMPLE_OUTPUTS.md includes at least one real deterministic JSON capture for the new composition
- [ ] Any prerequisite (e.g., install guardian package) is explicitly stated near the example output
- [ ] If semantics are ambiguous, an issue is opened and pinned before changes are proposed
