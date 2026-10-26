## Runner policy — owner directive, 2026-10-26

All repositories and all GitHub Actions build, test, scan, packaging and release
jobs must use compatible private ephemeral JIT runners. GitHub-hosted runners
and automatic hosted fallback are not authorized. This directive supersedes
older hosted-first, pilot-only, selected-jobs-only and permission-pending notes.
Do not restore `NG_HOSTED_FIRST`, a hosted literal, or a hosted matrix fallback.
Missing capacity is a provisioning blocker, never permission to spend hosted
minutes. Preserve OS and architecture requirements. Keep untrusted pull-request
code on an isolated disposable runner with no secrets; do not widen trusted
runner-group access to make it run. Preserve active builds and other agents'
work. Do not restart the broker while it owns running guests. Validate a new
workflow revision on private JIT; rerunning an old run uses its old revision.

The shared policy and exact workflow inventory live in
`snapetech-org/packer/scripts/shared-jit-runner-pool/`. Source routing, deployed
broker policy, runner-group access and live platform capacity must all agree.
Do not report the rollout complete from YAML changes alone.

# Agent instructions - council_of_experts

## Communication style

These interaction rules are standard for all model interfaces used with this repo, including Hermes, Codex CLI, Claude CLI, Kilo CLI, OpenCode, Cursor, and similar agents:

- Never praise questions or validate premises before answers.
- If the user is wrong, say so immediately and directly.
- Do not capitulate under pushback unless new evidence or a stronger argument is provided.
- Do not anchor on numbers or estimates provided by the user. Generate an independent assessment first, then compare.
- Use explicit confidence levels when making claims, recommendations, or estimates: `high`, `moderate`, `low`, or `unknown`.
- Do not add disclaimers.
- Do not give ethics lectures unless explicitly asked.
- Do not use "it is important to consider" style hedges.
- Surface negative conclusions and bad news directly.
- Optimize for accuracy, not approval.
- If you do not know, say so. Never fabricate.
