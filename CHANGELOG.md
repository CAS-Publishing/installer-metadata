# Changelog

All notable changes to this package will be documented in this file.

## [0.0.2-preview.23] - 2026-06-29

- Firebase `pluginFiles` (libFirebaseCpp*.a) so migrate auto-removes the native Plugins libs (new #8).

## [0.0.2-preview.22] - 2026-06-29

- Mark CAS config `adFormats` so the installer offers ad-format + audience/network controls (#4.5).

## [0.0.2-preview.21] - 2026-06-29

- Mark CAS managerId config rows `editable` so the installer's Configuration tab can edit them inline (#2.1b).

## [0.0.2-preview.20] - 2026-06-29

- **CAS-ID validation hints:** declare per-platform `regex` + `hint` on the CAS `config` rows
  (Android bundle / iOS numeric) so the installer's Welcome validation is catalog-driven.

## [0.0.2-preview.19] - 2026-06-29

- **CAS pin → 4.7.4:** bump CAS `recommendedVersion` and git tag from 4.7.0 to the current stable 4.7.4.
  Aligns the hub install with CAS's own stable channel (no more pointless in-CAS update nag, #4.3) and
  picks up CAS's signature fix, clearing the "Missing signature" warning that came from 4.7.0 (#5).

## [0.0.2-preview.18] - 2026-06-23

- **Tenjin `legacyAssetFiles` — runtime scripts.** Adds signatures for the SDK's RUNTIME scripts
  (`BaseTenjin.cs`, `Tenjin.cs`, `AndroidTenjin.cs`, `IosTenjin.cs`, `DebugTenjin.cs`,
  `Tenjin*Integration.cs`), each matched by name + content signature. Migrating a manual Tenjin
  install moved to a NON-standard path (e.g. `Assets/Scripts/Core/Tenjin`) now removes its scripts
  too — previously only editor/build helpers were covered, so the runtime scripts were left behind
  and collided with the UPM package. Needs installer ≥ 0.0.1-preview.24.

## [0.0.2-preview.17] - 2026-06-22

- **Tenjin `legacyAssetFiles`** — declares the SDK files the manual `.unitypackage` scatters outside
  `Assets/Tenjin` (`BuildPostProcessor.cs`, `Dependencies.xml`, `TenjinAssetSelector/EditorPrefs/Packager.cs`),
  each matched by name + content signature, so migrating a manual Tenjin to UPM removes them too.
  Needs installer ≥ 0.0.1-preview.23 (which reads the field).

## [0.0.2-preview.16] - 2026-06-22

- **Hotfix: Tenjin pin `1.15.14-psv.1` → `1.15.14-psv.2`.** psv.1 was missing
  `Plugins/iOS/TenjinSDK.xcframework.zip` (the iOS SDK binary) — `upm pack` silently dropped it.
  psv.2 is re-signed via `upm sign` + `npm pack` so the binary ships; same two source patches.

## [0.0.2-preview.15] - 2026-06-22

- Tenjin SDK pinned to PSV fork **1.15.14-psv.1** (`minVersion`/`recommendedVersion`/git `tag`):
  PackageCache-safe iOS post-build path (`Path.GetFullPath`) + editor types moved to the
  `TenjinEditor` namespace (drops the `Tenjin` namespace/class collision). Runtime API unchanged.
  Registry (`com.tenjin.sdk@1.15.14-psv.1`, signed) and GitHub mirror tag both live.

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
