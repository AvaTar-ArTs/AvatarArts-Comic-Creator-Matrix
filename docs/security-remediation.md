# Security Remediation Record

## Scope

This record closes the investigation findings for the six-repository review and tracks code-level remediation separately from operational credential rotation.

## Findings and status

| Finding | Repository | Code status | Operational action |
|---|---|---|---|
| Browser-exposed OpenAI key | ComicBook-AI | Fixed in draft PR #1 | Revoke the exposed key and configure server-side image generation |
| Embedded Gmail credential | comic-cult | Fixed in draft PR #1 | Revoke the credential and configure SMTP environment variables |
| Fixed recipient addresses | comic-cult | Fixed in draft PR #1 | Set COMIC_DELIVERY_TO at deployment time |
| Fragile panel parser | comics_generator | Fixed in draft PR #1 | Review JSON contract against the chosen LLM |
| Missing asset manifest | comics_generator | Fixed in draft PR #1 | Preserve manifests with generated output bundles |

## History policy

No Git history rewrite was performed. This preserves collaborator safety and avoids pretending that a public secret was never exposed. Provider-side revocation remains mandatory.

## Proprietary rule

AvatarArts Forge treats security, provenance, parsing integrity, and continuity as one trust boundary: an artifact is not publishable unless its source, transformation path, and configuration are inspectable.
