# Repository Investigation

This document records what each reference repository actually does, how it does it, and where its implementation boundary ends. Spirit Alley is analyzed as an authored AvatarArts project, but under the same evidence and critique standard as every other repository.

## 1. ai-comic-factory

Repository: https://github.com/AvaTar-ArTs/ai-comic-factory

### What it does
- Generates comic scenes from a prompt.
- Uses an LLM to produce scene/panel descriptions.
- Sends rendering requests through selectable providers.
- Supports visual families such as Japanese, Franco-Belgian, American, and other presets.
- Provides a Next.js interface with panel display, layout selection, settings, progress, editing, sharing, and continuation surfaces.

### How it works
- `src/app/engine/render.ts` selects OpenAI, Replicate, Hugging Face inference, or VideoChain-style backends through environment configuration.
- The render function builds a request, chooses dimensions from panel orientation, generates or receives a seed, and returns a render ID, status, asset URL, alt text, and error state.
- `src/app/engine/caption.ts` sends an image and prompt to an analysis endpoint and returns a textual result.
- `src/app/engine/presets.ts` couples family, color mode, font, LLM prompt additions, image prompt additions, and negative prompt additions.
- Frontend modules separate panels, layouts, bubbles, progress, settings, zoom, share, and authentication.

### Strengths
- Provider abstraction and asynchronous render status.
- Strongest existing reference for a full creator-facing generation loop.
- Style presets are structured data rather than scattered UI conditionals.
- Server-side credential handling is the correct direction.

### Limitations
- Style is mostly prompt vocabulary and preset metadata, not a deeper grammar of page rhythm, character state, or lore.
- Rendering and narrative continuity remain loosely coupled.
- The system is difficult to treat as a durable storyworld compiler without adding canonical schemas and provenance.

## 2. ComicBook-AI

Repository: https://github.com/AvaTar-ArTs/ComicBook-AI

### What it does
- React/Vite interface for generating, uploading, editing, searching, storing, sharing, downloading, and exporting comic cards.
- Uses Firebase/Firestore-oriented persistence and Firebase hosting.
- Uses Cypress end-to-end tests for core flows.

### How it works
- `ImageGenerator.jsx` collects a prompt, calls an image-generation endpoint, stores returned image URLs in React state, and provides downloads.
- `ComicBookPage.jsx` accepts uploaded images, pairs them with editable text, renders cards, and converts the card elements to a PDF through html2canvas and jsPDF.
- Search and upload surfaces are paired with cloud persistence in the Firebase layer.

### Strengths
- Clear creator UI and handoff model.
- Editable outputs instead of a one-shot generator.
- Practical publishing features: PDF, search, upload, and sharing.
- E2E testing gives a useful product-quality baseline.

### Limitations and security finding
- The inspected `ImageGenerator.jsx` contains a hardcoded OpenAI secret. This must be revoked and replaced with a server-side proxy and environment-managed credentials.
- The card model is primarily image plus text; it does not preserve panel purpose, speaker metadata, camera, references, seed, or continuity status.
- PDF export captures the UI rather than compiling from a semantic page specification.

## 3. comics_generator

Repository: https://github.com/AvaTar-ArTs/comics_generator

Default branch: `master`.

### What it does
- Converts a short scenario into a six-panel comic strip.
- Uses an LLM for panel decomposition.
- Generates each panel with Stable Diffusion/Stability API.
- Adds text with Pillow.
- Combines panels into a fixed 2x3 strip.

### How it works
- `generate_panels.py` asks an LLM to split a scenario into six blocks and extract description/text with regular expressions.
- The prompt repeats character physical descriptions in each panel to reduce identity drift.
- `add_text.py` appends a white text band below the image using a bundled manga font.
- `create_strip.py` resizes images, adds black spacing, places them into a 2x3 grid, and resizes the final strip to 1024x1536.

### Strengths
- Minimal and understandable scenario-to-panel pipeline.
- Explicit attempt to repeat character descriptors.
- Easy-to-replace Python stages.
- Demonstrates the value of style-specific output examples.

### Limitations
- Fixed six-panel structure.
- Regex parsing is brittle.
- Text is appended below the panel instead of composed as an integrated page element.
- No durable character registry, scene state, provenance, continuity review, or provider abstraction.

## 4. comic-cult

Repository: https://github.com/AvaTar-ArTs/comic-cult

Default branch: `backup-branch`.

### What it does
- Converts text into shorter character dialogue.
- Generates comic-style images with Stability AI.
- Composites dialogue and borders with Node Canvas.
- Builds a PDF.
- Delivers the result by email with Nodemailer.
- Includes feature-flag infrastructure.

### How it works
- `server/utils/Controller.js` asks Gemini to turn source text into dialogue lines.
- A simple speaker/dialogue parser converts lines into JSON-like records.
- Stability text-to-image receives one prompt per dialogue record, with a fixed comic-book preset, dimensions, steps, guidance, and seed.
- Node Canvas draws a large white dialogue area, writes speaker text, and adds a border.
- `server/index.js` orchestrates the request, image generation, PDF creation, and email delivery.

### Strengths
- Clear end-to-end delivery pipeline.
- Demonstrates dialogue generation as an independent stage.
- Includes server-side composition and PDF assembly.
- Feature flags and promise-based sequencing are useful operational patterns.

### Limitations and security finding
- The inspected server file contains embedded Gmail credentials and fixed recipient addresses. These must be treated as compromised and removed.
- The `diffusionKey` parameter is accepted but the controller uses an environment key, creating confusing credential semantics.
- Dialogue parsing is fragile and image prompts ask the image model to render readable dialogue, which is unreliable.
- Output files use random names and shared directories rather than job-scoped manifests.

## 5. Manga-Colorization-FJ

Repository: https://github.com/AvaTar-ArTs/Manga-Colorization-FJ

### What it does
- Detects grayscale input.
- Denoises manga imagery.
- Colorizes grayscale panels with a trained PyTorch generator.
- Supports tiled processing for limited GPU memory.
- Optionally applies Real-ESRGAN anime super-resolution.
- Copies already-colored files rather than recoloring them.

### How it works
- `inference.py` parses input/output, CPU/GPU, tile, denoise, and super-resolution options.
- `is_grayscale()` samples resized pixels and computes a color variance heuristic.
- `MangaColorizator.set_image()` denoises, resizes/pads to a compatible size, and prepares color hints.
- `colorize()` runs the generator, removes padding, then optionally runs tiled or full-image Real-ESRGAN.
- Outputs are written as WebP.

### Strengths
- A concrete finishing stage with memory-aware tiling.
- Separates restoration, colorization, and super-resolution.
- Useful for monochrome manga, rough ink, archival scans, and post-generation cleanup.

### Limitations
- It is an image postprocessor, not a comic-aware continuity system.
- Colorization is not linked to storyworld palette state, emotional state, or scene metadata.
- Model weights and runtime assumptions require explicit packaging and licensing review.

## 6. Spirit Alley

Repository: https://github.com/AvaTar-ArTs/spirit-alley

Authorship: authored AvatarArts project. This affects provenance, not its evaluation standard.

### What it does
- Models a personal evidence-grounded companion ecosystem.
- Separates catalog truth from personal state.
- Uses a ledger with `known`, `accepted`, `unlocked`, `active`, and `sealed` states.
- Supports rituals, source catalogs, session capsules, web companions, streaming overlays, and future voice interfaces.

### How it works
- `schemas/ledger.schema.json` defines typed entries, proof types, state transitions, source categories, spoiler modes, and stream-safe outputs.
- `catalog/doorways.yaml` stores structured content entries with starters, proofs, opens, pause points, sources, and public summaries.
- `docs/ARCHITECTURE.md` separates add-on, catalog, web, and live layers.
- The handoff capsule makes state portable between local runtime, web companion, NotebookLM-style packets, and streaming surfaces.

### Strengths
- Strongest evidence/proof model in the group.
- Separates reference knowledge from personal state.
- Treats progression as an interpretable state machine rather than a completion percentage.
- Designed for portability across interfaces.

### Limitations
- Its domain model is game-companion oriented and needs adaptation before it can represent panels, scenes, characters, motifs, and visual assets.
- Current foundation is schema/catalog heavy; execution layers are intentionally still future work.
- It does not yet provide a comic renderer, page composer, or image-generation adapter.

## Overall observation

These repositories are not interchangeable products. They represent different layers: generation, UI, decomposition, delivery, restoration, and evidence state. The proprietary system should preserve those distinctions while giving them one shared semantic contract.