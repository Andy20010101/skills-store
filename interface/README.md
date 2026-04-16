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
- capability booleans
- operation mappings from the host's native tools to the shared contract

### 3. Run Result

Each run should emit a `run-result.json` document validated by:
- [run-result.schema.json](run-result.schema.json)

This captures:
- run status
- whether evidence came from direct 1688 pages, mirror-assisted pages, or no usable pages
- where the Markdown report lives
- supplier count
- blockers and limitations

## Output Relationship

The structured result does not replace the human-readable report.

The Markdown report must still follow:
- [../core/output-contract.md](../core/output-contract.md)

## Suggested Runtime Flow

1. load `capability-manifest.json`
2. validate the incoming `request.json`
3. run preflight against the declared capabilities
4. execute the research workflow from `core/`
5. write the Markdown report
6. write `run-result.json`

## Example Files

Examples are provided in:
- [examples/research-request.example.json](examples/research-request.example.json)
- [examples/capability-manifest.example.json](examples/capability-manifest.example.json)
- [examples/run-result.example.json](examples/run-result.example.json)
