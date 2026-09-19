# Oxgram

An unofficial, open-source Telegram client for Android — a fork of the official
Telegram app, customized and built independently.

> ⚠️ **Disclaimer**: Oxgram is not affiliated with or endorsed by Telegram.
> All messaging is powered by the official Telegram API. Use at your own risk.

_Last updated: September 19, 2026_

## Features

- Everything from the official Telegram Android client (chats, channels, calls, stickers, etc.)
- Custom Oxgram branding and theme
- More features coming soon — contributions welcome!

## Download

APKs are built automatically by GitHub Actions.

[![Build Oxgram APK](https://github.com/OxClub/oxgram/actions/workflows/build.yml/badge.svg)](https://github.com/OxClub/oxgram/actions/workflows/build.yml)

1. Open the **Actions** tab above
2. Click the latest successful run
3. Scroll to **Artifacts** and download `oxgram-apk`
4. Install on your Android device (allow "install from unknown sources")

## Building from source

### Requirements
- Android Studio 2025.1.4 or newer
- JDK 17
- Android NDK 27.2.12479018
- Android SDK 36

### Steps
```bash
git clone --recursive https://github.com/OxClub/oxgram.git
cd oxgram
```

1. Open the project in Android Studio and let it sync Gradle
2. Fill in your `api_id` and `api_hash` in
   `TMessagesProj/src/main/java/org/telegram/messenger/BuildVars.java`
   (get them free at https://my.telegram.org → API Development Tools)
3. Build → Make Project, or from the terminal:
   ```bash
   ./gradlew assembleAfatDebug
   ```

The APK will be in `TMessagesProj/build/outputs/apk/`.

## CI

Every push to `main` automatically builds an APK via GitHub Actions
(see `.github/workflows/build.yml`). You can also trigger a build manually
from the Actions tab.

## Contributing

1. Fork the repository
2. Create a feature branch: `git checkout -b feature/my-feature`
3. Commit your changes and push
4. Open a Pull Request

CI will build an APK from your branch so it can be tested before merging.

## Roadmap

- [x] CI builds on every push
- [ ] Oxgram branding (name, icon, theme)
- [ ] Custom features (see FEATURES_GUIDE.md)
- [ ] Release signing + F-Droid / GitHub Releases distribution

## License

GPL-2.0 — same as the official Telegram Android app this project is forked from.
Your changes must remain open source under the same license.

See `LICENSE` for the full text.
