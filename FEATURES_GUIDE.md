# Oxgram — CI Setup & Feature Development Guide

## 1. What you got in this zip

```
oxgram_ci/
└── .github/
    └── workflows/
        └── build.yml      # GitHub Actions workflow that builds your APK
```

## 2. How to use it

1. Copy the `.github` folder into the ROOT of your forked Telegram repo
   (the folder that contains `settings.gradle`, `gradlew`, `TMessagesProj/`).
2. Commit and push to GitHub:
   ```bash
   git add .github
   git commit -m "Add CI build workflow"
   git push
   ```
3. Go to your repo on GitHub -> **Actions** tab -> watch the build run.
4. When it finishes, open the workflow run -> **Artifacts** -> download `oxgram-apk`.

You can also trigger it manually: Actions -> "Build Oxgram APK" -> "Run workflow".

## 3. Requirements in your repo (already satisfied by the official fork)

- JDK 17 (installed by the workflow)
- Android SDK 36, NDK 27.2.12479018, CMake 3.22.1 (installed by the workflow)
- Your `api_id` / `api_hash` filled into `TMessagesProj/src/main/java/org/telegram/messenger/BuildVars.java`

## 4. Build variants you can swap in

| Command | Result |
|---|---|
| `./gradlew assembleAfatDebug` | Universal debug APK (default in workflow) |
| `./gradlew assembleAfatRelease` | Universal release APK (needs real keystore + google-services.json) |
| `./gradlew assembleArm64Release` | Smaller APK, arm64 devices only |

## 5. Adding your own features

The codebase is large; here is where things live:

| What you want to change | Where to look |
|---|---|
| App name / branding | `TMessagesProj/src/main/res/values/strings.xml` (`AppName`) |
| Launcher icon | `TMessagesProj/src/main/res/mipmap-*/` |
| Theme / colors | `TMessagesProj/src/main/java/org/telegram/ui/ActionBar/Theme.java` |
| Chat list screen | `org/telegram/ui/DialogsActivity.java` |
| Chat / message bubbles | `org/telegram/ui/ChatActivity.java`, `org/telegram/ui/Cells/ChatMessageCell.java` |
| Settings screen | `org/telegram/ui/ProfileActivity.java`, `SettingsActivity.java` |
| New message handling | `org/telegram/messenger/NotificationCenter.java`, `MessagesController.java` |

### Safe workflow for each feature
1. Create a branch: `git checkout -b feature/my-feature`
2. Make small, isolated changes — one feature per branch
3. Push -> CI builds an APK automatically -> test the artifact on your phone
4. Merge to `main` when it works

### Beginner-friendly first features
1. Change default theme color in `Theme.java` (search for the blue `0xff` color constants)
2. Hide/show UI elements in `DialogsActivity` (e.g., remove the "Stories" row)
3. Change the app name and icon to Oxgram branding
4. Add a new entry in Settings that opens a simple info screen

## 6. Before publishing (important)

- Replace the dummy `release.keystore` with your own, store it as a GitHub Secret
  (`OXGRAM_KEYSTORE_BASE64`), and use the commented-out release block in the workflow
- Add your own `google-services.json` (Firebase) for release builds
- The fork is GPL-licensed: keep your source public under GPL
- Brand it clearly as "Oxgram — unofficial client", not as official Telegram
