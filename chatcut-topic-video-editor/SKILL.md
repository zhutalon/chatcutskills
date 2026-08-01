---
name: chatcut-topic-video-editor
description: "Use ChatCut to turn one or more speech-led videos, screen recordings, tutorials, interviews, or video-podcast clips into a concise, editable finished cut. Use when the user supplies video files, optional screenshots/reference media, and an optional topic and wants the complete workflow: order and transcribe the sources, remove fillers/retakes/repetition, build a source-derived opening hook, import every must-use supplied visual into the ChatCut project, place those visuals on the timeline at relevant speech moments, collect or create missing coverage, author Chinese-first Motion Graphics, smooth audio cuts, and verify the composed timeline before review or export."
---

# ChatCut Topic Video Editor

Turn raw speech-led footage into a structured, visually supported ChatCut timeline. Keep every editorial change editable in ChatCut.

## Load the ChatCut workflows

Before acting, read the available ChatCut skills that cover the requested stages:

- Always: `chatcut:chatcut-plugin-basics`
- Local or attached media: `chatcut:asset-import`
- Transcript work: `chatcut:transcription` and `chatcut:talking-head-guide`
- Motion Graphics: `chatcut:create-motion-graphics`
- Image generation, only when needed: `chatcut:image-gen`
- Final proof: `chatcut:verification`
- Export, only when requested: `chatcut:export`

If the ChatCut plugin or required direct-authoring tools are unavailable, report the missing dependency. Do not replace the editable workflow with a locally flattened video.

## Establish the brief

Extract these facts from the request and source files:

- Video paths or attachments
- Screenshot, image, reference-video, logo, document, or other supporting-media paths
- Intended source order
- Topic, thesis, or teaching goal
- Target platform, ratio, length, and pacing when provided
- Visual direction and language
- Whether the user requested an editable timeline, an export, or both

Infer numeric filename order such as `1.mp4`, `2.mp4`, `3.mp4` unless the user specifies another order. Inspect project state and media before asking questions. Ask only for a preference that would materially change the cut.

When the user writes in Chinese, make all newly authored titles, labels, explanations, and data callouts Chinese-first. Preserve unavoidable native text inside real software screenshots.

## Treat supplied visuals as required inputs

Unless the user explicitly labels a file as `style-only`, treat every supplied screenshot, image, reference clip, logo, or supporting visual as a must-use timeline asset.

Before editing, build an inventory with:

| Supplied file | Type | Intended role | Speech/topic match | Import status | Timeline status |
| --- | --- | --- | --- | --- | --- |

Import must-use visuals into the ChatCut project early, but place them only after A-roll timing is final. Importing a file into the media pool is not completion; the asset must appear on a video track for a deliberate duration and be visible in the composed frame.

Do not silently omit a supplied asset. If a file is unusable, unsafe, duplicative, clearly unrelated, or genuinely style-only, state that explicitly and give the reason. Ask for direction only when the choice would materially change the story.

## Run the workflow in dependency order

1. Create or target the ChatCut project and surface the live editor.
2. Import the original videos and all supplied supporting media. Wait for transcript readiness on spoken sources.
3. Read the transcript and representative source frames.
4. Build a content outline and a visual-material plan that assigns every must-use supplied asset.
5. Finalize the A-roll with Script.
6. Run `smooth_audio`.
7. Collect or create only the visual materials still missing after the supplied assets are mapped.
8. Resolve one project Design Style.
9. Place all must-use supplied visuals, then additional screenshots, B-roll, generated stills, and Motion Graphics against the final speech timing.
10. Re-read project structure and inspect composed frames.
11. Return the editable project for review. Export only when requested.

Do not place captions, B-roll, Motion Graphics, or music before the A-roll timing is final.

## Edit the A-roll

Read [references/editorial-workflow.md](references/editorial-workflow.md) before making transcript-based cuts.

Use this tool boundary:

- Fixed hesitation sounds and batch pauses: `clean_script`
- Meaning-based cuts, retakes, reordering, and source-derived hooks: `read_script` → edit full `timelineMd` → `apply_script`
- Phrase timing for later visual placement: `find_transcript`
- Never use `find_transcript` plus timeline trimming to decide what speech plays

Prefer a hook pulled from the original speech. Move a complete, strong claim, result, conflict, or counterintuitive idea to the opening; do not duplicate it later unless repetition is editorially intentional.

Preserve the speaker's meaning and natural rhythm. Remove defects, not personality.

## Prepare visual materials

Read [references/visual-assets.md](references/visual-assets.md) when the source lacks useful illustrations, product UI, screenshots, or explanatory graphics.

Create a compact material map before placement:

| Speech moment | Viewer need | Visual source | Required asset | Treatment |
| --- | --- | --- | --- | --- |
| Opening claim | Understand the thesis immediately | Supplied visual, Motion Graphic, or concept image | File/id | Full-screen hook |
| Named product/software | Recognize the real interface | Supplied or authentic screenshot | File/id | Large overlay or cutaway |
| Abstract method | Understand roles or sequence | Supplied reference or Motion Graphic | File/id | Diagram or step strip |
| Permission/risk | Understand the boundary | Supplied screenshot or Motion Graphic | File/id | Chinese path/callout |
| Quantified result | Remember the proof | Supplied result image or Motion Graphic | File/id | Stat and before/after |

Prefer authentic software screenshots for software-specific claims. When a generated still is needed, generate the scene without embedded text and add Chinese wording as an editable Motion Graphic.

When a new supplementary still will be model-generated, read the generated-image subsection in [references/visual-assets.md](references/visual-assets.md). Use `assets/generated-image-style` references only for those generated stills; screenshots, source media, captions, titles, callouts, and Motion Graphics do not inherit this style. Import the selected references as internal `style-only` assets, pass their project asset IDs in `referenceAssetIds`, and never place those internal references on the timeline unless separately requested as visible media.

## Apply one visual language

Use the active project Design Style when one exists. Otherwise:

- Apply the user's selected preset.
- If no style is selected and several Motion Graphics are planned, show the ChatCut visual preset picker.
- If the user explicitly says to proceed without asking, choose a coherent temporary direction and state it.

For Chinese graphics, search the renderer font catalog before authoring. Prefer cloud-safe families such as `Noto Sans SC` and `Noto Serif SC` only when `search_fonts` returns those exact names.

Create separate Motion Graphic assets for different viewer jobs. Reuse an asset only when the job, information structure, and form intentionally recur.

## Assemble the visual layers

Use the original speech footage as V1. Put full-screen screenshots, generated stills, or B-roll above it. Put transparent Motion Graphics on the highest relevant video layer.

Give user-supplied visuals placement priority over newly searched or generated substitutes. Use the supplied asset itself in the timeline; do not recreate it unless the user asks for a derivative treatment.

Protect readable interface text, logos, controls, and document edges:

- Use `contain` for dense UI when `cover` would crop important information.
- Use a deliberate background or large overlay box when aspect ratios differ.
- Use `cover` only after checking the source frame and protected regions.
- Inspect the target frame before choosing placement.

Keep ordinary explanatory Motion Graphics transparent. Use an opaque full-screen Motion Graphic only for an intentional title, hook, chapter beat, or information surface.

## Verify before reporting completion

Read [references/chatcut-operations.md](references/chatcut-operations.md) for tool-order and state-refresh rules.

Before the final response, read and apply [references/quality-checklist.md](references/quality-checklist.md).

At minimum:

- Confirm the final duration and track structure with `read_project`.
- Reconcile the supplied-asset inventory against current timeline items.
- Confirm all must-use supplied assets are placed, not merely present in the media pool.
- Render settled frames for the hook, each screenshot, each Motion Graphic, and any crop-sensitive still.
- Actually inspect the pixels.
- Check Chinese text, font loading, clipping, overlaps, safe zones, and protected UI.
- Check for black gaps and visual items extending beyond the real content end.

Keep the live ChatCut project as the review surface. Do not infer export intent from “剪辑”“精剪”“做一个版本” or similar wording.

## Default handoff

Report:

- Final approximate duration
- What was removed or restructured in plain language
- Which user-supplied screenshots and reference assets were integrated, and where
- Which screenshots, supplementary visuals, and Chinese Motion Graphics were added
- Any supplied asset not used, with the explicit reason
- Whether audio cuts were smoothed
- What was visually verified
- The localized ChatCut editor link
- Whether export remains pending

## Example invocation

```text
使用 $chatcut-topic-video-editor

视频：
- /path/to/1.mp4
- /path/to/2.mp4

配图和参考素材：
- /path/to/product-ui.png
- /path/to/result-before-after.jpg
- /path/to/reference-demo.mp4

主题：让 AI 操作专业软件完成任务
顺序：按文件编号
视觉：米白网格手账，新增文字以中文为主
交付：先给我 ChatCut 可编辑版本，暂不导出
```
