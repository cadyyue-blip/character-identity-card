---
name: ai-character-asset-reverse-prompt
description: Analyze one or more character reference images plus custom art direction, reverse-specify the visible identity, and optionally generate a production-ready multi-view character identity card for AI image or short-video workflows. Use for character sheets, identity locking, face-angle references, or headless distant-body assets; do not claim to recover an image's original hidden prompt.
---

# AI Character Asset Reverse Prompt

Turn user-supplied character references into a reusable identity specification, model-ready prompts, and—when requested—a generated character identity card.

## Required inputs

- At least one usable character reference image.
- The user's custom direction: wardrobe, age/presentation, realism, intended platform, and any must-keep or must-change traits.

Multiple angles improve reliability but are not mandatory. Separate what is **observed**, **requested**, and **inferred**. Never present inferred anatomy, body proportions, or hidden details as facts from the source image.

Before generating or editing, inspect every local image with the available image-viewing tool. Label each input image's role: identity anchor, body/wardrobe reference, style reference, or layout reference.

## Choose the deliverable

1. **Reverse prompt only** — identity specification plus long and compact prompts.
2. **Identity card** — specification, prompts, and a generated multi-panel card.
3. **Prompt adaptation** — rewrite the same identity for a named image/video platform without generating an image.

If the user asks for a card, use the image-generation capability. Read [references/card-spec.md](references/card-spec.md) before generation. Read [references/prompt-template.md](references/prompt-template.md) when drafting the generation prompt or compact platform prompt.

## Core workflow

1. Extract only visually supported identity anchors: facial geometry, hair silhouette, complexion range, apparent age range, body silhouette, wardrobe, and distinctive asymmetries.
2. Resolve contradictions across references by prioritizing, in order: the user's explicit instruction, the designated identity anchor, repeated evidence across images, then cautious inference.
3. Produce an identity lock that describes relationships and proportions, not vague beauty adjectives.
4. Select a body-panel mode:
   - `headless-body` for reliable distant-body assets. The front and side/three-quarter body panels are cleanly framed from the collar/shoulder line to the shoes, with white negative space above. The 180-degree back body panel is the required exception: show the complete rear figure from the back of the head to the shoes so the rear hairstyle and head silhouette remain visible. It must face directly away and reveal no facial features or side-face profile. Do not blur, mosaic, pixelate, erase, or show an anatomical neck stump.
   - `full-head` when the user explicitly needs conventional full-body turnarounds and accepts the higher risk of face drift.
5. Generate the card from the references, preserving identity and wardrobe. The reference image is evidence, not an edit target, unless the user explicitly requests an edit.
6. Inspect the result for identity drift, panel completeness, limb errors, garment inconsistency, accidental face content in the headless front/side panels, and a missing, cropped, or face-revealing head in the back panel. Make at most two focused revisions unless the user asks to continue.
7. Return the final image, the observed/requested/inferred identity specification, the exact generation prompt, and a compact prompt suitable for point-consuming tools.

## Non-negotiable invariants

- Every clear face panel must depict the same person: consistent skull shape, eye spacing, nose structure, lip shape, jawline, ears, hairline, hair color, and apparent age.
- Body panels must keep the same height impression, shoulder width, torso-to-leg ratio, garment construction, colors, accessories, and footwear.
- In `headless-body` mode, the back panel must preserve the complete rear head and hairstyle. If the reference does not show the rear hairstyle, derive the most conservative continuation of the visible hair silhouette and label it as inferred rather than observed.
- Use a neutral white studio background, soft standardized lighting, and panel separators. Do not introduce scenery, props, logos, captions, watermarks, or decorative typography unless requested.
- Preserve natural skin microtexture without beauty-filter smoothing, plastic skin, fake pore noise, aggressive sharpening, or exaggerated HDR.
- A reference-based result is an approximation. Do not claim the original generator prompt, seed, LoRA, model, or hidden settings were recovered.
- For an identifiable real person's likeness, confirm the user has permission for the intended reuse when that is not already clear. Do not frame an unauthorized likeness replica as a reusable commercial identity.

## Output structure

Keep the analysis concise and production-oriented:

```text
Mode: reverse prompt | identity card | prompt adaptation
Body-panel mode: headless-body | full-head
Observed identity anchors: ...
Requested direction: ...
Inferred or unresolved details: ...
Identity lock: ...
Long generation prompt: ...
Compact platform prompt: ...
Validation notes: ...
```

When an image is generated, save the final selected asset into the current workspace and report its absolute path.
