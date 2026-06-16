# Alloy release channel — Distribution Requirements

**Document ID:** WP-SI-REQ-ALLOY-REL-001
**29110 work product:** Requirements Specification (distribution deliverable)
**Process:** Software Implementation (SI)
**Governing CR:** CR-001 (issue #1)
**Last updated:** 2026-06-16

---

## 1. Purpose & baseline

The "software" delivered by this repo is a **distribution stream**, not application code. This
document specifies the requirements a published Alloy release must satisfy and traces each to how it
is met and verified (no separate traceability matrix is needed at this size).

**Status legend:** ✅ Met · 🔧 In progress / pending first release.

## 2. Constraint requirements

| ID | Requirement |
|---|---|
| RNF-1 | This repo contains **no application source** — binaries + appcast + docs only. |
| RNF-2 | Binaries target macOS 13+ on Apple Silicon. |
| RNF-3 | Every published release version **matches a tagged baseline** in `Alloy-native-private`. |
| RNF-4 | Appcast EdDSA private key is **never committed**; only the public key is embedded in the app. |

## 3. Functional (distribution) requirements

| ID | Requirement | How it's met | Verification | Status |
|---|---|---|---|---|
| RD-1 | Each release ships a downloadable `Alloy-<version>.dmg` | GitHub Releases attachment | VV §2 checklist (download + mount + install) | 🔧 |
| RD-2 | DMG drag-installs Alloy into Applications with branded background | `package.sh` (source repo) | install smoke test | 🔧 |
| RD-3 | Release notes accompany each version | GitHub Release body + `CHANGELOG.md` | review | 🔧 |
| RD-4 | Sparkle `appcast.xml` exposes the latest version to installed apps | `appcast.xml` in repo / mirror | appcast validates; app sees the update | 🔧 |
| RD-5 | Each appcast `<item>` carries correct version, DMG URL, length, and EdDSA signature | `generate_appcast` from the real artifact | signature verifies against embedded public key | 🔧 |
| RD-6 | Builds are signed with an Apple Developer ID and **notarized** (no Gatekeeper prompt) | `codesign` + `notarytool` in the pipeline | clean first launch on a fresh machine | 🔧 |
| RD-7 | Until RD-6, the Gatekeeper workaround is documented for users | `README.md` + app `INSTALL.md` | doc present + accurate | ✅ |
| RD-8 | Auto-update is delta-safe: a bad item never bricks installs | keep last-known-good; validate before publish | VV §2 release checklist | 🔧 |

## 4. Acceptance

A release is **accepted** when every applicable RD-* requirement passes its verification in
`VV-verification-validation.md`, the version matches a source-repo baseline (RNF-3), and the release
is logged in `CHANGELOG.md` (WP-CL-ALLOY-REL-001).
