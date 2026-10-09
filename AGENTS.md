# AIGC project guidance

This folder contains four project-local prompt-writing skills in `.agents/skills/`.
Read `introduction.md` for the user-facing workflow. Keep installation and updates
inside this project; do not install these skills globally.

## Choose the skill by task

- Script or scene description → storyboard: `director-advisor`.
- Character sheets or scene reference-image prompts: `ai-drama-reference-art`.
- MJ scene plates, posters, or VFX image prompts: `ksrmj`.
- Storyboard or shot description → Seedance video prompts: `seedance-clip-writer`.

Read the selected skill's `SKILL.md` and the references its workflow requires.
Resolve reference paths relative to the containing skill or reference file.
If a skill is absent from the current selector, read its project-local file directly.
Do not apply all four skills to every request. For a combined workflow, pass the
storyboard, character descriptions, palette, and actual reference assets between stages.

## Local compatibility

The reference-art skill includes a project-local indoor-scene section for layout,
actor access, derived views, and interaction checks. Follow that section for indoor
references; the original character-sheet and outdoor workflows remain in place.
Other downloaded skill documents are preserved unchanged. Apply these project
adaptations when their original environment assumptions do not fit:

- Save requested deliverables under `outputs/<scene>/` unless the user specifies
  another location. Return clickable local file links; the source instruction
  to “upload files” means file delivery here and does not require an external upload.
  Use available file-editing tools rather than expecting `write_file` or `edit_file`.
- `KSRIM-人设` and `KSRIM-生图` are not installed. Use `ai-drama-reference-art`
  for character-reference prompts. It does not replace the missing image-editing
  workflow; use available image-editing capabilities only when requested.
- For Seedance, declare `@Image` mappings once in the global anchor section;
  identify visible subjects in shots without repeating `@Image` tags. This resolves
  the conflicting per-shot and global-only instructions in the source.
- Keep BGM, voice characteristics, and sound effects in the sound-design section;
  place spoken lines and their timing in the shot timeline without duplicating them.
- Describe physical details that the camera can see. Close-ups do not require
  descriptions of off-screen feet or hidden body parts.
- If no existing CLIP is available, use the bundled V8 template. If inputs are
  incomplete, state reasonable assumptions; do not invent existing character files,
  uploaded reference images, audio assets, or completed clips.
- Platform versions, parameters, durations, asset limits, and model-behavior claims
  in the source are author assumptions. Check the user's target platform when those
  facts affect execution; do not present them as verified platform documentation.
- The user's requested language, style, and shot design take precedence over source
  defaults, including English-only dialogue and project-specific worldbuilding.
