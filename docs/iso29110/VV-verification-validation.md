# Alloy release channel — Verification & Validation Record

**Document ID:** WP-VV-ALLOY-REL-001
**29110 work products:** Verification Results, Validation Results
**Process:** Software Implementation (SI) + Project Management (PM)
**Governing CR:** CR-001 (issue #1)
**Last updated:** 2026-06-16

---

## 1. Verification strategy

Verification answers *"is the release built right?"* For a distribution channel that means: the
artifact is the intended baseline, it is correctly signed, and the appcast that advertises it is
well-formed and verifiable.

### 1.1 Pre-publish verification (run for every release)

- [ ] Release version **matches a tagged baseline** in `Alloy-native-private` (RNF-3).
- [ ] `codesign --verify --deep --strict Alloy.app` passes; `spctl -a -vv Alloy.app` accepts it
      (once notarized — RD-6).
- [ ] `appcast.xml` is valid XML and the new `<item>` has the correct `sparkle:version`,
      `url`, `length`, and `sparkle:edSignature` (RD-5).
- [ ] EdDSA signature verifies against the public key embedded in the shipped app (RD-5).
- [ ] DMG mounts and drag-installs cleanly (RD-1, RD-2).
- [ ] Last-known-good appcast item is retained so a bad publish can be rolled back (RD-8).

## 2. Validation strategy

Validation answers *"does the user actually get a working, updatable app?"* — confirmed on a real
machine.

### 2.1 Release validation checklist

On a clean macOS 13+ Apple Silicon machine:

- [ ] Download `Alloy-<version>.dmg` from Releases; mount; drag to Applications.
- [ ] **Notarized build:** launches with no Gatekeeper prompt (RD-6). *Until then:* the documented
      `xattr` / right-click-Open workaround succeeds (RD-7).
- [ ] App reports the expected version.
- [ ] From a prior installed version, the in-app Sparkle updater detects the new version, downloads,
      verifies the signature, and updates (RD-4, RD-8).

## 3. Results (snapshot 2026-06-16)

| Item | Result | Notes |
|---|---|---|
| Channel repo + governance docs (D1, D2) | **Pass** | this commit |
| Gatekeeper workaround documented (RD-7) | **Pass** | README + app `INSTALL.md` |
| First signed/notarized DMG (RD-1, RD-6) | **Pending** | awaiting Apple Developer ID |
| Appcast feed live + auto-update verified (RD-4, RD-5, RD-8) | **Pending** | awaiting first release + EdDSA keys |

## 4. Open items

- Generate Sparkle EdDSA keys (store the private key offline — RISK-R02) and embed the public key in
  the app build.
- Obtain the Apple Developer ID, wire `codesign` + `notarytool` into the pipeline, and publish the
  first notarized DMG.
- Once live, re-run §2 end-to-end (including an upgrade from a prior version) and record the result
  here.
