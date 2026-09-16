# Miku Watch

A single-file, dependency-free analog watch face in the browser — a Seiko-inspired
teal-and-magenta dial built as an anniversary piece, with a growing set of
mechanical and personalization touches layered on top.

No build step, no framework: it's one `index.html` with inline CSS and vanilla JS.
Clone the repo and open `index.html` directly in a browser to run it.

## Features

**Watch face collection**
- **Night Miku** — the default face: case/bezel/reflection stripped down to
  just the glowing teal-and-magenta face, with a magenta "01" marker, a date
  window, and a wordmark emblem. Unlocked from the start.
- **Cyan Circuit** 🔒 — an all-cyan futuristic reskin with a circuit-trace dial
  and hexadecimal hour numerals (A/B/C at 10/11/12). Unlocks when you set the
  timezone to California.
- **15th Anniversary** 🔒 — a warm gold accent variant with a "15" marker on
  the 3 o'clock tick. Unlocks the first time you witness a `:39` second glow
  (39 mode must be on).
- **Classic** 🔒 — a conventional silver-case, monochrome-hands watch with no
  color gimmick or glow. Unlocks when you switch to Tick seconds.
- **Pure White** 🔒 — white case and dial, black hands, a red second hand, no
  glow. Unlocks when you hide the date window.
- **Terminal Green** 🔒 — monochrome phosphor-green on black, hacker-terminal
  style. Unlocks when you enable sound.
- **Rose Gold** 🔒 — warm rose-gold case and hands on a dark dial. Unlocks
  when you hide the seconds hand.
- **Sakura** 🔒 — soft cherry-blossom pink, with a few decorative petals
  scattered across the dial. Unlocks when you switch to the Digital display
  format.
- **Snow** 🔒 — white case and dial with a light-blue accent, no glow.
  Unlocks the first time you enter Ambient mode.
- **Wood** 🔒 — warm wood-grain case and dial, no glow. Unlocks when you set
  the volume slider to 0.
- **Solar** 🔒 — a silicon-photovoltaic-cell grid dial (silver busbars over a
  dark blue cell), blue hands with an amber "sun" accent. Unlocks when you
  set the timezone to Tokyo.

Every face is one set of CSS custom-property overrides, so hands, ticks, the
case, and the hub all retheme automatically — no per-element styling needed
per face (the 39-mode glow and hex numerals read the same variables, so they
match too). The face picker shows a live "(x/11) unlocked" count, locks out
radios for faces you haven't earned yet (with a hint on how to unlock them),
and pops a toast the moment you unlock a new one.

The whole app is always true-black (OLED) with permanently luminous ticks and
numerals — there's no light/dark toggle, this is the one look.

**Analogue / Digital**
- A left/right toggle in Settings independent of the watch face: Digital
  swaps the hands and ticks for a big digital readout, but keeps whichever
  face's colors are active (same CSS custom properties), so it always
  matches the current theme rather than having its own fixed look.

**Mechanical realism**
- Smooth sweeping second hand (or switch to a discrete per-second "tick" in settings).
- Soft directional shadows cast by the hands onto the dial.
- A draggable, clickable crown: drag left/right to cycle timezones, click/tap to
  open the timezone picker directly.
- Changing timezone spins the hour and minute hands forward (clockwise only,
  never backward) at a fixed rate of 2 clock-hours per second of real time —
  the second hand keeps ticking live throughout.
- All three hands share a single, exact rotation axle.

**Personalization**
- **Watch face** — a standalone gallery box (see Layout below) holding the
  eleven-face collection described above. Its own open/closed state is tied
  to the settings panel's — the gear icon opens and closes both together.
- **Settings panel (gear icon)** — everything else:
  - **Watch** — Format (Analogue/Digital) and Seconds (Smooth/Tick) as
    left/right button toggles, plus show/hide date and seconds checkboxes.
  - **39 mode** — the second hand glows at `:39` seconds, and the minute
    hand briefly glows during the `:39` minute.
  - **Sound** — an enable checkbox plus a 0-100 volume slider controlling
    every synthesized tone's gain.
  - **Display** — Full/Ambient as a left/right button toggle.
  - **Timezone** — ~65 cities grouped into `<optgroup>`s by current UTC
    offset, plus Local Time and UTC pinned at the top.

All settings persist across reloads via `localStorage`.

**Ambient mode**
- Strips away the crown, bezel ring, glass reflection, and case/dial backgrounds,
  leaving just the glowing ticks and hands on a dark page — a minimalist,
  distraction-free clock.
- Tap/click the watch to exit back to Full mode (Escape also works).

**Sound**
- Fully synthesized with the Web Audio API — no audio files. A mechanical
  tick on each second, a crown detent click while dragging, a settings-button
  click, and a three-note startup chime, all scaled by the volume slider.
- Off by default; enabling it in Settings respects browser autoplay policy
  by only starting audio on a real user gesture.

**Layout**
- Centered on the page at any size. On wide viewports (≥1180px) the watch
  face gallery sits in its own persistent box to the *left* of the watch,
  and the settings panel opens to its *right* — neither shifts the watch
  from center. On narrower viewports both stack in normal document flow
  (face gallery above the caption, settings panel collapsible as usual).

**Touch gestures**
- Swipe left/right on the watch to switch between unlocked faces.
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
- [x] Watchmaker-style presets (fully-themed faces via CSS custom-property
      overrides — a lighter take than a freeform dial/hands/strap/case
      combinator, since this UI has no visible strap to customize)
- [x] Collection/unlock system (10 of 11 faces earned through real
      interactions: California timezone, a `:39` glow, tick seconds,
      hiding the date, enabling sound, hiding seconds, Digital format,
      Ambient mode, zero volume, and Tokyo timezone)

## Tech

Plain HTML + CSS + JavaScript. No dependencies, no bundler. Uses the
`Intl.DateTimeFormat` API for timezone-aware time formatting.
