# Contributing to Identity Auth Proxy

[Root README](README.md) · [Architecture](docs/ARCHITECTURE.md) · [Setup](docs/SETUP.md) · [API guide](docs/API.md) · [Network Ecosystem](README.md#network-ecosystem)

## Project status

This repository is documentation-only. No identity provider, credential protocol, inline proxy/auth-subrequest mode, policy engine, runtime stack, or automated test suite has been implemented or selected. Proposed security behavior must not be described as existing protection.

## Contribution workflow

Read the guides, agree a focused design or issue with the owner, and begin a local branch:

```sh
git clone https://github.com/OBAIAHMOPURI/identity-auth-proxy.git
cd identity-auth-proxy
git switch -c docs/describe-change
```

Use a narrowly scoped pull request for normal contributions. Direct-to-main publication for this documentation batch was explicitly approved and is not a standing merge rule. There are no supported install/run commands until a runtime is selected.

## Repository-specific priorities

- Decide the provider, credential type, deployment boundary, and decision-service versus inline-proxy model.
- Define deny-by-default resource/action policies and ownership of trusted identity/forwarding headers independently of a particular gateway.
- If signed tokens are selected, design signature/algorithm/issuer/audience/expiry validation, bounded clock skew, key rotation/caching, and failure behavior; decoding claims alone is not authentication.
- Define minimal forwarded identity, least privilege, redacted diagnostics, and protection against token leakage or replay.

## Quality, tests, and review evidence

For documentation, run `git diff --check`, inspect rendering, and verify root README, architecture/setup/API backlinks and all seven siblings. Clearly mark proposals and unsupported assumptions.

Future code must include synthetic credentials/fixtures and tests for missing/malformed credentials, invalid signatures, wrong issuer/audience, expiry, algorithm confusion, key rotation, stale caches, spoofed headers, policy denial, and provider outages. Report commands/versions actually used, outcomes, and checks not run; no existing test suite or CI success is implied. Pull requests should explain scope, rationale, threat/trust assumptions, compatibility, evidence, limitations, and rollback/configuration changes. Update contract documentation with behavior changes.

## Secret and operational handling

Never commit keys, tokens, passwords, provider secrets, real user claims, private operational notes, or raw authentication logs. Use approved sandbox identities and an owner-approved private reporting channel for vulnerabilities. Live provider configuration, production identity traffic, permission changes, and deployments require separate authorization. This guide selects no license.

## Sibling repository network

Navigation only; neither gateway nor either Java app is currently protected by this unimplemented repository.

- [alert-notification-dispatcher](https://github.com/OBAIAHMOPURI/alert-notification-dispatcher/blob/main/README.md)
- [Brainwave_Matrix_Intern — Banky Application](https://github.com/OBAIAHMOPURI/Brainwave_Matrix_Intern/blob/main/README.md)
- [BrainWave_Matrix_Intern1 — Hospital Management System](https://github.com/OBAIAHMOPURI/BrainWave_Matrix_Intern1/blob/main/README.md)
- [edge-gateway-service](https://github.com/OBAIAHMOPURI/edge-gateway-service/blob/main/README.md)
- [edge-gateway-service1](https://github.com/OBAIAHMOPURI/edge-gateway-service1/blob/main/README.md)
- [telemetry-stream-worker](https://github.com/OBAIAHMOPURI/telemetry-stream-worker/blob/main/README.md)
- [workflow-state-sync](https://github.com/OBAIAHMOPURI/workflow-state-sync/blob/main/README.md)
