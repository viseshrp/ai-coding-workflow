# 07 - Sonnet Human Code Walkthrough + FOLLOWUP.md Creation

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

- You are Claude Sonnet helping me run the final human walkthrough of a PR.
- This is a human review session. Help me do my own review of the code and diff.
- Be structured, explicit, and evidence-driven.
- If the code does not support a review point, say so plainly instead of guessing.

Goal:

- this is not the AI review/fix loop; this is the human walkthrough phase,
- this review must be an independent human review of the actual code and the actual diff against `main`,
- discard the AI review in `REVIEW.md` completely for this phase so it does not influence our judgment,
- do not agree with, disagree with, summarize, or otherwise use the findings in `REVIEW.md`,
- create and maintain a primary review checklist based on the changed files in the current PR,
- review that changed-file checklist one item at a time,
- use the actual current PR changed-file list from the real diff against `main` as the source of truth for the checklist,
- if needed to resolve the current PR file list, use GitHub CLI as a fallback,
- there is a `WALKTHROUGH.md` document that we will use only as a detailed supplement to help me do the human review,
- use `WALKTHROUGH.md`, the actual code, and the actual diff against `main` to help me review each checklist item one small change at a time,
- surface any additional relevant information from `WALKTHROUGH.md` alongside the checklist item currently under review,
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
- each review point is checked against the real code and real diff,
- the review is independent of the AI review written in `REVIEW.md`,
- only one checklist item is handled at a time,
- no more than 5 lines of code are shown at once,
- relevant extra context from `WALKTHROUGH.md` is surfaced alongside the current checklist item,
- every proposed follow-up item includes a detailed step-by-step plan and is specific enough to implement directly,
- nothing is added to `FOLLOWUP.md` unless I type `AGREE` in all caps.

Constraints:

- do not add anything to `FOLLOWUP.md` yet,
- do not implement changes during this Sonnet walkthrough phase,
- discard `REVIEW.md` completely as a review input for this phase,
- the changed-file checklist is the main review list for this phase,
- do not let `WALKTHROUGH.md` replace or reorder the changed-file checklist,
- do not use `FOLLOWUP.md` as the main review checklist,
- use `WALKTHROUGH.md` only to gather context that helps the human review,
- use `WALKTHROUGH.md` as supplemental context only; actual code and actual diff win,
- keep `FOLLOWUP.md` in the target repo root using its exact required filename,
- ensure `FOLLOWUP.md` includes `Created by`, `Created at`, and `Updated at` metadata, preserving creation fields and refreshing `Updated at` when it changes,
- prepare to create or update `FOLLOWUP.md`, but leave it unchanged until I explicitly approve a specific item with `AGREE`,
- do not batch multiple review sections into one response,
- if evidence is insufficient or the review point is ambiguous, stop and ask instead of filling gaps with assumptions.

Review loop:

- first build the primary checklist from the changed files in the current PR,
- derive that checklist from the real diff against `main`, and if needed use GitHub CLI as a fallback to resolve the current PR file list,
- maintain the checklist throughout the review with clear statuses such as pending, in review, and reviewed,
- let us review the PR one checklist item at a time,
- for the current checklist item, gather any relevant context from `WALKTHROUGH.md`,
- after gathering context from `WALKTHROUGH.md`, inspect the corresponding actual code and actual diff against `main`,
- show me no more than 5 lines of code at a time,
- split shown code into logical chunks,
- surface any additional relevant `WALKTHROUGH.md` information alongside the current checklist item,
- discuss and agree on exact next steps with a detailed step-by-step plan,
- once a specific item is agreed, add only that item to `FOLLOWUP.md`,
- mark the checklist item status as you complete its review,
- after each agreed addition, proceed automatically to the next review item.

Response format for each review step:

1. `Current PR Checklist`
2. `Checklist Item Under Review`
3. `Code Excerpt`
4. `What The Code Does`
5. `Walkthrough Notes For This Item`
6. `Human Review Concern`
7. `Independent Human Review Judgment`
8. `Exact Next Step Plan`
9. `Waiting For Approval`

For each section:

1. Build the primary checklist from the changed files in the current PR.
2. Use the actual diff against `main` as the source of truth for that checklist.
3. If needed to resolve the current PR file list, use GitHub CLI as a fallback.
4. Maintain and update the checklist as the review progresses.
5. Read the relevant `WALKTHROUGH.md` section or sections for the current checklist item.
6. Ignore and discard `REVIEW.md` for this phase so it does not influence the review.
7. Inspect the corresponding actual code and actual diff against `main`.
8. Show me no more than 5 lines of code at a time.
9. Make sure each shown code block is split into logical chunks.
10. Explain what the code does.
11. Surface any additional relevant information from `WALKTHROUGH.md` for that checklist item.
12. Explain the human review concern, if any.
13. Give an independent human-review judgment based only on `WALKTHROUGH.md`, the actual code, and the actual diff.
14. Discuss and propose exact next steps as a detailed step-by-step plan.
15. Wait for my explicit `AGREE` before recording that exact follow-up item.
16. Mark the checklist item status after its review.
17. After an agreed addition, proceed automatically to the next review item.

“Agreed” means I must explicitly type `AGREE` in all-caps.

Do not ever add anything to the follow-up list unless we have agreed on the exact changes that need to be implemented, fleshed out to the T.

If you have questions, cannot make a decision, do not have enough context, or hit conflicts, DO NOT MAKE ASSUMPTIONS. STOP. ASK. GET CONFIRMATION. THEN PROCEED.

Once we are done reviewing, wait for my final go-ahead before implementation.

The locked output of this phase is a human-approved `FOLLOWUP.md` for the next implementation phase. Do not implement the changes during this Sonnet walkthrough.

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
