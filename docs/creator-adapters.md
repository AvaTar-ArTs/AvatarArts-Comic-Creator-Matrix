# Creator Adapters and Unified Compiler

The repository combines proven ideas from the AvatarArts creator projects into one compiler rather than forcing every creator into one UI.

| Source capability | Adapter role |
|---|---|
| ai-comic-factory | Orchestration, providers, JSON panels, layout presets, continuation, export |
| ComicBook-AI | React editing surface, search, sharing, PDF, Firebase-style persistence |
| comics_generator | Scenario-to-panels, Pillow compositing, img2img, style presets |
| comic-cult | Dialogue generation, Canvas compositing, delivery workflows |
| Manga-Colorization-FJ | Denoise, colorization, tiling, restoration, upscaling |
| spirit-alley | Ledger, ritual, catalog, progression, evidence, and proof structures |

## Compiler layers

1. Storyworld canon
2. Narrative planning
3. Visual continuity
4. Generation orchestration
5. Page, scroll, and lettering composition
6. Finishing, provenance, and publishing

## Panel record

~~~json
{
  "panel_id": "ep01-p04",
  "purpose": "recognition",
  "caption": "The bottle was not where he left it.",
  "speech": [],
  "visual_instruction": "A scarlet bottle on a cold archive shelf, label facing away.",
  "layout_slot": "wide-03",
  "character_refs": ["cursemaster"],
  "realm_refs": ["archive-basement"],
  "palette_state": "self-control",
  "provider": "image-provider",
  "model": "configured-at-runtime",
  "seed": 1842,
  "prompt_version": "v1.2",
  "asset_versions": ["cursemaster-v3", "bottle-v2"],
  "continuity_status": "pending"
}
~~~

Security rule: never ship provider keys in browser code. Keep secrets server-side, use environment variables, and log provider/model/seed metadata for reproducibility.