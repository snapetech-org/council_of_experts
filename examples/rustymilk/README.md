# RustyMilk-Style Polyglot Repository

For repositories that combine Rust, browser packages, Node tooling, generated content, and release metadata, use Semgrep and Trivy for broad source, dependency, secret, and configuration scans.

When a finding is confirmed, record the specific behavior and affected surface, fix it, and add a focused regression test. Check related call sites for the same confirmed failure mode and keep boundary validators covered by the repository's existing regression gates.

The Council templates do not maintain candidate inventories, generated discovery reports, sweep counts, or custom semantic scanners. A clean scan is not a claim that no bugs remain.
