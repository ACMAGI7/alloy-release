# alloy-release

Public distribution channel for **Alloy** — the Claude-powered native macOS browser. This repo holds
**release artifacts only** (signed DMGs + the Sparkle **appcast** feed).

---

## What this repo is for

- Hosting downloadable **`Alloy-<version>.dmg`** builds (via GitHub Releases).
- Serving the **Sparkle appcast** (`appcast.xml`) that the in-app updater polls so existing installs
  can auto-update.
- Publishing **release notes** per version.

## Download & install

1. Grab the latest **`Alloy-<version>.dmg`** from the [Releases](../../releases) page.
2. Open the DMG and drag **Alloy** onto **Applications**.
3. **First launch (until the build is notarized):** macOS Gatekeeper may block an unsigned build.
   Either right-click `Alloy.app` → **Open**, or run:
   ```
   xattr -dr com.apple.quarantine /Applications/Alloy.app
   ```
   Full steps are in the app's `INSTALL.md`.

> A signed + notarized build (no Gatekeeper steps) and live Sparkle auto-update ship once the Apple
> Developer ID is in place.

## Auto-update (Sparkle)

The app reads its update feed from the raw `appcast.xml` in this repo (or its Pages/CDN mirror).
Each released version adds one `<item>` with the build's version, DMG URL, length, and EdDSA
signature. See [`docs/iso29110/CM-configuration-management.md`](docs/iso29110/CM-configuration-management.md)
for the appcast format and release procedure.

## Requirements

macOS 13 (Ventura) or newer · Apple Silicon (M1/M2/M3/M4).

## Repository layout

| Path | What it is |
|---|---|
| `appcast.xml` | Sparkle update feed (one `<item>` per release) — *added with the first published build* |
| GitHub Releases | The actual `.dmg` binaries + release notes |
| `CHANGELOG.md` | Release log (`WP-CL-ALLOY-REL-001`) |
| `docs/iso29110/` | ISO/IEC 29110 Basic Profile work products for the release channel |

## Governance — ISO/IEC 29110

This repo follows the **ISO/IEC 29110-5-1-2 Basic Profile**, scaled to a distribution channel. The
work products are in [`docs/iso29110/`](docs/iso29110/) and releases are logged in
[`CHANGELOG.md`](CHANGELOG.md) (doc-id `WP-CL-ALLOY-REL-001`). Adoption is governed by **CR-001**
(issue #1). Releases follow the procedure in the configuration-management plan and are verified
against the checklist in the verification & validation record before being published.

## License & ownership

Alloy is proprietary — © Refinery.co (ACMAGI7). All rights reserved. Distribution of the binaries is
permitted only through this official channel.
