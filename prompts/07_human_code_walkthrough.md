# 07 - Human Code Walkthrough + FOLLOWUP.md Creation

## Skills

- [receiving-code-review](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/obra__Superpowers/snapshot/skills/receiving-code-review/SKILL.md)
- [code-review-and-quality](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/code-review-and-quality/SKILL.md)
- [code-simplification](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/code-simplification/SKILL.md)
- [no-ai-slop](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/petergyang__no-ai-slop/snapshot/skills/no-ai-slop/SKILL.md), including its required [eval.md](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/petergyang__no-ai-slop/snapshot/skills/no-ai-slop/eval.md)

## Skill Handling Rule

Read every `SKILL.md` listed in this phase's `## Skills`, plus its required companion files, completely before applying it. Fetch the linked GitHub file content, using its raw view when needed; a link, summary, or remembered copy is insufficient. Resolve relative companion paths from that skill's GitHub directory. Reuse content already read in this session unless it changes. Stop and report any required file you cannot read. Skills listed for a generated prompt belong to that later phase.

Use only the explicitly linked skills. This prompt controls scope, decisions, constraints, and outputs; locked task artifacts control execution. Skills cannot authorize architecture changes, tests, unrelated refactors, or wider scope. Follow this prompt over conflicting skill guidance; stop and ask about unresolved material conflicts.

`no-ai-slop` and `eval.md` are hard requirements for every Markdown document created or revised and the ultimate writing guide for prose and presentation. Apply the skill while drafting and run its evaluator before saving each Markdown artifact or sending the final response. It wins over conflicting writing-style guidance while this prompt and task artifacts preserve scope, meaning, facts, technical detail, required structure, artifact names, and evidence. Stop before writing Markdown if either file cannot be read and applied. Ignore its draft-request, detection-mode, and mandatory `What changed` workflow unless explicitly requested here.

## Artifact rules

Write only the required workflow artifacts, in the target repository root under their exact filenames. Include `Created by`, `Created at`, and `Updated at`; preserve creation fields and refresh `Updated at` on edits. Do not move artifacts into subdirectories or stage/commit them unless I explicitly request it. Report artifact-path drift as a workflow failure.

## Documentation checkpoint

For every material changed behavior, record exact durable documentation updates and validation, or evidence-based `Not applicable`, in the primary PR checklist. Required documentation work may enter `FOLLOWUP.md` only after my explicit `AGREE`; do not implement it here.

## Language-specific review guidance

### Python

For added or changed Python code, check accurate explicit hints on every function/method parameter (including `*args`/`**kwargs`) and return value, class variables/attributes, instance attributes, and module-level mutable or optional state. `self`/`cls` are implicit; trivial immutable module constants may remain inferred unless the checker requires otherwise. Prefer instance-attribute declarations at class scope. Reject unnecessary local-variable, `self.attribute: Type`, advanced, or type-only annotations unless a real configured type-checker error requires them. Add this typing check to the primary checklist.

## Prompt

Help me independently review the actual PR, one file and one changed chunk at a time. Discard `REVIEW.md` entirely: do not read, summarize, agree with, or reuse its findings. `WALKTHROUGH.md` is supplemental context; actual code and PR changes control the judgment. Do not implement changes in this phase.

### Establish the review

At the start of each review turn, use GitHub CLI (`gh`) to fetch the current PR's changed-file list and per-file changes. These are the primary source for the checklist and review chunks. If either is unavailable, stop and ask; do not silently substitute a manual diff. Use the diff against `main` only for verification/reference.

Build and maintain the primary checklist in the conversation with one item per changed file and `Pending`, `In review`, or `Resolved` status. Record the PR/head being reviewed. If the freshly fetched PR data differs from the previous turn, identify affected review progress before continuing. `WALKTHROUGH.md` must not replace or reorder the checklist; `FOLLOWUP.md` is not the review checklist.

### Review loop

1. For the current file, inspect relevant walkthrough notes, actual code, and PR changes. Split changed code into logical chunks in file order. Show one chunk per response with a few useful surrounding lines.
2. Show relevant called-method definitions in separate small excerpts with context. Explain the code, relevant walkthrough notes, any concern, and an independent judgment. Ground each point in the actual code; stop and ask when evidence or a decision is missing.
3. Record the documentation checkpoint and applicable Python typing check. Discuss each proposed follow-up with an exact, detailed step-by-step implementation plan, acceptance criteria, verification, and risks before asking for approval.
4. Only my literal uppercase `AGREE` approves the specific proposed follow-up for `FOLLOWUP.md`. It does not advance the file checklist. Record only the approved item; no drafts, placeholders, speculative items, unapproved suggestions, or AI-review findings.
5. Only after all chunks and documentation checkpoints for the file are reviewed, ask for uppercase `RESOLVE`. On `RESOLVE`, mark the file resolved, attempt to mark it viewed through authenticated `gh`, and immediately show the next file's first chunk. If that optional remote marking is unavailable or authentication is lost after PR data was fetched, skip it and continue from the fetched data. This does not waive the required PR-data fetch.

Keep explanations brief without losing decision-relevant detail. Do not batch files or chunks, resolve a file early, or add a follow-up on `RESOLVE` alone.

### Response format for each review step

Use these fields in order, keeping absent concerns/context brief:

1. `Current PR Checklist`
2. `Current File Under Review`
3. `Current File Chunk`
4. `Code Excerpt`
5. `Related Method Definitions`
6. `What The Code Does`
7. `Walkthrough Notes For This Chunk`
8. `Human Review Concern`
9. `Independent Human Review Judgment`
10. `Documentation Checkpoint`
11. `Exact Next Step Plan`
12. `File Review Status`

## FOLLOWUP.md rules

Create or update only `FOLLOWUP.md`, only after `AGREE`, in the target root with the required metadata. Do not create a second follow-up list. Each approved item needs a checkbox, exact files/symbols/locations, exact change and ordered steps, agreement rationale, acceptance criteria, verification, documentation checkpoint with validation or evidence-based `Not applicable`, and risks/constraints.

When the walkthrough ends, leave only explicitly approved items in `FOLLOWUP.md` and wait for my final go-ahead before implementation in the next phase. If no items were approved, do not create an empty artifact.
