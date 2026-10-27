# Device Inspector

**A production-ready React Native diagnostic utility for developers.** Extract hardware identifiers, system diagnostics, and export comprehensive device reports with a beautiful glassmorphic interface.

**Version:** 1.0.0  
**Built with:** Expo SDK, React Native, Pure JavaScript  
**Platforms:** iOS & Android (Expo Go compatible)

---

## ✨ What's New in Version 1.0.0

### Core Features

#### 🔐 **Identity Vault**
- IDFA (iOS) / AAID (Android) retrieval with permission handling
- Android ID and IDFV (iOS) identifiers
- Bundle ID / Package Name
- Tracking permission status
- Install Referrer (Android)

#### ⚡ **Power Lab**
- Real-time battery percentage with color-coded health indicator
- Charging state detection (On Battery, Charging, Full)
- Low Power Mode status (iOS)

#### 💾 **Storage Analyst**
- Visual disk usage breakdown with progress bar
- Free, used, and total storage in GB
- Real-time storage monitoring

#### 📱 **Hardware Module**
- Device name (Android), model, brand, and manufacturer
- Total RAM in MB
- Device year class estimation
- Physical device detection

#### 🖥️ **Device Details**
- System uptime (formatted as days/hours)
- Product name (Android)
- Installation and last update timestamps

#### 📶 **Network & Connectivity**
- Connection type (WiFi, Cellular, None)
- Internet reachability status
- IP address display
- Airplane mode toggle (Android)
- SSID (Android)

#### 📡 **Carrier & SIM** (Android)
- Carrier name with MCC/MNC codes
- ISO country code
- VoIP capability status

#### 🔒 **Security & Lock Status**
- Device lock status
- Biometric authentication availability (Face ID, Touch ID, fingerprint)

#### 🌍 **Locale & Region**
- Language and region codes
- Timezone information
- Currency code
- 24-hour clock and metric system preferences

#### 📐 **Screen Technical Details**
- Screen resolution and window size
- Pixel ratio and font scale
- Display metrics for responsive design

#### 🛠️ **Deep Diagnostics (Developer Mode)**
- CPU architecture(s)
- OS build fingerprint (Android)
- Internal build ID (Android)
- Platform API level (Android)
- *Unlocked by tapping "OS Version" label 7 times*

#### 📤 **One-Touch Export**
- Generate timestamped JSON reports
- Share via native share sheet (AirDrop, Email, etc.)
- Complete diagnostic snapshot included

### UI/UX Enhancements

- **Glassmorphism Design:** Frosted glass cards with subtle highlights
- **System-aware Theming:** Dark/Light mode with System preference override
- **Copy-on-Tap:** Long-press any value to copy to clipboard (with toast feedback)
- **Smooth Animations:** Spring-based drawer, animated theme transitions
- **Responsive Layout:** Safe area support, landscape-friendly
- **Interactive Drawer:** Quick access to About, Privacy, Tutorials, and theme settings
- **Loading States:** Prevents UI freezing during async hardware polls

### Comprehensive Modals

- **About Modal:** Feature overview with 9+ diagnostic categories
- **Privacy Policy:** Data collection & usage transparency
- **Tutorials:** Step-by-step guides for all major features
- **Tracking Permission Alert:** Smart permission request UI

---

## 🚀 Quick Start

### Run With Expo Go (Default)

1. **Install dependencies:**
   ```bash
   npm install
   ```

2. **Start the development server:**
   ```bash
   npm start
   ```

3. **Scan the QR code** with Expo Go (iOS) or the Expo app (Android).

### Expo Support

Device Inspector is fully compatible with Expo Go. Features are gracefully degraded when unsupported:

| Feature | Expo Go | Dev Client |
|---------|---------|-----------|
| Device Info | ✅ Full | ✅ Full |
| Battery & Disk | ✅ Full | ✅ Full |
| Tracking Permission | ✅ Full | ✅ Full |
| IDFA/AAID Retrieval | ⚠️ N/A | ✅ Full |
| JSON Export & Share | ✅ Full | ✅ Full |

---

## 📦 Dependencies

**Strictly managed to avoid conflicts:**

- `expo-device` — Hardware/model info
- `expo-application` — App IDs and versions
- `expo-battery` — Power diagnostics with real-time listeners
- `expo-tracking-transparency` — IDFA permission & retrieval
- `expo-file-system` — JSON file generation
- `expo-sharing` — Native share sheet integration
- `expo-network` — Network state and IP address
- `expo-localization` — Locale, timezone, and regional preferences
- `expo-cellular` — Carrier and SIM information
- `expo-local-authentication` — Biometric hardware detection
- `expo-constants` — Environment detection (Expo Go vs. Dev Client)
- `react-native-safe-area-context` — Notch & edge support

---

## 🎯 Key Features by Platform

### iOS Specific
- IDFA retrieval with App Tracking Transparency permission
- IDFV (Identifier for Vendor)
- Secure Enclave / biometric type detection

### Android Specific
- AAID (Google Advertising ID)
- Android ID (16-character device identifier)
- Install Referrer tracking
- API Level and platform details
- Product name from build

---

## 🛠️ Developer Mode

**Unlock the Deep Diagnostics card:**
1. Navigate to the Software card
2. Tap the "OS Version" row exactly **7 times**
3. A developer badge and diagnostics card will appear

The Deep Diagnostics card includes:
- CPU architecture(s)
- OS Build Fingerprint (Android)
- Internal Build ID (Android)
- Platform API Level (Android)

---

## 📋 Permissions & Privacy

**This app respects user privacy:**
- ✅ No data is transmitted to external servers
- ✅ All diagnostics are read locally
- ✅ No analytics or tracking libraries
- ✅ IDFA/AAID shown locally only (not sent anywhere)
- ✅ User controls JSON report sharing via native UI

**Required Permissions:**
- `ACCESS_NETWORK_STATE` (Android) — Network diagnostics
- `READ_PHONE_STATE` (Android) — Carrier information
- `NSUserTrackingUsageDescription` (iOS) — IDFA access
- `NSLocalNetworkUsageDescription` (iOS) — Network diagnostics

---

## 🎨 UI Architecture

### Design System
- **Glassmorphism:** Cards with 0.06 opacity backgrounds and subtle borders
- **Dark Mode:** `#0A0A0F` background with `rgba(255,255,255,0.06)` cards
- **Light Mode:** `#EFF3FB` background with `rgba(255,255,255,0.80)` cards
- **Accent Color:** System blue (iOS) / Cyan (Android fallback)

### Component Hierarchy
- `LoadingScreen` — Initial loading with pulsing animation
- `GlassCard` — Reusable card container with highlight effect
- `CopyableRow` — Label-value pair with clipboard & toast feedback
- `BatteryBar` — Visual battery indicator with color states
- `StorageBar` — Segmented disk usage visualization
- `AboutModal`, `PrivacyModal`, `TutorialsModal` — Information modals
- `TrackingPermissionModal` — Permission request UI
- Animated drawer with theme selector

---

## 🔧 Optional Dev Client Path

For advanced native features beyond Expo Go, create an Expo Dev Client build:

```bash
expo prebuild --clean
eas build --platform ios --profile preview
```

This enables:
- Full IDFA/AAID retrieval in all scenarios
- Advanced biometric data
- Kernel version details
- Enhanced device lock status

---

## 📝 Export Format

JSON exports include:

```json
{
  "exportedAt": "2026-04-18T...",
  "device": { "name", "model", "brand", "manufacturer", "totalMemoryMB" },
  "identity": { "advertisingId", "bundleId", "trackingPermission" },
  "power": { "batteryLevel", "batteryState", "lowPowerMode" },
  "storage": { "totalGB", "freeGB", "usedGB" },
  "software": { "osName", "osVersion", "appVersion" },
  "localization": { "locale", "timezone", "currency" },
  "screen": { "screenResolution", "pixelRatio", "fontScale" },
  "deviceDetails": { "deviceType", "uptimeFormatted" },
  "deepDiagnostics": { "cpuArchitectures", "osBuildFingerprint" } // Dev mode only
}
```

---

## 🧪 Testing Tips

- **Copy-on-Tap:** Long-press any value for ~0.4s
- **Dev Mode:** Quickly tap "OS Version" 7 times (counter shows progress)
- **Theme Toggle:** Use hamburger menu → Appearance selector
- **Dark/Light:** Automatic with system, or override manually
- **Export:** Tap "Share JSON Report" to trigger native share

---

## 🐛 Known Limitations

- **Unsupported data is hidden, never shown as a placeholder.** Rows whose value the OS doesn't provide are not rendered.
- **iOS:** Device name (iOS 16+ returns a generic name), SSID, and Carrier & SIM (CTCarrier deprecated in iOS 16) are not shown.
- **Bootloader status:** Not exposed by any public iOS or Android API, so it isn't shown.
- **IDFA/AAID:** Requires permission grant or returns 'N/A in Expo Go'

---

## 📄 License

Built as a specialized developer utility for hardware diagnostics.

---

## 🚀 Performance Notes

All hardware queries are **fully asynchronous** with loading states to prevent UI blocking. The app uses:
- `Promise.all()` for parallel data fetching
- Real-time event listeners (battery, network)
- Memoized color schemes (no re-renders on theme toggle)
- Efficient storage calculations
- Platform-specific APIs for reliability
---

## 🍎 App Store Review Info

Copy/paste values for the App Store Connect listing.

### 1) Promotional Text (max 170 chars)

```
Instantly see your IDFA, device IDs, battery health, storage, and hidden system details. Export a full JSON diagnostic report in one tap.
```

### 2) Description (max 4000 chars)

```
Device Inspector is a fast, beautiful diagnostic tool that reveals the hard-to-find details about your iPhone, all in one place.

IDENTITY VAULT
• Advertising Identifier (IDFA) with App Tracking Transparency permission handling
• Identifier for Vendor (IDFV) and Bundle ID

POWER LAB
• Real-time battery percentage with color-coded health indicator
• Charging state and Low Power Mode status

STORAGE ANALYST
• Visual progress bar showing used vs. free disk space
• Total, used, and free storage in GB

HARDWARE & SOFTWARE
• Device model, brand, total RAM, and device class
• OS name, version, and app version
• System uptime and install time

NETWORK & SECURITY
• Connection type, reachability, and IP address
• Passcode lock and biometric availability (Face ID / Touch ID)

LOCALE & SCREEN
• Language, region, timezone, and currency
• Screen resolution, pixel ratio, and font scale

DEVELOPER MODE
Tap the OS Version label 7 times to unlock Deep Diagnostics: CPU architecture and build details.

ONE-TOUCH EXPORT
Generate a timestamped JSON report and share it via AirDrop, Messages, Mail, or any app on the share sheet.

COPY-ON-TAP
Long-press any value to copy it to your clipboard instantly.

DESIGNED FOR iOS
• Glassmorphism design with automatic Dark and Light mode
• Smooth, native-feeling animations
• Asynchronous hardware polling, so the UI never freezes

PRIVACY FIRST
All diagnostics are read locally on your device and are never uploaded. You control when a report is shared. The app is supported by ads; the advertising ID is only requested with your permission.

Perfect for developers, QA testers, IT support, and anyone curious about what's inside their device.
```

### 3) Keywords (max 100 chars, comma-separated)

```
device info,idfa,aaid,hardware,diagnostics,battery,storage,developer,device id,system info,specs
```

### 4) Support URL

```
https://cdn.delmo.net/device-inspector/
```

### 5) Marketing URL

```
https://cdn.delmo.net/device-inspector/
```

### 6) Copyright

```
© 2026 Lionel Delmo
```
