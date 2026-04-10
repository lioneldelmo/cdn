# Device Inspector

Device diagnostics app built with Expo.

## Expo Support

The default runtime target is Expo Go. Features not supported in Expo Go are skipped gracefully.

- Supported in Expo Go: device info, battery/disk data, tracking permission status, JSON export/share.
- Skipped in Expo Go: direct advertising identifier retrieval (IDFA/AAID).

## Run With Expo Go (default)

1. Install dependencies:

```bash
npm install
```

2. Start Expo:

```bash
npm start
```

3. Open in Expo Go on iOS/Android.

## Optional Dev Client Path

If you later need native-only features, use Expo Dev Client and keep those features isolated from the Expo Go path.

- This repository currently does not enable native ad ID retrieval by default.
- Add native dependencies only in a separate Dev Client branch or feature flag to preserve Expo Go compatibility.