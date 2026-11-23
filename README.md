# Carnet releases

Builds of **Carnet**, a minimal, private mail client for IMAP and SMTP with
calendar, contacts and notes, for Linux (Flatpak) and Android (arm64).

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

If you used the old Poste app, run `flatpak uninstall io.github.marc_mrt.Poste` first, then re-add your accounts in Carnet, since no data carries over.

## Android

The APK comes only with releases (`vX.Y.Z`), next to the Flatpak. Download
`carnet-android-arm64.apk` and `SHA256SUMS` from the
[latest release](https://github.com/marc-mrt/carnet-releases/releases/latest),
then check them:

```sh
sha256sum -c SHA256SUMS
gh attestation verify carnet-android-arm64.apk -R marc-mrt/carnet-releases
```

The release notes also give the SHA-256 digest of the signing certificate.

To install, download the APK on the phone, allow the browser or file manager
to install apps when Android asks, and open the file. A build signed with a
different key, such as a debug build, must be uninstalled first, and its local
data is lost.

### Maintainer setup

Builds are signed with a key only the maintainer holds. Create it once:

```sh
keytool -genkeypair -keystore carnet-release.p12 -storetype PKCS12 -alias carnet -keyalg RSA -keysize 4096 -validity 10000
```

Then give the workflow the keystore, its password and the key alias:

```sh
base64 < carnet-release.p12 | gh secret set ANDROID_KEYSTORE_BASE64 -R marc-mrt/carnet-releases
gh secret set ANDROID_KEYSTORE_PASSWORD -R marc-mrt/carnet-releases
gh secret set ANDROID_KEY_ALIAS -R marc-mrt/carnet-releases
```

Keep an offline backup of `carnet-release.p12` and its password. If the
keystore is lost, every future build is signed with a new key: each user must
uninstall Carnet and loses their local data.

## Issues

Bugs and ideas go in [issues](https://github.com/marc-mrt/carnet-releases/issues).
Report security problems privately through
[security advisories](https://github.com/marc-mrt/carnet-releases/security/advisories/new).

## License

MIT
