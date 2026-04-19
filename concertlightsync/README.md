# Concert Light Sync

![Version](https://img.shields.io/badge/version-1.0.5-FF6B00?style=flat-square)
![Platform](https://img.shields.io/badge/platform-iOS%20%7C%20Android-blue?style=flat-square)
![Expo](https://img.shields.io/badge/Expo-SDK%2054-4C97FB?style=flat-square)
![React Native](https://img.shields.io/badge/React%20Native-0.81-61DAFB?style=flat-square)
![License](https://img.shields.io/badge/license-MIT-green?style=flat-square)

> **Turn your smartphone into a real-time concert light controller.**

Concert Light Sync transforms your phone's screen into an audio-reactive concert light with nine stunning visual modes, gesture-based controls designed for dark venues, and 60fps animations powered by React Native Reanimated.

---

## Overview

Concert Light Sync was built for one purpose: making live music more immersive. Whether you're at a stadium show, a club night, or a festival, the app listens to the music around you and responds with synchronized light effects you control with a swipe.

**Who is this for?**
- Concert attendees who want to be part of the visual experience
- Festival-goers creating crowd light shows
- Anyone who wants a beautiful, responsive flashlight for live events

---

## Promotional Copy

### Tagline
**Feel the beat. Light the crowd. Own the moment.**

### Short Promo (App Store / Product Hunt)
Turn your phone into an audio-reactive concert light in seconds. Concert Light Sync listens to live music and transforms your screen into a vivid, high-brightness light show with immersive modes, smooth swipe controls, and one-handed dark-venue usability.

### Full Promo (Website / Press Kit)
Concert Light Sync is built for live music fans who want to become part of the show. From festivals and arenas to club nights and house parties, the app reacts to the sound around you in real time and turns your screen into a dynamic performance light.

Choose from multiple visual modes including Strobe, Pulse, Rainbow, Wave, Candle, and a 3D Disco Ball. Fine-tune brightness, color, and audio sensitivity, then switch modes instantly with simple gestures designed for crowded, low-light environments. With smooth 60fps animations, haptic feedback, and a dimmable control UI, Concert Light Sync gives you bold visuals without distracting glare.

If you're in the crowd, this is your light stick, your atmosphere, and your moment.

### Social Captions
- Your flashlight is now the light show. #ConcertLightSync
- Built for festivals, clubs, and stadium nights. Swipe, glow, repeat.
- Real-time audio-reactive visuals on your phone. No extra hardware needed.
- Pick your color. Raise your phone. Match the music.

---

## Features

### Lighting Modes
| Mode | Description | Audio Reactive |
|------|-------------|:--------------:|
| ⚡ Strobe | Rapid on/off flash, safety-capped at 6Hz | — |
| 📊 Meter | 10-bar VU meter, color-coded green/yellow/red | ✓ |
| 🪩 Disco Ball | Full 3D WebGL disco ball — rotating mirrored tiles, 8 spotlight beams, atmospheric fog | ✓ |
| 🕯 Candle | Animated flame that flickers and brightens relative to the audio level | ✓ |
| 〰 Wave | Rainbow sine wave with audio-modulated amplitude + scrolling dot-matrix marquee | ✓ |
| 🌈 Rainbow | Seven concentric arcs pulsing through the spectrum | ✓ |
| 🎤 K-pop | Animated wave pattern synced to fan chants and idol ballads | ✓ |
| 🪄 Light Stick | Interactive glowing stick that reacts to audio in real time | ✓ |
| ✨ Pulse | Spinning light ball with 8 orbiting colored ray dots that expand with the beat | ✓ |

### Controls
- **Swipe left/right** — cycle through modes instantly
- **Long-press (0.6s)** — toggle screen lock to prevent accidental taps
- **Long-press marquee (5s)** — edit the scrolling message displayed in Wave mode
- **Tap canvas** — trigger a one-shot audio pulse (tap-to-simulate, no mic required)
- **Color swatch** — opens a full HSV color picker with 7 presets
- **Icon picker** — choose a custom icon displayed on the canvas; tap once for single-select or tap multiple icons to enable auto-cycling; long-press any custom slot for 5 seconds to assign your own glyph or emoji; selection persists via AsyncStorage
- **Audio sensitivity slider** — drag to tune how strongly the visuals react to sound (0–100%); persists across sessions
- **Brightness slider** — independent brightness control
- **Dim UI** — fades the control panel to 7% opacity, keeping the light on without glare
- **Lock mode** — minimal overlay shows only the lock icon

### Audio Reactivity
- Live microphone input via `expo-audio`
- 20Hz polling rate balancing responsiveness and battery
- Exponential moving average smoothing (α=0.3) prevents jitter
- Adaptive beat-onset detection (slope + baseline threshold + refractory window)
- Graceful fallback to ambient level 0.25 if mic permission is denied

### New in v1.0.5 (Current Branch)
- **Production release pipeline hardening** — Added platform-specific store build pipelines that enforce a strict order: local native release compile -> version sync -> compliance validation -> EAS cloud build.
- **Store submission split by platform** — Added dedicated submission flows for App Store and Google Play so submit operations remain explicit and independently runnable.
- **Automated compliance gate** — Added `scripts/pre-submit-check.js` and integrated it into build/submit scripts. It validates version alignment, iOS permission strings, AdMob app IDs, Android minification settings, Android package/version/permissions, and privacy policy presence before upload.
- **Android native build stability fix** — Updated Android release compile flow to clear stale `.cxx`/autolinking artifacts and run `:app:generateCodegenArtifactsFromSchema` before `:app:assembleRelease`, resolving Ninja/CMake codegen directory failures.
- **Release docs overhaul** — Replaced deployment transcript docs with a structured release playbook in `README_DEPLOYMENT.md`, and added a Release Day checklist in this README for quick execution.
- **Script compatibility aliases preserved** — Kept `build:ios`, `build:android`, `submit:ios`, and `submit:android` mapped to new store-oriented commands to avoid breaking existing workflows.

### New in v1.0.4
- **Beat intelligence (onset detection)** — visuals now react to detected beat transients, not only raw loudness.
- **Beat controls** — Beat Accent slider + Beat On/Off toggle in the control panel, with AsyncStorage persistence.
- **Scene bundles** — save your complete setup (mode, color, brightness, sensitivity, beat settings, marquee settings, icon/glyph state) as reusable bundles.
- **Bundle Library** — dedicated screen to apply/delete saved bundles and browse curated packs.
- **Curated packs** — built-in bundles (Neon Surge, Sunset Chant, Ultra Violet) can be applied instantly or added to your personal bundle library.
- **Bundle transfer** — QR screen now supports bundle payload sharing and paste-based bundle import.
- **Immediate import refresh** — imported bundles appear in the library without requiring an app restart.

### New in v1.0.3
- **Disco Ball mode** — full 3D WebGL disco ball powered by Three.js (`components/DiscoBall.jsx`): rotating mirrored tiles, 8 colored spotlight beams, atmospheric fog, drag-to-tilt camera, spin/lights toggles, and audio-reactive glow
- **Mode rename** — ORB renamed to **Pulse** (spinning light ball with 8 orbiting colored ray dots)
- **Wave marquee** — a scrolling rainbow dot-matrix message appears at the top of the screen in Wave mode. Default text is "Concert Light Sync". Long-press the marquee for 5 seconds to edit the message; leave it empty to hide it. The message persists across sessions.
- **Marquee VU meter** — the 7 dot rows of the marquee light up progressively from bottom to top in sync with the audio level, mirroring the Meter mode's green/yellow/red behaviour.
- **Marquee glyph support** — the Wave marquee now renders any Unicode character outside the 5×7 dot-matrix font (emoji, music symbols, special glyphs) as native text, so any character can appear in the scrolling message.
- **Audio Sensitivity slider** — a 0–100% drag control in the control panel lets you tune exactly how strongly the visuals respond to ambient sound. Setting is persisted via AsyncStorage.
- **Icon multi-select and cycling** — tap multiple icons in the icon picker to enable auto-cycling between them at a configurable interval (1–10 s). Long-press any custom icon slot for 5 seconds to assign your own glyph or emoji.

### New in v1.0.2
- **3 new modes** — K-pop, Light Stick, and Pulse join the original six
- **Custom icon** — icon picker in the control panel with AsyncStorage persistence
- **Version check** — on launch, the app compares against the latest release and prompts users to update if a newer version is available (`utils/versionCheck.js`)
- **Tap-to-simulate audio** — tap anywhere on the canvas to fire a one-shot audio pulse without mic permission

### Navigation & Screens
- **Hamburger drawer** — Slides in from the left via a Reanimated spring; links to About, Tutorials, Privacy Policy, and Share
- **Bundle Library screen** — Manage saved bundles and curated packs with apply/delete/add actions
- **About screen** — App info with logo, version, developer, website, and support email
- **Privacy Policy screen** — WebView loading CDN-hosted HTML with loading indicator and error/retry state
- **Tutorials screen** — Scrollable glassmorphism cards covering every feature

### Battery & Brightness
- **Auto max brightness** — Sets screen to 100% when the app is active; silently restores the user's original brightness when backgrounded or closed
- **Low battery warning** — Amber banner with `FadeInDown` animation appears at ≤10% battery; suppressed on simulators (returns −1)

### UX & Safety
- Glassmorphism dark UI (#121212 base) designed for dark venues
- Safe area aware — header and UI respect Dynamic Island / notch via `useSafeAreaInsets`
- WCAG-compliant text contrast for readability under stage lights
- Photosensitivity warning modal before Strobe mode activates
- Haptic feedback on mode changes, color selection, and brightness notches
- Portrait-locked for one-handed use in crowds

---

## Tech Stack

| Category | Library | Version |
|----------|---------|---------|
| Framework | React Native | 0.81.5 |
| Runtime | Expo | ~54.0.0 |
| UI | React | 19.1.0 |
| Animations | react-native-reanimated | ~4.1.1 |
| Gestures | react-native-gesture-handler | ~2.28.0 |
| Audio | expo-audio | ~1.1.1 |
| Haptics | expo-haptics | ~15.0.8 |
| Gradients | expo-linear-gradient | ~15.0.8 |
| Worklets | react-native-worklets | ^0.5.1 |
| Navigation | @react-navigation/native-stack | ^7.14.4 |
| WebView | react-native-webview | 13.15.0 |
| Safe Area | react-native-safe-area-context | ~5.6.0 |
| Brightness | expo-brightness | SDK 54 |
| Battery | expo-battery | SDK 54 |

---

## Project Structure

```
concert-light-sync/
├── App.js                      # Root — NavigationContainer + MainScreen
├── index.js                    # Expo entry point
├── package.json
├── app.json                    # Expo config (permissions, icons, orientation)
├── babel.config.js             # Babel preset for Expo + Reanimated plugin
├── metro.config.js             # Metro bundler config
├── index.html                  # Static marketing landing page
├── CLAUDE.md                   # Original design specification
├── components/
│   ├── LightCanvas.js          # Reanimated rendering engine (all 9 modes)
│   ├── DiscoBall.jsx           # Three.js/WebGL 3D disco ball (expo-gl)
│   ├── ControlPanel.js         # Bento grid UI, mode selection, color/brightness
│   ├── ColorWheel.js           # HSV color picker with presets and haptics
│   ├── AudioReactivity.js      # Microphone polling and signal smoothing
│   ├── AppHeader.js            # Brand header with hamburger button (safe area aware)
│   ├── SideDrawer.js           # Sliding navigation drawer (Reanimated spring)
│   └── AdBanner.js             # AdMob banner (bottom of screen)
├── utils/
│   └── versionCheck.js         # Startup version comparison + update prompt
└── screens/
    ├── AboutScreen.js          # App info — version, developer, links
    ├── PrivacyPolicyScreen.js  # WebView loading CDN-hosted privacy policy HTML
    └── TutorialsScreen.js      # Scrollable feature guide
```

### Component Responsibilities

**`App.js`** — Orchestrates the app. Holds top-level state (mode, color, brightness, lock, dim). Creates the composed pan + long-press gesture for swiping and locking. Manages splash screen timing and Reanimated runtime initialization.

**`LightCanvas.js`** — The visual engine. Each mode has dedicated Reanimated `withRepeat`/`withTiming`/`withSequence` animation sequences running on the native thread. Polls `audioLevelRef` at 20Hz for audio-reactive modes (Pulse, Meter, Wave, Rainbow, Candle). Pulse renders three staggered concentric rings driven by `useFrameCallback`; Candle renders an animated flame GIF whose opacity and scale track the audio level.

**`ControlPanel.js`** — The 3×2 bento grid of mode tiles, brightness slider, color swatch, and top-bar toggles (Dim, Lock). Uses React Native `Animated` for the Dim UI fade since it doesn't need native-thread precision.

**`ColorWheel.js`** — HSV color picker. Two `PanResponder` handlers drive the hue and brightness sliders. Fires haptic feedback at primary hue nodes (0°, 60°, 120°, 180°, 240°, 300°). Converts HSV → Hex for the rest of the app.

**`DiscoBall.jsx`** — Three.js/WebGL 3D disco ball rendered inside an `expo-gl` GLView. Builds a high-fidelity mirrored-tile sphere, 8 rotating colored spotlight beams, and an atmospheric fog layer. Accepts `audioLevelRef` to modulate rotation speed and glow intensity. Uses `InteractionManager.runAfterInteractions` for deferred GL context initialization and cleans up all Three.js objects on unmount to prevent memory leaks.

**`AudioReactivity.js`** — Invisible component (returns `null`). Requests mic permission, starts `expo-audio` recording with metering enabled, and polls every 50ms. Writes the smoothed audio level to `audioLevelRef` — a ref, not state, so it never triggers re-renders.

**`AppHeader.js`** — Brand header rendered only when the control panel is visible. Uses `useSafeAreaInsets` to pad the Dynamic Island / notch. Returns `null` when hidden, contributing zero height to the layout.

**`SideDrawer.js`** — Custom drawer animated with `useSharedValue` + `withSpring`. Opened exclusively via the hamburger button (no edge swipe) to avoid conflicting with the existing `Gesture.Pan()` mode-change gesture. Overlay `pointerEvents` blocks click-through to the canvas when open.

---

## Getting Started

### Prerequisites

- [Node.js](https://nodejs.org) 18+
- [Expo CLI](https://docs.expo.dev/get-started/installation/) or `npx expo`
- iOS Simulator / Android Emulator **or** the [Expo Go](https://expo.dev/client) app on a physical device

### Installation

```bash
git clone https://github.com/your-username/concert-light-sync.git
cd concert-light-sync
npm install
```

### Run

```bash
# Start the Expo dev server
npx expo start

# Run directly on iOS simulator
npx expo run:ios

# Run directly on Android emulator
npx expo run:android
```

Scan the QR code with **Expo Go** (iOS/Android) to run on a physical device.

### Permissions

The app requests **microphone access** on first launch. Audio reactivity requires this permission. If denied, Pulse mode falls back to a constant ambient level of 0.25.

---

## Usage

| Action | Result |
|--------|--------|
| Swipe left / right | Previous / next lighting mode |
| Long-press (0.6s) | Toggle screen lock |
| Tap color swatch | Open HSV color picker |
| Drag brightness bar | Adjust brightness 0–100% |
| Tap **Dim** button | Fade control panel to 7% opacity |
| Tap **Lock** button | Toggle screen lock overlay |

### Strobe Mode
Selecting Strobe shows a photosensitivity warning. You must confirm before the mode activates. Frequency is hard-capped at 6Hz for safety.

### Runtime Warnings (Three.js / Expo GL)
- `THREE.Clock` deprecation warnings are resolved in current code by using an internal monotonic timer in `components/DiscoBall.jsx`.
- `EXGL: gl.pixelStorei() doesn't support this parameter yet!` comes from Expo GL native internals, not app code.
- In this project's current Disco Ball scene (no external texture upload path), this EXGL warning is non-blocking and can be safely ignored.

---

## Configuration

Key settings in `app.json`:

```json
{
  "expo": {
    "name": "Concert Light Sync",
    "slug": "concert-light-sync",
    "version": "1.0.5",
    "orientation": "portrait",
    "newArchEnabled": true,
    "ios": {
      "infoPlist": {
        "NSMicrophoneUsageDescription": "Used to react to music and ambient sound."
      },
      "supportsTablet": false
    },
    "android": {
      "permissions": ["android.permission.RECORD_AUDIO"]
    }
  }
}
```

### Babel
The Reanimated Babel plugin **must** be listed last in the `plugins` array in `babel.config.js`:

```js
module.exports = {
  presets: ['babel-preset-expo'],
  plugins: [
    'react-native-worklets/plugin',
    'react-native-reanimated/plugin', // must be last
  ],
};
```

---

## Architecture Notes

### Why Reanimated?
React Native's default `Animated` API runs on the JS thread. At 60fps, any JS work (state updates, event handlers) can cause dropped frames. Reanimated runs animation worklets on the native thread — the screen flicker is guaranteed smooth even on lower-end devices.

### Why a ref for audio level?
Audio polls at 20Hz. If the level were stored in React state, every update would trigger a full re-render of the component tree. Using a ref (`audioLevelRef`) means `LightCanvas` can read the latest value inside a Reanimated worklet with zero render overhead.

### Gesture composition
The root gesture is a `Composed` gesture wrapping a `LongPress` and a `Pan`. This lets both gestures coexist: a slow pan triggers swipe mode cycling, while a long stationary press triggers screen lock — without conflict.

---

## Release Day Checklist

Use the full deployment playbook in [README_DEPLOYMENT.md](README_DEPLOYMENT.md).

Quick release sequence:

1. `npm run build:ios:store`
2. `npm run submit:ios:store`
3. `npm run build:android:store`
4. `npm run submit:android:store`

Minimum pre-submit gates:

- `npm run pre-submit-check` passes.
- App Store Connect metadata and privacy details are complete.
- Google Play Data safety, content rating, ads disclosure, and policy fields are complete.

---

## Contributing

Contributions are welcome. Please:

1. Fork the repo and create a feature branch (`git checkout -b feature/my-feature`)
2. Keep changes focused — one feature or fix per PR
3. Test on both iOS and Android if possible
4. Open a pull request with a clear description

### Ideas for Contribution
- FFT-based spectrum analysis for frequency-specific reactivity
- Preset scene saving (party, concert, festival)
- BPM detection and tempo-locked strobing
- Accessibility improvements (reduced motion support)

---

## License

MIT License — see [LICENSE](LICENSE) for details.

---

*Concert Light Sync — Built for concert-goers, by concert-goers.*
