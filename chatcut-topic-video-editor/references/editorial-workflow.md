# Editorial workflow

Use this reference for transcript-driven A-roll cleanup, restructuring, and opening hooks.

## 1. Understand the source

Reconstruct complete ideas across adjacent ASR segments. Segment boundaries are not sentence boundaries.

Identify:

- The problem or inciting incident
- The core claim
- Supporting examples
- Product or software references
- Risks, permissions, or trade-offs
- Demonstration steps
- Quantified proof or result
- Closing takeaway

Choose a structure that serves the topic. A useful default for tutorials and reflective explainers is:

`Hook → problem → available options → chosen method → risk/boundary → demonstration → result → takeaway`

Do not force this structure when the footage clearly supports another one.

## 2. Run the mechanical pass first

When fixed fillers or long pauses are present:

1. Run `clean_script`.
2. For a concise but still natural Chinese tutorial, use `silence: "compress:400"` when the user has not supplied a threshold.
3. Re-read the refreshed `timelineMd`.
4. Treat the refreshed script as the only source of truth for semantic editing.

Audit the result for false filler removal. A fixed-token cleaner can damage a real word when ASR splits it badly. For example, removing `额` from `额外` can leave `外`. Restore the full source segment from `library/<filename>.md` when the automatic pass breaks a word or phrase.

## 3. Make semantic cuts

Remove:

- Abandoned starts that are completed later
- Repeated attempts at the same sentence
- Duplicate setup or conclusion
- Pricing or navigation tangents that do not support the thesis
- Empty verbal loops
- Comparisons that distract from the user's stated topic

Keep:

- Subjects, verbs, list labels, and connectors needed for grammar
- Setup that later sentences depend on
- Qualifiers that preserve accuracy
- Natural breathing room
- Useful emotion or personality

Prefer the later complete retake only when it is actually more complete. Do not stitch unfinished fragments from several attempts into a synthetic sentence.

Use inline strike syntax for a bad word inside an otherwise useful source row. Delete the full row only when the complete segment is unnecessary.

## 4. Build the hook

Prefer a source-derived hook in this order:

1. Strong counterintuitive claim
2. Clear quantified result
3. Risk or conflict
4. Specific viewer problem
5. Direct question

Move a complete semantic unit to the opening. Remove its original occurrence unless an intentional callback is useful.

Do not fabricate spoken wording inside Script. A newly written hook requires a separate title card, narration, or voiceover and user alignment when the direction is not already clear.

## 5. Preserve source order intentionally

Use numeric filename order as the initial sequence. Reorder complete ideas only when it materially improves clarity.

For several files that form one continuous recording:

- Keep the named order.
- Remove duplicated introductions at joins.
- Check whether the later file contains the demonstration or result and preserve its context.

## 6. Apply and review

1. Preview a large semantic edit with `apply_script(preview:true)`.
2. Check expected duration and removal scope.
3. Commit with `apply_script`.
4. Read the regenerated clean script.
5. Review the spoken flow from beginning to end.
6. Fix clear grammar, logic, or pacing problems through Script.
7. Run `smooth_audio` after the final structural edit.

Do not communicate internal segment ids to the user. Describe removed material in ordinary language.
