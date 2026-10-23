# Known issues, limitations, and verification status

Reviewed from the public source tree on **23 October 2026**. Items labeled **source-observed** can be seen in code or repository contents; their runtime impact was not independently tested.

| Area | Finding | Evidence / impact |
| --- | --- | --- |
| Android resource XML | **Source-observed:** `strings.xml` contains raw `destination 01/02/03` text lines not wrapped in valid resource elements/comments | Likely blocks Android resource compilation |
| Image assets | **Source-observed:** referenced drawables `bali`, `paris`, `singapore`, `trav`, `tra` do not appear in repository tree | Likely unresolved `R.drawable` references |
| Credentials | **Source-observed:** `UserDatabaseHelper` saves and reads password text without a password hash | Unsafe for production; test with dummy credentials only |
| Login validation | **Source-observed:** username lookup then direct string equality; no account lockout or secure auth controls | Prototype-only flow |
| Registration validation | **Source-observed:** only checks for non-empty fields, with no confirmed unique-username/email constraints | Invalid/duplicate account data may be accepted |
| Password recovery | **Source-observed:** "Forget password?" button has an empty click handler | Not implemented |
| Trip personalization | **Not found in reviewed flows:** plans are hard-coded for three destinations | Do not claim personalized planning |
| Trip tracking | **Not found in reviewed flows:** no location/progress tracking | Do not claim live travel tracking |
| Room | **Source-observed:** Room classes exist, while the actual auth screens use SQLiteOpenHelper | Do not call Room the active auth persistence layer |
| Automated tests | **Source-observed:** example template unit/instrumented tests exist | No evidence that app scenarios have been tested |
| Build | **Unverified:** no Android build executed in this review | Additional defects could exist |
| PDF documents | **Unverified contents:** linked PDFs exist but their contents were not read as part of this update | Do not attribute extra functionality to them |
| Screenshots | **Unverified:** no run screenshots supplied | Use placeholders, not fabricated captures |

## Suggested improvement order

1. Repair the XML resources and restore properly licensed images.
2. Establish a reproducible debug build and run through real device/emulator tests.
3. Replace plaintext password storage and direct matching with a secure authentication design before handling any personal accounts.
4. Add proper input validation, user uniqueness handling, and a real recovery flow (or remove the inactive button).
5. Consolidate the database approach if Room is intended to be used.
6. Implement and test personalization/tracking before advertising those features.

## Current state

This documentation does **not** certify that the repository builds, runs, or passes testing. No Kotlin app source files were changed by this documentation-only update.
