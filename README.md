# Wanderlust

**A Personalized Travel Planning and Tracking App**

An Android prototype built with Kotlin and Jetpack Compose for local account registration, destination browsing, and reading prewritten travel itineraries.

> **Project status:** Source-reviewed prototype; a successful build and current device run have not been verified. The checked-in source references missing image resources. See [Build status](#build-status) before attempting to run it.

## Overview

The current implementation contains a local registration/login flow, a catalog of **Bali, Paris, and Singapore**, and a dedicated itinerary screen for each destination. Navigation uses Android activities and explicit intents; account data is handled locally through `SQLiteOpenHelper`.

The project title and report describe a broader personalized travel planning concept. Recommendation algorithms, editable trip plans, and trip tracking are not implemented in the reviewed source.

## Features confirmed in source

These findings describe code that is present; they are not results of a successful runtime test.

| Feature | Verified behavior | Source |
| --- | --- | --- |
| Local registration | Accepts username, email, and password, checks for empty fields, inserts a local user record, and opens the login screen. | [RegisterActivity.kt](app/src/main/java/com/example/travelapp/RegisterActivity.kt) |
| Local login | Looks up a username in SQLite, compares the supplied password, shows validation/error text, and opens the destination catalog on a match. | [LoginActivity.kt](app/src/main/java/com/example/travelapp/LoginActivity.kt), [UserDatabaseHelper.kt](app/src/main/java/com/example/travelapp/UserDatabaseHelper.kt) |
| Destination catalog | Defines three clickable destination cards: Bali, Paris, and Singapore. | [MainActivity.kt](app/src/main/java/com/example/travelapp/MainActivity.kt) |
| Day-by-day itineraries | Displays static text organized into Day 1 through Day 7 sections. Singapore's Day 7 text is unfinished. | [BaliActivity.kt](app/src/main/java/com/example/travelapp/BaliActivity.kt), [ParisActivity.kt](app/src/main/java/com/example/travelapp/ParisActivity.kt), [SingaporeActivity.kt](app/src/main/java/com/example/travelapp/SingaporeActivity.kt) |
| Scrollable Compose screens | Uses Compose layouts, Material components, cards, images, text fields, and vertical scrolling. Image references are present, but their assets are missing from the checkout. | [Application source](app/src/main/java/com/example/travelapp) |

## Implementation scope and limitations

- **Fixed content:** Destination descriptions and itineraries are embedded in the app. The package description and price-like text in the catalog are static sample strings, not live quotes or bookable offers.
- **Local account prototype:** Passwords are stored and compared as plain text. Registration checks only that fields are nonempty; email verification, password recovery, and a secure authentication service are not implemented. The visible "Forget password?" button has an empty handler.
- **No implemented travel integrations:** The reviewed source contains no booking, payment, maps/GPS tracking, personalized recommendation engine, editable/saved itinerary workflow, or cloud synchronization implementation. Broader capabilities discussed in the report are concept-level material.
- **Two persistence approaches are present:** Login and registration use `UserDatabaseHelper`. Room entity, DAO, and database classes also exist, but they are not called by the inspected activity flow. No Room annotation processor is configured in the checked-in Gradle files.
- **Content completeness:** Singapore's final itinerary entry ends mid-sentence. Current UI behavior, older-device compatibility, and accessibility have not been verified on a device.

## Tech stack

| Component | Checked-in configuration |
| --- | --- |
| Language | Kotlin `1.7.0` |
| UI | Jetpack Compose UI/Material `1.2.0`; Compose compiler extension `1.2.0` |
| Android components | AndroidX `ComponentActivity`; activity navigation through explicit intents |
| Active local storage | Android SQLite via `SQLiteOpenHelper` |
| Additional persistence code | Room `2.5.0` dependencies and classes; not integrated into the current login/registration path |
| Build system | Gradle Wrapper `7.5`; Android Gradle Plugin `7.4.1`; Groovy Gradle scripts |
| Android SDK | Minimum `21`; compile `33`; target `33` |
| Java/Kotlin bytecode target | `1.8` |
| App identity | `com.example.travelapp`; version name `1.0`, version code `1` |
| Test dependencies | JUnit `4.13.2`, AndroidX JUnit `1.1.5`, Espresso `3.5.1`, Compose UI test dependency |

Versions come from [build.gradle](build.gradle), [app/build.gradle](app/build.gradle), and [gradle-wrapper.properties](gradle/wrapper/gradle-wrapper.properties).

## Build status

Verification snapshot: **23 October 2026**, against source commit [`3fea03b`](https://github.com/Javith07/Wanderlust-A-Personalized-Travel-Planning-and-Tracking-App/commit/3fea03bcb3a2f8dff92329bc4fdd09f7312146bf), dated 28 April 2023.

| Check | Result |
| --- | --- |
| Source, manifest, Gradle files, tests, and three PDF documents | Inspected. Historical report screenshots were visually reviewed. |
| Debug build attempt | `bash gradlew :app:assembleDebug --no-daemon --console=plain` stopped while downloading Gradle 7.5 with `java.net.SocketException: Network is unreachable`. Compilation was not reached. |
| Review environment | OpenJDK 17 was available; no Android SDK or `adb` installation was found. |
| Static resource inspection | Six referenced drawable names have no definitions in the checked-in resources: `bali`, `paris`, `singapore`, `trav`, `tra`, and `ic_launcher_background`. These need to be restored or their references repaired. |
| CI evidence | No workflow files, workflow runs, check runs, or commit status checks were found for the reviewed source revision. |
| Tests/device run | Not executed. Only the template arithmetic unit test and package-name instrumentation test are present. |

**A passing build is not established.** The network failure is an environment limitation; the missing resources are a separate, confirmed checkout issue. Additional build or runtime issues may become visible after those prerequisites are resolved.

## Setup and run

The steps below describe the configured project and the work needed to attempt a build. They have not been verified end to end.

### 1. Prepare the Android toolchain

- Use Android Studio with support for Android Gradle Plugin `7.4.1`.
- Select **JDK 11** as the Gradle JDK baseline for this legacy toolchain. AGP 7.4 lists JDK 11 and Gradle 7.5 in its [official compatibility table](https://developer.android.com/build/releases/agp-7-4-0-release-notes). The app's `1.8` bytecode target is separate from the JDK used to run Gradle.
- Install Android SDK Platform **33**, SDK Platform-Tools, and the SDK Build-Tools required by AGP. AGP 7.4 lists Build-Tools `30.0.3` as its default; the project does not override that version.
- Provide access to the Gradle distribution, Google Maven, Maven Central, and Gradle Plugin Portal for the initial sync.
- Configure the SDK path in Android Studio or an uncommitted `local.properties` file.

### 2. Clone and open the project

```bash
git clone https://github.com/Javith07/Wanderlust-A-Personalized-Travel-Planning-and-Tracking-App.git
cd Wanderlust-A-Personalized-Travel-Planning-and-Tracking-App
```

Open this repository root in Android Studio, where `settings.gradle` and `build.gradle` are located. The Gradle project is named `Travel App` and contains the `app` module. `Travel-Plan-App-master` is an empty file in the reviewed revision, not another project directory.

### 3. Restore missing resources

Recover the original images or repair the references for these resource names before attempting to launch the app:

- `bali`, `paris`, `singapore`: destination images used by the catalog and itinerary screens.
- `trav`, `tra`: images used by login and registration.
- `ic_launcher_background`: background referenced by the adaptive launcher icons.

Place restored drawable resources under an appropriate `app/src/main/res/drawable...` directory using valid Android resource names. Also validate launcher icon coverage for the declared minimum SDK: the checked-in launcher mipmap XML files only have API 26 and API 33 variants.

### 4. Sync and attempt a debug build

After configuring the SDK/JDK and repairing resources, sync the project in Android Studio and run:

**macOS/Linux**

```bash
bash gradlew :app:assembleDebug
```

**Windows PowerShell**

```powershell
.\gradlew.bat :app:assembleDebug
```

If successful, the expected debug APK path is `app/build/outputs/apk/debug/app-debug.apk`.

### 5. Run and check the app flow

Start an emulator or connect an Android device, select the `app` run configuration, and press **Run** in Android Studio. An API 33 emulator is a reasonable first verification target; support down to API 21 is declared but untested.

The launcher activity is `LoginActivity`. The source-defined flow is:

1. Open **Register** and enter disposable local test credentials.
2. Return to **Login** and sign in with the same username/password.
3. Select Bali, Paris, or Singapore in the destination catalog.
4. Scroll through the destination's fixed itinerary.

No backend endpoint or API-key setup is referenced by this activity flow. Its behavior still needs to be checked after a successful build.

### 6. Validate after build restoration

```bash
bash gradlew :app:testDebugUnitTest :app:lintDebug
bash gradlew :app:connectedDebugAndroidTest
```

The second command requires a running emulator or connected device. On Windows, use `.\gradlew.bat` in place of `bash gradlew`. Existing tests are Android Studio template checks; they do not verify registration, login, navigation, or itinerary content.

## Screenshots

Historical screenshots are embedded in the [project report](Wanderlust-Documentation.pdf), pages **4-7**. They are documentation evidence, not captures from a verified build of the current checkout.

| Screen | Existing report evidence | Current-build screenshot placeholder |
| --- | --- | --- |
| Login | Page 4 | Pending: add a capture after build restoration. |
| Registration | Page 5 | Pending: add a capture after build restoration. |
| Destination catalog | Page 6 | Pending: add a capture after build restoration. |
| Bali itinerary | Page 7 | Pending: add a capture after build restoration. |
| Paris itinerary | No dedicated screenshot found in the report. | Pending: add a capture after build restoration. |
| Singapore itinerary | No dedicated screenshot found in the report. | Pending: add a capture after build restoration. |

No standalone screenshot image files are included in the reviewed repository. Add verified captures before replacing these placeholders with image links.

## Documentation

| Document | Contents and evidence notes |
| --- | --- |
| [Project report](Wanderlust-Documentation.pdf) | Nine pages: project concept, embedded empathy map (page 2), ideation material (page 3), historical UI screenshots (pages 4-7), and narrative discussion. Broader feature descriptions do not establish implementation. |
| [Brainstorming board](brainstrom.pdf) | One-page ideation export covering travel considerations such as budget, time, safety, interests, and prioritization; some template prompts remain. The filename is preserved as committed. |
| [Standalone empathy map export](empathy%20map.pdf) | The one-page standalone PDF rendered as a blank gray area during review. Use the visible embedded empathy map on page 2 of the project report for the available design evidence. |

## Source guide

| Area | Location |
| --- | --- |
| App module and dependencies | [app/build.gradle](app/build.gradle) |
| Launcher and activity declarations | [AndroidManifest.xml](app/src/main/AndroidManifest.xml) |
| Login and registration | [LoginActivity.kt](app/src/main/java/com/example/travelapp/LoginActivity.kt), [RegisterActivity.kt](app/src/main/java/com/example/travelapp/RegisterActivity.kt) |
| Destination catalog | [MainActivity.kt](app/src/main/java/com/example/travelapp/MainActivity.kt) |
| Destination itineraries | [BaliActivity.kt](app/src/main/java/com/example/travelapp/BaliActivity.kt), [ParisActivity.kt](app/src/main/java/com/example/travelapp/ParisActivity.kt), [SingaporeActivity.kt](app/src/main/java/com/example/travelapp/SingaporeActivity.kt) |
| Active local user database | [UserDatabaseHelper.kt](app/src/main/java/com/example/travelapp/UserDatabaseHelper.kt) |
| Additional Room classes | [User.kt](app/src/main/java/com/example/travelapp/User.kt), [UserDao.kt](app/src/main/java/com/example/travelapp/UserDao.kt), [UserDatabase.kt](app/src/main/java/com/example/travelapp/UserDatabase.kt) |
| Shared Compose theme | [ui/theme](app/src/main/java/com/example/travelapp/ui/theme) |
| Tests | [Local unit tests](app/src/test/java/com/example/travelapp), [instrumentation tests](app/src/androidTest/java/com/example/travelapp) |

## License

No license file is included in the reviewed repository; reuse permissions are not specified here.
