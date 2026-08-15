# Comparative Analysis

## Capability matrix

| Capability | ai-comic-factory | ComicBook-AI | comics_generator | comic-cult | Manga-Colorization-FJ | Spirit Alley |
|---|---|---|---|---|---|---|
| Narrative decomposition | Strong | Minimal | Strong but fixed | Dialogue-focused | None | Strong state interpretation |
| Image generation | Multi-provider | DALL-E client | Stability API | Stability API | Local PyTorch postprocess | None |
| UI/editor | Strong | Strong | None | Basic web flow | CLI | Web foundation |
| Storage/search | Community/share surfaces | Firebase/search | Filesystem | Filesystem/PDF/email | Input/output dirs | Catalog and capsules |
| Layout/composition | Presets and panels | UI cards/PDF capture | Fixed 2x3 strip | Canvas text band/PDF | None | None |
| Typography | Font/preset metadata | Editable text | Pillow font | Canvas text | None | None |
| Continuity/provenance | Partial render metadata | Weak | Weak | Weak | File-level only | Strong evidence model |
| Finishing | Basic rendering | Browser export | Pillow assembly | Canvas/PDF | Denoise/color/upscale | None |
| Delivery | Share/export | PDF/share/cloud | Local strip | Email/PDF | Local output | Web/live handoff |

## What should be learned

- From ai-comic-factory: provider adapters, render status, style records, server-side configuration, and a real creator workflow.
- From ComicBook-AI: editable cards, upload/search, cloud persistence, PDF export, and end-to-end testing.
- From comics_generator: small decomposable Python stages and explicit scenario-to-panel prompting.
- From comic-cult: dialogue as a separate stage, server-side compositing, job sequencing, and delivery.
- From Manga-Colorization-FJ: postprocess stages, grayscale detection, tiling, denoise, and super-resolution.
- From Spirit Alley: proof-aware state, source versus personal state separation, portable capsules, catalogs, and stateful progression.

## What should not be copied

- Hardcoded credentials or browser-side API keys.
- Asking image models to render final readable dialogue.
- Fixed six-panel assumptions.
- Regex-only parsing for structured story data.
- Random filenames without asset manifests.
- UI-capture-based publishing as the canonical data model.
- Treating external reference pages as proof of a user's personal state.
- Treating style as a list of famous labels rather than a controlled visual grammar.

## Architectural conclusion

The right abstraction is not an AI comic factory. It is a **Storyworld Compiler**.

Inputs become typed evidence, canon, intention, and constraints. The compiler then produces narrative beats, panel records, visual prompts, assets, page compositions, finishing passes, and publishing packages. Every output remains traceable to the storyworld state that produced it.

## Proprietary differentiator

AvatarArts should own the semantic layer:

- canon and contradiction management
- character identity anchors
- motif and relic state
- curse/psychology mechanics
- proof and revision states
- format-aware visual grammar
- asset provenance
- reader simulation

Providers, renderers, fonts, cloud storage, and postprocessors become replaceable adapters around that layer.