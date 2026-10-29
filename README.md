# AI Character Asset Reverse Prompt

An Agent Skill for turning one or more character references plus art direction into a reusable identity specification, model-ready prompts, and production-oriented multi-view character identity cards.

中文：这是一个用于 AI 图片与短视频角色资产生产的 Agent Skill。它会区分参考图中可观察到的特征、用户明确提出的要求和必要推定，并生成稳定的角色身份锁、多视角身份卡提示词及精简平台提示词。

## What it does

- Extracts visually supported face, hair, body, and wardrobe directions.
- Separates **observed**, **requested**, and **inferred** information.
- Produces a geometry-based identity lock instead of vague beauty adjectives.
- Supports reverse-prompt-only, identity-card, and platform-adaptation deliverables.
- Provides `headless-body` and `full-head` body-panel modes.
- Validates identity consistency, garment continuity, anatomy, skin texture, and panel completeness.
- Keeps the complete rear head and hairstyle visible in the back body panel while avoiding distant-face drift in front and side body panels.

## Safety and scope

- This Skill does not recover an original hidden prompt, seed, model, LoRA, or private generation settings.
- Reference-based results are approximations.
- Do not use identifiable real-person likenesses without permission for the intended reuse.
- When permission is unavailable, use references only for broad, non-identifying directions and create a new fictional identity.
- Do not publish user reference images or generated likeness assets without the necessary rights.

## Repository structure

```text
ai-character-asset-reverse-prompt/
├── SKILL.md
├── agents/
│   └── openai.yaml
└── references/
    ├── card-spec.md
    └── prompt-template.md
```

## Installation

### Codex

```bash
git clone https://github.com/cadyyue-blip/ai-character-asset-reverse-prompt.git \
  ~/.codex/skills/ai-character-asset-reverse-prompt
```

Restart the agent session if the new Skill is not discovered immediately.

### Other Agent Skills-compatible tools

Clone or copy this repository into the tool's Skill directory. The entry point is `SKILL.md`; supporting rules are under `references/`.

## Usage

Invoke the Skill and provide at least one usable character reference plus the intended direction:

```text
Use $ai-character-asset-reverse-prompt.
Create an identity card from these references.
Wardrobe: minimal basics.
Presentation: photorealistic young adult.
Body-panel mode: headless-body.
Must keep: the rear hairstyle visible in the back body panel.
```

The Skill can return:

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

Image generation is performed by the image-generation capability available in the host agent. This repository does not bundle a model, API key, or image-generation backend.

## Using it with LibTV / LiblibAI

This repository is a **character-design and prompt-construction Skill**. LibTV's official `libtv-skill` is a separate execution Skill that connects an agent to LibTV for image and video generation.

Recommended composition:

1. Install this Skill to analyze references and produce the identity lock, long prompt, compact prompt, and validation rules.
2. Install the official [`libtv-labs/libtv-skills`](https://github.com/libtv-labs/libtv-skills) integration and configure its required LibTV access credentials according to its documentation.
3. Ask the agent to use this Skill first, then pass the finalized generation prompt and permitted reference assets to `libtv-skill` for execution.
4. Keep the generated identity card as the identity anchor for later LibTV image-to-video or multi-shot workflows.

Publishing this repository on GitHub does not automatically list it inside LibTV. To request inclusion in LibTV's official repository, open an Issue or submit a Pull Request to [`libtv-labs/libtv-skills`](https://github.com/libtv-labs/libtv-skills) and follow the maintainers' review requirements.

## License

MIT. See [LICENSE](LICENSE).

