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
- **Stable-named `Alloy.dmg` download asset** (IR-5, `Alloy-native-private`#67 / PR #68): each release now
  also publishes a constant `Alloy.dmg` (identical bytes to the versioned DMG, download-only — **not** in
  the appcast, so Sparkle keeps using the versioned enclosure) so `refinery-agi.com/alloy` can link to
  `releases/latest/download/Alloy.dmg` (always the newest release). v0.2.10 backfilled.

### Shipped (supersedes the earlier "Pending — first release" list)
- Signed `Alloy-<version>.dmg` builds published to GitHub Releases + the Sparkle `appcast.xml` feed
  (EdDSA-signed enclosures) are live.
- **Apple Developer ID signing + notarization + stapling has been live since 0.2.3** — builds launch with
  no Gatekeeper steps (verified `spctl -a -t exec` → "Notarized Developer ID"). This corrects the earlier
  note that listed these as pending.

---

## [0.0.0] — 2026-06-16 · Channel created

### Added
- Repository created as the public distribution channel for Alloy (releases + Sparkle appcast,
  no source).
