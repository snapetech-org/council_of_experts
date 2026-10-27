# Example: TypeScript / JavaScript repository

Use the repository's Semgrep and Trivy workflows for broad source, dependency, secret, and configuration scans. Keep any existing ESLint rules for routine style and project-specific correctness checks.

For a confirmed issue, add a focused behavior test, fix the code, and check nearby call sites for the same specific failure mode. Keep known trust boundaries and their validators covered by the repository's existing regression gates.

Do not maintain a separate regex candidate scanner or generated candidate queue in the Council templates. Review scanner output before treating it as a confirmed bug.
