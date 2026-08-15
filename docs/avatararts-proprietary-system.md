# AvatarArts Proprietary Storyworld Compiler

## Working name

**AvatarArts Forge: the Evidence-to-Artifact Storyworld Compiler**

## Core principle

Do not begin with an image prompt. Begin with a world-state claim.

The system asks:

> What is true, what is believed, what is witnessed, what is desired, and what must remain visually consistent?

## Six semantic layers

1. **Intent** — brief, audience, genre, format, emotional contract.
2. **World** — canon, lore, locations, factions, rules, eras, myth systems.
3. **Identity** — character anchors, relationships, wounds, desires, transformations, forbidden drift.
4. **Dramaturgy** — beats, choices, reversals, secrets, consequences, page-turn questions.
5. **Evidence** — references, proofs, motifs, relics, contradictions, approvals, unresolved uncertainty.
6. **Artifact** — prompts, generated assets, panels, lettering, pages, scrolls, video shots, exports.

## Agent roles

- **Spark**: expands a premise into divergent concepts.
- **Cartographer**: maps realms, factions, routes, resources, and visual cultures.
- **Canonist**: freezes rules and flags contradictions.
- **Psychologist**: turns wound, desire, fear, and behavior into visual action.
- **Dramaturge**: builds beats and consequences.
- **Panelwright**: converts beats into panel records and layout grammar.
- **Promptsmith**: compiles provider-neutral prompts from canon and scene state.
- **Forge**: calls image, dialogue, colorization, and rendering adapters.
- **Letter-Witch**: applies voice-specific lettering and sound design.
- **Archivist**: writes manifests, versions, sources, seeds, and approvals.
- **Red Pen**: performs visual, canon, continuity, and reader simulation checks.
- **Publisher**: creates print, manga, comic, webtoon, video, and archive packages.

## Canonical objects

- `Storyworld`: rules, themes, eras, sources, and visual thesis.
- `Character`: identity anchors, relationships, psychology, state, and forbidden changes.
- `Realm`: geography, atmosphere, materials, customs, threats, and palette behavior.
- `Motif`: recurring object, symbol, phrase, gesture, or composition with changing meaning.
- `Beat`: intention, conflict, choice, reveal, and consequence.
- `Panel`: visual action, camera, layout slot, text, references, and continuity status.
- `Asset`: provider, model, seed, prompt version, source assets, postprocess, and approval.
- `Publication`: format, dimensions, order, lettering, export, and rights/provenance.

## Pipeline

~~~text
brief
  -> brainstorm
  -> research packet
  -> storyworld canon
  -> character and realm registry
  -> beat map
  -> panel plan
  -> prompt compilation
  -> generation adapters
  -> continuity review
  -> lettering and composition
  -> finishing adapters
  -> reader simulation
  -> publication bundle
~~~

## State model

Every important claim and artifact uses a state:

- `proposed`: an idea under consideration.
- `observed`: present in a source, reference, or generated output.
- `canon`: accepted as a rule of the storyworld.
- `generated`: produced by an adapter.
- `needs_revision`: conflicts with canon, quality, or intent.
- `approved`: accepted for downstream use.
- `published`: included in a released package.
- `superseded`: retained for provenance but no longer current.

## Format adapters

- Comic page: page turns, gutters, balloons, panel hierarchy.
- Manga: monochrome control, decompression, reaction timing, right-to-left option.
- Webtoon: vertical rhythm, scroll gaps, mobile lettering, sequential reveal.
- Graphic novel: chapter architecture, recurring visual motifs, long-form continuity.
- Animation: keyframe panels, motion causality, sound/lettering timing.
- Archive: source packets, manifests, prompt history, and rejected alternatives.

## Build boundary

The proprietary core must remain provider-neutral. AI image vendors, LLM vendors, Firebase-like storage, PDF libraries, Canvas, PyTorch colorizers, and super-resolution models are adapters. They should be replaceable without changing the storyworld or panel schemas.

## First implementation slice

1. Expand the existing storyworld and panel schemas.
2. Add character, realm, motif, beat, asset, and publication schemas.
3. Build a local JSON/YAML compiler that turns a brief into a validated panel plan.
4. Add one image adapter and one deterministic page compositor.
5. Add manifest and continuity reports.
6. Add the remaining providers and finishing stages behind adapters.

## Ownership boundary

The unique AvatarArts value is not any single model call. It is the accumulated system of world logic, visual identity, psychological progression, evidence, state, and artifact provenance that makes outputs recognizably yours.