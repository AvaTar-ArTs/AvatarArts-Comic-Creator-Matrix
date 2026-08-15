# Prompt Compiler

Prompts are compiled from stable canon blocks plus scene-specific state. The compiler must preserve identity while allowing action, lighting, and emotion to change.

## Block order

1. CANON: storyworld rules and visual thesis.
2. CHARACTER: silhouette, face anchors, clothing anchors, forbidden mutations.
3. CURSE STATE: hunger, price, activated behavior, palette state.
4. REALM: location, material culture, weather, historical texture.
5. ACTION: one readable verb and one displaced object.
6. EMOTION: private feeling expressed through posture or composition.
7. COMPOSITION: page type, camera, focal hierarchy, reading direction.
8. LIGHT: key, fill, shadow behavior, color-state.
9. LETTERING: voice role and reserved text regions.
10. TEXTURE: paper, ink, grain, stain, print imperfection.
11. NEGATIVE: generic fantasy ornament, random wings or horns, extra limbs, unreadable text, floating props, continuity drift.

## Prompt rule

One panel gets one primary visual action. If the prompt contains more than one dramatic verb, split the panel or choose the dominant verb.

## Identity rule

Every generated panel must include character references, asset versions, palette state, seed, prompt version, and continuity status.