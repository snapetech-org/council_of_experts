# Council of Experts

This repository contains templates for handling **confirmed findings** and making fixes durable through focused regression checks. General source, dependency, secret, and configuration scanning belongs to the existing Semgrep and Trivy workflows; the Council templates no longer include candidate scanners, generated bughunt reports, sweep-count gates, or custom Roslyn analyzers.

## What remains

| Template | Purpose |
| --- | --- |
| Remediation ledger and severity schema | Track reported and confirmed findings through a fix. |
| Sibling-search guidance | Check related call sites after a specific issue is confirmed. |
| Negative-space gate | Keep known trust-boundary validators and their regression anchors wired. |
| Behavior-pinning guidance | Add a focused runtime test for each confirmed fix. |
| Adversarial fuzz guidance | Preserve hostile inputs that reproduce a known failure mode. |
| Regression phase tracker | Keep focused remediation and regression work resumable. |

## Repository layout

```text
council_of_experts/
├── README.md
├── LICENSE
├── templates/
│   ├── scripts/       # remediation, boundary, and regression gates
│   └── docs/          # ledger, fix, boundary, and regression guidance
└── examples/          # short examples per ecosystem
```

## How to use the templates

1. Use the repository's Semgrep and Trivy workflows for broad source, dependency, secret, and configuration scans.
2. When a finding is confirmed, record it in the remediation ledger, classify its severity, and implement the fix.
3. Add a focused behavior test and check related call sites for the same confirmed issue.
4. Update the remediation baseline and negative-space gate for the affected boundary.
5. Run the repository's regression command and its normal test suite.

The templates do not generate candidate queues or claim that a clean scan proves the absence of bugs.

## License

MIT. See `LICENSE`.

## Local security scanning

Run `./scripts/security-scan-local.sh` for local Semgrep CE and the Trivy scanners that fit this repository. The installed pre-commit hook runs Semgrep on staged source/config files only; Trivy runs on demand or in CI. This public repository also runs Semgrep CE in GitHub Actions on changes and weekly. See [security-scanning.md](docs/security-scanning.md). Use `./scripts/update-security-tools.sh` to refresh local scanner data and the Trivy database.
