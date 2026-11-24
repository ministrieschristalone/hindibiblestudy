# Changelog — शिष्यता रोडमेप (Shishyata Roadmap)

All notable changes to the APK. Content-only updates (text/audio/video)
are **not** listed here — they ship through the GitHub `manifest.json`
pipeline and never touch the APK.

---

## [1.0.0] — 2026-11-24 (Play-Store-ready)

First complete release build. Signed with release keystore
(see `SIGNATURE.md` — local only, never published to GitHub).

### Added — App
- 4 bottom tabs: **उद्देश्य** (default) · **विश्वास** · **रोडमेप** · **प्रगति**
- उद्देश्य screen with exact aim text + scripture references (no scroll)
- विश्वास: view-only statement of faith (12 declarations, 3 sections)
- रोडमेप: 3-level curriculum (भाग → गोला → उप-विषय → nested) with
  ⬜→🟡→✅ tap progression, x/y parent badges, breadcrumbs
- प्रगति: progress report across the curriculum
- Settings: Light/Dark · 3-level font size · रीसेट
- Light theme default, dark toggle

### Added — Remote content pipeline (no rebuild ever needed)
- `manifest.json` auto-fetch from GitHub raw on launch + 🔄 refresh button
- Offline cache fallback → bundled copy fallback (3-layer)
- Stable slug keys per topic for permanent content linking
- 📝🎧🎬 badges on every leaf (grey = "coming soon")
- In-app text modal, in-app audio mini-player, in-app video overlay
  (direct MP4 or YouTube embed — never leaves the app)
- **🎬 परिचय** pill (centered, white) on roadmap screen → plays
  `roadmap.overview` intro video in-app
- Content propagates to users within ~5 minutes of a GitHub commit

### Fixed — YouTube player (2026-11-24, on-device report)
- **Error 153 "Video player configuration error":** since Sep 2025 YouTube
  requires an `HTTP Referer` on embed requests; `file://` pages send none.
  The bundled HTML now loads with an https base URL (`loadDataWithBaseURL`)
  so the iframe request carries `Referer: https://org.shishyataroadmap.app/`
  (Google's documented method + Referer format for side-loaded apps)
- Swallow non-http(s) schemes (`intent://`, `market://`, …) in the WebView —
  the player's "Watch video on YouTube" button can no longer show the
  "Web page not available / ERR_UNKNOWN_URL_SCHEME" error page
- Enable third-party cookies for the YouTube player session
- One-time note: the WebView storage origin changed (`file://` →
  `https://org.shishyataroadmap.app/`), so progress/edits made before this
  build reset once — content itself is unaffected (fetched from GitHub)

### Fixed — Security audit (2026-11-24, SAST + DAST + Android layer)
- **HIGH:** added missing `android.permission.INTERNET` — without it the
  manifest fetch and YouTube player silently failed on real devices
- **MEDIUM:** replaced debug keystore signing with release keystore
  (`CN=Christ Alone Ministries`, valid to 2054) — required for Play Store
- MainActivity: `setMediaPlaybackRequiresUserGesture(false)` so in-app
  video autoplays on tap

### Security posture (verified)
- 0 hardcoded secrets · 0 dangerous functions · all manifest data escaped
  (compromised GitHub content cannot execute code)
- HTTPS only, no cleartext, single exported activity, minimal permissions
- Remaining accepted LOWs: `allowBackup=true` (progress restore feature),
  dev-only preview-server headers → **enable 2FA on GitHub account**

### Changed
- भाग A restructured: 4 circles (परमेश्वर विषय अध्ययन 0/16 · परमेश्वर का
  वचन 0/6 · परमेश्वर के लोग 0/20 · परमेश्वर का कैलेंडर 0/3) incl.
  "Jesus as King" sub-topic
- Roadmap overview transcript text ships as `roadmap.overview.text`

### Planned (pre-Play-Store)
- Bump `targetSdkVersion` 34 → 35+ to meet Google Play's target-API
  rule for new apps (found by the Android APK audit module)

---

## Pre-release (superseded)

- **2026-11-22** — initial curriculum build, debug-signed
  (`Roadmap.apk` / early `Shishyata_Roadmap.apk`). Uninstall before
  installing any release build (signature mismatch).
