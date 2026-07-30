# Quality checklist

Apply this checklist before reporting the edit as complete.

## Content

- Source files appear in the intended order.
- The opening communicates a clear reason to keep watching.
- Obvious fillers, retakes, repetition, and abandoned starts are gone.
- The speaker's meaning and natural voice remain intact.
- The cut has no broken sentence, missing subject, or misleading join.
- The demonstration and result retain enough context.

## Audio

- Long pauses are compressed without making speech rushed.
- Hard speech cuts have been processed with `smooth_audio`.
- No audible pop, click, duplicated syllable, or missing word is obvious from the edit structure.
- No accidental music, captions, or effects were added.

## Visual materials

- Every user-supplied screenshot/reference asset has been classified.
- Every `must-use` supplied asset is imported and placed on a visible timeline track.
- A media-pool entry is not being mistaken for timeline integration.
- Every `style-only`, `alternate`, or `blocked` supplied asset has an explicit reason.
- Every named software/product that needs identification has suitable coverage.
- Authentic screenshots are distinguishable from conceptual visuals.
- Generated images do not contain unreliable critical text.
- Added explanations are Chinese-first when the user speaks Chinese.
- Official product names remain correct.

## Motion Graphics

- One confirmed Design Style governs the batch.
- Chinese fonts are cloud-safe and returned by `search_fonts`.
- Text is readable at video scale.
- No clipping, overflow, collision, or accidental line break harms meaning.
- Accent colors emphasize only important values or phrases.
- Transparent overlays do not cover important UI.
- Full-screen graphics are intentional.

## Timeline

- V1 contains the speech cut.
- User-supplied visual items are placed on higher video tracks at relevant speech moments.
- Same-track items do not overlap.
- No black gap appears on the only visible video layer.
- Added visuals end at or before the real content end.
- The final duration is confirmed from current project state.

## Pixel proof

Inspect at least:

- A settled opening-hook frame
- One frame for every must-use supplied screenshot, image, logo, or reference clip
- One frame for every additional software screenshot
- One settled frame for every Motion Graphic form
- Every frame using a crop-sensitive generated image
- The final result emphasis frame

Compare screenshots at full enough resolution to judge Chinese text and protected UI.

## Handoff

- The current editor points to the correct project.
- The user receives a localized editor link.
- The summary describes changes without internal ids.
- The summary names the supplied visuals integrated into the timeline.
- Any supplied visual not used is disclosed with the reason.
- The response distinguishes editable project completion from MP4 export.
- Export is not started unless requested.
