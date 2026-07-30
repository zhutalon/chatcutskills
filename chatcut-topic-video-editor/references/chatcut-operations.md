# ChatCut operations

Use this reference for state refresh, tool boundaries, timeline layering, and verification order.

## Contents

- Project and import
- Tool boundary
- Refresh state before mutation
- Suggested track organization
- Motion Graphic authoring
- Visual placement
- Verification
- Export boundary

## Project and import

1. Create or target the exact project.
2. Keep the live editor on the same project.
3. Inventory primary videos and every supplied screenshot/reference asset.
4. Import all local files through the ChatCut asset-import workflow, using additional import sessions when the helper's per-session file limit is reached.
5. Record each returned asset id against the supplied-asset inventory.
6. Wait for transcript readiness before Script work.
7. Wait for upload readiness before cloud frame rendering or export.

Use local `ffmpeg` only for read-only source inspection. Do not pre-edit or flatten the deliverable outside ChatCut.

## Tool boundary

| Goal | Surface |
| --- | --- |
| Read current speech cut | `read_script` |
| Remove/reorder spoken content | `apply_script` |
| Fixed fillers and batch pauses | `clean_script` |
| Locate speech for visual timing | `find_transcript` |
| Add screenshots, B-roll, or Motion Graphics | `edit_item` |
| Create authored Motion Graphics | `create_motion_graphic_from_code` |
| Smooth hard speech cuts | `smooth_audio` |
| Inspect project topology | `read_project` |
| Inspect a source asset | `inspect_asset` |
| Inspect composed timeline pixels | `view_timeline_frames` |

Never use timeline trimming as a shortcut for meaning-based speech editing.

## Refresh state before mutation

Project state may change while the editor is open.

- Read project summary first.
- Read `view:"timeline"` to discover tracks.
- Read only the target track before item edits.
- Re-read Script after `clean_script`.
- Re-read track state after visual placement.
- Use exact item or asset ids returned by current tools.

Do not rely on ids from a previous project or a previous edit session.

## Suggested track organization

- V1: primary speech footage
- V2: user-supplied screenshots, reference clips, and other must-use visuals
- V3: Motion Graphics that must sit above V2
- Higher tracks: additional supplied visuals, searched/generated coverage, or another intentional layer

Sequential items can share a track. Overlapping items need separate tracks.

## Motion Graphic authoring

Before authoring:

1. Apply or inspect the project Design Style.
2. Search cloud-safe fonts.
3. Inspect the target frame.
4. Decide content, timing, form, placement, and background.
5. Match the asset duration to the intended timeline span.

Use a natural-box asset for transparent overlays and project dimensions only for intentional full-screen graphics.

Create inline JSX through `create_motion_graphic_from_code`. Do not stage JSX in repository files or temporary servers.

## Visual placement

For screenshots and generated stills:

- Use `fit:"contain"` for protected UI.
- Use `fit:"cover"` for close-aspect conceptual imagery only after source inspection.
- Pass an explicit rectangle for large overlays.
- Use native `borderRadius` only when it suits the selected visual system.

For Motion Graphics:

- Place with explicit frame start and duration.
- Use explicit geometry for natural-box overlays.
- Keep full-screen opaque graphics responsible for their own background.

For every must-use supplied asset:

1. Locate its relevant final speech phrase with `find_transcript` when speech provides the anchor.
2. Inspect the target timeline frame and source asset.
3. Add the original supplied asset with `edit_item`.
4. Record the committed timeline item id.
5. Read the affected track back.
6. Render and inspect a frame where the asset is fully visible.

An imported media-pool asset without a timeline item does not satisfy the integration requirement.

## Verification

Verification needs both structure and pixels.

1. Read V1 and every added visual track.
2. Reconcile every must-use supplied asset id with a committed timeline item.
3. Confirm exact frame ranges.
4. Inspect source assets for crop-sensitive visuals.
5. Render settled frames after each entrance animation and every supplied visual placement.
6. Download temporary frame links when necessary.
7. Inspect the actual images.
8. Compare source and composed frames for crop safety.

A successful tool response is not visual proof.

## Export boundary

Return an editable timeline by default.

Run the ChatCut export workflow only when the user explicitly requests a rendered file, download, final delivery, or an already-approved final export.
