# Alloy release channel — Project Management Plan

**Document ID:** WP-PM-ALLOY-REL-001
**29110 work product:** Project Plan (incl. risk register)
**Process:** Project Management (PM)
**Governing CR:** CR-001 (issue #1)
**Owner:** Jay — Pontakorn Kleebkaew (MD, `YmBal`)
**Last updated:** 2026-06-16

---

## 1. Description

`alloy-release` is the **public distribution channel** for Alloy, the native macOS browser. It
publishes signed `.dmg` builds and the Sparkle **appcast** feed used for in-app auto-update. It holds
no source. The deliverable of this "project" is a correct, trustworthy, auto-updating release stream.

## 2. Scope & deliverables

| # | Deliverable | State | Reference |
|---|---|---|---|
| D1 | Public GitHub repo for releases (no source) | Done | this repo |
| D2 | Channel README + governance docs | Done | `README.md`, `docs/iso29110/` |
| D3 | First published `Alloy-<version>.dmg` (GitHub Release) | **Open** | from `package.sh` in source repo |
| D4 | Sparkle `appcast.xml` feed (first item) | **Open** | `appcast.xml` |
| D5 | Apple Developer ID signing + notarization | **Open** | release pipeline |
| D6 | EdDSA signing keys for appcast items | **Open** | Sparkle `generate_keys` |

**Out of scope:** application source, feature development (owned by `Alloy-native-private`); ISO 9001.

## 3. Roles & responsibilities

| Role | Person | Responsibility |
|---|---|---|
| MD / Release authority | Jay (`YmBal`) | Approves a release, owns distribution risk, accepts the build |
| Build / packaging | Project team | Produces the signed DMG (`package.sh`) and appcast item |
| Customer / acceptance | End user | Downloads, installs, receives auto-updates |

## 4. Schedule

| Step | Theme | Status |
|---|---|---|
| 0 | Channel repo + governance docs | **Done (2026-06-16)** |
| 1 | Apple Developer ID + notarization workflow | Open |
| 2 | First signed/notarized DMG published as a Release | Open |
| 3 | Sparkle appcast live + in-app update verified end-to-end | Open |

## 5. Risk register

| ID | Risk | Sev | Mitigation / control | Status |
|---|---|---|---|---|
| RISK-R01 | Builds not yet notarized → Gatekeeper blocks first launch | High | Documented workaround in README/`INSTALL.md`; obtain Developer ID + notarize (D5) | **Open** |
| RISK-R02 | Appcast EdDSA signing key compromised or lost | High | Private key stored offline / in a secret manager, never committed; rotate + re-sign if exposed | **Open** (key not yet generated) |
| RISK-R03 | Malformed/unsigned appcast item bricks auto-update for all installs | Med | Validate `appcast.xml` + signature before publish (VV checklist); keep last-known-good item | Controlled by procedure |
| RISK-R04 | Tampered binary served from the channel | Med | Releases only via official channel; Sparkle verifies EdDSA signature against the embedded public key | Controlled |
| RISK-R05 | DMG URL / length mismatch in the appcast | Low | Generate the `<item>` from the actual artifact (size + hash) at publish time | Controlled by procedure |
| RISK-R06 | Source/release version drift (release tag ≠ source baseline) | Low | Release version must match a tagged baseline in `Alloy-native-private`; recorded in both CHANGELOGs | Controlled |

## 6. Communication & resources

- **Repository:** `ACMAGI7/alloy-release` (public). Issues + CHANGELOG are the formal record.
- **Tooling:** `package.sh` (source repo) for the DMG; Sparkle (`generate_keys`, `generate_appcast`)
  for the feed; Apple `notarytool` / `codesign` for signing.

## 7. Change & version control

Releases follow the procedure in `CM-configuration-management.md`. Any change to the channel's scope
or procedure is raised as a `change-request` issue approved by `@YmBal`.
