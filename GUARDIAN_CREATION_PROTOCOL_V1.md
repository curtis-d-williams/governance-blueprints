# Guardian Creation Protocol (V1)

Purpose: deterministically produce Tier 1 guardians using Claude Code with minimal human oversight and no drift.

Status: V1 frozen.

This protocol is the canonical factory procedure.

---

## Inputs

- Template repo: mcp-guardian-template (tag v0.1.0)
- Tier 1 eligibility rules: MCP_FACTORY_SPEC_V1.md (tag v0.1.0)

---

## Hard Rules (Immutable Under V1)

A Tier 1 guardian MUST:

- Expose exactly one tool
- Be deterministic (no timestamps, randomness, environment-derived metadata)
- Be network-free
- Be read-only (no disk writes, no repo mutation)
- Fail-closed on invalid input or internal error
- Produce stable output schema keys and types
- Provide canonical example output (byte-identical under deterministic JSON serialization)
- Provide deterministic tests that fail if nondeterminism or schema drift is introduced

Any violation requires V2 designation in that guardian repo.

---

## Factory Procedure (Stepwise, Non-Skippable)

### Step 1 — Scaffold from template

- Start a new repo by cloning mcp-guardian-template at tag v0.1.0.
- Create a new package name and module path (no leftovers from template namespace).

Required updates:
- pyproject.toml: project.name, version, entrypoint module path
- src package directory name
- console script name
- FastMCP server name string

### Step 2 — Define the guardian tool contract

- Tool name: choose a stable name aligned to the guardian purpose.
- Inputs: keep minimal and deterministic.
- Output schema:
  - Must be a JSON object (dict)
  - Must include at least: tool, repo_path, ok, fail_closed
  - Any additional keys must be stable and justified by the guardian’s purpose
- Fail-closed:
  - On invalid inputs: ok=false, fail_closed=true, stable error code
  - On internal errors: ok=false, fail_closed=true, stable error code

### Step 3 — Implement deterministic checks only

Allowed:
- Pure reads of repository files
- Deterministic parsing
- Deterministic rule evaluation

Not allowed under V1:
- Network calls
- Time-based logic
- Randomness
- Writing to disk
- Executing repo code
- “Helpful” heuristics, scoring, ranking, or interpretation

### Step 4 — Freeze contract + examples

Must update:
- docs/V1_CONTRACT.md
- docs/EXAMPLE_OUTPUTS.md

EXAMPLE_OUTPUTS.md must contain:
- At least one canonical JSON output example for a stable input (e.g., repo_path=".")
- Canonical JSON must be stable and reproducible

### Step 5 — Determinism + schema guardrails

Must include tests that:
- Assert repeated calls produce identical canonical JSON
- Assert output schema keys are exactly the expected set
- Fail if any non-deterministic data appears

### Step 6 — Integrity verification (must pass)

- pytest -q
- python3 -m build --sdist --wheel

### Step 7 — Freeze milestone tag

Once stable:
- Tag v0.1.0 in the new guardian repo
- Push main and tags

---

## Drift Triggers (Stop Immediately)

If any proposal includes:
- Dynamic discovery
- Plugin registries
- Entry point scanning
- Schema normalization/harmonization
- Output interpretation or ranking
- Adding extra tools

Then stop and require:
- V2 designation
- Migration notes
- Version tag

---

## Output of This Protocol

A new guardian repo that is Tier 1 eligible and ready for orchestrator composition without additional governance negotiation.