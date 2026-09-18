# Changelog

All notable changes to this project are documented here. Format follows
[Keep a Changelog](https://keepachangelog.com/en/1.1.0/), versioning follows
[Semantic Versioning](https://semver.org/) (pre-1.0: minor bumps are new
features, patch bumps are fixes/tweaks — anything may still change).

## [0.15.0] - 2026-09-18

### Added
- **Solar Eclipse** watch face (14 total): a black case with a real annular
  solar eclipse photo as the dial, dark hands, and a fiery orange accent.
  Unlocks when you set the timezone to Chicago.
- Footer credit updated: "Built by TheBooleanJulian. Moon and solar eclipse
  photos by Accurova."

## [0.14.0] - 2026-09-17

### Added
- **Lunar** watch face (13 total): a grey metallic case with a real full-moon
  photo as the dial, dark hands, and a muted gold accent. Unlocks when you
  set the timezone to Kiritimati.
- Footer credit: "Built by TheBooleanJulian. Moon photo by Accurova."

### Fixed
- The moon photo initially left a black rim around the dial edge
  (`background-size:cover` only fills the container with the photo's own
  rectangle, not with the moon inside it) and later showed faint rendering
  seams from combining `cover` with a large CSS `transform:scale`. Fixed at
  the source: cropped the photo tightly to the moon's actual pixel bounding
  box and resized it down (2.4MB → ~85KB), so a plain `cover` fill now works
  with no CSS zoom trick needed.
- Mobile layout: the page previously had `overflow:hidden`, which is
  invisible on desktop (panels open to the side) but on mobile, where the
  watch, face gallery, and settings panel all stack vertically, could make
  the bottom of an open panel unreachable. The page now scrolls vertically
  whenever stacked content exceeds the viewport.

## [0.13.0] - 2026-09-17

### Added
- **Racing** watch face (12 total): black case/dial, white hour/minute hands
  and ticks, a bright red second hand/hub/marker, and a checkered-flag icon.
  Unlocks at maximum volume.
- Watch faces now appear in a permanent, deliberate order (signature →
  neutral/white → warm/natural → tech → bold → special-edition) instead of
  unlock or alphabetical order.

### Fixed
- The flag icon's outer silhouette used smooth Bézier curves but its
  internal checker cells were flat rects clipped to it, so the grid looked
  straight while only the outline curved. Rebuilt each cell's edges as exact
  mathematical subdivisions of the same curves used for the silhouette, so
  the grid ripples in identical phase with the outline.
- An earlier version of the wavy clip path had its wave amplitude too large
  relative to its wavelength, collapsing each column into a diamond/bowtie
  shape instead of a flag ribbon.

## [0.12.0] - 2026-09-17

### Added
- "Reset unlocked faces" button in Settings → Collection, with a
  confirmation dialog, to re-lock every face except Night Miku.

## [0.11.0] - 2026-09-16 – 2026-09-17

### Added
- **Wood** and **Solar** faces (11 total).
- Hexadecimal hour numerals (A/B/C at 10/11/12) on the Cyan Circuit face.
- Sakura petal decorations and a snowflake icon on the Snow face.

### Changed
- Renamed "Classic" → "Monochrome" and "Pure White" → "Classic".
- Terminal Green's second hand is now white instead of matching green.
- The watch face gallery and settings panel now share one open/closed
  state, driven by the same gear button, instead of the gallery hiding
  only when settings opened.

### Fixed
- A rollover glitch where the second hand jumped erratically for a split
  second every time it ticked from `:59` to `:00` in Tick-seconds mode —
  the angle was recomputed fresh each second (354° → 0°) and the CSS
  transition animated that as a near-full-circle spin backward instead of
  a 6° step forward. Now tracks a continuously-growing angle so the
  rollover always advances forward.
- The 39-mode glow and various hand/hub accents were hardcoded to a fixed
  magenta color instead of each face's own accent variable, so faces like
  Classic and Wood (which intentionally disable glow) still showed a pink
  glow regardless.
- A stale-face-id bug where localStorage entries for faces removed in
  earlier versions (`seiko`, `digital`) inflated the "unlocked" count
  beyond the actual total (e.g. showing "12/11").
- Cyan Circuit never overrode its glow color variable, so it fell back to
  the default pink instead of cyan.

## [0.10.0] - 2026-09-16

### Added
- Independent Analogue/Digital display-format toggle — Digital is no longer
  its own watch face; it now inherits whichever face's theme colors are
  active.
- Left/right button toggles for Seconds (Smooth/Tick) and Display (Full/
  Ambient), replacing radio-button pairs.
- A volume slider (0–100) alongside the sound-enable checkbox.
- Snow watch face.

### Removed
- The "Show timezone" checkbox (the readout is now always shown).
- The Digital watch face (superseded by the Format toggle).

## [0.9.0] - 2026-09-16

### Changed
- Removed the Seiko Miku face, which overlapped too much visually with
  Night Miku's chrome-free look. **Night Miku is now the default face.**

## [0.8.0] - 2026-09-16

### Added
- Four new watch faces (10 total).

### Changed
- The watch face picker moved out of the collapsible settings panel into
  its own persistent box, positioned to the left of the watch on desktop
  (mirroring the settings panel's position on the right) so neither shifts
  the watch off-center.
- Removed the Appearance toggle (OLED/Night/Light) entirely — the app is
  now always true-black with permanently luminous ticks and numerals.

### Removed
- Capture/Share and Time Capsule (see 0.7.0) — dropped entirely, including
  the canvas rendering code and the localStorage-based keepsake list.

### Fixed
- A dark smudge on the Pure White face's dial, caused by a shared radial
  gradient with hardcoded dark color stops that only respected the
  `--dial` variable in its middle stop.

## [0.7.0] - 2026-09-16

### Added
- Watch face collection with an unlock system: most faces start locked and
  unlock through real interactions (switching a setting, changing
  timezone, etc.), with a toast notification and a live "(x/n) unlocked"
  counter.
- Capture/Share: a `<canvas>`-rendered preview of the watch (redrawn from
  the live hand angles and active theme, not a DOM screenshot) with
  1:1/4:5/9:16/16:9 crop options and PNG download. *(Removed in 0.8.0.)*
- Time Capsule: saved timestamped keepsake snapshots with thumbnails.
  *(Removed in 0.8.0.)*

## [0.6.0] - 2026-09-16

### Added
- Mobile touch gestures: swipe left/right to switch faces, swipe up to
  open settings, single-finger drag for a 3D "inspect" tilt, two-finger
  pinch to zoom, double-tap to enter Ambient mode, and tapping the
  timezone readout to open the picker.

## [0.5.0] - 2026-09-16

### Added
- Fully synthesized sound design via the Web Audio API (no audio files):
  a mechanical tick each second, a crown detent click, a settings-button
  click, and a startup chime — gated behind an "Enable sound" toggle that
  respects browser autoplay policy.

## [0.4.0] - 2026-09-16

### Added
- Ambient display mode: strips the crown, bezel ring, glass reflection,
  and case/dial backgrounds down to just the glowing ticks and hands.
  Tap the watch (or press Escape) to return to Full mode.
- Internal scrolling for the settings panel once its content grows taller
  than the viewport allows.

## [0.3.0] - 2026-09-16

### Added
- On wide viewports (≥1180px), the settings panel opens to the side of the
  watch instead of pushing content below it, so the watch never shifts
  from center.
- A Light appearance mode (later removed in 0.8.0).

### Changed
- Replaced the "Dark" appearance option with OLED (true black) as the
  default.

## [0.2.0] - 2026-09-16

### Added
- Mechanical realism: directional hand shadows, a draggable/clickable
  crown (drag to cycle timezones, click to open the picker), and a
  clockwise-only hand-spin animation when changing timezone.
- A settings panel covering appearance, watch display options, 39-mode,
  and the timezone dropdown (grouped by UTC offset).
- Multiple watch faces (Seiko Miku, Digital) with basic switching.

### Fixed
- The three hands previously rotated around slightly different pivot
  points (each offset by half its own width) instead of one shared axle.

## [0.1.0] - 2026-09-16

### Added
- Initial release: a Seiko-inspired analog watch face with a teal-and-
  magenta dial, a signature magenta "01" hour marker, a live date window,
  and a timezone selector covering ~65 cities grouped by UTC offset.
