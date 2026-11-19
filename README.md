# 🐛️ Thebugsmith's Morphe Patches

Patch source for [Morphe](https://morphe.software), the patcher for Android apps.

[![Add to Morphe](.github/assets/add-to-morphe.svg)](https://morphe.software/add-source?github=thebugsmith/bugsmith-morphe-patches)

## Supported apps

<!-- PATCHES_START EXPANDED -->
> **[v1.0.0](https://github.com/thebugsmith/bugsmith-morphe-patches/releases/tag/v1.0.0)**&nbsp;&nbsp;•&nbsp;&nbsp;`main`&nbsp;&nbsp;•&nbsp;&nbsp;5 patches total
<details open>
<summary>📦 Chessbook&nbsp;&nbsp;•&nbsp;&nbsp;1 patch</summary>
<br>

**Package name:** `com.chessbook.android`

**🎯 Supported versions:**

| 1.3.54 |
| :---: |

| 💊&nbsp;Patch | 📜&nbsp;Description | ⚙️&nbsp;Options |
|----------|----------------|-----------|
| [Chessbook local gates](#chessbook-local-gates) | Remove local move admission/locks, skip optional onboarding account/link prompts and disable automatic OTA. Server auth/billing and explicit login remain unchanged. |  |

</details>

<details open>
<summary>📦 Pingo&nbsp;&nbsp;•&nbsp;&nbsp;3 patches</summary>
<br>

**Package name:** `com.picoai.languageapp.android`

**🎯 Supported versions:**

| 5.4.8 |
| :---: |

| 💊&nbsp;Patch | 📜&nbsp;Description | ⚙️&nbsp;Options |
|----------|----------------|-----------|
| [Pingo Google login](#pingo-google-login) | Replaces the signature-bound GMS Google Sign-In with a browser OAuth code flow (PKCE) against the app's own installed-app OAuth client so Google login works on a re-signed build. |  |
| [Pingo Google login (manifest)](#pingo-google-login-manifest) | Registers the OAuth redirect activity and its com.googleusercontent.apps intent filter so the browser-based Google login can receive the authorization code. |  |
| [Pingo Premium](#pingo-premium) | Unlocks premium features by bypassing Superwall paywall checks. |  |

</details>

<details open>
<summary>🌐 Universal&nbsp;&nbsp;•&nbsp;&nbsp;1 patch</summary>
<br>

| 💊&nbsp;Patch | 📜&nbsp;Description | ⚙️&nbsp;Options |
|----------|----------------|-----------|
| [Remove ads and trackers](#remove-ads-and-trackers) | Stops the ad, analytics and crash-reporting SDKs an app contains and drops the advertising ID. Universal: apps without those SDKs patch untouched. | • Ads<br>• Analytics and crash reporting<br>• Advertising ID |

</details>

<!-- PATCHES_END -->

### Patch details

- **Remove ads and trackers** (universal) - works on any app; each SDK is looked up first and skipped when missing, so an app without ads still patches cleanly. Options: **Ads** stubs the start-up and ad-request entry points of AdMob, AppLovin MAX, Unity Ads, Pangle, Meta Audience Network, InMobi, ironSource/LevelPlay, Vungle, Mintegral, myTarget and BIGO; **Analytics and crash reporting** turns off Firebase Analytics and Crashlytics, the Facebook SDK, AppMetrica, AppsFlyer and the Play install referrer, and sets the WebView metrics opt-out; **Advertising ID** drops `AD_ID` / `ACCESS_ADSERVICES_AD_ID` and disables Firebase's ad-ID collection. Options are applied at patch time - there is no in-app menu.
- **Pingo Premium** - bypasses the Superwall paywall (`Entitlement.isActive`), the Pairip installer check (`performLocalInstallerCheck`) and the login gate (`IdentityManager.isLoggedIn`).
- **Pingo Google login** - replaces the signature-bound GMS Google Sign-In with a browser OAuth 2.0 code flow (PKCE) against the app's own installed-app OAuth client, so login works on a re-signed build. Requires **Pingo Google login (manifest)**, which registers the redirect activity and its `com.googleusercontent.apps` intent filter.
- **Chessbook local gates** - removes local move admission limits and repertoire locks, skips the optional onboarding account/link prompts, and disables automatic OTA updates so the patched JS bundle is not overwritten. Server-side auth, billing and explicit login are untouched.

