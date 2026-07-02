# Clarke & Park Transforms as Geometry

Interactive 3-D teaching instrument for the abc → αβ0 → dq0 transforms. Companion piece to
`transmission_line_transients/LineWave3D.html` (same stack: single self-contained HTML file,
Three.js via CDN import map, OrbitControls, lil-gui, UnrealBloomPass).

**Files**

- `ClarkePark3D.html` — the tool (v2)
- `ClarkePark3D.v1-mvp.html` — the original MVP, kept for reference (safe to delete)

## The idea

Plot the instantaneous point **(i_a, i_b, i_c)** in a 3-D space whose axes are the three phases.

- **Balanced** signals never leave the plane **a + b + c = 0** (the tilted disc). Clarke is
  revealed as a rename: α, β span the disc, the purple 0-axis is perpendicular to it.
- **Park** is a change of observer: toggle the Park frame and the world eases into
  counter-rotation — the vector freezes, the abc axes spin backwards, AC becomes DC.

## v2 features

**Guided tour** — 9 scripted scenes ("Three waveforms, one point" → "But who tells you θ?")
with eased camera flights and parameter morphs, including "Why 120° apart? Watch the shadow" —
the orthogonal measurement axes collapsing into the classic 120° space-vector diagram as the
camera sinks onto the 0-axis. Start it from the HUD button.

**Pedagogical devices** (Display folder / keyboard):

- *Tip-to-tail construction* (C) — a·x̂ + b·ŷ + c·ẑ chained arrows landing on the ball
- *Sequence epicycles* (E) — the exact decomposition into a +ω circle, a −ω circle
  (unbalance → ellipse), −5ω / +7ω harmonic circles, and a zero-sequence leg off the plane;
  the chain tip lands on the ball to machine precision (`__cp.selftest()`)
- *Orbit preview* — dashed closed orbit for the current signal recipe, tinted purple where
  zero-sequence lifts it off the disc
- *dq-frame locus* — green comet drawn in the rotating frame: a dot when balanced, a 2ω circle
  under unbalance, a 6ω rosette with 5th/7th harmonics
- *Live matrix panel* — the Clarke and Park matrices with numbers flowing through them;
  amplitude-invariant (2/3) vs power-invariant √(2/3) toggle (power-invariant is an orthonormal
  rotation: watch ‖abc‖ = ‖αβ0‖ lock in the HUD)

**Controls-engineering layer**:

- *Frame angle source*: locked open-loop ω, detuned ω (watch dq slowly precess — why PLLs
  exist), or a live **SRF-PLL** with a bandwidth knob
- *Grid events*: ⚡ +30° phase jump and ⚡ 3-cycle unbalanced sag, with scope markers; fire a
  jump against the PLL and watch θ̂ slew, overshoot, and re-lock (red arc = angle error)
- *Harmonics with sequence identity*: 3rd (triplen → pure zero-sequence, invisible to dq),
  5th (negative) and 7th (positive) — both fold to the same 6ω dq ripple
- HUD *ripple line* states which dq ripple frequencies the current signal produces

**Signals & scope**: θ-stamped HiDPI scope (3 cycles, 90° gridlines, event markers); hover it
to inspect values and see a ghost ball at that instant on the 3-D orbit.

**Scenario chips**: Balanced · Unbalanced sag · Rectifier harmonics · Triplen 3rd · Everything.

**Camera**: free tumble (TrackballControls) with four presets — hero, down 0-axis, plane
edge-on, standard î-ĵ-k̂ (keys 1–4) — plus an *auto-rotate view* checkbox (auto-enabled in
tour scenes 1, 2 and 8; auto-disabled when you look straight down the 0-axis, where an orbit
would be pure roll). The app opens inside the guided tour, and the transport bar has a
**θ slider** to scrub the whole simulation to any electrical angle (pauses playback).

**Responsive / mobile**: on phones (≤640px or coarse-pointer ≤900px) the app opens with the
detailed controls hidden for a clean 3-D view; a ⚙ button (top-right) reveals the lil-gui
panel, HUD readouts and ripple line. One-finger drag rotates, two-finger pinch zooms. The
transport bar wraps and the tour panel repositions above it automatically.

**Keyboard**: Space play/pause · P Park · E epicycles · C construction · 1/2/3/4 camera views ·
←/→ step θ ±2° while paused (or navigate the tour) · Esc exit tour.

## Conventions & geometry notes

- Readouts follow the selected convention; the 3-D geometry itself is convention-free
  (a circle of amplitude A has geometric radius √(3/2)·A in abc-space — exactly the
  power-invariant Clarke magnitude).
- Harmonic sequence identities fall out of the math literally: the code applies
  cos(h·(θ − j·120°)) and h = 3, 5, 7 automatically produce zero / negative / positive sequence.

## Run

Open `ClarkePark3D.html` in any browser (internet needed for the Three.js CDN), or serve the
folder with any static server. `window.__cp` exposes params, tour control, PLL state, camera
presets and `selftest()` for scripting.

## Roadmap ideas (from the design review)

Split-screen stationary-vs-rotating observer, machine-stator MMF inset ("the winding layout IS
the Clarke transform"), instantaneous p-q power (2ω ripple hitting the DC link), SVM hexagon
voltage limit, dq spectrum bars (DC/2ω/6ω/12ω), DDSRF/T-half filtering demo, real 50/60 Hz
time base with slow-motion factor, touch/mobile bottom-sheet layout.

by: David Urbaez
