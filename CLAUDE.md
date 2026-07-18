# CLAUDE.md

Guidance for Claude Code (and future contributors) working in this repo.

## What this is

Paperwork is a Flutter budget/expense tracker, forked from
[Cashew](https://github.com/jameskokoska/Cashew) (GPLv3, credit: James Kokoska). The app itself
lives in `budget/`; everything else at the repo root (`promotional/`, `scripts/`, `LICENSE`) came
over from the same fork. See the README's Fork Notice and `CHANGELOG.md` for what's been changed
since the import.

- Stack: Flutter, Drift (SQL) for local storage, Firebase for auth/sync/backup.
- Entry point: `budget/lib/main.dart`. Most app code is under `budget/lib/`.
- Package name is still `budget` (i.e. imports are `package:budget/...`) - this was not renamed
  because it touches every file in the project; only user-facing branding was changed.

## Standing instructions

- **Always keep `README.md`, `CLAUDE.md`, and `CHANGELOG.md` up to date** when making changes.
  - `README.md`: update the Fork Notice / feature description if the app's identity or
    capabilities change; don't touch the historical "Upstream Release (Cashew)" section, it
    describes the original project, not this fork.
  - `CLAUDE.md`: update this file when the architecture, build process, or working
    conventions change.
  - `CHANGELOG.md`: add a dated entry under a new version heading for any user-visible change,
    following Keep a Changelog style. Bump `version:` in `budget/pubspec.yaml` to match when
    cutting a release.
- Don't rename the `applicationId`/bundle identifier or touch the Firebase project config
  (`budget/android/app/google-services.json`, `budget/.firebaserc`,
  `budget/lib/firebase_options.dart`) without being asked - they're still tied to upstream
  Cashew's Firebase project and changing them silently would break sign-in/sync for anyone
  testing against it.

## Releases

- `.github/workflows/release-apk.yml` builds a release APK with Flutter and attaches it to a
  GitHub Release whenever a tag matching `v*` is pushed.
- The release APK is unsigned (debug-signed) - fine for sideloading/testing, not for a Play
  Store submission. Signing needs a real keystore, which isn't set up yet.
- To cut a release: bump `version:` in `budget/pubspec.yaml`, add a `CHANGELOG.md` entry, commit,
  tag (`git tag vX.Y.Z && git push origin vX.Y.Z`), and the workflow does the rest.

## Local development

Flutter/Android SDKs are not available in this sandboxed environment (outbound network policy
blocks `dl.google.com`, where the Android SDK is fetched from), so builds can't be verified here -
only via CI or on a machine with the full toolchain installed. Double-check Dart syntax carefully
(brace/paren balance, etc.) since there's no local `flutter analyze` to catch mistakes.
