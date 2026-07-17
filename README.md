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

Do **not** put secrets in this repo. Only signed public APKs + version feed.
