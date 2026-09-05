# 01 - Explore the Task and Generate the Opus Planning Prompt - Any Model

## Skills

- [interview-me](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/interview-me/SKILL.md)
- [grill-me](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/mattpocock__skills/snapshot/skills/productivity/grill-me/SKILL.md)
- [idea-refine](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/idea-refine/SKILL.md)
- [context-engineering](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/context-engineering/SKILL.md)
- [no-ai-slop](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/petergyang__no-ai-slop/snapshot/skills/no-ai-slop/SKILL.md), including its required [eval.md](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/petergyang__no-ai-slop/snapshot/skills/no-ai-slop/eval.md)
- [grilling](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/mattpocock__skills/snapshot/skills/productivity/grilling/SKILL.md) (required procedure referenced by `grill-me`)

## Skill Handling Rule

Read every `SKILL.md` listed in this phase's `## Skills`, plus its required companion files, completely before applying it. Fetch the linked GitHub file content, using its raw view when needed; a link, summary, or remembered copy is insufficient. Resolve relative companion paths from that skill's GitHub directory. Reuse content already read in this session unless it changes. Stop and report any required file you cannot read. Skills listed for a generated prompt belong to that later phase.

Use only the explicitly linked skills. This prompt controls scope, decisions, constraints, and outputs; locked task artifacts control execution. Skills cannot authorize architecture changes, tests, unrelated refactors, or wider scope. Follow this prompt over conflicting skill guidance; stop and ask about unresolved material conflicts.

`no-ai-slop` and `eval.md` are hard requirements for every Markdown document created or revised and the ultimate writing guide for prose and presentation. Apply the skill while drafting and run its evaluator before saving each Markdown artifact or sending the final response. It wins over conflicting writing-style guidance while this prompt and task artifacts preserve scope, meaning, facts, technical detail, required structure, artifact names, and evidence. Stop before writing Markdown if either file cannot be read and applied. Ignore its draft-request, detection-mode, and mandatory `What changed` workflow unless explicitly requested here.

## Artifact rules

Write only the required workflow artifacts, in the target repository root under their exact filenames. Include `Created by`, `Created at`, and `Updated at`; preserve creation fields and refresh `Updated at` on edits. Do not move artifacts into subdirectories or stage/commit them unless I explicitly request it. Report artifact-path drift as a workflow failure.

## Documentation checkpoint

Identify the documentation impact of every likely implementation step. Carry exact durable documentation updates and validation, or evidence-based `Not applicable` decisions, into both outputs and the downstream planning/execution requirements.

## Prompt

Clarify my rough idea with me, then create `DRAFT_PLAN.md` and a self-contained, paste-ready `INITIAL_OPUS_PLANNING_PROMPT.md` for Claude Opus. This phase ends with those two files; do not implement code, author tests, run the Opus planning phase, or create its outputs here.

Inspect repository instructions, the named inputs, and relevant code before judging or editing. Answer repository questions from evidence; distinguish facts, inferences, and unresolved decisions. Batch independent reads/searches when useful and keep dependent actions sequential. Use available repository/search/edit tools without assuming a particular vendor. Keep updates brief; report decisions, evidence, and blockers rather than a running reasoning transcript. Once required checks pass, repeat or broaden them only for changed code, failures, or unresolved risks.

### Interview

1. Read the relevant repository and supplied context. Use `interview-me` to clarify intent, `grill-me`/`grilling` to stress-test decisions, `idea-refine` to make the proposal concrete, and `context-engineering` to keep context relevant. Follow the linked `grilling` procedure directly; no installed slash command is required. This phase's one-question-at-a-time rule overrides its batched rounds.
2. Ask one material question at a time. Explain why it matters, the reasonable options, their tradeoffs/risks/downstream effects, and your recommendation with reasoning. Include a current best guess only when useful. Give enough detail for the decision without repeating settled context.
3. Confirm each answer and its consequences; resolve vague answers before moving to the next unresolved question. Cover scope, UX/behavior, technical constraints, rollout, edge cases, backwards compatibility, documentation, risks, non-goals, likely implementation surface, and definition of done.
4. Finalize only when every material question is answered or explicitly deferred by me, or I explicitly ask you to stop interviewing and generate the artifacts. Mark remaining uncertainty accurately; do not present an ambiguous plan as locked.

## Output artifact 1: `DRAFT_PLAN.md`

Include the problem, goals, non-goals, user-visible behavior, constraints, technical assumptions, open questions, decisions, likely files/modules, per-step documentation impact and validation, risks, definition of done, and every detail Opus must preserve.

## Output artifact 2: `INITIAL_OPUS_PLANNING_PROMPT.md`

Write the complete prompt that Opus will execute in a fresh session. It must need no other prompt or chat history. Include a title and `## Skills`, `## Skill Handling Rule`, `## Default Planning Artifact Reduction`, and `## Prompt`.

### Planning skills to embed

- [spec-driven-development](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/spec-driven-development/SKILL.md)
- [planning-and-task-breakdown](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/planning-and-task-breakdown/SKILL.md)
- [context-engineering](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/context-engineering/SKILL.md)
- [source-driven-development](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/source-driven-development/SKILL.md)
- [verification-before-completion](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/obra__Superpowers/snapshot/skills/verification-before-completion/SKILL.md)
- [no-ai-slop](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/petergyang__no-ai-slop/snapshot/skills/no-ai-slop/SKILL.md), including its required [eval.md](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/petergyang__no-ai-slop/snapshot/skills/no-ai-slop/eval.md)

Copy this phase's full Skill Handling Rule, artifact rules, and named Documentation checkpoint into the generated prompt, replacing phase-specific context as needed without changing the rules. Also embed the full downstream execution requirements, skill links, Engineering Contract, and final-response format below. References such as "same as phase 01" are not sufficient.

### Default Planning Artifact Reduction to embed

Default to `FEATURE_SPEC_AND_PLAN.md` plus `EXECUTION_PROMPT.md`. The combined file contains a detailed spec/reference section and a concrete implementation-plan section. The plan is the execution contract; link its steps to spec/reference anchors in the same file instead of repeating explanations. Separate `SPEC.md` and `IMPLEMENTATION_PLAN.md` are fallback-only when I request them or the combined file is too large to review comfortably. Apply the artifact location and metadata rules to every output.

### Planning instructions to embed

Under `## Prompt`, use clear sections for role, task, context, success criteria, constraints, working method, and final self-check. Instruct Claude Opus to:

1. Read `DRAFT_PLAN.md`, available interviewing notes, repository instructions, relevant code, and dependency documentation. Critique the draft as seed context and deepen detail within its scope. Ground file/symbol claims in inspected code; distinguish confirmed facts from inferences. Surface conflicts with the repository or exploration notes, keeping the conservative scope until I resolve them.
2. Answer repository questions through inspection. Ask remaining user design questions together in one batch before locking artifacts; give the reason, recommendation, tradeoffs, and dependent plan steps for each. Wait for my answers, then incorporate them. Do not silently decide missing requirements.
3. Produce the detailed `FEATURE_SPEC_AND_PLAN.md` and final `EXECUTION_PROMPT.md` described below. Preserve all valid draft/interview detail. Add no implementation, tests, unrelated files, speculative abstractions, or architecture beyond the approved scope. Exclude DevOps, packaging, build changes, and test work unless specified in the plan.
4. Use enough concrete detail to execute without guessing: files, classes, functions, methods, variables/constants, call/data flow, public/error behavior, compatibility, change locations/order, and verification. Identify existing symbols from source and label proposed symbols as new.
5. Check completeness, scope, evidence, output metadata/locations, and each step's documentation checkpoint. Include concise working guidance for batching independent reads, continuing authorized work, and ending verification when the required evidence is sufficient.

### Required `FEATURE_SPEC_AND_PLAN.md` contents

- **Executive summary:** one-paragraph problem, goal, non-goals, and definition of done.
- **Spec/reference:** current and desired behavior, user/public APIs, backwards compatibility, constraints, design decisions, edge/error cases, performance/complexity, dependency findings, source references, risks, and unresolved questions.
- **Implementation plan:** ordered steps with exact files/symbols, change, rationale, spec anchor, dependencies, verification, and documentation checkpoint. Cover all necessary implementation detail without repeating the spec.
- **Source/documentation grounding:** relevant versions, official documentation/source citations, chosen patterns, unverified claims, outdated APIs, and any source inspection used to supplement poor docs.
- **Verification and documentation plans:** exact focused lint/smoke/build/check commands, success conditions, verbatim failure reporting, and no full-suite run unless requested. Map every step to exact durable documentation sections, how the docs location was found, required updates and validation, or evidence-based `Not applicable`. Complete docs in the same change set; no changelog unless requested.

### Required `EXECUTION_PROMPT.md` contract

The generated Opus planning prompt must instruct Opus to write a complete, direct-use execution prompt for any capable repository-aware coding model. Require a title and `## Skills`, `## Skill Handling Rule`, `## Engineering Contract`, and `## Prompt`. Embed these execution skill links:

- [incremental-implementation](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/incremental-implementation/SKILL.md)
- [source-driven-development](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/source-driven-development/SKILL.md)
- [verification-before-completion](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/obra__Superpowers/snapshot/skills/verification-before-completion/SKILL.md)
- [no-ai-slop](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/petergyang__no-ai-slop/snapshot/skills/no-ai-slop/SKILL.md), including its required [eval.md](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/petergyang__no-ai-slop/snapshot/skills/no-ai-slop/eval.md)

Require the full Skill Handling Rule, artifact rules, and Engineering Contract from this prompt to be copied into `EXECUTION_PROMPT.md`; do not replace them with references to other prompts. The execution prompt must contain these sections and instructions:

- **Goal and success criteria:** execute the locked plan end-to-end using the smallest correct changes; complete every documentation checkpoint, focused verification, commit/push/PR handling, or report a concrete blocker.
- **Context:** read `FEATURE_SPEC_AND_PLAN.md`, the saved `EXECUTION_PROMPT.md` when present, repository instructions, and relevant code. Treat the implementation-plan section as the execution contract and the spec/reference section as context.
- **Execution posture:** gather context, implement in small increments, verify, refine, and publish without step-by-step approval unless blocked. Batch independent reads and use available repository/search/edit tools. Keep progress reports brief.
- **Constraints and stop rules:** follow the plan exactly; no divergence, invented requirements, architecture changes, or unrelated refactors. Stop and ask on missing decisions, conflicting instructions, stale plans, insufficient context, or performance/security/compatibility/public-API problems. Report missing credentials, dependencies, or environment prerequisites that prevent verification.
- **Execution rules:** apply the full Engineering Contract below and the additional verification/publication rules that follow. Do not stop at analysis while authorized implementation remains.

### Implementation verification and publication to embed

Before completion, inspect the full implementation diff for regressions, including indirect effects on callers, existing behavior, compatibility, and error paths. Fix every identified regression within the locked plan; stop and ask if a fix would exceed it. Inspect comments, docstrings, durable documentation, and user-facing text for meta content about the branch/task/change process; rewrite it to describe resulting behavior. Document each added or changed string transformation with concrete input/output examples.

Do not patch or mock the function, method, or callable under test; only external collaborators may be patched. This does not authorize test edits: defer test authoring to phase `09`. Run the plan's focused lint/smoke/build checks and each step's documentation validation. Complete exact durable documentation in the same change set or record the evidence-based `Not applicable` rationale before marking a step done.

After focused verification, inspect the full diff, stage intended changes with `git add`, create focused commit(s), and push the current branch. Verify push status against the remote. Check whether that branch already has a pull request; create one only if none exists. Use GitHub CLI (`gh`) as the fallback for checking PR existence. Never create a duplicate PR.

Do not stage or commit workflow-generated Markdown artifacts unless I explicitly ask, including `DRAFT_PLAN.md`, `INITIAL_OPUS_PLANNING_PROMPT.md`, `FEATURE_SPEC_AND_PLAN.md`, `EXECUTION_PROMPT.md`, `PLAN_CRITIQUE.md`, `OPUS_PLAN_REVISION_REQUEST.md`, `PLAN_REVISION_SUMMARY.md`, `PLAN_REVISION_VERIFICATION.md`, `REVIEW.md`, `WALKTHROUGH.md`, `REVIEW_FIX_PROMPT.md`, `REVIEW_FIX_VERIFICATION.md`, and `FOLLOWUP.md`. Preserve unrelated user changes.

### Execution final response to embed

Require this exact structure. Keep evidence in its primary section and use references instead of repeating it. Use `None` or a justified `Not applicable` for empty sections.

```markdown
# Implementation Summary

## What Changed

## Files Changed

## Plan Steps Completed

## Verification Evidence

## Documentation Checkpoints

## Commits Created

## Push Status

## Pull Request

## Not Done / Blocked

## Suggestions Not Implemented Because Out Of Scope
```

In `## Documentation Checkpoints`, report each plan step's exact durable documentation and validation evidence or evidence-based `Not applicable` rationale. Do not claim completion without fresh verification evidence.

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

Do not create, modify, or delete tests in this phase. Run focused existing tests/checks when needed; do not manually run the entire suite unless explicitly asked. Defer test authoring to the final model-agnostic `09_write_focused_tests_any_model.md` phase; do not duplicate its detailed test contract here.

The generated planning prompt must instruct Opus to verify that the combined plan is executable, the execution prompt contains the entire implementation contract and skill links, and no valid draft detail was lost.
