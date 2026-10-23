# Features — implementation-verified inventory

This document distinguishes features supported by inspected source code from features that cannot currently be claimed.

## Confirmed in source

| Feature | Implementation evidence | Scope |
| --- | --- | --- |
| Local user registration | `RegisterActivity.kt` and `UserDatabaseHelper.insertUser` | Collects username, email, password; inserts a record |
| Local login | `LoginActivity.kt` and `UserDatabaseHelper.getUserByUsername` | Retrieves a saved user by username and compares passwords |
| Form feedback | `LoginActivity.kt`, `RegisterActivity.kt` | Displays empty-field/login feedback |
| Browse destinations | `MainActivity.kt` | Clickable cards for Bali, Paris, Singapore |
| Bali itinerary | `BaliActivity.kt` | Hard-coded day-by-day travel text |
| Paris itinerary | `ParisActivity.kt` | Hard-coded day-by-day travel text |
| Singapore itinerary | `SingaporeActivity.kt` | Hard-coded day-by-day travel text |
| Activity navigation | `AndroidManifest.xml`, activity `Intent` calls | Login/register/main/destination activities |

The destination cards also display static copy from `strings.xml` such as a seven-day/two-person label and a budget claim; neither is a dynamic calculation.

## Present in source but not used in confirmed screen flows

- `User.kt` contains a Room-annotated user entity.
- `UserDao.kt` defines suspend database operations.
- `UserDatabase.kt` defines a Room database builder.
- The current login and registration activities instead instantiate `UserDatabaseHelper` (SQLiteOpenHelper).

These files demonstrate **data-layer exploration**, not proof that the Room pathway is active.

## Not confirmed / not implemented in inspected app flows

- Dynamic or personalized itinerary generation.
- Live GPS trip tracking, visited-place check-ins, or progress tracking.
- Maps, routing, booking, payments, weather, or API integration.
- Cloud authentication, account synchronization, or password reset.
- Persisted user-created travel plans or itinerary editing.
- Complete tested build / verified runtime behavior.

The repository's longer title expresses the project concept. Public descriptions should reflect what the source actually shows.

## Source references

- [MainActivity.kt](../app/src/main/java/com/example/travelapp/MainActivity.kt)
- [LoginActivity.kt](../app/src/main/java/com/example/travelapp/LoginActivity.kt)
- [RegisterActivity.kt](../app/src/main/java/com/example/travelapp/RegisterActivity.kt)
- [UserDatabaseHelper.kt](../app/src/main/java/com/example/travelapp/UserDatabaseHelper.kt)
- [BaliActivity.kt](../app/src/main/java/com/example/travelapp/BaliActivity.kt)
- [ParisActivity.kt](../app/src/main/java/com/example/travelapp/ParisActivity.kt)
- [SingaporeActivity.kt](../app/src/main/java/com/example/travelapp/SingaporeActivity.kt)
