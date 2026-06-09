# Changelog

All notable changes to this package will be documented in this file.

## [0.0.2-preview.9] - 2026-05-27

- Tenjin SDK (`com.tenjin.sdk`) recommended version pinned to **1.15.14** (was 1.16.3).

## [0.0.2-preview.8] - 2026-05-26

- **Default Tenjin component is now the raw `com.tenjin.sdk`** (registry `psv`,
  `com.tenjin` scope), replacing the `com.psvgamestudio.tenjin` wrapper — the
  wrapper is deferred to a later release. Pairs with installer ≥ 0.0.1-preview.11.

## [0.0.2-preview.7] - 2026-05-25

- Added per-platform post-install **config requirements** (CAS / Tenjin / Firebase)
  for the installer's Configuration readiness checklist.

## [0.0.2-preview.6] - 2026-05-22

- **Track packaging-fix republishes for analytics / remoteconfig.**
  `com.psvgamestudio.analytics` bumped 0.0.1-preview.2 → 0.0.1-preview.3
  and `com.psvgamestudio.remoteconfig` bumped 0.0.1-preview.1 →
  0.0.1-preview.2 — both republished to ship Unity `.meta` files that
  were missing from the previous tarballs. Catalog now points at the
  fixed versions so installer clients pick them up.

## [0.0.2-preview.1] - 2026-05-21

- **CAS external entry fixes.** UPM package id corrected from `com.cleversolutions.ads.mediation` to the real OpenUPM name `com.cleversolutions.ads.unity`. Added `minVersion: "4.5.4"` (lowest version seen in PSV client projects — `rainbow-high-beauty-salon`) and `recommendedVersion: "4.7.0"` (current OpenUPM latest as of 2026-05-18). With these the migrator can now plan an `AddPackage` for CAS instead of just registering the scope.
- `catalogVersion` bumped to `0.0.2-preview.1`.

## [0.0.1-preview.1] - 2026-05-21

- First preview release — published to Verdaccio for installer self-bootstrap.
- Installer (`com.psvgamestudio.installer`) now detects absence of this package on first run, ensures the PSV scoped registry in `manifest.json`, and installs this version via UPM `Client.Add` without requiring a manual `manifest.json` edit.

## [0.0.1] - 2026-05-21

- Phase 1 skeleton: package manifest, schema for `catalog.json`, registries block.
- CAS external entry pointing at OpenUPM.
- No PSV package records yet — to be populated from existing Verdaccio packages.
