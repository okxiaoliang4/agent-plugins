---
name: cinematic-3d-sites
description: Direct and build distinctive cinematic 3D websites when a marketing experience uses WebGL or Three.js, scroll-directed
  scenes, interactive models, scientific structures, or product storytelling. Use for concept prompts, art direction, shot
  design, 3D asset strategy, implementation, or focused refinement; ordinary UI pages and analytical 3D charts remain outside
  this workflow.
---

# Cinematic 3D Sites

Direct a film with an interactive subject, not a page with a 3D decoration. Repeat the decision process; vary every visual answer.

## Route the request

- For a concept, prompt, treatment, or storyboard, read [references/prompt-grammar.md](references/prompt-grammar.md). Stop after the requested planning artifact unless implementation is also requested.
- For visual exploration or a new aesthetic direction, read [references/direction-fingerprint.md](references/direction-fingerprint.md).
- For implementation or refinement of a working site, read [references/threejs-production.md](references/threejs-production.md).

Read every reference required by the active branch before acting.

## Direct the experience

### 1. Earn the third dimension

Name the meaning carried by depth, camera, lighting, or model state. Prefer a 2D or hybrid treatment when 3D adds only ornament or loading cost.

Complete when one sentence connects a 3D behavior to the audience's understanding or emotion.

### 2. Ground the subject

Inspect supplied references, the current site, existing code, models, and brand assets. Separate real source data from illustrative states. Preserve provenance for scientific or product models; label simulated candidates, measurements, and scores as demonstrations.

Complete when every visible 3D subject has a source, generation plan, or explicit demo status.

### 3. Lock a direction fingerprint

Use the fingerprint reference to derive the spatial metaphor, composition, camera grammar, material logic, light logic, interface voice, and signature transition from this brief. Generate three substantially different fingerprints internally. Present alternatives only when exploration is requested; otherwise select the strongest and state it in a compact direction memo.

Complete when the chosen fingerprint would still be recognizable with brand names and colors removed.

### 4. Write the shot logic

Treat scroll as time. Give each beat a purpose and define the starting and ending state of camera, model, light, atmosphere, copy, and interface. A beat earns its place by changing meaning, not by replacing text. Use quiet holds between dense transformations.

Complete when every beat changes the subject or the viewer's relationship to it, and every transition has an entry, hold, and exit.

### 5. Bind interface to model state

Make panels, labels, selections, and measurements describe the state visible in 3D at that moment. Candidate selection changes the model. Sequence selection highlights the corresponding residue. Focus states suppress context until one relationship is unmistakable.

Complete when every interactive or scroll-selected UI state has a matching model, camera, material, or annotation state.

### 6. Build a tracer scene

Implement the smallest scene that proves the direction: one real subject, one camera move, one lighting/material treatment, one synchronized interface state, and reduced-motion behavior. Expand only after this scene works. Preserve the repository's stack and patterns.

Complete when the tracer scene runs locally, reverses cleanly with scroll, and demonstrates the fingerprint without relying on later scenes.

### 7. Expand and prove

Add only the beats needed for the narrative. Verify build/type checks, loading and model failures, desktop and mobile framing, scroll reversal, reduced motion, device-pixel-ratio limits, and cleanup of WebGL resources. Respect a user's choice to perform visual judgment themselves; report functional checks separately from visual acceptance.

Complete when the requested experience works, the narrowest relevant checks pass, and unverified visual or device behavior is named.

## Invariants

- Keep the 3D subject stateful and causally tied to the story.
- Derive material and light from the subject's world; a dark background, neon accent, and glass surface are choices, not defaults.
- Concentrate attention. During a highlight, dim or hide bulk geometry before adding more glow.
- Keep cinematic motion interruptible and reversible. Scroll may retarget continuously without restarting an entrance.
- Prefer transform and opacity for DOM motion. Interpolate camera and model state in the render loop without per-frame React state or repeated DOM queries.
- Give reduced motion an authored composition, not a broken still frame.
- Preserve truth: real measurements come from real geometry; illustrative values carry an explicit demo label.
