# PSV Installer Metadata

Data-only UPM package consumed by `com.psvgamestudio.installer`. Carries the live catalog of every PSV / CAS package the installer manages — npm ids, legacy npm ids, legacy `Assets/` paths to clean up, registries, categories, and version policy.

> **Status:** phase 1 skeleton — schema and the CAS external entry only; no PSV package records yet.

## Why this lives in a separate package

The installer pulls this package as a UPM dependency and **also checks Verdaccio for a newer version on Unity load**, auto-updating it silently. So new packages and migration rules reach client projects without releasing a new installer.

## `catalog.json` schema

```jsonc
{
  "schemaVersion": 1,
  "catalogVersion": "x.y.z",
  "registries": {
    "psv":     "https://npm.psvgamestudio.com/",
    "openupm": "https://package.openupm.com"
  },
  "categories": [
    { "id": "core", "displayName": "Core" }
  ],
  "packages": [
    {
      "id":                  "com.psvgamestudio.<name>",
      "displayName":         "PSV <Name>",
      "registry":            "psv",
      "category":            "core",
      "legacyNpmIds":        ["com.psv.<name>"],
      "legacyAssetPaths":    ["Assets/PSV/<Folder>"],
      "minVersion":          "1.0.0",
      "recommendedVersion":  "1.2.0"
    }
  ],
  "external": [
    {
      "id":          "com.cleversolutions.ads.mediation",
      "registry":    "openupm",
      "scopes":      ["com.cleversolutions"],
      "category":    "ad"
    }
  ],
  "overrides": {}
}
```

## Field semantics

| Field | Purpose |
|---|---|
| `legacyNpmIds` | Old npm ids the scanner searches for in the client's `manifest.json`. Match means "migrate to the new id". |
| `legacyAssetPaths` | Folder paths under `Assets/` the scanner looks for. Match means "legacy `.unitypackage` install detected — needs migration". |
| `minVersion` | If installed version < this, the UI shows a strong warning. |
| `recommendedVersion` | If installed version < this, the UI shows a soft suggestion. |
| `external` | Packages from other registries (e.g. CAS on OpenUPM). The installer registers their scopes in the client's manifest. |
| `overrides` | Reserved for edge cases that cannot be described declaratively. |
