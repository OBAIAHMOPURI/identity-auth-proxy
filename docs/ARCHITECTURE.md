# Identity Auth Proxy — Architecture

[README](../README.md) · [Setup](SETUP.md) · [Network Ecosystem](../README.md#network-ecosystem)

## Evidence and design status

Audit date: 13 November 2026; branch: `main`. Only a title-only README existed; no application source, build manifest, tests, or deployment configuration was present. No implementation, build manifest, tests, or runtime integrations were found. All components and contracts below are **proposed design notes for owner review**, not verified runtime behavior.

## Intended responsibility and boundaries

A candidate boundary for validating caller identity and applying explicit access policy before a protected upstream request. No identity provider, token format, or authorization model has been selected.

This repository must not acquire authority to send messages, update third-party systems, expose production endpoints, or process sensitive data merely because those operations appear in a design. Confirm scope and approval gates before implementation.

## Candidate data flow

```text
Protected request -> credential validation -> identity normalization -> policy decision -> trusted allow/deny response
```

| Proposed component | Responsibility |
| --- | --- |
| Credential validator | If signed tokens are chosen, validate signature, issuer, audience, expiry, and allowed algorithms; never trust decoded claims alone. |
| Identity context | Create a minimal, versioned identity context; strip spoofable incoming identity headers. |
| Policy engine | Make deny-by-default decisions with explicit resource and action scopes. |
| Upstream boundary | Forward only necessary context over a trusted channel; do not leak bearer tokens into logs or telemetry. |

## Contract-first implementation

Specify credential transport, decision request/response schemas, identity header ownership, status codes, and policy versioning. All contracts remain proposed.

Record payload limits, validation rules, identity/trust boundaries, correlation identifiers, timeout budgets, supported errors, and compatibility/versioning rules. Choose actual transports and persistence only after those contracts are reviewed. No endpoint, broker, storage engine, or deployment topology is prescribed by the current repository.

## Reliability and observability requirements

Classify permanent and transient errors. Bound retries with backoff/jitter and an overall deadline; do not automatically repeat a side effect without an idempotency strategy. Use explicit recovery/checkpoint behavior where persistence is involved. Track throughput, error/latency distributions, and queue depth or outstanding work where relevant. Diagnostics should use stable event/request identifiers rather than credentials or raw sensitive payloads.

## Security and data handling requirements

Validate all external input. Grant only necessary permissions and keep secrets in a managed secret store or a reviewed local development mechanism. Define log/retention/redaction policy before collecting real data. Default to sandbox destinations; do not infer deployment or sending authorization from this document.

## Proposed verification

Test missing/malformed credentials, invalid signature, wrong issuer/audience, expired tokens, algorithm confusion, key rotation, cache expiry, spoofed headers, and deny-by-default behavior.

No such test suite exists yet and no test results are claimed.

## Open architecture decisions

- Select the identity provider and decide whether this is an auth subrequest service or an inline proxy.
- Define key rotation, bounded key caching, clock-skew policy, revocation/logout expectations, and outage behavior.
- Define service-to-service trust and policy ownership independently of a particular gateway implementation.

## Ecosystem boundary

The [sibling repository index](../README.md#network-ecosystem) is documentation navigation only. Integration with a gateway, identity service, telemetry worker, workflow synchronizer, notification dispatcher, or either Java app requires a separately implemented and tested contract. The two gateway names do not establish a canonical/secondary or versioned relationship.
