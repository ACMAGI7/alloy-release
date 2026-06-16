# Changelog

All notable changes to the **Alloy release channel** (distribution + Sparkle appcast) are documented
here. Format: [Keep a Changelog](https://keepachangelog.com/en/1.0.0/) · Versioning: [SemVer](https://semver.org/)
Configuration-management work product **WP-CL-ALLOY-REL-001** (ISO/IEC 29110 Basic Profile).

> This log tracks **release-channel** changes (published builds, appcast updates, channel docs).
> Application source/feature history lives in `Alloy-native-private`'s `CHANGELOG.md` (WP-CL-ALLOY-001).

---

## [Unreleased]

### Added
- **ISO/IEC 29110 Basic Profile adoption** (CR-001, issue #1): full `README.md`, this `CHANGELOG.md`
  (`WP-CL-ALLOY-REL-001`), and the `docs/iso29110/` work-product set scaled to a distribution
  channel — project plan (`WP-PM-ALLOY-REL-001`), distribution requirements (`WP-SI-REQ-ALLOY-REL-001`),
  verification & validation / release checklist (`WP-VV-ALLOY-REL-001`), and configuration-management
  + appcast plan (`WP-CM-ALLOY-REL-001`).

### Pending (first release)
- Publish the first signed `Alloy-<version>.dmg` to GitHub Releases.
- Add the initial `appcast.xml` Sparkle feed (first `<item>`).
- Apple Developer ID signing + notarization so the build launches with no Gatekeeper steps.

---

## [0.0.0] — 2026-06-16 · Channel created

### Added
- Repository created as the public distribution channel for Alloy (releases + Sparkle appcast,
  no source).
