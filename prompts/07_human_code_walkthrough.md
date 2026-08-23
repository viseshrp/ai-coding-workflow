# 07 - Human Code Walkthrough + FOLLOWUP.md Creation

## Skills

- [receiving-code-review](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/obra__Superpowers/snapshot/skills/receiving-code-review/SKILL.md)
- [code-review-and-quality](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/code-review-and-quality/SKILL.md)
- [code-simplification](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/code-simplification/SKILL.md)
- [ponytail-review](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/DietrichGebert__ponytail/snapshot/skills/ponytail-review/SKILL.md)
- [no-ai-slop](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/petergyang__no-ai-slop/snapshot/skills/no-ai-slop/SKILL.md), including its required [eval.md](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/petergyang__no-ai-slop/snapshot/skills/no-ai-slop/eval.md)

## Skill Handling Rule

Use only the explicitly linked skills listed in this prompt.

The prompt is the contract. The locked task artifact is the contract for execution. Skills are supporting procedures only.

If a skill conflicts with this prompt, this prompt wins.

If a conflict is material, stop and ask instead of silently choosing.

Do not use any skill to expand scope, add architecture changes, add tests, add unrelated refactors, or override my explicit instructions.

Apply `ponytail-review` only after the independent human-review judgment for the current changed chunk has been recorded. Use it as a secondary over-engineering check, verify each result against the actual code, and present valid results through this walkthrough's `AGREE` and `FOLLOWUP.md` gates. Do not emit its standalone one-line report or line-count score. Never let line reduction weaken clarity, explicit requirements, correctness, validation, error handling, security, accessibility, backwards compatibility, performance constraints, documentation checkpoints, or the test-review contract.

`no-ai-slop` is a hard requirement for every Markdown document this phase creates or revises. Treat it as the ultimate writing guide and final authority for prose and presentation after satisfying this prompt's factual, technical, structural, and output requirements. If another skill or instruction conflicts only on writing style, `no-ai-slop` wins; this prompt and locked task artifacts still control scope, meaning, required structure, artifact names, constraints, and evidence.

Apply `no-ai-slop` while drafting and run its `eval.md` self-check before saving each Markdown artifact or sending the final response. If its `SKILL.md` or `eval.md` cannot be read and applied, stop before creating or revising Markdown and report the blocker. Ignore its draft-request, detection-mode, and mandatory `What changed` workflow unless this prompt explicitly asks for them.

## Documentation checkpoint

Documentation is a required human-review checkpoint, not final cleanup. For every material changed behavior, use the primary PR checklist to record the exact durable documentation update and its validation, or an evidence-based `Not applicable` decision. This phase must not implement documentation changes; a required documentation change becomes a `FOLLOWUP.md` item only after I explicitly type `AGREE`.

## Language-specific review guidance

### Python

When the current PR's changed code uses Python, add an explicit typing-compliance check to the primary checklist:

- Every parameter, including `*args` and `**kwargs`, and return value of an added or changed function or method must have an explicit, accurate type hint. Treat `self` and `cls` as implicit; do not require annotations for them.
- Every added or changed class variable, class attribute, instance attribute, and module-level mutable or optional state must have an explicit, accurate type hint. A trivial immutable module constant may remain inferred unless the configured type checker needs an annotation.
- Instance-attribute types should be declared at class scope where feasible. Do not require local-variable or `self.attribute: Type` annotations inside function or method bodies unless a real configured type-checker error requires one.
- Required annotations must stay simple and accurate; do not accept advanced type constructs or type-only refactors that the configured type checker does not require.

## Prompt

Role:

- You are GPT or Claude Sonnet helping me run the final human walkthrough of a PR.
- This is a human review session. Help me do my own review of the code and diff.
- Be structured, explicit, and evidence-driven.
- Be terse and brief without losing detail as you move through the review.
- If the code does not support a review point, say so plainly instead of guessing.

Goal:

- this is not the AI review/fix loop; this is the human walkthrough phase,
- this review must be an independent human review of the actual code and the actual PR changes,
- discard the AI review in `REVIEW.md` completely for this phase so it does not influence our judgment,
- do not agree with, disagree with, summarize, or otherwise use the findings in `REVIEW.md`,
- create and maintain a primary review checklist based on the changed files in the current PR,
- review that changed-file checklist one file at a time,
- pull the current PR changed-file list from GitHub CLI (`gh`) and use that as the source of truth for the checklist,
- pull the actual per-file PR changes from GitHub CLI (`gh`) and use those as the primary source for the review chunks,
- use the manual diff against `main` only for verification and reference,
- if GitHub CLI (`gh`) cannot provide the current PR file list or the PR changes, stop and ask instead of silently falling back to the manual diff,
- as the review progresses, resolve files only when moving to the next file,
- when resolving reviewed files, use GitHub CLI if available and authenticated,
- if GitHub CLI is unavailable or I am not logged in, skip the resolution step without erroring and continue the review,
- there is a `WALKTHROUGH.md` document that we will use only as a detailed supplement to help me do the human review,
- use `WALKTHROUGH.md`, the actual code, and the PR changes from GitHub CLI (`gh`) to help me review each file one small chunk at a time,
- perform a documentation checkpoint for every material changed behavior: identify the affected durable user-, operator-, API-, configuration-, or developer-facing documentation, then record the exact update and validation or an evidence-based `Not applicable` decision in the primary checklist,
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

- the current PR changed-file list from GitHub CLI (`gh`),
- the current PR per-file changes from GitHub CLI (`gh`),
- `WALKTHROUGH.md`,
- the current branch diff against `main` for verification/reference only,
- the actual code referenced by the section under discussion.

Success criteria:

- the main review list is a maintained checklist derived from the changed files in the current PR,
- that changed-file checklist is pulled from GitHub CLI (`gh`),
- each checklist item is a changed file from the current PR,
- each reviewed chunk is pulled from the PR changes returned by GitHub CLI (`gh`),
- the manual diff against `main` is used only to verify or cross-check the PR data,
- each review point is checked against the real code and real PR changes,
- the review is independent of the AI review written in `REVIEW.md`,
- only one file is handled at a time,
- within a file, only one chunk is handled at a time,
- each chunk includes a few intelligently selected surrounding lines around the change,
- if method calls appear in the excerpt, the relevant method definitions are also shown in separate small excerpts with context,
- relevant extra context from `WALKTHROUGH.md` is surfaced alongside the current file chunk,
- each material changed behavior has an explicit documentation-checkpoint result before its file can be resolved,
- each changed chunk receives a secondary `ponytail-review` simplification check only after the independent human-review judgment,
- typing `RESOLVE` in all caps advances the review to the next file only after the current file is fully reviewed,
- every proposed follow-up item includes a detailed step-by-step plan and is specific enough to implement directly,
- nothing is added to `FOLLOWUP.md` unless I type `AGREE` in all caps.

Constraints:

- do not add anything to `FOLLOWUP.md` yet,
- do not implement changes during this human walkthrough phase,
- discard `REVIEW.md` completely as a review input for this phase,
- the changed-file checklist is the main review list for this phase,
- do not build the changed-file checklist from the manual diff against `main`,
- do not build the review chunks from the manual diff against `main`,
- use GitHub CLI (`gh`) as the primary source for both the PR file list and the PR changes,
- use the manual diff against `main` only for verification/reference,
- do not let `WALKTHROUGH.md` replace or reorder the changed-file checklist,
- do not use `FOLLOWUP.md` as the main review checklist,
- do not resolve a file until its material changed behavior has a documentation-checkpoint result in the primary checklist; record required documentation work in `FOLLOWUP.md` only after I type `AGREE`, and record an evidence-based `Not applicable` decision in the primary checklist when no durable documentation change is needed,
- use `WALKTHROUGH.md` only to gather context that helps the human review,
- use `WALKTHROUGH.md` as supplemental context only; actual code and the PR changes from GitHub CLI (`gh`) win,
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
- pull that checklist from GitHub CLI (`gh`),
- maintain the checklist throughout the review with clear statuses such as pending, in review, and resolved,
- let us review the PR one file at a time,
- for the current file, gather any relevant context from `WALKTHROUGH.md`,
- after gathering context from `WALKTHROUGH.md`, inspect the corresponding actual code, the PR changes from GitHub CLI (`gh`), and the manual diff against `main` only as verification/reference,
- identify the durable documentation affected by each material changed behavior and record its update-and-validation requirement or evidence-based `Not applicable` rationale in the primary checklist,
- break the current file into logical changed chunks and review one chunk at a time in file order,
- for each changed chunk, show a few intelligently selected surrounding lines around the change,
- if method calls appear in the shown excerpt, show the relevant method definitions in separate small excerpts with context,
- surface any additional relevant `WALKTHROUGH.md` information alongside the current file chunk,
- after recording the independent human-review judgment, apply `ponytail-review` to the current changed chunk and verify any result against the surrounding code and required behavior,
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
10. `Ponytail Simplification Check`
11. `Documentation Checkpoint`
12. `Exact Next Step Plan`
13. `File Review Status`

For each review turn:

1. Build the primary checklist from the changed files in the current PR.
2. Pull that changed-file checklist from GitHub CLI (`gh`) and treat it as the source of truth.
3. Pull the per-file PR changes from GitHub CLI (`gh`) and treat them as the primary source for the review chunks.
4. Maintain and update the checklist as the review progresses.
5. Treat each checklist item as one file from the current PR.
6. Read the relevant `WALKTHROUGH.md` section or sections for the current file.
7. Ignore and discard `REVIEW.md` for this phase so it does not influence the review.
8. Inspect the corresponding actual code and the PR changes from GitHub CLI (`gh`).
9. Review the current file one changed chunk at a time.
10. For each changed chunk, show a few intelligently selected surrounding lines around the change.
11. If method calls appear in the shown excerpt, show the relevant method definitions in separate small excerpts with context.
12. Make sure each shown code block is split into logical chunks.
13. Explain what the code does.
14. Surface any additional relevant information from `WALKTHROUGH.md` for that file chunk.
15. Explain the human review concern, if any.
16. Use the manual diff against `main` only to verify or cross-check the PR data from GitHub CLI (`gh`); do not use it as the primary review source.
17. Give an independent human-review judgment based only on `WALKTHROUGH.md`, the actual code, and the PR changes from GitHub CLI (`gh`), using the manual diff against `main` only for verification/reference.
18. Only after that independent judgment, apply `ponytail-review` to the current changed chunk and verify any simplification result against the actual code and required behavior.
19. Record the documentation checkpoint for each material changed behavior: exact durable documentation and validation, or an evidence-based `Not applicable` rationale.
20. Discuss and propose exact next steps as a detailed step-by-step plan.
21. If I type `AGREE`, record that exact follow-up item in `FOLLOWUP.md`.
22. Only after the current file is fully reviewed and its documentation checkpoint is recorded, ask whether I want to `RESOLVE` that file.
23. If I type `RESOLVE`, mark the current file resolved and proceed to the next file.
24. When processing `RESOLVE`, attempt to resolve the checklist item with GitHub CLI if available and authenticated.
25. If GitHub CLI is unavailable or I am not logged in, skip that resolution step without erroring and continue.
26. After `RESOLVE`, immediately display the review for the next file starting with its first chunk.

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
- documentation checkpoint: exact durable documentation file/section, update, and validation, or the evidence-based `Not applicable` rationale,
- any risks or constraints.

Do not include speculative items.

Do not include optional suggestions unless I explicitly agree.

Do not include an item from `REVIEW.md`. Discard the AI review completely in this phase.

Do not add placeholder, draft, or "to discuss" items to `FOLLOWUP.md`.
