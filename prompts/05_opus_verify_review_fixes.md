# 05 - Opus Verifies Review Fixes

## Skills

- [code-review-and-quality](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/code-review-and-quality/SKILL.md)
- [code-simplification](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/code-simplification/SKILL.md)
- [source-driven-development](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/source-driven-development/SKILL.md)
- [verification-before-completion](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/obra__Superpowers/snapshot/skills/verification-before-completion/SKILL.md)
- [receiving-code-review](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/obra__Superpowers/snapshot/skills/receiving-code-review/SKILL.md)
- [no-ai-slop](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/petergyang__no-ai-slop/snapshot/skills/no-ai-slop/SKILL.md), including its required [eval.md](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/petergyang__no-ai-slop/snapshot/skills/no-ai-slop/eval.md)

## Skill Handling Rule

Read every `SKILL.md` listed in this phase's `## Skills`, plus its required companion files, completely before applying it. Fetch the linked GitHub file content, using its raw view when needed; a link, summary, or remembered copy is insufficient. Resolve relative companion paths from that skill's GitHub directory. Reuse content already read in this session unless it changes. Stop and report any required file you cannot read. Skills listed for a generated prompt belong to that later phase.

Use only the explicitly linked skills. This prompt controls scope, decisions, constraints, and outputs; locked task artifacts control execution. Skills cannot authorize architecture changes, tests, unrelated refactors, or wider scope. Follow this prompt over conflicting skill guidance; stop and ask about unresolved material conflicts.

`no-ai-slop` and `eval.md` are hard requirements for every Markdown document created or revised and the ultimate writing guide for prose and presentation. Apply the skill while drafting and run its evaluator before saving each Markdown artifact or sending the final response. It wins over conflicting writing-style guidance while this prompt and task artifacts preserve scope, meaning, facts, technical detail, required structure, artifact names, and evidence. Stop before writing Markdown if either file cannot be read and applied. Ignore its draft-request, detection-mode, and mandatory `What changed` workflow unless explicitly requested here.

## Engineering Contract

Apply these standards within this phase's write permissions. Review and planning phases assess them; implementation phases execute them.

### Plan adherence

Follow a user-provided plan exactly, without divergence, invented requirements, or architecture changes. Stop and ask if a decision is missing, context is insufficient, instructions conflict, the plan contradicts code, or execution would harm performance, security, backwards compatibility, or public APIs. Do not assume an answer to a material question. Continue authorized work without step-by-step approval when no blocker remains.

### Scope control

Make the smallest necessary changes; explain any required surrounding-code edit. Keep unrelated refactors and improvements in `Not Doing / Suggestions`. Exclude DevOps, packaging, build changes, and test authoring unless the plan or phase authorizes them; focused verification commands remain allowed. Keep UI changes in UI code unless the plan requires otherwise. Match repository style. Do not write the changelog unless explicitly requested.

### Performance and complexity

Avoid waiting hacks and ad hoc retry loops. Weigh time/space complexity and readability; do not use brute-force or quadratic operations unless the plan justifies them and data sizes make them safe. Prefer readable solutions over complicated optimizations. Before implementing a performance regression, stop and explain the impact in terms a junior developer can understand.

### Dependencies, frameworks, and documentation grounding

Do not add third-party libraries without explicit approval. Justify library/framework use and verify it against official documentation for the repository's installed or locked version. Use current supported APIs compatible with that version; flag outdated APIs without silently upgrading dependencies. If documentation is insufficient and source is open, clone the matching source into a temporary directory and inspect the relevant implementation. State anything still unverified; do not guess API behavior.

### Public APIs and exceptions

Preserve backwards compatibility unless the app version is unreleased. Keep public APIs intuitive, consistently named, and aligned with existing interfaces. Translate library/framework exceptions into existing or appropriate custom public errors. Avoid exception chains that expose implementation details; log debugging traces through the existing logger when available.

### Code quality and maintainability

Reuse existing code, preserve DRY, separation of concerns, and single responsibility. Stop and flag duplication or reinvention. Use proper imports; never load source as a blob and execute it. Allow assertions only in tests. Surface assumptions. Reuse constants or define them in the appropriate location instead of hardcoding numbers, versions, or other shared values.

### Types

Use accurate, readable types. Avoid filler or overly generic types, type-ignore comments, and casts added merely to satisfy a checker. Prefer the simplest accurate annotation or a well-named type alias over crowded, nested, or repetitive types.

### Python

Apply only to added or changed Python code:

- Explicitly type every function/method parameter, including `*args` and `**kwargs`, and return value; `self` and `cls` are implicit.
- Explicitly type class variables, class/instance attributes, and module-level mutable or optional state. Trivial immutable module constants may remain inferred unless the configured checker requires otherwise.
- Declare instance-attribute types at class scope where feasible. Do not add local-variable or `self.attribute: Type` annotations inside methods/functions unless a real configured type-checker error requires them.
- Keep annotations simple and accurate; avoid advanced constructs and type-only refactors unless the configured checker requires them.

### Comments and documentation

Explain non-obvious code with brief comments sufficient for a junior developer; describe resulting behavior instead of the task or change process. Correct stale comments within scope. Document every added or changed string transformation with representative input and expected-output examples. Locate durable documentation through docs-build configuration, GitHub Actions, or Makefiles, and update existing sections or add needed ones.

### Documentation checkpoint

At each planning, implementation, review, verification, and handoff checkpoint, map every material behavior or implementation step to affected user-, operator-, API-, configuration-, or developer-facing documentation. Require exact durable files/sections, updates in the same change set, and docs-build, link, rendering, or focused validation evidence; otherwise record an evidence-based `Not applicable` decision. Implementation/fix phases must complete this before marking work done. Review-only phases report gaps. Code comments, commit messages, and workflow artifacts do not replace durable documentation.

### Cross-platform behavior

Support both Linux and Windows. macOS is outside the required platform scope.

### Git and verification

When committing is authorized, use small logical commits with detailed messages explaining the change, rationale, and verification; split large changes sensibly. Run applicable focused lint and smoke checks for each commit unless command execution is unavailable or forbidden. Require fresh verification evidence before claiming completion. For failed commands, report the exact command and error/log without paraphrasing. State credential, dependency, or environment blockers precisely.

### Tests

Do not create, modify, or delete tests in this phase. Run focused existing tests/checks when needed; do not manually run the entire suite unless explicitly asked. Verify test-related fixes against the accepted `REVIEW.md` finding and focused evidence, without inventing new test policy. Defer test authoring to the final model-agnostic `09_write_focused_tests_any_model.md` phase; do not duplicate its detailed test contract here.

## Artifact rules

Write only the required workflow artifacts, in the target repository root under their exact filenames. Include `Created by`, `Created at`, and `Updated at`; preserve creation fields and refresh `Updated at` on edits. Do not move artifacts into subdirectories or stage/commit them unless I explicitly request it. Report artifact-path drift as a workflow failure.

## Prompt

As Claude Opus, verify every prior blocking and non-blocking finding against the actual fixes. Write only `REVIEW_FIX_VERIFICATION.md`; do not modify code/tests or create a fix prompt.

Read original `REVIEW.md` and `WALKTHROUGH.md`, the current diff against `main`, affected code, and, when present, `REVIEW_FIX_PROMPT.md`, the fix model's summary, and `FEATURE_SPEC_AND_PLAN.md`.

Inspect repository instructions, the named inputs, and relevant code before judging or editing. Answer repository questions from evidence; distinguish facts, inferences, and unresolved decisions. Batch independent reads/searches when useful and keep dependent actions sequential. Use available repository/search/edit tools without assuming a particular vendor. Keep updates brief; report decisions, evidence, and blockers rather than a running reasoning transcript. Once required checks pass, repeat or broaden them only for changed code, failures, or unresolved risks.

For each original finding, inspect the changed code, classify it as `Resolved`, `Partially Resolved`, `Not Resolved`, or `Invalid Finding`, and explain the code evidence and remaining action. A model's claim is insufficient evidence. Surface new issues introduced by fixes.

### Documentation checkpoint verification

Inspect every material changed behavior's exact durable documentation, validation evidence, or evidence-based `Not applicable` rationale. Missing, inaccurate, or unvalidated required documentation remains unresolved.

## Required output: `REVIEW_FIX_VERIFICATION.md`

```markdown
# Review Fix Verification

## Verdict
- All valid blocking and non-blocking review findings resolved: Yes/No
- Documentation checkpoints complete: Yes/No
- Ready to finalize review/walkthrough docs: Yes/No

## Finding-by-Finding Verification

| Original Finding | Status | Evidence | Remaining Action |
|---|---|---|---|

## Documentation Checkpoint Verification

## New Issues Introduced

## Remaining Blocking Issues

## Remaining Non-Blocking Issues

## Required Next Action
```

If any issue remains, return to `04_opus_review_branch.md`, the sole producer of `REVIEW_FIX_PROMPT.md`. Report missing or incomplete fix instructions as an upstream failure; do not write a replacement here. Only when all valid blocking and non-blocking findings and documentation checkpoints are resolved, declare readiness for final `REVIEW.md` / `WALKTHROUGH.md` refresh.
