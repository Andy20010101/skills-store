# Agent Interface

This directory defines a machine-readable interface so the same supplier-discovery package can be used by different agents and hosts without rewriting the business contract.

## Required Exchange Surfaces

### 1. Request

The caller provides a `request.json` document validated by:
- [research-request.schema.json](research-request.schema.json)

This captures:
- product direction
- search phrases when available
- price / MOQ / region constraints
- operator notes
- output preferences

### 2. Capability Manifest

Each host or adapter provides a `capability-manifest.json` document validated by:
- [capability-manifest.schema.json](capability-manifest.schema.json)

This captures:
- adapter identity
- agent family
- validation status
- which authentication mode that validation status applies to
- capability booleans
- operation mappings from the host's native tools to the shared contract

### 3. Run Result

Each run should emit a `run-result.json` document validated by:
- [run-result.schema.json](run-result.schema.json)

This captures:
- run status
- whether evidence came from direct 1688 pages, mirror-assisted pages, or no usable pages
- which authentication mode the run actually used
- where the Markdown report lives
- supplier count
- blockers and limitations

## Recommended Intermediate Surfaces For Staged Runs

These are not required for every host, but they are the preferred path for brittle browser sessions or hosts with tight turn budgets.

### 4. Candidate Set

The search-harvest phase can emit a `candidate-set.json` document validated by:
- [candidate-set.schema.json](candidate-set.schema.json)

This captures:
- which phrases were attempted
- which result pages were opened
- the bounded candidate URLs selected for deeper inspection
- the visible clues that justified keeping each candidate

### 5. Evidence Notes

The evidence-review phase can emit an `evidence-notes.json` document validated by:
- [evidence-notes.schema.json](evidence-notes.schema.json)

This captures:
- which candidates were kept, rejected, or blocked
- which product and supplier pages were actually inspected
- the visible facts, judgments, unknowns, and representative products collected before report synthesis

## Output Relationship

The structured result does not replace the human-readable report.

The Markdown report must still follow:
- [../core/output-contract.md](../core/output-contract.md)

`report_artifacts.report_markdown_ref` should point to the clean canonical report artifact.
If a host produces noisy raw output that still needs to be preserved, store that separately and point `report_artifacts.run_notes_ref` at the raw transcript or operator notes.

## Suggested Runtime Flow

1. load `capability-manifest.json`
2. validate the incoming `request.json`
3. run preflight against the declared capabilities
4. if the host session is expensive or brittle, emit `candidate-set.json` first
5. review only the bounded candidate set and emit `evidence-notes.json`
6. synthesize the final Markdown report from the reviewed evidence
7. normalize the canonical Markdown report artifact if the host emitted wrappers or duplicate content
8. write the Markdown report artifact reference
9. write `run-result.json`

For stable hosts, steps 4 through 6 may still happen inside one run.
For unstable hosts, keeping the intermediate artifacts is strongly preferred.

## Authentication Semantics

Some marketplaces do not support a self-managed persistent login path for the agent host.
In those cases, an operator-provided authenticated browser session is a supported access mode, not a downgrade by itself.

Recommended interpretation:
- `validation_status` answers whether the workflow is proven under the declared access mode
- `validated_auth_mode` in `capability-manifest.json` declares which access mode that validation applies to
- `auth_mode` in `run-result.json` records which access mode the specific run used

For example, a host can honestly be:
- `validation_status = validated_direct`
- `validated_auth_mode = operator_authenticated`

when the direct workflow is proven, but the user must still log in first and let the agent reuse that session.

## Example Files

Examples are provided in:
- [examples/research-request.example.json](examples/research-request.example.json)
- [examples/capability-manifest.example.json](examples/capability-manifest.example.json)
- [examples/candidate-set.example.json](examples/candidate-set.example.json)
- [examples/evidence-notes.example.json](examples/evidence-notes.example.json)
- [examples/run-result.example.json](examples/run-result.example.json)
