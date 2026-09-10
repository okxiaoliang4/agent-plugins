# Three.js production notes

Use these notes for implementation or targeted refinement. Match the repository's rendering layer: plain Three.js, React Three Fiber, or another existing WebGL stack.

## Timeline architecture

- Keep the viewport stage sticky and let document height provide scroll travel.
- Normalize scroll to `0..1`, then map it to semantic phases. Store scene values in keyframes or named state functions rather than scattering thresholds.
- Smooth continuous camera/model values with reversible interpolation or a damped spring. Use discrete thresholds only for labels and semantic selection, with hysteresis when jitter is possible.
- Keep one render loop. Update refs and Three.js objects directly; keep per-frame values out of React state.
- Query DOM nodes once and retain references. Do not search the DOM from every frame.

## Scene graph

Separate groups by meaning: target, designed object, alternatives, annotations, measurements, particles, atmosphere, and background ghosts. Each group needs independent visibility and opacity control.

For scientific or configurable subjects, retain data identifiers on geometry: chain, residue, atom, part, variant, or assembly step. UI selection should resolve through these identifiers rather than screen coordinates.

## Model state patterns

### Define

Introduce a constraint with a model-space marker plus a screen-space label. Sequence the entrance: scan/reveal → land on geometry → label. Project the model position into screen coordinates every frame.

### Generate

Move a particle cloud or coarse representation toward real geometry. The final object owns the silhouette; particles explain generation and then leave.

### Compare

Show alternatives in the model, not only in a panel. Crossfade or morph variants in the same spatial context, synchronize the selected row, and make the final lock visually decisive. Label transformed clones as demonstrations unless they are actual candidates.

### Select or edit

Highlight the same entity in the UI and model. Keep a small context window in the sequence/list, dim the rest, and reveal only the corresponding atoms, part, or surface patch. A selected value without a selected shape is an incomplete state.

### Focus and measure

Center the camera on the actual target point. Fade bulk ribbons, atoms, particles, previous copy, and background geometry aggressively; render the measurement and selected atoms above context. Prefer subtraction before glow.

## Materials and light

Start with motivated key, fill, and rim roles. Tune roughness, transmission, clearcoat, attenuation, emissive response, and environment intensity as one material system. Physically plausible response is more convincing than high saturation.

Use transparency sparingly: overlapping translucent surfaces and atom clouds quickly destroy hierarchy. When a selected structure becomes noisy, lower bulk opacity below the contact visualization or hide it entirely.

## Performance and resilience

- Cap device pixel ratio and adapt it for mobile or sustained slow frames.
- Instance repeated atoms or particles; merge static geometry where selection does not require separate objects.
- Avoid allocations inside the render loop. Reuse vectors, matrices, and typed arrays.
- Lazy-load heavy models, show a designed fallback, and handle asset failure without trapping the page behind a blank canvas.
- Dispose geometries, materials, textures, render targets, observers, and listeners.
- Author a reduced-motion state with stable framing, direct state changes, and restrained fades.

## Proof

Check build and type safety first. Then verify first load, reverse scroll, rapid direction changes, resize, mobile crop, touch behavior, reduced motion, model failure, and focus readability. Record visual approval separately when the user owns the final aesthetic judgment.
