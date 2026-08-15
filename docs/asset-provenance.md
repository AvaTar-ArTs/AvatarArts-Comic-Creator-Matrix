# Asset Provenance and Continuity

Every image, panel, page, video shot, and export receives a durable identity.

## Required metadata

- storyworld_id
- episode_id and panel_id or shot_id
- character, realm, relic, and motif references
- provider and model
- seed and generation timestamp
- prompt version and negative prompt version
- source asset versions
- postprocess operations
- human approvals and revision notes
- export dimensions and format

## Continuity protocol

1. Freeze canon before generation.
2. Generate with explicit reference IDs.
3. Compare silhouette, face, costume, palette, setting, and motif state.
4. Mark each panel approved, needs revision, or rejected.
5. Keep rejected outputs linked rather than silently deleting them.
6. Archive the final page with its panel manifest.

## Proof over confidence

When an asset conflicts with canon, the system should show the conflict and request a decision. It must never hide uncertainty behind fluent prose.