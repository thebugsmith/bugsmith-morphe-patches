# 🐛️ Thebugsmith's Morphe Patches

Patch source for [Morphe](https://morphe.software), the patcher for Android apps.

[![Add to Morphe](.github/assets/add-to-morphe.svg)](https://morphe.software/add-source?github=thebugsmith/bugsmith-morphe-patches)

## Supported apps

<!-- PATCHES_START EXPANDED -->

| App | Package | Version | Patches |
|-----|---------|:-------:|---------|
| Pingo — Language Learning: Pingo AI | `com.picoai.languageapp.android` | 5.4.8 | • Pingo Premium<br>• Pingo Google login<br>• Pingo Google login (manifest) |
| Chessbook — Master openings | `com.chessbook.android` | 1.3.54 | • Remove Move Limits |

<!-- PATCHES_END -->

### Patch details

- **Pingo Premium** - bypasses the Superwall paywall (`Entitlement.isActive`), the Pairip installer check (`performLocalInstallerCheck`) and the login gate (`IdentityManager.isLoggedIn`).
- **Pingo Google login** - replaces the signature-bound GMS Google Sign-In with a browser OAuth 2.0 code flow (PKCE) against the app's own installed-app OAuth client, so login works on a re-signed build. Requires **Pingo Google login (manifest)**, which registers the redirect activity and its `com.googleusercontent.apps` intent filter.
- **Chessbook local gates** - removes local move admission limits and repertoire locks, skips the optional onboarding account/link prompts, and disables automatic OTA updates so the patched JS bundle is not overwritten. Server-side auth, billing and explicit login are untouched.

