# Changelog

All notable changes to Paperwork (this fork) are documented in this file.
Upstream Cashew's own history is in its [commits](https://github.com/jameskokoska/Cashew/commits/main)
and [changelog](https://github.com/jameskokoska/Cashew/blob/main/budget/lib/widgets/showChangelog.dart).

## [1.0.0] - 2026-07-18

Initial release of Paperwork, forked from [Cashew](https://github.com/jameskokoska/Cashew) v5.4.3.

- Imported the full Cashew source tree (GPLv3) as the starting point for this app.
- Default currency is now always INR, regardless of device locale.
- Default theme is black and white: seeded the Material color scheme with black instead of
  upstream's blue, disabled dynamic system color, and defaulted to dark mode.
- Default home page layout: wallet cards, expense/income summary, spending graph, then the
  transactions list. Pinned budgets are hidden by default.
- Bottom navigation is now a floating, icon-only rounded pill instead of an edge-to-edge bar.
- Renamed the app to "Paperwork" (app label, web title/manifest) and reset versioning to 1.0.0.
- Added a GitHub Actions workflow that builds a release APK and attaches it to a GitHub
  Release whenever a `v*` tag is pushed.

### Known limitations

- The release APK is unsigned (debug-signed) - fine for sideloading, not for a Play Store
  submission.
- The Android `applicationId` / iOS bundle identifier and Firebase project are still
  upstream Cashew's own - they need to be swapped for our own before shipping any
  account/sync features.
- In-app copy (About page, store links, translations) still references Cashew in a few
  places; only the app label/title and top-level branding were updated for this release.
