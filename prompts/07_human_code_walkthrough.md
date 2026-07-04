# 07 - Human Code Walkthrough + FOLLOWUP.md Creation

## Skills

- [receiving-code-review](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/obra__Superpowers/snapshot/skills/receiving-code-review/SKILL.md)
- [code-review-and-quality](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/code-review-and-quality/SKILL.md)
- [code-simplification](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/code-simplification/SKILL.md)

## Skill Handling Rule

Use only the explicitly linked skills listed in this prompt.

The prompt is the contract. The locked task artifact is the contract for execution. Skills are supporting procedures only.

If a skill conflicts with this prompt, this prompt wins.

If a conflict is material, stop and ask instead of silently choosing.

Do not use any skill to expand scope, add architecture changes, add tests, add unrelated refactors, or override my explicit instructions.


## Prompt

Role:

- You are GPT or Claude Sonnet helping me run the final human walkthrough of a PR.
- This is a human review session. Help me do my own review of the code and diff.
- Be structured, explicit, and evidence-driven.
- Be terse and brief without losing detail as you move through the review.
- If the code does not support a review point, say so plainly instead of guessing.

Goal:

- this is not the AI review/fix loop; this is the human walkthrough phase,
- this review must be an independent human review of the actual code and the actual diff against `main`,
- discard the AI review in `REVIEW.md` completely for this phase so it does not influence our judgment,
- do not agree with, disagree with, summarize, or otherwise use the findings in `REVIEW.md`,
- create and maintain a primary review checklist based on the changed files in the current PR,
- review that changed-file checklist one file at a time,
- use the actual current PR changed-file list from the real diff against `main` as the source of truth for the checklist,
- if needed to resolve the current PR file list, use GitHub CLI as a fallback,
- as the review progresses, resolve files only when moving to the next file,
- when resolving reviewed files, use GitHub CLI if available and authenticated,
- if GitHub CLI is unavailable or I am not logged in, skip the resolution step without erroring and continue the review,
- there is a `WALKTHROUGH.md` document that we will use only as a detailed supplement to help me do the human review,
- use `WALKTHROUGH.md`, the actual code, and the actual diff against `main` to help me review each file one small chunk at a time,
- for each changed chunk, include a few lines selected intelligently around the change so the code is easier to understand,
- if method calls appear in the shown excerpt, also show the relevant method definitions in separate small excerpts with context,
- surface any additional relevant information from `WALKTHROUGH.md` alongside the current file chunk under review,
- create or update `FOLLOWUP.md` as the checklist for necessary changes, but do not record any item until I explicitly approve it with `AGREE`,
- discuss and agree on exact next steps with a detailed step-by-step plan before recording any follow-up item.

Artifact location rule:

- all workflow-generated Markdown artifacts for this workflow must live in the target repo root using the exact required filenames,
- all workflow-generated Markdown artifacts must include `Created by`, `Created at`, and `Updated at` metadata, preserving creation fields and refreshing `Updated at` on edits,
- if `FOLLOWUP.md` is created or updated, it must be created or updated only in the target repo root and nowhere else.

Context to read before starting:

- the current PR changed-file list from the actual diff against `main`,
- `WALKTHROUGH.md`,
- the current branch diff against `main`,
- the actual code referenced by the section under discussion.

Success criteria:

- the main review list is a maintained checklist derived from the changed files in the current PR,
- each checklist item is a changed file from the current PR,
- each review point is checked against the real code and real diff,
- the review is independent of the AI review written in `REVIEW.md`,
- only one file is handled at a time,
- within a file, only one chunk is handled at a time,
- each chunk includes a few intelligently selected surrounding lines around the change,
- if method calls appear in the excerpt, the relevant method definitions are also shown in separate small excerpts with context,
- relevant extra context from `WALKTHROUGH.md` is surfaced alongside the current file chunk,
- typing `RESOLVE` in all caps advances the review to the next file only after the current file is fully reviewed,
- every proposed follow-up item includes a detailed step-by-step plan and is specific enough to implement directly,
- nothing is added to `FOLLOWUP.md` unless I type `AGREE` in all caps.

Constraints:

- do not add anything to `FOLLOWUP.md` yet,
- do not implement changes during this human walkthrough phase,
- discard `REVIEW.md` completely as a review input for this phase,
- the changed-file checklist is the main review list for this phase,
- do not let `WALKTHROUGH.md` replace or reorder the changed-file checklist,
- do not use `FOLLOWUP.md` as the main review checklist,
- use `WALKTHROUGH.md` only to gather context that helps the human review,
- use `WALKTHROUGH.md` as supplemental context only; actual code and actual diff win,
- keep the review terse and brief without losing detail,
- review each file one chunk at a time instead of trying to cover the whole file at once,
- always include a few intelligently chosen surrounding lines around each changed chunk,
- if method calls appear in the excerpt, show the relevant method definitions in separate small excerpts with context,
- do not advance to the next checklist item on `AGREE` alone,
- do not ask for `RESOLVE` until the current file is fully reviewed,
- keep `FOLLOWUP.md` in the target repo root using its exact required filename,
- ensure `FOLLOWUP.md` includes `Created by`, `Created at`, and `Updated at` metadata, preserving creation fields and refreshing `Updated at` when it changes,
- prepare to create or update `FOLLOWUP.md`, but leave it unchanged until I explicitly approve a specific item with `AGREE`,
- do not batch multiple review sections into one response,
- if evidence is insufficient or the review point is ambiguous, stop and ask instead of filling gaps with assumptions.

Review loop:

- first build the primary checklist from the changed files in the current PR,
- derive that checklist from the real diff against `main`, and if needed use GitHub CLI as a fallback to resolve the current PR file list,
- maintain the checklist throughout the review with clear statuses such as pending, in review, and resolved,
- let us review the PR one file at a time,
- for the current file, gather any relevant context from `WALKTHROUGH.md`,
- after gathering context from `WALKTHROUGH.md`, inspect the corresponding actual code and actual diff against `main`,
- break the current file into logical changed chunks and review one chunk at a time in file order,
- for each changed chunk, show a few intelligently selected surrounding lines around the change,
- if method calls appear in the shown excerpt, show the relevant method definitions in separate small excerpts with context,
- surface any additional relevant `WALKTHROUGH.md` information alongside the current file chunk,
- discuss and agree on exact next steps with a detailed step-by-step plan,
- once a specific item is agreed, add only that item to `FOLLOWUP.md`,
- when the current file is fully reviewed, ask whether I want to `RESOLVE` that file and move on,
- when I type `RESOLVE` in all caps, mark the current file resolved and then move to the next file,
- when moving to the next file, attempt to resolve the checklist item with GitHub CLI if available and authenticated,
- if GitHub CLI is unavailable or not authenticated, skip that resolution step without erroring and continue,
- after `RESOLVE`, immediately display the review for the next file starting with its first chunk.

Response format for each review step:

1. `Current PR Checklist`
2. `Current File Under Review`
3. `Current File Chunk`
4. `Code Excerpt`
5. `Related Method Definitions`
6. `What The Code Does`
7. `Walkthrough Notes For This Chunk`
8. `Human Review Concern`
9. `Independent Human Review Judgment`
10. `Exact Next Step Plan`
11. `File Review Status`

For each review turn:

1. Build the primary checklist from the changed files in the current PR.
2. Use the actual diff against `main` as the source of truth for that checklist.
3. If needed to resolve the current PR file list, use GitHub CLI as a fallback.
4. Maintain and update the checklist as the review progresses.
5. Treat each checklist item as one file from the current PR.
6. Read the relevant `WALKTHROUGH.md` section or sections for the current file.
7. Ignore and discard `REVIEW.md` for this phase so it does not influence the review.
8. Inspect the corresponding actual code and actual diff against `main`.
9. Review the current file one changed chunk at a time.
10. For each changed chunk, show a few intelligently selected surrounding lines around the change.
11. If method calls appear in the shown excerpt, show the relevant method definitions in separate small excerpts with context.
12. Make sure each shown code block is split into logical chunks.
13. Explain what the code does.
14. Surface any additional relevant information from `WALKTHROUGH.md` for that file chunk.
15. Explain the human review concern, if any.
16. Give an independent human-review judgment based only on `WALKTHROUGH.md`, the actual code, and the actual diff.
17. Discuss and propose exact next steps as a detailed step-by-step plan.
18. If I type `AGREE`, record that exact follow-up item in `FOLLOWUP.md`.
19. Only after the current file is fully reviewed, ask whether I want to `RESOLVE` that file.
20. If I type `RESOLVE`, mark the current file resolved and proceed to the next file.
21. When processing `RESOLVE`, attempt to resolve the checklist item with GitHub CLI if available and authenticated.
22. If GitHub CLI is unavailable or I am not logged in, skip that resolution step without erroring and continue.
23. After `RESOLVE`, immediately display the review for the next file starting with its first chunk.

“Agreed” means I must explicitly type `AGREE` in all-caps.

“Resolved” means I must explicitly type `RESOLVE` in all-caps.

`AGREE` approves a follow-up item for `FOLLOWUP.md`.

`RESOLVE` advances the checklist to the next file after the current file is fully reviewed.

Do not ever add anything to the follow-up list unless we have agreed on the exact changes that need to be implemented, fleshed out to the T.

If you have questions, cannot make a decision, do not have enough context, or hit conflicts, DO NOT MAKE ASSUMPTIONS. STOP. ASK. GET CONFIRMATION. THEN PROCEED.

Once we are done reviewing, wait for my final go-ahead before implementation.

The locked output of this phase is a human-approved `FOLLOWUP.md` for the next implementation phase. Do not implement the changes during this human walkthrough.

## FOLLOWUP.md rules

Create/update `FOLLOWUP.md` only with explicitly agreed items, keep it in the target repo root, and include `Created by`, `Created at`, and `Updated at` metadata.

Also create a follow-up list markdown file to track a checklist of the changes that are necessary.

Do not use `FOLLOWUP.md` as the main review checklist for the current PR. The changed-file checklist is the main review list, and `FOLLOWUP.md` is only for explicitly agreed changes that need implementation.

Each item must include:

- checkbox,
- exact file(s),
- exact symbol(s)/location(s),
- exact change to make,
- why we agreed to it,
- acceptance criteria,
- verification needed,
- any risks or constraints.

Do not include speculative items.

Do not include optional suggestions unless I explicitly agree.

Do not include an item from `REVIEW.md`. Discard the AI review completely in this phase.

Do not add placeholder, draft, or "to discuss" items to `FOLLOWUP.md`.
