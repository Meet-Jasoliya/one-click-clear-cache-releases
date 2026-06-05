# One Click Clear Cache — Releases

This repository hosts the OTA (over-the-air) update manifest and APK releases for the **One Click Clear Cache** Android app.

---

## How It Works

The app checks `update.json` on startup (silently, in background). If `build_number` in this file is higher than the installed app's build number, an **update dialog** is shown to the user.

The user can:
- **Download** the new APK directly inside the app
- **Install** it immediately via Android's package installer
- Or tap **Later** to skip (if not mandatory)

---

## Publishing a New Release

### Step 1 — Build the APK

```bash
flutter build apk --release --build-name=X.Y.Z --build-number=N
# Output: build/app/outputs/flutter-apk/app-release.apk
```

> Replace `X.Y.Z` with new version and `N` with next build number.
> Also update `kCurrentBuildNumber` in `lib/core/services/update_service.dart`.

### Step 2 — Create a GitHub Release

1. Go to: https://github.com/Meet-Jasoliya/one-click-clear-cache-releases/releases/new
2. Tag: `vX.Y.Z` (e.g. `v1.1.0`)
3. Title: `vX.Y.Z — What changed`
4. Upload `app-release.apk` as a release asset
5. Publish release

### Step 3 — Update `update.json`

Edit this file and push:

```json
{
  "version": "X.Y.Z",
  "build_number": N,
  "download_url": "https://github.com/Meet-Jasoliya/one-click-clear-cache-releases/releases/download/vX.Y.Z/app-release.apk",
  "release_notes": "• What's new in this version\n• Bug fixes",
  "mandatory": false
}
```

> Set `"mandatory": true` to force users to update (dialog can't be dismissed).

### Step 4 — All Done!

Every installed device will see the update dialog the next time they open the app. ✅

---

## Files

| File | Purpose |
|------|---------|
| `update.json` | Update manifest checked by all installed apps |
| `app-release.apk` (in Releases) | The downloadable APK asset |

---

*Created by MEET JASOLIYA*
