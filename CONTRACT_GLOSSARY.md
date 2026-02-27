# Contract Glossary

This glossary defines canonical meanings for recurring terms across MCP governance repos.

Execution success:
- The orchestrator ran deterministically and produced an output object.

Policy success:
- All invoked guardians approved the target (ok == true for each).

Fail-closed:
- On uncertainty or inability to evaluate reliably, the system returns a failing outcome rather than a permissive one.

Deterministic:
- Given the same inputs and environment constraints, output is identical (canonical JSON).

Auditable:
- Outputs, semantics, and change history are inspectable and traceable.

Composable:
- Multiple guardians can be coordinated without semantic ambiguity or interference.

Contract-frozen (V1):
- Output semantics and structure are stable; changes require explicit versioning and migration policy.
