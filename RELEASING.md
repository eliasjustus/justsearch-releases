# Releasing

Release runbook for JustSearch. This repo (`justsearch-releases`) hosts
public-facing release artifacts; the build itself is driven from the
(currently private) main source repo.

## Tag namespaces

| Prefix | Purpose | Example |
|---|---|---|
| `v<semver>` | App releases — Windows installer | `v0.1.0-alpha` |
| `models-*` | Model asset bundles consumed by the app's "Install AI" flow | `models-v1` |

Model asset releases are long-lived and treated as **immutable** — the
app's `model-registry.v2.json` hard-codes asset URLs by tag, so
renaming or deleting a model tag breaks installed clients. To ship a
new model set, publish a new tag (`models-v2`, `models-2026-04`, etc.)
and update the registry in lockstep.

Changelog (`CHANGELOG.md`) tracks **app releases only**. Model release
notes live on the individual tag pages.

## App release runbook

1. **Bump version**: update `version=` in the main repo's
   `gradle.properties`.
2. **Propagate**: run `scripts/ci/sync-version.ps1` — propagates to
   `tauri.conf.json`, shell `package.json`, `Cargo.toml`.
3. **Local gate**: `./gradlew.bat build` then `.\scripts\gate.ps1`.
4. **Build installer**: `.\scripts\ci\package-installer-win.ps1`
   (omit `-Release` until a code-signing cert is available — the
   `-Release` flag requires `JUSTSEARCH_CODESIGN_*` env vars).
5. **Capture SHA-256**: hash the produced `*-setup.exe`.
6. **Changelog**: in this repo, move `[Unreleased]` content to a new
   version heading in `CHANGELOG.md` with today's date.
7. **Release notes**: draft the release body. Required sections:
   - Quick summary / what changed
   - Download link
   - SHA-256 verify instructions (both PowerShell and `certutil`)
   - SmartScreen expectation (unsigned installer will be warned by
     Windows; users verify via SHA-256)
   - Install-AI step and approximate download size
   - Log file paths for bug reports
     (`%APPDATA%\io.justsearch.shell\logs\`)
   - Known limitations
8. **Publish**: create a GitHub release against the new tag, attach
   the installer + a combined `SHA256SUMS.txt` covering every asset
   in the release.
9. **Prerelease flag**: mark as prerelease until the version leaves
   `-alpha` / `-beta` / `-rc`.
10. **Latest flag**: set `make_latest=true` so `/releases/latest` and
    `/releases/latest/download/<asset>` resolve to this release.
11. **Attribution check**: verify `THIRD_PARTY_NOTICES.txt` still
    covers everything bundled in the installer.

## Model asset release runbook

1. **Build / quantize** models in the main repo under `models/`. See
   `scripts/models/` for reproducible build scripts.
2. **Compute SHA-256** for every file (`model.onnx`, `model_fp16.onnx`,
   tokenizers, configs).
3. **Update** `modules/ui/src/main/resources/ai/model-registry.v2.json`
   with the new URLs + hashes, pointing at the unreleased tag.
4. **Smoke test**: run the app's Install AI flow against a local
   fixture to confirm the manifest resolves cleanly.
5. **Publish**: create a GitHub release against the new `models-*`
   tag, attach all assets + one combined `sha256sums-models.txt`.
6. **Mark prerelease** (asset bundles are not user-facing "latest").
7. **Release body**: required sections — included models table (name,
   purpose, source HF URL, license), modification notices under
   Apache-2.0 §4(b) where applicable, compat note, SHA verify
   instructions, link to `THIRD_PARTY_NOTICES.txt`.
8. **Coordinate** app build + model tag — ship an app release that
   bumps the manifest to the new tag.

## What this repo does not do

- No codesigning yet — installers ship unsigned. SmartScreen warning
  is expected; the SHA-256 verify path is the authenticity story.
- No auto-update channel — users download manually per release.
- No macOS / Linux builds — Windows-only.

## When in doubt

Tempdoc 409 (main repo `docs/tempdocs/409-releases-repo-audit-and-rework.md`)
records the audit that produced this runbook and the reasoning behind
each convention.
