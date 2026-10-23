# Setup, run, and verification guide

> **Status:** Instructions are based on checked-in configuration. Running the application successfully was **not** verified.

## Prerequisites

- Android Studio with support for Android Gradle Plugin **7.4.1** and Kotlin **1.7.0**.
- A compatible JDK (JDK **11** is the usual baseline for AGP 7.4.x).
- Android SDK Platform **33** installed for the configured `compileSdk`.
- Emulator or Android device running **API level 21+**.
- Internet access for the first Gradle dependency sync.

## Clone and open

```bash
git clone https://github.com/Javith07/Wanderlust-A-Personalized-Travel-Planning-and-Tracking-App.git
cd Wanderlust-A-Personalized-Travel-Planning-and-Tracking-App
```

Open this root directory in Android Studio, not just the `app` subfolder. Let Gradle load the `:app` module.

## Fix source-tree blockers first

1. `app/src/main/res/values/strings.xml` contains bare text lines (`destination 01`, `destination 02`, `destination 03`) directly inside `<resources>`. These are not valid Android string resource entries. Remove them or convert them to XML comments.
2. Kotlin code references `R.drawable.bali`, `R.drawable.paris`, `R.drawable.singapore`, `R.drawable.trav`, and `R.drawable.tra`. Those named image assets were not found in the inspected repository tree. Supply **appropriately licensed** images with matching resource names, or update the code to point to actual resources.
3. Sync Gradle again. Resolve any additional compile or dependency errors reported by the IDE. Do not assume these are the only build blockers.

## Attempt a debug build

macOS/Linux:

```bash
./gradlew assembleDebug
```

Windows:

```powershell
.\gradlew.bat assembleDebug
```

If the build succeeds, select the `app` run configuration and run on an API 21+ emulator or device.

## Manual test checklist (NOT yet verified)

- [ ] Registration view opens from Login.
- [ ] Register a disposable **test-only** account.
- [ ] Return to Login and sign in using the same local credentials.
- [ ] Wrong login credentials show an error.
- [ ] Bali, Paris, and Singapore cards open the expected destination screen.
- [ ] Seven-day itinerary text scrolls correctly.
- [ ] App launches correctly after restart.

**Security:** The current helper stores passwords without hashing. Use only dummy test data, never any real/reused password.

## Reporting test results

After validating the project, record Android Studio version, JDK version, emulator/device/API level, build output, actual test results, and dated screenshots in a new test log. Do not mark the checklist above completed without running it.
