# Alloy release channel — Configuration Management Plan

**Document ID:** WP-CM-ALLOY-REL-001
**29110 work product:** Software Configuration / version control + release procedure
**Process:** Project Management (PM)
**Governing CR:** CR-001 (issue #1)
**Last updated:** 2026-06-16

---

## 1. Repository & configuration items

- **Repository:** `ACMAGI7/alloy-release` (public), default branch `main`.
- **Configuration items under control:**
  - `appcast.xml` — the Sparkle update feed (added with the first release)
  - `README.md`, `CHANGELOG.md`
  - ISO 29110 work products — `docs/iso29110/`
- **Managed outside git (by GitHub Releases):** the `.dmg` binaries themselves (attached to tagged
  releases), and their release notes.
- **Never committed:** the Sparkle **EdDSA private key**, Apple signing identities / API keys, any
  notarization credentials.

## 2. Versioning & baselines

- **Versioning:** SemVer, identical to the source-repo baseline being shipped (RNF-3). A release tag
  here (`vMAJOR.MINOR.PATCH`) corresponds 1:1 to a tagged baseline in `Alloy-native-private`.
- A release is "baselined" by creating a GitHub Release with the DMG attached, adding the matching
  `appcast.xml` item, and writing the `CHANGELOG.md` entry (WP-CL-ALLOY-REL-001).

## 3. Release procedure

```
1. BUILD    → in Alloy-native-private: ./build.sh then ./package.sh → Alloy-<version>.dmg
2. SIGN     → codesign with the Apple Developer ID; notarize (notarytool); staple
3. PUBLISH  → create a GitHub Release here (tag = vX.Y.Z), attach the DMG + release notes
4. APPCAST  → generate_appcast → add/update the <item> (version, url, length, edSignature) in appcast.xml
5. VERIFY   → run the VV pre-publish + validation checklists (WP-VV-ALLOY-REL-001)
6. CHANGELOG→ add the release entry to CHANGELOG.md (WP-CL-ALLOY-REL-001)
```

- **Labels:** `feat`, `bug`, `req`, `risk`, `change-request`, `iso29110`, `docs`.
- **Change requests** (`change-request`, `iso29110`) — channel/procedure changes need `@YmBal`
  approval before close.

## 4. Sparkle appcast format

Each release adds one `<item>` to `appcast.xml`:

```xml
<item>
  <title>Alloy 1.2.0</title>
  <sparkle:version>1.2.0</sparkle:version>
  <sparkle:minimumSystemVersion>13.0</sparkle:minimumSystemVersion>
  <enclosure url="https://github.com/ACMAGI7/alloy-release/releases/download/v1.2.0/Alloy-1.2.0.dmg"
             sparkle:edSignature="<EdDSA-signature>"
             length="<bytes>"
             type="application/octet-stream" />
</item>
```

- The `length` and `sparkle:edSignature` are generated from the **actual** published artifact
  (RD-5). The private signing key stays offline (RISK-R02); only the public key is embedded in the
  app build.

## 5. Integrity, rollback & backup

- Sparkle verifies each download's EdDSA signature against the app's embedded public key before
  applying — a tampered or mis-signed binary is rejected (RISK-R04).
- The **previous appcast item is retained** so a bad publish can be rolled back by reverting
  `appcast.xml` to the last-known-good state (RD-8 / RISK-R03).
- Source of record is the GitHub remote + Releases; the DMG artifacts are reproducible from the
  matching source baseline.
