# AIGC skills — project introduction

This project has four local skills for turning a story idea into storyboards, image prompts, and video prompts. They are installed in `.agents/skills/` inside this project. No global installation is required.

The skills contain instructions and reference documents, not generation engines. You can use them to prepare prompts here, then run those prompts with your chosen image or video platform. Installing them does not connect an MJ or Seedance account.

## 1. What was organized

The directory names now match the skills' declared names. At initial installation, all four `SKILL.md` files and all ten reference documents were preserved byte-for-byte. The reference-art skill now includes a project-local indoor-scene workflow. Finder `.DS_Store` files were removed.

| Downloaded location | Installed location | Purpose |
| --- | --- | --- |
| Root `SKILL.md` | `.agents/skills/ai-drama-reference-art/` | Character and scene reference-image prompts |
| `KSR导演顾问/` | `.agents/skills/director-advisor/` | Storyboard design with explanations |
| `KSR电影机分镜提示词书写/` | `.agents/skills/seedance-clip-writer/` | Seedance video prompts and revisions |
| `ksrmj/` | `.agents/skills/ksrmj/` | Cinematic MJ image prompts |

```text
s-video/
├── introduction.md                 ← this guide
├── AGENTS.md                       ← task routing and local compatibility rules
└── .agents/
    └── skills/
        ├── ai-drama-reference-art/
        │   └── SKILL.md
        ├── director-advisor/
        │   ├── SKILL.md
        │   └── references/         ← rhythm, shot grammar, film examples
        ├── ksrmj/
        │   ├── SKILL.md
        │   └── references/         ← templates, mood recipes, cinematic thinking
        └── seedance-clip-writer/
            ├── SKILL.md
            └── references/         ← V8 template, execution model, fixes, fights
```

`.agents` is a hidden folder; on macOS, press **Command + Shift + .** in Finder to show it.

## 2. How to invoke a skill

Keep this folder open as your Codex project. In your next message, name the skill with `$` and describe the task:

```text
$director-advisor Turn this scene into a storyboard: two sisters argue in a
small kitchen at night; one leaves, and the other notices a letter on the table.
Target length: 15 seconds. Explain why each shot works.
```

You can also write naturally, such as “帮我把这场戏排成分镜” or “write an MJ prompt for this scene.” Codex can select a relevant skill from its description; naming it explicitly makes your choice clear.

The local installation path and explicit invocation follow the [official OpenAI skill documentation](https://learn.chatgpt.com/docs/build-skills). Codex detects newly installed skills automatically. If one is missing from the selector, restart Codex and reopen this project. You can also ask it to read the local `SKILL.md` directly:

```text
Read .agents/skills/director-advisor/SKILL.md and use it to storyboard my scene.
```

You do not need to paste the entire skill into chat or run an installation command again. These downloaded skills are scoped to this project; your existing global skills remain separate.

## 3. Choose the right skill

### `director-advisor` — 导演顾问

Use this when you have a script, a scene description, or even a single sentence, and need to decide **how to shoot it**.

**Provide:** what happens, the characters and their relationship, the location, the emotional turning point, and your target duration. A rough description is enough to start.

**Expect:** scene analysis and a storyboard table containing shot number, framing, camera movement, visible action, duration, transition, and a reason for each choice. It also explains the rhythm and offers film examples from its reference library. The source generally favors short shots and a maximum of 14 shots per scene.

```text
$director-advisor
两姐妹在夜晚的小厨房争吵，姐姐摔门离开，妹妹发现桌上的信。
做成15秒、6镜以内的分镜。每镜解释设计理由，标出需要的人物图和场景图。
保存到 outputs/kitchen/storyboard.md。
```

Start here if you are unsure which shots your video needs. This produces the shot plan; the Seedance skill turns that plan into generation instructions.

[Read the skill](.agents/skills/director-advisor/SKILL.md).

### `ai-drama-reference-art` — AI短剧参考图

Use this to write prompts for **consistent character and scene reference images**.

**Provide:** age, face and body features, costume, identifying props, palette, visual style, and which characters must look different. For a scene, describe its layout, materials, light sources, and time of day.

**Expect:** a character prompt using a 2×2 sheet—front face, side face, front body with the face deliberately omitted, and back body—or scene-reference prompts. Indoor scenes start with a usable master view, then add the views required by the storyboard. Actor access and furniture use are checked; a staged interaction frame is added when needed. A nine-panel sheet is optional for indoor scenes. Other scene work retains the existing 3×3 approach. The downloaded character template uses a cool gray studio background and a single side/back light.

```text
$ai-drama-reference-art
为姐姐和妹妹分别写GPT Image角色参考图提示词。
姐姐32岁、短黑发、较高、灰色工作外套；妹妹24岁、长黑发、较瘦、蓝色针织衫。
两人的脸型、体态和姿势要明确区分。每人一张2×2角色设定图。
再写同一个夜晚厨房的3×3场景参考图提示词，统一冷灰蓝色调。
保存到 outputs/kitchen/reference-prompts.md。
```

This writes the reference-image prompts. To create the images too, explicitly ask to generate them with the available image-generation tool, or paste the prompts into your image platform. Keep the actual resulting images for the video stage.

[Read the skill](.agents/skills/ai-drama-reference-art/SKILL.md).

### `ksrmj` — KSR MJ提示词系统

Use this for the **first visual pass** of a cinematic scene, establishing shot, poster, or VFX image. It emphasizes composition, camera position, light, materials, and controlled negative prompts.

**Provide:** the image type, subject, story moment, environment, framing, aspect ratio, lighting, and what you want to exclude.

**Expect:** Chinese and English prompts, each written as one continuous paragraph with five parts: image type → composition → subject/environment → light/materials → negatives/parameters. It can offer several small variations for comparison.

```text
$ksrmj
为夜晚小厨房写一张电影场景空镜提示词：门刚关上，桌上有一封信，
冷色窗光照到磨损的木桌，人物不入镜。21:9，平视广角，克制、真实材质。
输出中文直输版和英文版，再给3个只改变构图的变体。
保存到 outputs/kitchen/mj-prompts.md。
```

Choose this for exploring a compelling scene image; choose `ai-drama-reference-art` for standardized character sheets or a multi-view scene reference. The MJ source includes Neo-specific version and parameter assumptions, so tell Codex which platform you actually use before asking for runnable parameters.

[Read the skill](.agents/skills/ksrmj/SKILL.md).

### `seedance-clip-writer` — Seedance视频提示词

Use this when you already know the shot sequence and need **a video-generation prompt** with timing and continuity.

**Provide:** the storyboard, character descriptions, total duration, aspect ratio, dialogue language, palette, and the actual reference images and their intended upload order. If voice references exist, provide their mapping too.

**Expect:** a CLIP document with usage instructions, a separate director rationale, STYLE LOCK, global image mappings, timed shots, sound design, and targeted negative instructions. It describes emotions through visible actions and checks continuity, light, motion, and unwanted duplicate characters.

```text
$seedance-clip-writer
读取 outputs/kitchen/storyboard.md 和 outputs/kitchen/reference-prompts.md。
基于已确认的6镜方案写15秒CLIP，16:9，冷灰蓝色调，无BGM，中文对白。
我会按姐姐、妹妹、厨房的顺序上传3张参考图；先列出对应@Image映射。
尚未提供实际图片的地方明确标为待补充，不要假装已上传。
把导演说明和可复制的生成提示词分开，保存到 outputs/kitchen/clip-v1.md。
```

Before running it, replace any pending mappings with the actual uploaded assets. Copy the generation sections specified in “使用方式,” including relevant sound and negative instructions; leave out the director rationale and editing notes.

For a revision, report the visible failure and name the existing file:

```text
$seedance-clip-writer
修改 outputs/kitchen/clip-v1.md：生成结果中姐姐被复制，厨房颜色偏暖。
只改角色数量锁定和光源/色调两项，保留成功的镜头与节奏。
保存为 outputs/kitchen/clip-v2.md，并列出改动。
```

[Read the skill](.agents/skills/seedance-clip-writer/SKILL.md).

## 4. A practical workflow

1. **Write the scene.** State what the characters want, what changes, and the target length.
2. **Plan shots with `director-advisor`.** Review the sequence and decide which version to use.
3. **Create consistent references with `ai-drama-reference-art`.** Generate the actual character and scene images from those prompts. Optionally use `ksrmj` first to explore the scene's composition and lighting.
4. **Write the CLIP with `seedance-clip-writer`.** Supply the approved storyboard, character information, and real asset mappings.
5. **Run it on your generation platform.** Upload assets in the documented order and paste the generation prompt.
6. **Revise one or two variables per attempt.** Describe what failed, keep what worked, and save a new version.

You can request the writing stages together:

```text
Use this project's AIGC skills for the kitchen scene. First design a 15-second
storyboard, then write character and scene reference prompts, then draft a
Seedance CLIP. Keep identities and palette consistent. Save the files under
outputs/kitchen/. Mark image mappings as pending until I provide the actual images.
```

Suggested output filenames are `storyboard.md`, `reference-prompts.md`, optional `mj-prompts.md`, and `clip-v1.md`. These are future deliverables, not files generated by the installation.

## 5. Source quirks and project adaptations

The reference-art skill has been customized locally with an indoor-scene section. The other downloaded skill documents retain their original content. [AGENTS.md](AGENTS.md) records this and supplies the following local adaptations:

- **Missing companion skills:** the MJ skill mentions `KSRIM-人设` and `KSRIM-生图`, which were not included in your downloads. The installed reference-art skill covers character-reference prompts. A separate GPT image-stabilization/editing skill has not been installed.
- **Conflicting image rules:** the Seedance document says both “reference images only once globally” and “reference the focal image in each shot.” This project uses one global mapping and avoids repeated `@Image` tags in shots.
- **Sound placement:** dialogue belongs in the shot timeline at its speaking time; BGM, voice characteristics, and sound effects are managed in the sound section.
- **File delivery:** requests to “upload a file” are handled by saving a local file and linking it here. References to `write_file`/`edit_file` are adapted to the file tools available in Codex.
- **Framing:** physical detail must fit what the camera sees; a close-up does not need off-screen foot placement. With no previous CLIP available, the bundled V8 template is the starting point.
- **Your preferences:** specify dialogue language and visual style. The original Seedance default is English dialogue; your explicit request can override that. MJ worldbuilding rules such as “永恒黄昏” apply only when you ask for that setting.

The downloads also contain claims about MJ/Neo versions and flags, Seedance durations and reference limits, and how models interpret prompts. Those claims are the author's workflow assumptions; they were not verified as current platform specifications during this installation. Match them to your chosen platform before execution.

## 6. Maintaining these skills

To update one, replace its files inside `.agents/skills/<skill-name>/`, keeping `SKILL.md` and its relative `references/` paths together. To add another downloaded skill, give it its own folder under `.agents/skills/` and use its declared `name` as the folder name. Avoid keeping a second active copy with the same name.

Keep reusable skill instructions in `.agents/skills/`, project adaptations in `AGENTS.md`, and generated scene work in `outputs/`. You can remove a local skill's directory to uninstall that copy from this project.
