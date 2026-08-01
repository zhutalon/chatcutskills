# Visual assets

Use this reference to plan and acquire software screenshots, supplementary images, and Chinese-first Motion Graphics.

## Contents

- Source priority
- Supplied-asset inventory
- Integrating reference media
- Software screenshots
- Supplementary images
- Generated-image style references
- Text inside generated images
- Chinese-first Motion Graphics
- Style alignment
- Placement

## Source priority

For named software, products, or services, search in this order:

1. User-provided screenshots, images, clips, logos, and other supporting files
2. Matching assets already imported into the project media pool
3. Official product website, documentation, press kit, or support page
4. Reputable review or tutorial showing the required interface
5. Generated explanatory visual when an authentic screenshot is unavailable or insufficient

Do not import duplicate assets. Do not include credentials, personal notifications, private documents, or user-identifying data.

## Supplied-asset inventory

Inspect every supplied supporting file before formal visual editing.

Classify each file as:

- `must-use`: visible in the final timeline
- `style-only`: influences design but does not appear in the final video
- `alternate`: redundant option; use the best candidate and report the unused alternative
- `blocked`: unsafe, unreadable, unsupported, corrupt, or unrelated

Default screenshots, images, reference clips, logos, and supporting visuals to `must-use`. Use `style-only` only when the user says so or the file is unmistakably a moodboard/style reference.

For each `must-use` file, record:

- Source path or attachment name
- Imported ChatCut asset id
- Intended speech phrase or topic
- Planned start and duration
- Full-screen, large overlay, PiP, background, or Motion Graphic property use
- Fit/crop strategy
- Final timeline item id
- Verified composed frame

Do not mark the asset complete after import. Completion requires a placed timeline item and pixel proof.

## Integrating reference media

Use the supplied media itself whenever practical:

- Screenshot/image: place as an `image` item.
- Reference video: select the relevant visual range and place it as B-roll; preserve the main speech audio unless the user requests the reference audio.
- GIF or SVG: import and place in its supported native type.
- Logo: place directly or bind it through an editable Motion Graphic property.
- PDF, slide, or document: render the relevant page to an image before importing when ChatCut cannot place the original format.

Do not substitute a searched or generated asset for a supplied asset unless the provided file is unusable or the user asks for a replacement.

## Software screenshots

Choose screenshots that prove the exact point being spoken:

- Product overview for identification
- Maintenance or cleanup page for capability
- Permissions page for access requirements
- Result page for outcome

Preserve complete UI and readable controls. For a dense interface:

- Prefer a large centered overlay or full-screen contain treatment.
- Avoid aggressive cover crops.
- Keep the native language of the real software interface.
- Add a separate Chinese explanation instead of altering authentic UI text.

## Supplementary images

Use a new supplementary still only after the supplied-asset inventory shows a real coverage gap. Use it when the speech describes an abstract relationship, unseen action, or missing process.

Good uses:

- AI sending a task into a professional tool
- A controlled permission gate
- A process changing disorganized files into organized output
- A before/after storage or workflow concept

Avoid generating a screenshot that could be mistaken for the real product interface.

## Generated-image style references

- **Scope:** newly generated supplementary stills only; never authentic screenshots, source media, captions, titles, callouts, or Motion Graphics.
- **Style:** warm off-white paper, bold black hand-drawn outlines, simple doodle/infographic forms, cyan and yellow accents, optional pale-green shadow, and generous whitespace.
- **Selection:** choose 1–3 images by target aspect ratio and diagram complexity:
  - `16:9` → `assets/generated-image-style/16_9.png` plus one relevant diagram example
  - `3:4` → `assets/generated-image-style/3_4.png`
  - `4:3` → `assets/generated-image-style/4_3.png`
  - Diagram-heavy → `assets/generated-image-style/vibewriting.png`, `assets/generated-image-style/交互.png`, or `assets/generated-image-style/手速跟不上脑速.png`
- **ChatCut flow:** import selected files as internal `style-only` assets, then pass their returned project asset IDs in `referenceAssetIds`. Never place these internal references on the timeline unless separately requested as visible media.
- **Prompt:** transfer style only; do not copy wording, logos, subject matter, or exact composition.
- **Text:** keep important Chinese wording out of generated pixels and add it later as editable Motion Graphics.
- **Override:** obey an explicit task-level generated-image style instead.
- **Fallback:** if references cannot be passed, use this written style contract and disclose the fallback.

## Text inside generated images

Do not rely on image-generation models for important Chinese wording. Generate the visual without text, then add exact Chinese text as a ChatCut Motion Graphic.

This keeps the wording:

- Correct
- Editable
- Searchable
- Consistent with the project Design Style
- Reliable in export

## Chinese-first Motion Graphics

Use Chinese as the dominant hierarchy when the user communicates in Chinese.

Useful roles:

- Opening thesis
- Chapter marker
- Three-step workflow
- Permission path
- Risk or boundary note
- Key quote
- Quantified result
- Before/after comparison

Keep English product names such as ChatGPT, OnyX, Claude, or macOS where they are the official names.

Expose visible text, colors, and fonts as editable Motion Graphic properties.

## Style alignment

Use one visual system for the whole video:

- One background/material language
- One heading/body font logic
- One accent/highlight policy
- One motion rhythm

Let each Motion Graphic use a form suited to its job. Do not turn every explanation into the same rounded card.

For a warm editorial notebook style, a useful vocabulary is:

- Off-white paper
- Fine grid or ruled lines
- Black and gray typography
- Sparse orange or yellow emphasis
- Serif Chinese title plus sans-serif utility text
- Measured staged reveals

Use this vocabulary only when the user selected or approved that direction.

## Placement

Inspect the composed target frame before placement.

For screen recordings with a centered white workspace:

- Large software screenshots can occupy the central canvas.
- Bottom or side Motion Graphics can cover low-information areas.
- A full-screen hook can intentionally replace the source for its duration.

Do not overlap separate visual treatments unless they form one planned composition. If a concept still and a workflow strip are paired, keep the strip legible and verify the combined frame.

When several supplied visuals match the same section:

- Sequence them on one visual track when each deserves separate screen time.
- Build an intentional comparison layout when they must be seen together.
- Avoid stacking images randomly on several tracks.
- Keep every must-use asset visible long enough to understand.
