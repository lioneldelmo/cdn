# DASHDOT

**Morse Code Radio for iOS & Android**

[![Expo](https://img.shields.io/badge/Expo-54.0.33-000000?style=flat&logo=expo&logoColor=00FF41)](https://expo.dev)
[![React Native](https://img.shields.io/badge/React_Native-0.81.5-000000?style=flat&logo=react&logoColor=00FF41)](https://reactnative.dev)
[![JavaScript](https://img.shields.io/badge/JavaScript-ES2022-000000?style=flat&logo=javascript&logoColor=00FF41)](https://developer.mozilla.org/en-US/docs/Web/JavaScript)
[![License: MIT](https://img.shields.io/badge/License-MIT-000000?style=flat&logoColor=00FF41)](LICENSE)

---

DashDot turns any two smartphones into a Morse code radio. One device **transmits** text as camera flash pulses — the other **receives** and decodes the flashes back into text in real time. No internet. No Bluetooth. Just light.

---

## Features

| | Feature | Description |
|---|---|---|
| **TX** | Flash Transmission | Camera torch pulses International Morse Code |
| **TX** | Vibration Sync | Haptic motor mirrors every dot and dash |
| **TX** | Live Preview | Scrollable Morse pattern before you send |
| **TX** | Adjustable Speed | 60–200 ms unit time (4–20 WPM range) |
| **RX** | Camera Decoding | ~12 frames/sec brightness sampling via `takePictureAsync` |
| **RX** | Two-Step Calibration | Dark baseline + bright baseline → midpoint threshold |
| **RX** | Live Signal Bar | Real-time brightness meter with threshold marker |
| **RX** | Decoded Terminal | Scrolling output with blinking cursor |
| **App** | In-App Guide | Swipeable 6-slide tutorial, always accessible via `?` |
| **App** | OLED Design | Pure black + terminal green aesthetic, SpaceMono font |

---

## How It Works

### Transmitting (TX)

1. Type your message in the input field
2. Set transmission speed with the slider
3. Tap **TRANSMIT** — the camera flash pulses Morse code while the vibration motor syncs each signal

The timing follows the **1 : 3 : 7 ratio** (ITU standard):

| Element | Duration |
|---------|----------|
| Dot | 1 × unit |
| Dash | 3 × unit |
| Element gap | 1 × unit |
| Letter gap | 3 × unit |
| Word gap | 7 × unit |

### Receiving (RX)

1. Tap **RX ▶** in the HomeScreen header
2. Calibrate: cover the camera (SAMPLE DARK), then point at the sender's torch (SAMPLE BRIGHT)
3. Tap **RECEIVE** — decoded text appears in real time

**How decoding works:**

- `takePictureAsync({ quality: 0.01, base64: true, skipProcessing: true })` is called in a loop targeting ~80 ms/frame
- Brightness is estimated from the base64 JPEG data: the middle third of the string is sampled, character codes (range 43–122) are averaged and normalized to 0–1
- A three-state machine (`IDLE → SIGNAL_ON → SIGNAL_OFF`) classifies each edge:
  - **Falling edge:** ON duration < 2× speed → dot, ≥ 2× speed → dash
  - **Rising edge from OFF:** gap ≥ 5× speed → flush char + space; gap ≥ letterGap → flush char
- Minimum decodable speed: **150 ms** (camera polling latency limit)

---

## Getting Started

### Prerequisites

- **Node.js** 18+
- **Expo CLI** — `npm install -g expo-cli`
- **Expo Go** app on a physical iOS or Android device (simulator has no camera)

### Install & Run

```bash
git clone https://github.com/your-username/dashdot.git
cd dashdot
npm install
npx expo start --clear
```

Scan the QR code with Expo Go (Android) or the Camera app (iOS).

### Build for Production

```bash
# iOS
eas build --platform ios

# Android
eas build --platform android
```

Requires an [Expo EAS](https://expo.dev/eas) account.

---

## Architecture

```
dashdot/
├── src/
│   ├── components/
│   │   ├── GhostCamera.js       — Hidden CameraView for torch control (iOS workaround)
│   │   ├── MorseDisplay.js      — Scrollable live Morse preview strip
│   │   ├── TextInputArea.js     — Message input with character counter
│   │   ├── TransmitButton.js    — Animated circular TX button
│   │   ├── StatusBar.js         — Active character + symbol highlight during TX
│   │   └── SpeedSlider.js       — PanResponder drag slider (60–200 ms)
│   ├── hooks/
│   │   ├── useMorseTransmitter.js  — TX loop, cancelRef, torch + vibration sync
│   │   └── useMorseReceiver.js     — RX poll loop, state machine, calibration
│   ├── screens/
│   │   ├── HomeScreen.js        — TX UI (preview, input, speed, transmit button)
│   │   ├── ReceiverScreen.js    — RX UI (camera, calibration, terminal, controls)
│   │   ├── OnboardingScreen.js  — First-launch swipeable intro (6 slides)
│   │   └── GuideScreen.js       — Persistent in-app guide (same slides, goBack)
│   ├── store/
│   │   └── useMorseStore.js     — Zustand store (TX state + RX state)
│   └── constants/
│       ├── morse.js             — MORSE_DICT, REVERSE_MORSE_DICT, decodeSymbol()
│       └── theme.js             — COLORS, FONTS, SPACING, RADIUS
├── assets/
│   └── fonts/SpaceMono-Regular.ttf
├── index.js                     — registerRootComponent(App)
├── src/App.js                   — Navigation stack (Onboarding → Home → Receiver / Guide)
├── app.json                     — Expo config, camera permissions
└── package.json
```

---

## Tech Stack

| Layer | Library | Version |
|-------|---------|---------|
| Framework | Expo (managed) | 54.0.33 |
| Runtime | React Native | 0.81.5 |
| Language | JavaScript | ES2022 (strict mode) |
| Camera / Torch | expo-camera | 17.0.10 |
| Haptics | expo-haptics | 15.0.8 |
| State | Zustand | 4.5.7 |
| Navigation | @react-navigation/native-stack | 7.3.21 |
| Styling | NativeWind (Tailwind) + StyleSheet | 4.1.23 |
| Storage | @react-native-async-storage | 2.2.0 |
| Font | expo-font (SpaceMono) | 14.0.11 |

---

## Morse Code Reference

| Char | Code | | Char | Code | | Char | Code |
|------|------|-|------|------|-|------|------|
| A | `·−` | | J | `·−−−` | | S | `···` |
| B | `−···` | | K | `−·−` | | T | `−` |
| C | `−·−·` | | L | `·−··` | | U | `··−` |
| D | `−··` | | M | `−−` | | V | `···−` |
| E | `·` | | N | `−·` | | W | `·−−` |
| F | `··−·` | | O | `−−−` | | X | `−··−` |
| G | `−−·` | | P | `·−−·` | | Y | `−·−−` |
| H | `····` | | Q | `−−·−` | | Z | `−−··` |
| I | `··` | | R | `·−·` | | | |

| Digit | Code | | Digit | Code |
|-------|------|-|-------|------|
| 0 | `−−−−−` | | 5 | `·····` |
| 1 | `·−−−−` | | 6 | `−····` |
| 2 | `··−−−` | | 7 | `−−···` |
| 3 | `···−−` | | 8 | `−−−··` |
| 4 | `····−` | | 9 | `−−−−·` |

---

## Design Decisions

**Ghost Camera pattern** — On iOS, the torch can only be controlled through a mounted `CameraView`. DashDot mounts the camera view absolutely behind the UI with a near-opaque overlay, making it invisible to the user while keeping torch access alive.

**Base64 brightness heuristic** — Decoding a JPEG frame in JavaScript at 12 fps would be too slow. Instead, DashDot samples the middle third of the raw base64 string. At quality 0.01, the JPEG DC coefficients dominate and correlate strongly with overall luminance — good enough for flash detection without any pixel decoding.

**Ref-based hot loop** — The receiver state machine runs entirely in `useRef` values (`stateRef`, `signalStartRef`, `symbolBufRef`). Zustand setters are only called for UI-visible updates (brightness bar, signal dot, terminal text) to avoid React re-renders in the tight polling loop.

**Calibration over fixed threshold** — A fixed brightness threshold would fail in different lighting environments and across device cameras. The two-step calibration (dark sample → bright sample → midpoint) makes the receiver device-agnostic and environment-agnostic.

---

## License

MIT © 2026 [LLD](mailto:dashdot@delmo.net)
