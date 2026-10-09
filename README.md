# s-video

Project-local skills for AI-generated short films: turn a scene into a storyboard, create reference-image prompts, and write video-generation prompts.

This repository contains four skills and their supporting reference documents. They prepare prompts and production plans. Image and video generation requires your chosen generation tools and accounts.

## Included skills

| Skill | Use it for | Main output |
| --- | --- | --- |
| [director-advisor](.agents/skills/director-advisor/SKILL.md) | Plan how to shoot a script or scene | Storyboard, shot timing, camera choices, and design reasons |
| [ai-drama-reference-art](.agents/skills/ai-drama-reference-art/SKILL.md) | Define consistent characters and locations | Character sheets and scene reference-image prompts |
| [ksrmj](.agents/skills/ksrmj/SKILL.md) | Explore cinematic composition, light, and atmosphere with MJ | Chinese and English image prompts |
| [seedance-clip-writer](.agents/skills/seedance-clip-writer/SKILL.md) | Convert a storyboard into a Seedance video prompt | Timed shots, asset mappings, sound design, and revision instructions |

The skill instructions are primarily in Chinese. Request the output language you need.

## Get started

```bash
git clone https://github.com/sses79/s-video.git
cd s-video
```

Open this folder as your project in Codex. The skills stay under `.agents/skills/` in this project; there is no global installation step.

Ask for a skill by name, or explicitly ask the assistant to read its local file:

```text
Read .agents/skills/director-advisor/SKILL.md and follow AGENTS.md.
Plan a 20-second scene with two characters in a small study.
An old moneylender thinks his servant stole his money. The servant thinks
he has been caught secretly engaged to the moneylender's daughter.
Use short dialogue and end with the misunderstanding revealed.
Save the storyboard under outputs/confession/.
```

Choose the skill for the current task. Read its required reference documents before writing the deliverable.

## Workflow

1. **Write the scene.** State each character's goal, what changes, the dialogue, and the target length.
2. **Plan the shots.** Use `director-advisor` to define framing, timing, actor positions, and camera placement.
3. **Create the references.** Use `ai-drama-reference-art` for characters and locations. Optionally use `ksrmj` to explore composition and lighting first. Generate the actual images with your image tool.
4. **Write the video prompt.** Use `seedance-clip-writer` with the storyboard, character descriptions, palette, and actual reference assets. Declare the upload order and image mappings.
5. **Generate the video.** Select the platform settings, upload the assets, and paste the generation prompt. Confirm the settings and limits supported by your platform.
6. **Revise a small number of variables.** Describe the visible failure, keep successful choices, and save a new version.

Pass the same story, character identities, layout, and palette between stages. Mark missing assets as pending. Separate production notes from the prompt you paste into the generation platform.

## Indoor scenes

The reference-art skill includes a local indoor-scene workflow:

- Define the actions before adding decoration. Establish which side of a desk or other object the actor uses.
- Check actor access, movement paths, furniture clearance, and how doors or drawers open.
- Create one main room image, then derive only the views needed by the storyboard.
- Add a staged interaction reference when the action depends on physical contact with furniture or props.
- Check geometry, eyelines, character scale, light direction, and continuity across views.

Before regenerating an indoor reference, review the scene and storyboard. Changes to furniture, access, camera placement, or movement require updated staging. A decoration change usually needs a lighter review. Keep the written ending of one clip consistent with the opening of the next clip.

## Project layout

```text
s-video/
├── README.md
├── AGENTS.md
├── introduction.md
└── .agents/skills/
    ├── ai-drama-reference-art/
    │   └── SKILL.md
    ├── director-advisor/
    │   ├── SKILL.md
    │   └── references/
    ├── ksrmj/
    │   ├── SKILL.md
    │   └── references/
    └── seedance-clip-writer/
        ├── SKILL.md
        └── references/
```

Generated work belongs in `outputs/<scene>/`. The `outputs/` directory is ignored by Git and is not included in this repository.

## Guides and maintenance

- [Introduction](introduction.md): detailed skill explanations and example requests.
- [Project guidance](AGENTS.md): task routing and compatibility rules.

Keep updates inside `.agents/skills/<skill-name>/`. Preserve each skill's relative reference paths. The indoor-scene section is a project customization; the other downloaded skill documents retain their original content.

Some source instructions refer to companion skills or tools that are not included here. `AGENTS.md` records the local adaptations. Platform versions, parameters, and model-behavior claims in the downloaded documents must be checked against your target platform when they affect execution.
