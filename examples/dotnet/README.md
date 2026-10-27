# Example: .NET repository

Use Semgrep and Trivy for broad source, dependency, secret, and configuration scans. Keep Council templates focused on findings that have been confirmed and their regression coverage.

For a confirmed issue:

1. Record it in the remediation ledger with severity and confidence.
2. Fix the issue and check related call sites for the same specific failure mode.
3. Add a focused behavior test that would fail before the fix.
4. Update the boundary gate and remediation notes when the finding concerns a trust boundary.
5. Run the repository's normal focused checks and test suite.

Do not turn scanner output into a candidate backlog or treat a clean scan as proof that the repository has no bugs.
