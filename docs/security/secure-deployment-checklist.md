# Secure Deployment Checklist (Local + Full Online)

Use this checklist before running OpenHuman in a company network.

- [ ] Keep OpenHuman updated to latest supported release.
- [ ] Set `OPENHUMAN_SECURITY_PROFILE=enterprise`.
- [ ] Keep `OPENHUMAN_CORE_HOST=127.0.0.1` unless remote bind is strictly required.
- [ ] If remote bind is required, set `OPENHUMAN_CORE_ALLOW_NON_LOOPBACK=1` explicitly and restrict network exposure (firewall/VPN/allowlist).
- [ ] Set a strong `OPENHUMAN_CORE_TOKEN` for any non-desktop/non-localhost deployment.
- [ ] Keep `OPENHUMAN_AUTO_UPDATE_RPC_MUTATIONS_ENABLED=false` unless operationally required.
- [ ] Do not set `OPENHUMAN_BROWSER_ALLOW_ALL=1` in enterprise deployments.
- [ ] Run CI security gates (CodeQL, Dependency Review, Security Audit) as required checks.
- [ ] Enable GitHub secret scanning + push protection at repo level.
- [ ] Verify no secrets are committed in `.env*`, logs, scripts, or test fixtures.
- [ ] Confirm OAuth/API credentials are least-privilege and rotated.
- [ ] Review threat-model focus areas at least quarterly and after major architecture changes.

## Full Online/Remote Operation Extra Controls

- [ ] Terminate TLS at edge/proxy for any remote access path.
- [ ] Restrict inbound access to trusted network ranges only.
- [ ] Centralize logs and alert on auth failures + repeated RPC denial events.
- [ ] Run periodic dependency + vulnerability scans outside CI cadence.
