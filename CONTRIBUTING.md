# Contributing

Thanks for your interest in contributing.

This repository is a fork of [mantlenetworkio/mantle](https://github.com/mantlenetworkio/mantle) with a Chaintable pipeline-compatible historical block RPC. It is maintained to serve Mantle pre-Bedrock block data, not as a general-purpose Mantle client fork.

First determine where the change belongs:

- **Mantle client changes** — consensus, peer-to-peer networking, EVM behavior, transaction handling, standard RPCs, or storage should be contributed upstream through its contribution process. If an upstream fix matters here, open an issue linking the upstream change so it can be incorporated deliberately.
- **Chaintable changes** — `trace_debankBlock`, historical replay and output, the Docker image, CI workflows, and documentation for this node belong in this repository.

---

## Development Process

### Requirements

- Go 1.23.12, as selected by `l2geth/go.mod`
- Docker with Buildx for the release image
- the native build prerequisites required by `l2geth`

### Workflow

1. Fork the repository.
2. Create a branch from `main`.
3. Make a focused change.
4. Run the relevant local checks.
5. Open a pull request with the motivation, testing evidence, and compatibility impact.

### Local Checks

Build the same image used by CI:

```bash
docker build -f l2geth/Dockerfile .
```

For Go changes, run targeted tests for the packages you modified. The repository-level `go.work` targets an older Go version, so run `l2geth` tests with its workspace disabled and its pinned toolchain selected:

```bash
cd l2geth
GOWORK=off GOTOOLCHAIN=go1.23.12 go test ./path/to/changed/package
```

If a pre-existing failure prevents a clean run, include the exact command and failure in the pull request.

### Code Guidelines

- Keep changes focused on the Chaintable-maintained surface.
- Match the existing style and run `gofmt` on changed Go files.
- Prefer explicit, minimal changes over broad refactors.
- Include tests where practical, or document the chain, block range, and reference data used for manual verification.

### Pull Requests

Pull requests should include:

- a concise summary and motivation;
- test and build results;
- any effect on RPC output compatibility or image consumers.

Pull requests build and smoke-test the image without publishing it. Merges to `main` and GitHub Releases publish images from trusted repository revisions.

### Releases

Release tags follow `v<base-version>-ct.N`, where `ct` means Chaintable. A GitHub Release publishes the corresponding multi-architecture image.

### Reporting Issues

Include the commit or image tag, block height, reproduction steps, and expected versus actual output.

### Security

Do not disclose vulnerabilities publicly. Follow [SECURITY.md](./SECURITY.md).

### License

Contributions remain under the license that applies to their path. General repository files use the [MIT License](./LICENSE); `l2geth` retains [GPL-3.0](./l2geth/COPYING) and [LGPL-3.0](./l2geth/COPYING.LESSER) terms.
