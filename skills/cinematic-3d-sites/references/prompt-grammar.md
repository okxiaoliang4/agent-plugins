# Prompt grammar

Write cinematic 3D prompts as direction documents. Describe relationships and state changes more precisely than surface style.

## Prompt structure

```markdown
Create a cinematic 3D web experience for [subject, audience, outcome].

Meaning of 3D
- Depth/model/camera helps the audience understand or feel [specific result].

Direction fingerprint
- Spatial metaphor: [domain-derived world]
- Composition: [frame and negative-space logic]
- Camera grammar: [limited vocabulary of moves]
- Material logic: [physical response tied to subject]
- Light logic: [motivated sources]
- Interface voice: [typographic/information role]
- Signature transition: [subject-specific transformation]

Narrative beats
For each beat, specify purpose and the start → hold → end state of:
- camera
- model/particles
- light/atmosphere
- copy/interface

3D subject
- Source or creation plan: [GLB/glTF/PDB/procedural/generated]
- Required representations: [surface/ribbon/atoms/exploded/sectioned/etc.]
- Interactive states: [focus, compare, edit, select, measure]
- Truth status: [real data vs explicitly labeled demonstration]

Interaction contract
- Map scroll/pointer/touch actions to both interface and model changes.
- Define focus suppression: what fades, what stays, and why.
- Define reverse-scroll and reduced-motion behavior.

Technical envelope
- Stack and existing repository constraints: [actual stack]
- Performance target: [devices, DPR cap, asset budget, loading behavior]
- Accessibility: [contrast, readable copy, reduced motion, keyboard semantics]
- Acceptance: [functional checks and who performs visual approval]

Originality constraints
- Derive the look from [domain cues and references by attribute].
- Keep [two or three deliberate contrasts].
- Make the signature transition impossible to reuse unchanged for another subject.
```

## Prompt quality checks

- Replace adjectives such as "premium," "futuristic," and "cool" with observable light, material, framing, or timing behavior.
- Name what the model does during every scroll beat. "Parallax" alone is not choreography.
- Name what becomes quiet during focus. Highlights fail when all other geometry stays equally legible.
- Ask for source-backed geometry or label procedural alternatives as demos.
- State whether the agent should align on direction before building, create variants, implement directly, or leave visual judgment to the user.

## Compact request

When the user wants a short prompt, retain five things: meaning of 3D, fingerprint, signature transition, model/UI synchronization, and acceptance criteria. Remove prose before removing these constraints.
