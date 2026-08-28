# Security Policy

This repository is a fork of [mantlenetworkio/mantle](https://github.com/mantlenetworkio/mantle) with a Chaintable pipeline-compatible historical block RPC.

First determine whether the issue reproduces on an unmodified upstream build.

- **Upstream issue** — reproduces on the upstream client and concerns consensus, peer-to-peer networking, EVM execution, transaction handling, a standard RPC, or storage. Follow the [upstream security policy](https://github.com/mantlenetworkio/mantle/security/policy), not this document.
- **This fork's issue** — only reproduces with this fork, or concerns `trace_debankBlock`, historical block replay and output, the Docker image, or the CI workflows. Follow the process below.

---

## Our Process

### Supported Versions

We provide security updates for the latest `main` branch and recent releases.

| Version | Supported |
|---------|-----------|
| main | Yes |
| Latest release | Yes |
| Older versions | No |

### Reporting a Vulnerability

Do not open a public issue for a suspected vulnerability. Report it privately through either:

- a GitHub Security Advisory on this repository (preferred), or
- email to `bugbounty@debank.com`.

Include the affected commit or image tag, impact, reproduction steps, and a proof of concept when available.

### Response Process

We aim to acknowledge reports within 72 hours, provide an initial assessment within 3–5 days, and release a fix according to severity.

### Disclosure Policy

- Fixes may be developed privately before release.
- Coordinate public disclosure with the maintainers.
- Credit will be given unless the reporter requests otherwise.

### Scope

Security-relevant areas maintained by Chaintable include:

- integrity of `trace_debankBlock` output;
- historical transaction replay and state-diff generation;
- resource exhaustion introduced by the added tracer or RPC;
- the published Docker images and CI workflows.

The RPC output is consumed by downstream indexing and query systems, so data-integrity issues may propagate beyond this node.
