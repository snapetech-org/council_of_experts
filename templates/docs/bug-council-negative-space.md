# Bug Council Negative-Space Gate — TEMPLATE

Copy into `docs/dev/bug-council-negative-space.md` and replace the boundaries below with the trust boundaries of your codebase.

This document declares known trust boundaries and the validator each one must run, so a missing validator is itself a CI failure. Use Semgrep and Trivy for broad source, dependency, secret, and configuration scans.

The gate is enforced by `scripts/check-council-negative-space.sh`, which is invoked from `scripts/check-remediation-baseline.sh`.

## Boundaries

A boundary is a code seam where data crosses from a less-trusted source into your runtime. For every boundary, this document records:

- **Source** — where the data comes from.
- **Sink file(s)** — the file(s) where the boundary is implemented.
- **Required validator** — a symbol that must appear in the sink file. The symbol's presence does not prove correctness; it proves the developer thought about the boundary. Behavior is pinned separately by `bug-council-behavior-pinning.md`.

| Boundary | Source | Sink file(s) | Required validator |
| --- | --- | --- | --- |
| _replace_with_your_boundary_ | _network input_ | `src/path/to/sink.ext` | `ValidateInputName` |

## Adding a new boundary

When a new public surface accepts untrusted input:

1. Add a row above with the boundary, the file(s) it lives in, and the validator symbol you've placed in those file(s).
2. Add a PAIR of lines to `scripts/check-council-negative-space.sh`:
   - `assert_validator_present "<boundary>" "<sink>" "<symbol>"` — catches "validator deleted."
   - `assert_baseline_anchor "<boundary>" "<symbol>"` — catches "remediation gate silently removed." Both halves required.
3. Add a behavior-pinned test per `bug-council-behavior-pinning.md`.

## Why two halves

The single-half version of this gate (validator-symbol-only) was insufficient. A maintainer could remove the corresponding `require_pattern` in `scripts/check-remediation-baseline.sh` while the symbol still existed, and the gate would pass — silently weakening the fix gate. The two-half pattern requires both the symbol AND the baseline check to remain, so a half-removal fails CI.

## Removing a boundary

Removing a row requires a short rationale explaining why the boundary no longer exists (refactored away, code deleted, or source moved to trusted). Update the remediation baseline in the same change.

## Why this matters

Many boundary regressions happen when a guard is added for one input path but forgotten for a related path. The negative-space gate lists each known boundary and asserts its guard remains in place.
