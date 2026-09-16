# Miku Watch

A single-file, dependency-free analog watch face in the browser — a Seiko-inspired
teal-and-magenta dial built as an anniversary piece, with a growing set of
mechanical and personalization touches layered on top.

No build step, no framework: it's one `index.html` with inline CSS and vanilla JS.
Clone the repo and open `index.html` directly in a browser to run it.

## Features

**Watch faces**
- **Seiko Miku** — the default analog face: teal ticks, a magenta "01" marker,
  a date window, and a wordmark emblem.
- **Digital** — a cyan/magenta digital readout sharing the same case.

**Mechanical realism**
- Smooth sweeping second hand (or switch to a discrete per-second "tick" in settings).
- Soft directional shadows cast by the hands onto the dial.
- A draggable, clickable crown: drag left/right to cycle timezones, click/tap to
  open the timezone picker directly.
- Changing timezone spins the hour and minute hands forward (clockwise only,
  never backward) at a fixed rate of 2 clock-hours per second of real time —
  the second hand keeps ticking live throughout.
- All three hands share a single, exact rotation axle.

**Personalization (Settings panel)**
- **Watch face** — Seiko Miku / Digital.
- **Appearance** — OLED (true black), Night (boosted luminous ticks/numeral),
  or Light (a light page with the watch itself staying a dark object).
- **Watch** — smooth vs. tick seconds, and show/hide date, seconds, and the
  timezone readout.
- **39 mode** — a small identity touch: the second hand glows at `:39` seconds,
  and the minute hand briefly glows during the `:39` minute.
- **Timezone** — ~65 cities grouped into `<optgroup>`s by current UTC offset,
  plus Local Time and UTC pinned at the top.

All settings persist across reloads via `localStorage`.

**Ambient mode**
- Strips away the crown, bezel ring, glass reflection, and case/dial backgrounds,
  leaving just the glowing ticks and hands on a dark page — a minimalist,
  distraction-free clock.
- Tap/click the watch to exit back to Full mode (Escape also works).

**Sound**
- Fully synthesized with the Web Audio API — no audio files. A mechanical
  tick on each second, a crown detent click while dragging, a settings-button
  click, and a three-note startup chime.
- Off by default; enabling it in Settings respects browser autoplay policy
  by only starting audio on a real user gesture.

**Layout**
- Centered on the page at any size; on wide viewports (≥1180px) the settings
  panel opens to the side of the watch instead of pushing it off-center.

**Touch gestures**
- Swipe left/right on the watch to switch faces (Seiko Miku ↔ Digital).
- Swipe up to open the settings panel.
- Drag a single finger to tilt the watch in 3D for a quick "inspect" look —
  it springs back to flat on release.
- Pinch with two fingers to zoom the watch (0.85x–1.8x).
- Double-tap to enter Ambient mode; a single tap while in Ambient exits
  back to Full.
- Tap the timezone readout to open the timezone picker (same as tapping
  the crown).

## Roadmap

This project is being built incrementally. Rough phases, in order:

- [x] Mechanical realism (hand shadows, crown interaction, timezone spin)
- [x] Settings panel
- [x] Multiple watch faces (Seiko Miku, Digital)
- [x] Ambient display mode
- [x] Sound design (synthesized tick, crown click, UI click, startup chime)
- [x] Mobile gestures (swipe faces, swipe-up settings, tilt, pinch zoom, taps)
- [ ] Capture/share mode (export a shareable image of the watch + moment)
- [ ] Time Capsule (save a timestamped snapshot as a keepsake)
- [ ] Watchmaker customizer (build your own dial/hands/strap/case combo)
- [ ] Collection/unlock system (earn additional faces through use)

## Tech

Plain HTML + CSS + JavaScript. No dependencies, no bundler. Uses the
`Intl.DateTimeFormat` API for timezone-aware time formatting.
