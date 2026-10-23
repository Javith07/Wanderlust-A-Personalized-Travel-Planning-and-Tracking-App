# Technology stack and configuration

Values below are transcribed from the existing repository source. They are **configured values**, not proof of a successful build.

| Component | Verified configuration | Source |
| --- | --- | --- |
| Primary language | Kotlin | `*.kt` files |
| Android Gradle Plugin | 7.4.1 | Root `build.gradle` |
| Kotlin Android plugin | 1.7.0 | Root `build.gradle` |
| Gradle wrapper | 7.5 | `gradle/wrapper/gradle-wrapper.properties` |
| Jetpack Compose UI | 1.2.0 | Root `build.gradle` |
| Compose compiler extension | 1.2.0 | `app/build.gradle` |
| Compose Material | 1.2.0 | `app/build.gradle` |
| compileSdk / targetSdk | 33 / 33 | `app/build.gradle` |
| minSdk | 21 | `app/build.gradle` |
| Application ID | `com.example.travelapp` | `app/build.gradle` |
| AndroidX Activity Compose | 1.3.1 | `app/build.gradle` |
| AndroidX Core KTX | 1.7.0 | `app/build.gradle` |
| AndroidX Lifecycle Runtime KTX | 2.3.1 | `app/build.gradle` |
| Room common / KTX | 2.5.0 | `app/build.gradle` |
| Unit / instrumentation test deps | JUnit 4.13.2, AndroidX test, Espresso, Compose UI test | `app/build.gradle` |
| Local account storage used by screens | Android SQLiteOpenHelper | `UserDatabaseHelper.kt` |

## Important distinctions

**Jetpack Compose** is actively used for the screen UI. **Android Activity and Intent** are used for navigation.

**SQLiteOpenHelper** is used for registration/login. Room entity, DAO, and database classes are present, but the reviewed screen code does not call them; do not describe this app as using Room for its active authentication flow.

There is no verified Firebase integration, remote REST API, cloud database, Maps SDK, third-party booking service, or real-time tracking implementation in the inspected code.

## Reproducibility

The wrapper and dependency versions describe a 2023-era Android configuration. A recent Android Studio version may require compatibility work. A clean build has not been performed as part of this documentation update.
