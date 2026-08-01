# Generated Image Style References Design

## Goal

Make AI-generated supplementary stills in `chatcut-topic-video-editor` consistently follow the six reference images currently stored in the repository-level `references/` directory, while keeping screenshots and text graphics independent from that style.

## Scope boundary

Apply the reference-image style only when ChatCut creates a new still with an image-generation model.

Do not apply it to:

- Authentic software screenshots or screen-recording frames
- User-provided images, videos, logos, documents, or other source media
- Captions, subtitles, titles, labels, callouts, or Motion Graphics
- Text overlays added after image generation

Reference images control visual treatment only. Generated output must use the current video's topic and must not copy reference-image wording, logos, named subjects, or exact compositions.

## Portable resource layout

Copy the six source images into:

```text
chatcut-topic-video-editor/assets/generated-image-style/
```

Keep the repository-level originals unchanged. Bundling copies inside the Skill ensures the style references remain available when users install only `chatcut-topic-video-editor/`.

## Style contract

Generated stills should inherit these shared qualities when compatible with the subject:

- Warm off-white paper background
- Bold black hand-drawn outlines
- Simple doodle or explanatory-infographic forms
- Cyan and yellow as the main accents
- Optional pale-green shadow or secondary accent
- Generous whitespace and an uncluttered hierarchy
- Friendly, editorial, idea-sketch character rather than photorealism

The subject matter, objects, layout, and aspect ratio must still serve the current speech moment.

## Generation flow

1. Confirm that a real coverage gap remains after user-supplied media and authentic screenshots are mapped.
2. Determine whether the missing visual should be a generated still. If it is a screenshot or a text-only explanation, do not use these style references.
3. Select one to three bundled reference images that best match the target aspect ratio or diagram complexity.
4. Import those selected files into the active ChatCut project as internal `style-only` assets. They are not must-use timeline media.
5. Generate the still through `chatcut:image-gen`, passing the imported asset IDs in `referenceAssetIds`. Prefer the image model with stronger reference fidelity when style consistency is the main requirement.
6. In the prompt, explicitly request style transfer only and prohibit copying reference text, logos, specific subject matter, and exact composition.
7. Keep important wording out of the generated pixels. Add required Chinese wording later as editable ChatCut Motion Graphics.
8. Place and visually verify only the generated result on the timeline. Do not place internal style references unless the user separately requests them as visible media.

## File changes

- Add the six images under `chatcut-topic-video-editor/assets/generated-image-style/`.
- Add a concise generated-image style section to `references/visual-assets.md`.
- Add the conditional rule and resource link to `SKILL.md`.
- Update `README.md` to describe the behavior and repository structure.
- Leave `agents/openai.yaml` unchanged unless validation shows its prompt is stale.

## Error handling

- If a bundled reference cannot be imported, continue with the remaining references and report the issue.
- If reference-image input is unavailable, use the written style contract as the fallback prompt and disclose the fallback.
- If the user specifies another generated-image style for a particular task, the explicit task-level instruction overrides this default reference set.
- If a real screenshot is needed, never generate a fake product interface merely to match the style.

## Verification

- Validate the Skill structure and YAML frontmatter.
- Confirm all six bundled images exist and are readable.
- Confirm the rule distinguishes generated stills from screenshots and Motion Graphics.
- Confirm internal style references are classified `style-only` and excluded from the must-use timeline inventory.
- Confirm generated-image instructions use `referenceAssetIds` and preserve editable Chinese text.
- Check that README examples and directory structure match the actual files.

## Non-goals

- Restyling authentic screenshots
- Applying the reference look to all timeline graphics
- Replacing the active ChatCut Design Style for titles or Motion Graphics
- Recreating the topics or wording shown in the six reference images
