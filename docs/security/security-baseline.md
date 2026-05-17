# OpenHuman Security Baseline (Company Network + Local/Online)

This baseline defines the minimum controls expected for enterprise-facing deployments.

## CI + Supply Chain Controls

- CodeQL enabled for Rust and JavaScript/TypeScript.
- Dependency Review enabled on pull requests with `fail-on-severity: high`.
- Blocking dependency audits:
  - `cargo audit` on root and Tauri lockfiles.
  - `pnpm audit --audit-level=high` on root + `app` workspace.
- Dependabot enabled for:
  - GitHub Actions
  - npm (root + app)
  - cargo (root + app/src-tauri)

## Runtime Hardening Defaults

- `config.update.rpc_mutations_enabled` defaults to `false`.
- Core RPC bind is loopback-only unless explicitly allowed with:
  - `OPENHUMAN_CORE_ALLOW_NON_LOOPBACK=1`
- `OPENHUMAN_SECURITY_PROFILE=enterprise` enforces:
  - update RPC mutations disabled
  - browser allow-all bypass disabled (`OPENHUMAN_BROWSER_ALLOW_ALL` ignored)

## Manual GitHub Security Settings (Repository Admin)

These are required but cannot be fully enforced in-repo by source files alone:

1. Enable **Secret scanning**.
2. Enable **Push protection** for secrets.
3. Enable branch protection/rulesets requiring:
   - Test
   - Type Check
   - Coverage Gate
   - Security Audit
   - Dependency Review
   - CodeQL

## Threat Model Focus Areas

Validate and periodically pen-test:

1. RPC auth boundary (`OPENHUMAN_CORE_TOKEN`, relay path, auth middleware).
2. Browser/webview URL and domain allowlist controls.
3. File-system and tool execution boundaries.
4. Update/restart mutation controls (`update.apply` / `update.run`).
5. Credential handling + log redaction.

## Risk Tracking + SLA

Use this severity policy for tracking and remediation:

- **Critical**: fix or mitigate within 24 hours.
- **High**: fix or mitigate within 7 days.
- **Medium**: fix or mitigate within 30 days.
- **Low**: fix in regular maintenance backlog.
