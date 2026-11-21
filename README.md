# Carnet releases

Builds of **Carnet**, a minimal, private mail client for IMAP and SMTP with
calendar, contacts and notes, for Linux (Flatpak). Android builds come later.

> [!WARNING]
> **Heavily work in progress.** Carnet is an experiment, fully vibe-coded to
> test an idea: almost all of its code was written by AI agents, with a human
> deciding what to build and reviewing the result. Expect rough edges and
> breaking changes, and don't trust it with mail you can't afford to lose.

The source is not public. This repository only builds it and publishes the
result: each release's workflow run, its logs and the provenance attestation
are here for anyone to check.

## Install

Download `carnet.flatpak` and `SHA256SUMS` from the
[latest release](https://github.com/marc-mrt/carnet-releases/releases/latest), then:

```sh
sha256sum -c SHA256SUMS
gh attestation verify carnet.flatpak -R marc-mrt/carnet-releases
flatpak install --user carnet.flatpak
```

## Issues

Bugs and ideas go in [issues](https://github.com/marc-mrt/carnet-releases/issues).
Report security problems privately through
[security advisories](https://github.com/marc-mrt/carnet-releases/security/advisories/new).

## License

MIT
