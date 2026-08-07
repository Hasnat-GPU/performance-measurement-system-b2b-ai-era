# Security Policy

This repository contains a design document and its supporting configuration. It
ships no executable application, no dependencies that run on your machine, and
no service. The realistic security surface is therefore small — but not zero,
and this policy covers what there is.

## Supported versions

| Version | Supported |
|---|---|
| 1.0.x | ✅ |
| < 1.0 | ❌ (no such versions exist) |

## What counts as a security issue here

- A **GitHub Actions workflow** in `.github/workflows/` with an injection risk,
  an over-broad permission, or an unpinned third-party action that could be
  used to compromise the repository or its secrets.
- A **malicious or compromised link** in the document or README pointing
  somewhere harmful.
- **Credentials, tokens, keys or personal data** accidentally committed to the
  repository or its history.
- A **supply-chain concern** in the pinned actions this repository consumes.

## What does not

Disagreeing with the design, finding an error in a citation, or spotting a
broken link are all welcome — but they are not security issues. Please use the
[normal issue templates](../../issues/new/choose) for those; they get a faster
and more useful response.

## Reporting

**Please do not open a public issue for a security report.**

Use GitHub's private vulnerability reporting:

1. Go to the [Security tab](../../security/advisories/new).
2. Click **Report a vulnerability**.
3. Describe the issue, the impact you think it has, and how to reproduce it.

This channel is private between you and the maintainer until a fix is published.

If private reporting is unavailable to you, contact
[@Hasnat-GPU](https://github.com/Hasnat-GPU) directly on GitHub and ask for a
private channel before sharing details.

## What to expect

| Stage | Target |
|---|---|
| Acknowledgement | Within 5 days |
| Initial assessment | Within 14 days |
| Fix or documented decision not to act | Within 30 days for anything confirmed |

This is a personal project maintained without a team behind it, so these are
honest targets rather than a commercial SLA.

## Disclosure

Coordinated disclosure, please. Once a fix is published, you are welcome to
write about it publicly, and you will be credited in the advisory and the
[changelog](CHANGELOG.md) unless you prefer not to be.

## Hardening already in place

- All third-party GitHub Actions are **pinned to a full commit SHA**, not a
  moving tag, so a compromised upstream tag cannot silently change what runs.
- Workflows declare **least-privilege `permissions`** explicitly rather than
  inheriting the default token scope.
- Dependabot monitors the Actions used here and opens PRs for updates.
