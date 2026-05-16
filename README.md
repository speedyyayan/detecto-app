# Detecto - Android App Detector

A standalone Android Accessibility Service that detects when apps are opened and sends the package name to your Render dashboard.

## Features

- ✅ Runs as an Accessibility Service
- ✅ Detects package name of any app opened on your phone
- ✅ Sends package data to your Render URL via GET request
- ✅ Minimal battery/network overhead
- ✅ Auto-compiles to APK via GitHub Actions

## Setup

### 1. Manual Build Locally

```bash
./gradlew build
./gradlew assembleRelease
```

The APK will be in `app/build/outputs/apk/release/`

### 2. GitHub Actions Auto-Compilation

Every push to this repository will automatically compile the APK.

Check the **Actions** tab to download the compiled APK.

### 3. Installation

1. Download the APK from GitHub Actions or build locally
2. Enable "Installation from Unknown Sources" in your Android Settings
3. Install the APK
4. Go to **Settings > Accessibility > Detecto** and enable it
5. Grant necessary permissions when prompted

## How It Works

1. The app registers as an Accessibility Service
2. It listens for `TYPE_WINDOW_STATE_CHANGED` events
3. When an app window changes, it captures the package name
4. It sends a GET request to: `https://global-remote.onrender.com/update?app=[packageName]`
5. Your Render dashboard receives and processes the data

## Configuration

To change the Render URL, edit:

```java
// app/src/main/java/com/guard/detecto/MyService.java
private static final String RENDER_URL = "https://your-url.onrender.com";
```

## Requirements

- Android 7.0+ (API 24+)
- Target Android 14 (API 34)
- Internet Permission
- Accessibility Service Permission

## Project Structure

```
detecto-app/
├── app/
│   ├── build.gradle
│   ├── proguard-rules.pro
│   └── src/
│       └── main/
│           ├── AndroidManifest.xml
│           ├── java/
│           │   └── com/guard/detecto/
│           │       └── MyService.java
│           └── res/
│               ├── xml/
│               │   └── accessibility_service_config.xml
│               └── values/
│                   ├── strings.xml
│                   └── themes.xml
├── build.gradle
├── settings.gradle
└── README.md
```

## How to Get the APK

1. Navigate to the **Actions** tab in your GitHub repository
2. Click on the latest workflow run
3. Download the `app-release` artifact
4. Extract the ZIP file to get `app-release.apk`

## License

MIT
