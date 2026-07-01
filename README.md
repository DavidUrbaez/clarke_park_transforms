# Clarke & Park Transforms as Geometry

Interactive 3-D visualization of the abc → αβ0 → dq0 transforms. Companion piece to
`transmission_line_transients/LineWave3D.html` (same stack: single self-contained HTML file,
Three.js via CDN import map, OrbitControls, lil-gui).

## The idea

Plot the instantaneous point **(i_a, i_b, i_c)** in a 3-D space whose axes are the three phases.

- **Balanced** three-phase signals never leave the plane **a + b + c = 0** — shown as a tilted
  translucent disc. The trajectory is a circle in that plane.
- The **Clarke transform** is just a change of axes: α and β span the disc, the 0-axis
  (purple, along (1,1,1)) is perpendicular to it.
- The **Park transform** is a frame rotating with the vector. The "Park (dq) frame" toggle
  rotates the whole world by −θ about the 0-axis, so the space vector freezes and the abc
  axes visibly spin backwards.

## Things to try

| Action | What it teaches |
|---|---|
| ▶ look down 0-axis | a, b, c axes project 120° apart — the classic space-vector diagram |
| Park (dq) frame toggle | rotating-frame intuition: vector freezes, world counter-rotates |
| negative seq A₂ | circle → ellipse; d and q wobble at 2ω (why unbalance hits controllers) |
| zero seq A₀ | the ball leaves the plane, sliding along the 0-axis (what αβ can't see) |
| 5th harmonic A₅ | lobed orbit; 6ω ripple in dq |

Conventions: amplitude-invariant Clarke (α = (2a−b−c)/3, β = (b−c)/√3, 0 = (a+b+c)/3).
Note the geometric radius of the circle in abc-space is √(3/2)·A for amplitude A — the HUD
readouts show the amplitude-invariant Clarke/Park values, not the raw geometric length.

## Run

Open `ClarkePark3D.html` in any browser (needs internet access for the Three.js CDN),
or serve the folder with any static server.

A `window.__cp` handle (params, camera presets, transform functions) is exposed in the
console for testing/scripting.
