# HabitStat Android releases

Public OTA channel for HabitStat (sideload APK).

## Manifest (in-app update)

```
https://raw.githubusercontent.com/0xakki/habitstat-release/main/version.json
```

## Latest APK

- [habitstat-latest.apk](https://github.com/0xakki/habitstat-release/raw/main/apk/habitstat-latest.apk)

## How updates work

1. App fetches `version.json`
2. If remote `versionCode` > installed build, user is prompted
3. Download opens the `downloadUrl` APK
4. If the manifest has a `sha256` field, the app verifies the downloaded APK's
   SHA-256 against it before invoking the installer. This is the only
   integrity check standing between an authentic release and a swapped-in
   APK if this repo/account is ever compromised — **do not skip it.**

## Cutting a release

Every release **must** publish a `sha256` field alongside `downloadUrl` in
both `version.json` and `ota.json`. The app treats a missing/empty `sha256`
as "no checksum available" and falls back to size + ZIP-magic checks only —
so skipping this step silently disables tamper detection for that release.

1. Build and sign the APK as usual, copy it into `apk/`.
2. Compute its SHA-256:
   - Windows: `certutil -hashfile apk\habitstat-<version>.apk SHA256`
   - Git Bash / Linux / macOS: `sha256sum apk/habitstat-<version>.apk`
   (Recompute once and diff against the first run before publishing — a
   fumbled copy-paste here defeats the whole check.)
3. Update `version.json` and `ota.json` together:
   - `version`, `versionCode`, `downloadUrl` — as before
   - `sha256` — the lowercase hex digest from step 2
   - `releaseNotes`, `publishedAt`
4. Commit and push. Do not publish `downloadUrl` without a matching `sha256`.

Do **not** put secrets in this repo. Only signed public APKs + version feed.
