# Example: Rust repository

Use the repository's Semgrep and Trivy workflows for broad source, dependency, secret, and configuration scans. Use ordinary Rust linting, such as Clippy, where the project already relies on it.

For a confirmed issue, add a Rust regression test that reproduces the failure, fix the behavior, and check related call sites for the same specific failure mode. Keep those focused checks in the normal project test workflow.

The Council templates do not add candidate scanners, custom semantic analyzers, or generated bughunt reports. Scanner findings still need review and reproduction before they are tracked as confirmed issues.
