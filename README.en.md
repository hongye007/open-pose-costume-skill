# Open Pose & Costume Skill

[中文](README.md) · **English**

A Codex skill that combines **pose + costume + character** into one character image. The character reference guides identity and style, the pose reference guides the gesture, and the costume reference guides the outfit.

[Reference gallery](https://hongye007.github.io/open-pose-costume/) · [Skill instructions](skills/pose-costume-character/SKILL.md) · [Download the skill](https://github.com/hongye007/open-pose-costume-skill/releases/latest)

## Features

- Combine character, pose and costume references into a single image.
- Accept attached images, local files, accessible image URLs and clear text descriptions.
- Select references from Open Pose & Costume by ID or keyword, such as `P047` and `SPR-0050`.
- Guide facial identity, hair, body support, garment shape and materials separately, avoiding mannequin lines or the outfit model's face.
- Inspect, save and display the generated result.

## Install

Ask Codex:

> Use skill-installer to install skills/pose-costume-character from hongye007/open-pose-costume-skill.

Or use the bundled Codex installer on macOS / Linux:

```sh
python3 "${CODEX_HOME:-$HOME/.codex}/skills/.system/skill-installer/scripts/install-skill-from-github.py" \
  --repo hongye007/open-pose-costume-skill \
  --path skills/pose-costume-character
```

Restart Codex after installation to discover the skill. If a skill with the same name already exists, back it up before updating; avoid nesting another copy inside it.

The [release page](https://github.com/hongye007/open-pose-costume-skill/releases/latest) also provides a `.skill` ZIP archive containing `pose-costume-character/`. Extract that folder into `$CODEX_HOME/skills/` (default: `~/.codex/skills/`).

## Usage

After attaching three images:

```text
Use $pose-costume-character.
Image 1 is the character, image 2 the pose, and image 3 the costume.
Preserve the character's face, hair and visual style.
Apply the referenced gesture and outfit to produce one complete character image.
```

Use gallery IDs with an attached character image:

```text
Use $pose-costume-character with my attached character photo,
pose P047 and costume SPR-0050. Preserve the character's face and hair.
```

Or describe the inputs in words:

```text
Use $pose-costume-character to illustrate an adult woman with short black hair,
sitting sideways with one arm raised, wearing a beige cardigan and white trousers.
```

The default is one output image. A text-only character input creates a character from the description; a character image guides an existing identity. Results depend on the model and reference quality.

## Image generation and configuration

The host environment must provide image generation with multiple references. The skill defaults to Codex's available built-in image tool and follows the environment's `imagegen` instructions. This repository supplies the workflow and prompt templates.

When a compatible API is explicitly selected, the default model is `gpt-image-2`. For Atomflow, the service preset is `https://atomflow.vip/v1`. The active task and local configuration determine the service, model and credentials. Keep API keys in local environment variables or trusted configuration. Provider usage fees may apply.

When the character is described in text, two images are submitted for pose and costume. When all three inputs are images, all three references are submitted. The prompt identifies the actual image order and each reference's role.

## Structure

```text
skills/pose-costume-character/
├── SKILL.md                         # Workflow and reference roles
├── agents/openai.yaml               # Codex interface metadata
└── references/
    ├── gallery.md                   # Gallery selection by ID or keyword
    └── prompt-template.md           # Multi-reference prompt template
```

The skill resolves selected references through the public catalog and retrieves only the needed assets. It reports unavailable image services or missing generation capabilities rather than presenting a prompt as a completed image.

## License and sources

Original skill documentation and templates use the [MIT license](LICENSE). Character images, gallery references and external services retain their respective rights. Gallery images and the complete dataset are excluded from this package. See [SOURCES.md](SOURCES.md) for links and usage restrictions.

Related project: [Open Pose & Costume](https://github.com/hongye007/open-pose-costume) · Author on X: [HongyeMain](https://x.com/HongyeMain)
