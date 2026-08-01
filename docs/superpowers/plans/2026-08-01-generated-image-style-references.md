# Generated Image Style References Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Bundle the six repository reference images with `chatcut-topic-video-editor` and make them the default style anchors only for AI-generated supplementary stills.

**Architecture:** Store portable copies under the Skill's `assets/` directory, describe their visual contract in the visual-assets reference, and add a concise conditional instruction in `SKILL.md`. ChatCut imports selected references as internal `style-only` assets and passes their project asset IDs through `referenceAssetIds`; screenshots and Motion Graphics stay on their existing independent paths.

**Tech Stack:** Markdown Codex Skill instructions, PNG reference assets, ChatCut `asset-import`, ChatCut `image-gen`, Git, Skill Creator `quick_validate.py`

## Global Constraints

- Apply the bundled style only to newly generated still images.
- Do not apply it to authentic screenshots, screen-recording frames, user media, captions, titles, callouts, or Motion Graphics.
- Use reference images for visual treatment only; do not copy their text, logos, named subjects, or exact compositions.
- Preserve important Chinese wording as editable ChatCut Motion Graphics, not generated pixels.
- Keep all six repository-level originals unchanged.
- Treat bundled reference images as internal `style-only` assets, never default `must-use` timeline media.
- Explicit user instructions for another generated-image style override this default set.

---

### Task 1: Characterize the missing behavior

**Files:**
- Read: `chatcut-topic-video-editor/SKILL.md`
- Read: `chatcut-topic-video-editor/references/visual-assets.md`
- Read: `references/*.png`
- Create during execution: `/tmp/chatcut-style-baseline.txt`

**Interfaces:**
- Consumes: The current unmodified Skill and a prompt requiring one generated still, one software screenshot, and one Chinese text card.
- Produces: A baseline report showing whether the current Skill discovers the six images, uses them only for the generated still, and excludes the screenshot/text card.

- [ ] **Step 1: Run the baseline scenario without the new rule**

Ask a fresh-context agent to use the current Skill and respond with an execution plan for:

```text
Use $chatcut-topic-video-editor at /Users/talon/Proj/chatcutskills/chatcut-topic-video-editor.
The repository also contains /Users/talon/Proj/chatcutskills/references.
Plan a Chinese talking-head edit that needs: (1) one AI-generated abstract workflow still, (2) one authentic software screenshot, and (3) one Chinese Motion Graphic text card. State which files influence each visual, whether each file is placed on the timeline, and which ChatCut image-generation parameters are used.
```

- [ ] **Step 2: Record the expected baseline failure**

Save the response to `/tmp/chatcut-style-baseline.txt`. Confirm at least one failure:

```text
- The six repository reference images are not discovered or used.
- No rule limits those references to generated stills.
- References are not identified as style-only and excluded from the timeline.
- Imported reference asset IDs are not passed through referenceAssetIds.
```

Expected: FAIL because the current Skill has no bundled style-reference contract or asset path.

---

### Task 2: Bundle portable style-reference assets

**Files:**
- Create: `chatcut-topic-video-editor/assets/generated-image-style/16_9.png`
- Create: `chatcut-topic-video-editor/assets/generated-image-style/3_4.png`
- Create: `chatcut-topic-video-editor/assets/generated-image-style/4_3.png`
- Create: `chatcut-topic-video-editor/assets/generated-image-style/vibewriting.png`
- Create: `chatcut-topic-video-editor/assets/generated-image-style/交互.png`
- Create: `chatcut-topic-video-editor/assets/generated-image-style/手速跟不上脑速.png`

**Interfaces:**
- Consumes: The six PNG files under repository-level `references/`.
- Produces: Six byte-identical, readable PNG files installed with the Skill.

- [ ] **Step 1: Run the pre-copy existence test**

```bash
test -d chatcut-topic-video-editor/assets/generated-image-style && \
test "$(find chatcut-topic-video-editor/assets/generated-image-style -maxdepth 1 -type f -name '*.png' | wc -l | tr -d ' ')" = 6
```

Expected: FAIL because the destination does not exist.

- [ ] **Step 2: Copy the six assets without changing the originals**

```bash
mkdir -p chatcut-topic-video-editor/assets/generated-image-style
cp references/16_9.png chatcut-topic-video-editor/assets/generated-image-style/16_9.png
cp references/3_4.png chatcut-topic-video-editor/assets/generated-image-style/3_4.png
cp references/4_3.png chatcut-topic-video-editor/assets/generated-image-style/4_3.png
cp references/vibewriting.png chatcut-topic-video-editor/assets/generated-image-style/vibewriting.png
cp references/交互.png chatcut-topic-video-editor/assets/generated-image-style/交互.png
cp references/手速跟不上脑速.png chatcut-topic-video-editor/assets/generated-image-style/手速跟不上脑速.png
```

- [ ] **Step 3: Verify count, format, and byte identity**

```bash
test "$(find chatcut-topic-video-editor/assets/generated-image-style -maxdepth 1 -type f -name '*.png' | wc -l | tr -d ' ')" = 6
for image in 16_9.png 3_4.png 4_3.png vibewriting.png 交互.png 手速跟不上脑速.png; do
  cmp "references/$image" "chatcut-topic-video-editor/assets/generated-image-style/$image"
  sips -g format -g pixelWidth -g pixelHeight "chatcut-topic-video-editor/assets/generated-image-style/$image"
done
```

Expected: six PNG files; every `cmp` exits 0; every image reports positive dimensions.

- [ ] **Step 4: Commit the bundled assets**

```bash
git add chatcut-topic-video-editor/assets/generated-image-style
git commit -m "assets: bundle generated image style references"
```

---

### Task 3: Add the conditional generated-image contract

**Files:**
- Modify: `chatcut-topic-video-editor/SKILL.md`
- Modify: `chatcut-topic-video-editor/references/visual-assets.md`

**Interfaces:**
- Consumes: `assets/generated-image-style/*.png`, `chatcut:asset-import`, and `chatcut:image-gen`.
- Produces: A decision rule routing only generated stills through bundled reference assets and `referenceAssetIds`.

- [ ] **Step 1: Run contract checks before editing**

```bash
rg -n 'assets/generated-image-style|referenceAssetIds|internal `style-only`' \
  chatcut-topic-video-editor/SKILL.md \
  chatcut-topic-video-editor/references/visual-assets.md
```

Expected: FAIL to find the complete contract.

- [ ] **Step 2: Add the minimal rule to `SKILL.md`**

Under visual-material preparation, require the agent to:

```text
- Read the generated-image subsection in references/visual-assets.md whenever a new still will be generated.
- Use assets/generated-image-style references only for model-generated stills.
- Exclude screenshots, source media, and text/Motion Graphics from this style rule.
- Import selected references as internal style-only assets and pass their IDs in referenceAssetIds.
- Never place internal style references on the timeline unless separately requested as visible media.
```

- [ ] **Step 3: Add the detailed contract to `references/visual-assets.md`**

Add `Generated-image style references` with:

```text
Scope: newly generated supplementary stills only.
Style: warm off-white paper, bold black hand-drawn outlines, simple doodle/infographic forms, cyan and yellow accents, optional pale-green shadow, generous whitespace.
Selection: choose 1–3 images by target aspect ratio and diagram complexity.
ChatCut flow: import selected files as internal style-only assets, then pass returned project asset IDs in referenceAssetIds.
Prompt: transfer style only; do not copy wording, logos, subject matter, or exact composition.
Text: keep important Chinese wording out of generated pixels and add it later as editable Motion Graphics.
Override: obey an explicit task-level generated-image style instead.
Fallback: if references cannot be passed, use the written style contract and disclose the fallback.
```

Include this source map:

```text
16:9 → assets/generated-image-style/16_9.png plus one relevant diagram example
3:4 → assets/generated-image-style/3_4.png
4:3 → assets/generated-image-style/4_3.png
Diagram-heavy → vibewriting.png, 交互.png, or 手速跟不上脑速.png
```

- [ ] **Step 4: Re-run the contract checks**

```bash
rg -n 'assets/generated-image-style|referenceAssetIds|internal `style-only`|Motion Graphics|screenshots' \
  chatcut-topic-video-editor/SKILL.md \
  chatcut-topic-video-editor/references/visual-assets.md
```

Expected: hits for resource path, conditional scope, style-only handling, ChatCut parameter, and exclusions.

- [ ] **Step 5: Commit the Skill contract**

```bash
git add chatcut-topic-video-editor/SKILL.md chatcut-topic-video-editor/references/visual-assets.md
git commit -m "feat: anchor generated stills to bundled style references"
```

---

### Task 4: Document and verify the completed Skill

**Files:**
- Modify: `README.md`
- Verify: `chatcut-topic-video-editor/agents/openai.yaml`
- Verify: `chatcut-topic-video-editor/SKILL.md`
- Verify: `chatcut-topic-video-editor/assets/generated-image-style/*.png`

**Interfaces:**
- Consumes: Completed asset directory and conditional Skill contract.
- Produces: User-facing documentation matching the package and a validated deployable Skill.

- [ ] **Step 1: Run the README check before editing**

```bash
rg -n 'generated-image-style|AI 生成图片|截图.*不' README.md
```

Expected: FAIL because the new behavior and directory are undocumented.

- [ ] **Step 2: Update README behavior and tree**

Document exactly:

```text
- The six bundled references are default style anchors only for AI-generated supplementary stills.
- Authentic screenshots and editable Chinese text/Motion Graphics do not inherit the reference-image style.
- Explicit per-task generated-image styles override the bundled default.
- The tree contains chatcut-topic-video-editor/assets/generated-image-style/.
```

- [ ] **Step 3: Validate frontmatter, package layout, and metadata**

```bash
python3 /Users/talon/.codex/skills/.system/skill-creator/scripts/quick_validate.py \
  /Users/talon/Proj/chatcutskills/chatcut-topic-video-editor
python3 - <<'PY'
from pathlib import Path
import yaml

root = Path('/Users/talon/Proj/chatcutskills/chatcut-topic-video-editor')
images = sorted((root / 'assets/generated-image-style').glob('*.png'))
assert len(images) == 6, images
assert all(image.stat().st_size > 0 for image in images)
yaml.safe_load((root / 'agents/openai.yaml').read_text())
print('validated:', len(images), 'style references and openai.yaml')
PY
```

Expected: `Skill is valid!` and `validated: 6 style references and openai.yaml`.

- [ ] **Step 4: Re-run the original scenario with the revised Skill**

Use the Task 1 prompt with a fresh-context agent. Expected response:

```text
- One to three bundled references influence only the AI-generated workflow still.
- Selected references are imported as internal style-only assets.
- Their project asset IDs are sent through referenceAssetIds.
- The authentic screenshot does not inherit the illustrated style.
- The Chinese Motion Graphic remains an independent editable text treatment.
- Internal style references are not placed on the timeline.
```

- [ ] **Step 5: Review diff and commit documentation**

```bash
git diff --check
git status --short
git diff -- README.md chatcut-topic-video-editor/SKILL.md chatcut-topic-video-editor/references/visual-assets.md
git add README.md
git commit -m "docs: explain generated image style behavior"
```

- [ ] **Step 6: Confirm final repository state**

```bash
git log -5 --oneline --decorate
git status --short
```

Expected: only pre-existing out-of-scope files remain untracked or modified; no uncommitted changes from this implementation remain.
