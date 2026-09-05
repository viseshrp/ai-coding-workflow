# 04 - Opus Reviews Implemented Branch

## Skills

- [code-review-and-quality](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/code-review-and-quality/SKILL.md)
- [code-simplification](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/code-simplification/SKILL.md)
- [source-driven-development](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/source-driven-development/SKILL.md)
- [verification-before-completion](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/obra__Superpowers/snapshot/skills/verification-before-completion/SKILL.md)
- [no-ai-slop](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/petergyang__no-ai-slop/snapshot/skills/no-ai-slop/SKILL.md), including its required [eval.md](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/petergyang__no-ai-slop/snapshot/skills/no-ai-slop/eval.md)

## Skill Handling Rule

Read every `SKILL.md` listed in this phase's `## Skills`, plus its required companion files, completely before applying it. Fetch the linked GitHub file content, using its raw view when needed; a link, summary, or remembered copy is insufficient. Resolve relative companion paths from that skill's GitHub directory. Reuse content already read in this session unless it changes. Stop and report any required file you cannot read. Skills listed for a generated prompt belong to that later phase.

Use only the explicitly linked skills. This prompt controls scope, decisions, constraints, and outputs; available locked task artifacts are authoritative context. Missing prior planning or execution artifacts do not block this review or its generated fix pass. Skills cannot authorize architecture changes, tests, unrelated refactors, or wider scope. Follow this prompt over conflicting skill guidance; stop and ask about unresolved material conflicts.

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

Do not create, modify, or delete tests. Run focused existing tests/checks to substantiate findings, never the full suite unless asked. Apply the review rules below; defer test authoring to `09_write_focused_tests_any_model.md`.

## Artifact rules

Write only the required workflow artifacts, in the target repository root under their exact filenames. Include `Created by`, `Created at`, and `Updated at`; preserve creation fields and refresh `Updated at` on edits. Do not move artifacts into subdirectories or stage/commit them unless I explicitly request it. Report artifact-path drift as a workflow failure.

## Prompt

As Claude Opus, review all changes on the current branch against `main` and any available locked planning artifacts. Write only `REVIEW.md`, `WALKTHROUGH.md`, and `REVIEW_FIX_PROMPT.md`; do not implement proposed changes during this review.

Read the branch diff, affected code/callers, public interfaces, configuration, durable documentation, and existing tests. Also read `FEATURE_SPEC_AND_PLAN.md`, `SPEC.md`, `IMPLEMENTATION_PLAN.md`, root `PLAN*.md` files, and `EXECUTION_PROMPT.md` when present. These artifacts are optional: their absence must not block standalone review, become a finding, or trigger a request to recreate them.

Inspect repository instructions, the named inputs, and relevant code before judging or editing. Answer repository questions from evidence; distinguish facts, inferences, and unresolved decisions. Batch independent reads/searches when useful and keep dependent actions sequential. Use available repository/search/edit tools without assuming a particular vendor. Keep updates brief; report decisions, evidence, and blockers rather than a running reasoning transcript. Once required checks pass, repeat or broaden them only for changed code, failures, or unresolved risks.

Record the branch/base/head used for comparison. Distinguish branch changes from changes made only on `main`. With a plan, assess full compliance; otherwise use the branch diff as the scope boundary and existing behavior, APIs, docs, configuration, and tests as evidence. Do not invent undocumented intent; label intent-dependent conclusions as open questions.

## Review dimensions

Apply every Engineering Contract requirement to the diff. Backwards compatibility has priority. In particular:

- Trace regressions through changed code and indirect effects on callers, existing behavior, compatibility, and error paths. Check public API usability, naming, exception translation, performance/complexity, Linux/Windows support, justified dependencies, and version-correct APIs.
- Assess readability, idiomatic language/standard-library use, proportionate accurate types, reuse/DRY, separation of concerns, assumptions, and production assertions. Flag unnecessary edits to surrounding code and excess change scope.
- Check non-obvious code comments, stale/bloated comments, and concrete input/output examples for every added or changed string transformation. Flag comments, docstrings, docs, or user-facing text about the task/branch/implementation process instead of resulting behavior.
- Record a documentation-checkpoint result for every material behavior: exact durable documentation and validation evidence, or evidence-based `Not applicable`. Missing, inaccurate, or unvalidated required docs are valid findings.
- Ground each issue in exact diff/code/contract evidence. Separate confirmed defects and plan divergence from preferences, open questions, and optional suggestions. A preference alone is not a blocker.

### Python

Apply the Engineering Contract's Python typing requirements to every added or changed symbol. Missing or inaccurate required parameter/return/state/attribute hints are blocking findings. Exempt `self`, `cls`, and trivial immutable module constants unless the configured checker requires an annotation. Flag unnecessary local/advanced/type-only annotations and non-idiomatic Python or standard-library use.

## Test review rules

Review existing or changed tests without authoring them:

- Require the fewest tests for distinct behavior and material regression risk, one behavior per test, and small linear functions/fixtures/helpers. Flag duplicate, transient, temporary-hack, and coverage-only tests.
- Prefer repository fixtures, native test-framework APIs, configuration, and installed extensions over hand-rolled infrastructure.
- Never accept patching or mocking the function/method/callable under test. Limit mocks to impractical external collaborators; flag internal call choreography and implementation-detail assertions.
- Check deterministic isolation. Flag mutated global state, private helpers/constants, incidental error wording, non-contract layout assumptions, real time/network dependencies, and expected values that mirror production logic.
- Assess at least 85% coverage for new or changed lines using existing tooling and focused evidence. Report missing evidence explicitly; test authoring remains in phase `09`.

### Python / pytest

For pytest tests, prefer existing fixtures and native APIs: `monkeypatch`, `tmp_path`, capture fixtures, `pytest.raises`, `pytest.warns`, parametrization, and an installed mock fixture when appropriate. Classify brittleness concerns as real flake risks, acceptable contract tests, or maintainability concerns, with a behavior-level alternative when practical.

## Required output 1: `REVIEW.md`

Use the structure below. Give findings stable IDs, exact file/line or contract evidence, impact, and required action. Categorize every valid finding under `Blocking Issues` or `Non-Blocking Issues`; both categories require fixes. Use `Suggestions` only for optional improvements. Place related suggestions below their finding and cross-reference them instead of repeating the text across sections. Use `None` or justified `Not applicable` for empty sections.

```markdown
# Review

## Verdict

## Review Basis

## Plan Compliance

## Blocking Issues

## Non-Blocking Issues

## Backwards Compatibility

## Public API Review

## Performance / Complexity Review

## Source Documentation Grounding

## Code Quality / Readability

## Python Typing Review

## Reuse / DRY / Duplication

## Assumptions Surfaced

## Assert Usage

## Cross-Platform Review

## Test Review

## Documentation Review

## Suggestions
```

In `Review Basis`, record the comparison, inspected evidence, and available artifacts; state when review is standalone. With no plan, write `Not assessed - no planning artifacts were provided.` under `Plan Compliance`. In `Documentation Review`, record each material behavior's documentation-checkpoint evidence or gap.

## Required output 2: `WALKTHROUGH.md`

Explain every changed line in context for a beginner reviewing from scratch. Put an English explanation next to each line of code, including changed/deleted code and the context needed to understand it. Use small per-file tables such as `Line | Code | Explanation`, with escaped Markdown where needed. The walkthrough must support review without opening the source; do not replace line-by-line explanations with a summary. Keep it readable and proportionate without omitting lines.

## Required output 3: `REVIEW_FIX_PROMPT.md`

Create the complete, paste-ready prompt for any capable repository-aware coding model to fix every valid blocking and non-blocking finding, including minor issues. Phase `04` is its sole producer; verification returns here for another fix request. Do not produce a wrapper, partial checklist, or prompt that relies on another prompt or hidden chat history.

Include a title and `## Skills`, `## Skill Handling Rule`, `## Engineering Contract`, and `## Prompt`. Embed these skills:

- [incremental-implementation](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/incremental-implementation/SKILL.md)
- [source-driven-development](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/source-driven-development/SKILL.md)
- [verification-before-completion](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/obra__Superpowers/snapshot/skills/verification-before-completion/SKILL.md)
- [receiving-code-review](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/obra__Superpowers/snapshot/skills/receiving-code-review/SKILL.md)
- [no-ai-slop](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/petergyang__no-ai-slop/snapshot/skills/no-ai-slop/SKILL.md), including its required [eval.md](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/petergyang__no-ai-slop/snapshot/skills/no-ai-slop/eval.md)

Copy the full Skill Handling Rule, artifact rules, and Engineering Contract into the generated fix prompt. Include the no-test-authoring boundary without requiring this review prompt's test-review section. Preserve the optional-input rule: prior planning/execution artifacts are authoritative when present and unnecessary when absent.

Under `## Prompt`, include goal, success criteria, context, execution posture, constraints, per-review-item process, focused verification, and required final response. Instruct the fix model to:

1. Read `REVIEW.md`, `WALKTHROUGH.md`, the current diff against `main`, repository instructions, and affected code. Read `FEATURE_SPEC_AND_PLAN.md` and `EXECUTION_PROMPT.md` when present; do not request or recreate missing planning artifacts.
2. Verify every finding against actual code before editing. Fix all valid `Blocking Issues` and `Non-Blocking Issues`; optional `Suggestions` require explicit approval. Stop and ask about a wrong/stale finding, conflict, missing design decision, ambiguity, or inadequate context.
3. Keep fixes within the review and branch scope and any available original plan. Preserve backwards compatibility; make no architecture changes, unrelated refactors, or tests. Continue through implementation and focused verification without step-by-step approval unless blocked.
4. Complete each item's documentation checkpoint before checking it off: update and validate exact durable documentation in the same change set or record evidence-based `Not applicable`. Treat valid documentation gaps as required fixes; ask if resolving one would exceed scope.
5. Run focused checks relevant to the fixes, including documentation validation. Inspect the final diff for regressions and the Engineering Contract. Check off verified fixes when a checklist exists and complete publication using the rules below.

### Publication rules to embed

After focused verification, inspect the full diff, stage intended changes with `git add`, create focused commit(s), and push the current branch. Verify push status against the remote. Check whether that branch already has a pull request; create one only if none exists. Use GitHub CLI (`gh`) as the fallback for checking PR existence. Never create a duplicate PR.

Do not stage or commit workflow-generated Markdown artifacts unless I explicitly ask, including `DRAFT_PLAN.md`, `INITIAL_OPUS_PLANNING_PROMPT.md`, `FEATURE_SPEC_AND_PLAN.md`, `EXECUTION_PROMPT.md`, `PLAN_CRITIQUE.md`, `OPUS_PLAN_REVISION_REQUEST.md`, `PLAN_REVISION_SUMMARY.md`, `PLAN_REVISION_VERIFICATION.md`, `REVIEW.md`, `WALKTHROUGH.md`, `REVIEW_FIX_PROMPT.md`, `REVIEW_FIX_VERIFICATION.md`, and `FOLLOWUP.md`. Preserve unrelated user changes.

### Fix-pass final response to embed

```markdown
# Review Fix Summary

## Review Items Fixed

## Review Items Not Fixed And Why

## Files Changed

## Verification Evidence

## Documentation Checkpoints

## Commits Created

## Push Status

## Pull Request

## Remaining Questions / Blockers
```

Under `Documentation Checkpoints`, report each review item's exact durable documentation and validation evidence or evidence-based `Not applicable` rationale. Require fresh verification evidence before claiming completion.
