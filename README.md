# Offswitch

Minimalist Android app: plays white noise when opened, keeps playing in the background (even after swiping away from recents), stops when you tap "Stop" on the notification. UI: black screen with "Zzzz" in the center.

## Prerequisites

1. **Java 11+** (JDK) - Set `JAVA_HOME` or have `java` on your `PATH`.
   - For this project, Java 11 is used (Java 17+ also works).
   - If you have Java 25, you may need to use Java 11/17 instead due to Kotlin compatibility.

2. **Android SDK** - Required for building Android apps.
   - Install Android Studio (includes SDK), or
   - Install command-line tools: https://developer.android.com/studio#command-tools
   - Set `ANDROID_HOME` environment variable, or
   - Create `local.properties` in project root with: `sdk.dir=/path/to/android/sdk`

## Build and run

1. Ensure prerequisites are installed (see above).
2. Build the debug APK:
   ```bash
   ./gradlew assembleDebug
   ```
   Output: `app/build/outputs/apk/debug/app-debug.apk`
3. Install on a device or emulator:
   ```bash
   adb install -r app/build/outputs/apk/debug/app-debug.apk
   ```
   Then open "Offswitch" from the launcher.

## Sideloading (manual distribution)

To build a self-signed APK for direct installation on a device:

```bash
./gradlew assembleDebug
```

Output: `app/build/outputs/apk/debug/app-debug.apk`

The debug build is automatically signed with the local debug keystore (`~/.android/debug.keystore`), which is sufficient for sideloading.

**Install via ADB:**
```bash
adb install -r app/build/outputs/apk/debug/app-debug.apk
```

**Install manually:** Transfer the APK to the device and open it. Requires *Install unknown apps* enabled for the file manager or browser used to open it.

## Behavior

- **Open app** → White noise starts; black screen with "Zzzz".
- **Send to background** → Keeps playing (foreground notification).
- **Swipe app from recents** → Keeps playing.
- **Stop** action on the notification → Stops white noise and exits.
