# ISO/IEC 29110 — Basic Profile Work Products (release channel)

**Repository:** ACMAGI7/alloy-release — Alloy distribution + Sparkle appcast (no source)
**Standard:** ISO/IEC 29110-5-1-2:2011 — Software Engineering — Lifecycle Profiles for
Very Small Entities (VSEs) — Management and Engineering Guide — Basic Profile
**Governing change request:** CR-001 (issue #1)
**Maintained by:** Jay (MD, `YmBal`) · Refinery.co
**Last updated:** 2026-06-16

---

## Purpose

This folder holds the ISO 29110 Basic Profile work products for the **Alloy release channel**. Because
this repo carries **no application source** — only published binaries and the Sparkle appcast — the
Software Implementation (SI) process here covers the *distribution* deliverable (a correct, verifiable,
auto-updating release), not feature construction. Feature-level 29110 work products live in the
private source repo (`Alloy-native-private/docs/iso29110/`).

## Document set

| File | 29110 process | Work product |
|---|---|---|
| `PM-project-plan.md` | Project Management | Release-channel plan + risk register |
| `SI-requirements-spec.md` | Software Implementation | Distribution requirements (binary + appcast) |
| `VV-verification-validation.md` | Both | Release verification checklist + validation record |
| `CM-configuration-management.md` | Project Management | Release/config management + appcast procedure |
| `../../CHANGELOG.md` | Project Management | Configuration-management change log (WP-CL-ALLOY-REL-001) |

> A standalone traceability matrix is intentionally omitted here: the distribution requirements are
> few and are traced inline in `SI-requirements-spec.md`. Feature traceability is in the source repo
> (`WP-SI-TRC-ALLOY-001`).

## Relationship to the source repo

| Concern | This repo (`alloy-release`) | Source repo (`Alloy-native-private`) |
|---|---|---|
| Code & features | — | Yes (`Sources/`, `chrome/`) |
| Built `.dmg` binaries | Yes (GitHub Releases) | produced by `package.sh` |
| Sparkle appcast feed | Yes (`appcast.xml`) | — |
| Feature CHANGELOG | — | `WP-CL-ALLOY-001` |
| Release CHANGELOG | `WP-CL-ALLOY-REL-001` | — |

## How this set is kept current

- Update these documents when the release procedure, signing/notarization status, the appcast format,
  or the distribution risk register changes — always referencing the governing issue ID.
- Every published release and appcast change is logged in `CHANGELOG.md` (WP-CL-ALLOY-REL-001).
