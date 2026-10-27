# 🎬 CineSync — Watch Together, Google Drive & VLC Studio

**Live Production App**: **[https://cinephile-web.pages.dev](https://cinephile-web.pages.dev)**  
**Custom Short Domain**: **`cinephile.dev`** (Cloudflare Pages mapped)

**CineSync** is a standalone, single-file Watch Party & real-time synchronized video streaming application ([`watch-together.html`](file:///C:/Users/sk621/.gemini/antigravity/scratch/cinesync/watch-together.html) / [`cinesync-watch-together.html`](file:///C:/Users/sk621/.gemini/antigravity/scratch/cinesync/cinesync-watch-together.html)) built with Tailwind CSS, HTML5 Media APIs, Web Audio API, and PeerJS WebRTC networking.

---

## 🌐 Live Production Deployment

* **Production URL**: [https://cinephile-web.pages.dev](https://cinephile-web.pages.dev)
* **Clean Watch Route**: [https://cinephile-web.pages.dev/watch-together](https://cinephile-web.pages.dev/watch-together)
* **Custom Domain**: Bound to `cinephile.dev` & `www.cinephile.dev` on Cloudflare Pages.
* **Hosting Platform**: Cloudflare Pages with edge caching, automated HTTPS, and zero-config WebRTC signaling.
* **GitHub Repository**: [https://github.com/sami9dev/cinephile-web](https://github.com/sami9dev/cinephile-web)

---

## 🎨 Visual Identity & Tri-Theme Design System

CineSync features a refined, streamlined, and lightweight UI/UX that eliminates bulky visual clutter. Choose from three curated cinematic styles via the **Theme Switcher** in the top bar or inside the **Settings Modal**:

| Style | Color Palette | Visual Identity & Atmosphere |
|---|---|---|
| 🤎 **Warm Earth** | `#211B1A` · `#382A28` · `#60433D` · `#916B60` · `#C1A094` · `#E8D8CE` | Warm, elegant, premium cinema tones with soft copper accents and cozy glow. |
| 💙 **Blue Hour** | `#111522` · `#1E263B` · `#303D59` · `#536684` · `#98A9C4` · `#DCE3EF` | Modern, cinematic, calm midnight-blue aesthetics with cyan highlight neon. |
| 💜 **Midnight Lavender** | `#17151C` · `#292531` · `#45404F` · `#716879` · `#AAA2B3` · `#E2DDE7` | Sophisticated, atmospheric violet hues with delicate silvery-lavender accents. |

### How It Works Under the Hood
* **Instant Dynamic Adaptation**: CSS custom properties (`--cs-bg-base`, `--cs-bg-surface`, `--cs-bg-card`, `--cs-bg-elevated`, `--cs-border`, `--cs-accent`, `--cs-text-main`, `--cs-ambient`) automatically re-skin the entire application with smooth CSS color transitions.
* **Ambient Lighting Glow**: The theater stage's back-glow (`.ambient-lighting`) dynamically shifts between warm amber, oceanic cyan, and ethereal lavender.
* **Persistent Preferences**: Your selected style is saved to `localStorage` (`cinesync_visual_theme`) and persists across browser reloads.

---

## 🚀 De-Bulked, Streamlined UI & UX

1. **Ultra-Slim Header (48px)**:
   - Unified **Room Hub Capsule**: Packs P2P status dot, `HOST`/`GUEST` role badge, Room Code, 1-click **Copy**, **Link**, **Join**, and **Leave** buttons into a compact, elegant pill.
   - **Quick-Switch Theme Pill**: Instant 1-click toggle between `🤎 Earth`, `💙 Blue`, and `💜 Lavender`.
   - Compact **Google Profile** & **Simulation Mode** controls.
2. **Floating Cinema Player Bar**:
   - Airy glassmorphism player controls floating gently over the bottom of the video stage.
   - Slim timeline scrubber with glowing thumb that subtly expands on hover.
   - Single-line transport controls: Play/Pause, timecode (`00:00 / 03:00`), -10s, +10s, frame step (+1f), A–B loop, volume slider, speed selector, resync, snapshot, and fullscreen.
3. **Optimized Video Call Dock & Sidebar**:
   - Modern 4:3 / 16:9 webcam cards with rounded-xl corners and smooth border highlights.
   - **Companion Call Volume Slider**: Embedded directly below the companion video feed in a clean micro-strip, keeping call volume strictly isolated from the 200% movie volume graph.
   - Minimalist 3-tab sidebar (**Chat**, **Sync Log**, **Shared Playlist**) with clean, non-cluttered message bubbles.

---

## 🎯 Core Features & Watch Modes

### 1. Honest Watch Modes & Playback Sync
* **Shared Local-File Mode (Zero Upload)**:
  * Each participant picks their own copy of the movie file (`.mp4`, `.mkv`, `.webm`, `.mov`).
  * No video files are uploaded to any server. Timestamps, play/pause states, and playback rates sync over the WebRTC DataChannel.
  * **Intelligent Drift Correction**:
    * If drift $> 1.5\text{s}$, a clean timestamp seek occurs automatically.
    * If $0.25\text{s} < \text{drift} \le 1.5\text{s}$, playback rate is subtly nudged ($1.06\times$ or $0.94\times$ for $1.2\text{s}$) to smoothly converge timelines without audio pops.
  * **Host-Only vs Shared Control**: Host can lock playback controls in Settings so only the host can scrub, play, pause, or change media.
* **VLC Window Screen Share**:
  * Uses the browser Screen Capture API (`navigator.mediaDevices.getDisplayMedia`) to capture your running VLC Media Player window along with system audio.
  * *Honest Disclosure*: Streams the host's live desktop output directly to the companion without pretending to remotely operate the guest's desktop VLC player.
* **Google Drive & Direct URL Modes**:
  * Direct streaming works with CORS-enabled URLs and public Drive streams (`uc?export=download`).
  * Seamless fallback to **Drive Embed Mode** with honest status banners when cross-origin or large-file warnings occur.
* **Built-in Procedural Cinema Synthesizer**:
  * Real-time canvas animation paired with a Web Audio API synth oscillator for instant latency and ducking tests without needing a video file.

---

### 2. Audio Separation & Smart Voice Ducking
* **Independent Companion Call Volume**:
  * Exclusively controls your friend's incoming WebRTC voice stream (`remoteCamVideo.volume`).
  * Strictly decoupled from the movie audio graph, ensuring call clarity is never compromised.
* **200% VLC Master Volume Boost**:
  * Movie audio routes through an isolated Web Audio gain node allowing up to **200% volume amplification** without clipping.
* **Smart Voice Ducking**:
  * When your friend speaks, movie volume ducks automatically to your configured level (default: 35%) and smoothly restores when speaking stops.

---

### 3. WebRTC Video Calling & Hardware Selection
* **P2P Video & Screen Sharing**:
  * Built-in webcam, microphone, screen sharing, and mute controls wired directly to standard browser media APIs.
* **Hardware Device Switching**:
  * Enumerate cameras, microphones, and output speakers via `navigator.mediaDevices.enumerateDevices()`. Select preferred hardware in the Settings dialog.
* **Call Quality Presets & Live Negotiated Stats**:
  * Choose between **Auto**, **Data Saver** (320x240, 15fps, 150kbps), **Balanced** (640x480, 24fps, 600kbps), and **HD** (1280x720, 30fps, 1.8Mbps).
  * Outgoing WebRTC stream parameters (`RTCRtpSender.setParameters`) are applied dynamically with real-time stats display in Settings.
* **Explicit Simulation Mode**:
  * Solo simulation mode (Aarav) is explicitly badged as `[Simulation]` / `[Bot]` and never masquerades as a real connection.

---

### 4. Settings Dialog (Grouped & Saved to `localStorage`)
Access via the **⚙️ Settings Gear** in the top navigation bar:
1. **🎨 Visual Style**: Interactive cards with 6-color swatch bars for 🤎 Warm Earth, 💙 Blue Hour, and 💜 Midnight Lavender.
2. **📞 Call Quality & Network**: Preset selector, live negotiated resolution & FPS monitor, signaling disclosures.
3. **🎬 Playback & Sync**: Video fit modes, default playback speed, voice ducking toggle & level, host-only playback control toggle, shared playlist auto-next toggle.
4. **💬 Subtitles**: Toggle subtitle rendering, font size, text color, and background backdrop opacity.
5. **🎙️ Hardware Devices**: Select active Camera, Microphone, and Audio Output Speaker.
6. **🔒 Room Privacy & Role**: Room lock toggle (blocks incoming connections), Host Role Handoff button.

---

## ⌨️ Desktop Hotkeys Reference

| Key | Action |
|---|---|
| <kbd>Space</kbd> | Play / Pause Synced |
| <kbd>←</kbd> / <kbd>→</kbd> | Seek -10s / +10s |
| <kbd>↑</kbd> / <kbd>↓</kbd> | Volume Boost up to 200% |
| <kbd>M</kbd> | Mute / Unmute Movie |
| <kbd>A</kbd> | Cycle Aspect Ratio (16:9 Fit, 21:9 Cinema, 4:3 Classic, Fill/Crop) |
| <kbd>E</kbd> | Frame Step (+1 frame forward) |
| <kbd>G</kbd> / <kbd>H</kbd> | Subtitle Delay (-100ms / +100ms) |
| <kbd>J</kbd> / <kbd>K</kbd> | Audio Delay (-50ms / +50ms) |
| <kbd>Ctrl</kbd> + <kbd>B</kbd> | Bookmark current timestamp |

---

## 📁 File Structure

```
cinesync/
├── index.html                    # Production entrypoint for Cloudflare Pages
├── watch-together.html           # Main application file with full features & styles
├── cinesync-watch-together.html  # Standalone distributable single-file app
└── README.md                     # Architecture, features, and setup guide
```
