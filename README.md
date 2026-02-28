# Governance Blueprints

This repository contains reusable, governance-grade patterns for building deterministic, auditable, composable MCP infrastructure.

Principles:
- Deterministic outputs (canonical JSON, stable sorting, reproducible runs)
- Auditable boundaries (explicit contracts, clear semantics)
- Composable guardians (multi-guardian orchestration with precise aggregation rules)
- Release-safe change control (V1 freeze, V2 proposals with migrations)

Non-goals:
- No product features live here
- No runtime dependencies required to read these docs
- This is not "anti-automation" — it is structured automation with verifiable boundaries

Start here:
- MULTI_GUARDIAN_STRATEGY.md
- COMPOSITION_CHECKLIST.md
- CONTRACT_GLOSSARY.md

---

## Reference Implementations

The following repositories apply the governance patterns defined here:

### mcp-governance-orchestrator
https://github.com/curtis-d-williams/mcp-governance-orchestrator

Implements:
- Deterministic guardian coordination
- Canonical JSON output
- Explicit execution vs policy semantics (see docs/SEMANTICS.md)
- Fail-closed behavior at guardian level
- Reproducible clean-room validation
- Versioned governance hardening (v0.2.5)
- Tier 2 deterministic multi-guardian composition proof documented in docs/EXAMPLE_OUTPUTS.md (byte-identical, clean-room reproducible)

This repository serves as a Tier 1+ reference for multi-guardian orchestration.

Additional guardians and MCP implementations will be listed here as they reach Tier 1 maturity.
