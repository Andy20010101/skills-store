# Codex + Hermes Interop Test

- Test date: 2026-04-16
- Request file: `verification/codex-hermes-interop-2026-04-16/request.json`
- Codex result: `verification/codex-hermes-interop-2026-04-16/codex-run-result.json`
- Hermes result: `verification/codex-hermes-interop-2026-04-16/hermes-run-result.json`
- Hermes session id: `20260416_111236_9f594f`

## Test Goal

Verify that Codex and Hermes can consume the same request and emit compatible `run-result.json` outputs using the shared interface layer.

## Test Mode

This was an interop test over existing repo evidence, not a fresh dual-agent web research run.

Both sides were constrained to:
- use the same request id
- use only local repository evidence
- reflect the same direct-site failure boundary
- emit JSON matching `interface/run-result.schema.json`

## Environment Notes

- Hermes exists locally as `/home/administrator/.local/bin/hermes`
- Hermes required execution outside the filesystem sandbox because it writes logs under `/home/administrator/.hermes/`
- The first sandboxed attempt failed before model execution due read-only filesystem restrictions on Hermes log output
- The escalated Hermes run succeeded

## Result Summary

### Shared Outcome

Both Codex and Hermes produced:
- `status = partial`
- `evidence_mode = mirror_assisted`
- `supplier_count = 3`
- the same three supplier names
- the same report artifact references

### Differences

- Codex summary text is phrased as adapter-oriented reuse of existing repo evidence
- Hermes summary text is phrased as a direct narrative of the validated outcome
- Hermes lists one more limitation line than Codex

These are wording differences only, not contract differences.

## Conclusion

The shared interface is usable across Codex and Hermes for this request shape.

What this test proves:
- both agents can target the same `request.json`
- both agents can emit semantically aligned `run-result.json`
- the adapter boundary is concrete enough for cross-agent interop

What this test does not prove:
- a fresh dual-agent live browse on direct `1688.com`
- that Hermes currently has direct-site validation in its own host environment
