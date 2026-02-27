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
