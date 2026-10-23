# Architecture and app flow

## Observed user flow

```text
LoginActivity (launcher)
  ├── Register button → RegisterActivity
  │                        └── Save to local SQLite → LoginActivity
  └── Successful local login → MainActivity
                                  ├── Bali card → BaliActivity
                                  ├── Paris card → ParisActivity
                                  └── Singapore card → SingaporeActivity
```

The flow is inferred from the code paths and `AndroidManifest.xml`, **not confirmed by executing the app**.

## UI layer

- Kotlin activities use Jetpack Compose with `setContent { ... }`.
- `MainActivity` renders a vertically scrollable list of destination cards.
- Individual destination activities render images and static itinerary descriptions.
- Navigation uses Android `Intent` rather than Compose Navigation.

## Data layer

```text
RegistrationScreen / LoginScreen
          |
          v
  UserDatabaseHelper
  (SQLiteOpenHelper)
          |
          v
    UserDatabase.db
       user_table
```

The helper defines columns `id`, `first_name`, `last_name`, `email`, and `password`. Login selects rows using `first_name` as the username.

A separate Room entity/DAO/database set exists in the source, but no confirmed login or registration path calls it. These should not be presented as an integrated Room architecture.

## Data flow and security observations

- The form currently passes raw password text into local storage and compares it directly at login.
- Registration inserts a user without confirmed duplicate checking, email format validation, or password policy.
- The "Forget password?" control in `LoginActivity` has an empty click handler.
- The local user flow does not establish production authentication or an online backend.

## Source map

| Area | Files |
| --- | --- |
| Launcher and navigation declarations | `app/src/main/AndroidManifest.xml` |
| Auth screens | `LoginActivity.kt`, `RegisterActivity.kt` |
| Active local database helper | `UserDatabaseHelper.kt` |
| Alternative Room classes | `User.kt`, `UserDao.kt`, `UserDatabase.kt` |
| Destination selection and guides | `MainActivity.kt`, `BaliActivity.kt`, `ParisActivity.kt`, `SingaporeActivity.kt` |

Paths to Kotlin classes are relative to `app/src/main/java/com/example/travelapp/`.
