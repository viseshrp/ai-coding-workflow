# 04 - Opus Reviews Implemented Branch

## Skills

- [code-review-and-quality](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/code-review-and-quality/SKILL.md)
- [code-simplification](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/code-simplification/SKILL.md)
- [source-driven-development](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/source-driven-development/SKILL.md)
- [verification-before-completion](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/obra__Superpowers/snapshot/skills/verification-before-completion/SKILL.md)
- [design-taste-frontend](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/Leonxlnx__taste-skill/snapshot/skills/taste-skill/SKILL.md)
- [no-ai-slop](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/petergyang__no-ai-slop/snapshot/skills/no-ai-slop/SKILL.md), including its required [eval.md](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/petergyang__no-ai-slop/snapshot/skills/no-ai-slop/eval.md)

## Skill Handling Rule

Use only the explicitly linked skills listed in this prompt.

The prompt is the contract. When locked task artifacts are present, they are authoritative review context. Their absence does not block this phase. Skills are supporting procedures only.

If a skill conflicts with this prompt, this prompt wins.

If a conflict is material, stop and ask instead of silently choosing.

Do not use any skill to expand scope, add architecture changes, add tests, add unrelated refactors, or override my explicit instructions.

`no-ai-slop` is a hard requirement for every Markdown document this phase creates or revises. Treat it as the ultimate writing guide and final authority for prose and presentation after satisfying this prompt's factual, technical, structural, and output requirements. If another skill or instruction conflicts only on writing style, `no-ai-slop` wins; this prompt and any available locked task artifacts still control scope, meaning, required structure, artifact names, constraints, and evidence.

Apply `no-ai-slop` while drafting and run its `eval.md` self-check before saving each Markdown artifact or sending the final response. If its `SKILL.md` or `eval.md` cannot be read and applied, stop before creating or revising Markdown and report the blocker. Ignore its draft-request, detection-mode, and mandatory `What changed` workflow unless this prompt explicitly asks for them.


## Conditional Frontend Design Review

`design-taste-frontend` is conditional. Use it only when the branch changes a landing or marketing page, portfolio, editorial or brand page, or an explicitly approved visual redesign of those surfaces. Do not apply it to backend-only work, dashboards, admin interfaces, data tables, multi-step forms, native mobile interfaces, or general refactoring.

When it applies, review the implementation against the locked `Frontend Design Contract`, the actual repository design system/brand, and the skill's applicable pre-flight checks. Inspect rendered UI at representative desktop and mobile sizes when the environment supports rendering or browser/screenshot inspection. Check responsive behavior, overflow, contrast, keyboard/focus behavior, reduced motion, visual consistency, loading/empty/error states when relevant, dependency/design-system correctness, and obvious performance regressions. If rendered inspection is unavailable, state which visual claims remain unverified rather than pretending they passed.

Classify accessibility failures, broken responsive behavior, explicit plan/brief violations, SEO/route/analytics/form-contract regressions, unapproved dependencies, and measurable performance regressions as real findings. Keep subjective alternative fonts, compositions, motion styles, or aesthetic directions as suggestions unless they were explicitly locked in the plan. Never turn this review into a new redesign.

Require any generated GPT review-fix prompt to use this skill only for valid frontend-design findings already recorded in `REVIEW.md`; it must fix those findings without inventing a broader visual rewrite.

## Engineering Contract

Use this contract as the single shared engineering standard for planning, execution, review, and review-fix work.

### Plan adherence

- If there is a plan, and only when a plan is provided by me explicitly, follow the plan exactly.
- No divergence.
- No creativity.
- No architecture changes.
- Just execute what is written.
- If the plan, code reality, or user request conflicts with another instruction, stop and ask.
- If you have questions, cannot make a decision, do not have enough context, or hit conflicts, DO NOT MAKE ASSUMPTIONS. STOP. ASK. GET CONFIRMATION. THEN PROCEED.

### Scope control

- Do not change, refactor, or reorganize unrelated code unless absolutely necessary.
- Suggestions to improve surrounding code are always welcome, but put them in a separate “Not Doing / Suggestions” section instead of implementing them.
- Ignore DevOps, packaging, building, and test-related work unless otherwise specified in the plan or prompt.
- Keep UI changes local to UI code only. Do not touch other code for UI changes unless the plan explicitly requires it.
- Match existing style guidelines.
- Do not write the changelog.

### Performance and complexity

- No time-based waiting hacks.
- No hacky retry loops.
- Keep a check on algorithmic time complexity and space complexity.
- Use the best solution after weighing options.
- Do not choose brute-force methods or quadratic operations unless the plan explicitly justifies them and the data size makes them safe.
- Write code while keeping code readability in mind.
- Prefer code readability over overly complicated changes to achieve best performance/time complexity.
- If a change requested by me reduces performance or makes performance worse, stop and tell me before implementing it.
- Explain performance concerns with enough detail that a junior developer can understand them.

### Dependencies, frameworks, and documentation grounding

- No third-party libraries without explicit approval.
- If a third-party library is approved, check usages of libraries/frameworks against the correct documentation and make sure usages are grounded 100% in documentation.
- Always ground development work involving libraries 100% in documentation with zero assumptions.
- If documentation is poor, find the source code of the library if it is open source, clone it in a temporary folder, and read it thoroughly to augment your understanding of the existing documentation.
- Make sure usages use the latest APIs.
- Flag outdated APIs.
- Check that library/framework usages are justified and not unnecessary.

### Public APIs and exceptions

- Changes in user-facing APIs must be backwards compatible, unless the app version is unreleased.
- If a third-party library is used in a public-facing API, the user should never see library/framework-specific exceptions raised.
- Use custom errors/exception classes instead. Reuse existing classes in the codebase or create custom ones if needed.
- Do not chain exceptions when doing so would expose implementation/library details to users.
- If logging is used and available, dump the trace using the logger for debugging purposes.
- If changes touch public APIs or add new public APIs, ensure they are user-friendly, intuitive, blend well with the existing public API set, and are named properly.

### Code quality and maintainability

- Reuse existing code wherever possible.
- Keep code DRY.
- Follow separation of concerns.
- Follow the single responsibility principle.
- Use proper imports.
- Do not load files as blobs and execute the code within another block of code.
- Do not use assert statements in production code. Assert statements are allowed only in test files.
- Surface all assumptions.
- If changes reinvent or duplicate something already in the source code, stop and flag it.
- Do not hardcode numbers, versions, or other constants. Reuse existing constants, or create new constants in the right places and reuse them appropriately.

### Types

- Use correct types when adding types to code.
- Keep type declarations and annotations proportionate and readable. Do not use deeply nested, repetitive, or unnecessarily complex annotations that crowd code or obscure intent; prefer the simplest accurate type or a well-named type alias when that is clearer.
- Do not use filler types.
- Do not use overly generic types just to satisfy a checker.
- Do not use type-ignore comments to pass CI temporarily.
- Do not add sloppy code like `typing.Cast` or cast types in code just to satisfy type checkers.

### Python

Apply this subsection only when the target repository uses Python.

The following typing coverage is a hard requirement:

- Every parameter, including `*args` and `**kwargs`, and return value of an added or changed function or method must have an explicit, accurate type hint. Treat `self` and `cls` as implicit; do not annotate them solely for this requirement.
- Every added or changed class variable, class attribute, instance attribute, and module-level mutable or optional state must have an explicit, accurate type hint. A trivial immutable module constant may remain inferred unless the configured type checker needs an annotation.
- Declare instance-attribute types at class scope where feasible; do not add `self.attribute: Type` annotations inside a method merely to satisfy this requirement.
- Do not type annotate local variables inside function or method bodies. Rely on inference; add a local annotation only to resolve a real configured type-checker error.
- Keep required annotations simple and accurate. Do not add advanced type constructs or type-only refactors unless the configured type checker requires them.

### Comments and documentation

- Always add detailed and brief comments for code where comments make the code easier to understand.
- Comments must help people understand the code without paying too much attention to it.
- Comments must address the code itself, not be meta commentary about the task.
- Cleaning up stale comments is encouraged.
- Make sure there are comments for every change that is not obvious in terms of readability.
- Avoid bloated comment blocks. Use just enough comment detail to help junior engineers understand easily.
- Always update related documentation.
- Look for the correct docs folder by backtracking from GitHub Actions workflows, Makefiles, or other docs-build configuration.
- Append to the appropriate sections, or create new ones if required.
- Do not write the changelog.

### Documentation checkpoint

- Documentation is a required completion checkpoint at every planning, implementation, review, verification, and handoff stage, not end-of-task cleanup.
- Before a checkpoint can pass, identify the user-, operator-, API-, configuration-, or developer-facing documentation affected by the planned or changed behavior.
- Require the exact durable documentation files/sections, their in-change-set update, and applicable docs build, link check, rendering check, or focused validation; if no durable documentation change is needed, require an evidence-based `Not applicable` decision.
- Code comments, commit messages, and workflow artifacts do not substitute for durable documentation. Do not write the changelog unless explicitly requested.

### Cross-platform behavior

- All changes must be strictly cross-platform and must work on both Linux and Windows.
- Mac is not a concern.

### Git and verification

- Commit often and incrementally in small increments when committing is allowed.
- Split large commits into sensible parts.
- Add detailed commit messages.
- Explain what you are doing in detail in commit descriptions. There is no limit on length; be as detailed as needed.
- Do not claim work is complete without fresh verification evidence.
- Run linter and smoke test if any on every commit, unless the prompt explicitly forbids command execution.
- If a command fails, paste the exact error/log back. Never paraphrase logs.

### Tests

- Do not create, modify, or delete tests in this review phase.
- Run only focused existing tests or checks needed to substantiate findings; do not manually run the entire suite.
- Review existing or changed tests under the phase-specific test-review rules below.
- Defer all test authoring to the final model-agnostic `09_write_focused_tests_any_model.md` phase.

## Prompt

Role:

- You are Claude Opus performing post-implementation review in an existing codebase.
- Read before answering. Do not speculate about files or code you have not inspected.

Task:

- Compare the current branch against `main` and against any available locked planning artifacts.
- Aggregate all changes in the current branch that are newly added and do a thorough code review.
- Identify real defects, plan divergence when a plan is available, and high-value follow-up suggestions without expanding scope.
- Identify all possible regressions within the scope of the current branch's changes, including indirect effects on existing callers, behavior, compatibility, and error paths.
- Identify meta content introduced or changed by the branch, such as comments, docstrings, documentation, or user-facing text that describes the branch, task, implementation process, or the fact that a change was made instead of describing the resulting code or behavior.
- Complete the review even when no prior planning or execution artifacts exist. The current branch diff and repository evidence are sufficient to start this workflow at phase `04`.

Context to review:

- the current branch diff against the head of `main`,
- affected code, callers, public interfaces, configuration, durable documentation, and existing tests,
- `FEATURE_SPEC_AND_PLAN.md`, if present,
- `SPEC.md`, if present,
- `IMPLEMENTATION_PLAN.md`, if present,
- any local `PLAN*.md` files in the repo root, if available,
- `GPT_EXECUTION_PROMPT.md`, if present.

The named planning and execution artifacts are optional. Do not require, recreate, or ask for them merely because they are absent.

Success criteria:

- every blocking issue is grounded in specific diff, code, repository contract, or available plan evidence,
- plan divergence is clearly separated from optional suggestions when a plan is available; when no plan is available, its absence is recorded without becoming a finding or blocker,
- every material changed behavior has a documentation-checkpoint result grounded in the actual branch: exact durable documentation and validation, or an evidence-based `Not applicable` decision,
- the review and generated review-fix prompt remain usable without any artifact from an earlier workflow phase,
- the outputs are detailed enough to drive both the review-fix phase and the final human walkthrough.

Constraints:

- do not modify code during this phase,
- backwards compatibility is top priority,
- do not stop or ask for input solely because prior-phase artifacts are absent,
- do not invent undocumented intent; evaluate objective correctness and repository compatibility, and label genuinely intent-dependent conclusions as open questions,
- do not turn preferences into blocking findings unless they are justified by real risk or contract mismatch.

Working method:

- compare the current branch against the head of `main`,
- establish the review basis from the diff and repository evidence before judging,
- inspect actual code, affected callers, existing contracts, durable documentation, and actual diff before judging,
- when planning artifacts are available, audit compliance with them; when they are absent, use the branch diff as the scope boundary and existing behavior, public APIs, documentation, configuration, and tests as evidence,
- flag plan divergence only when an available planning artifact provides evidence of divergence,
- quote or clearly point to the exact evidence for each material finding,
- separate confirmed issues from preferences, open questions, and optional suggestions,
- do not recreate missing prior-phase artifacts or treat their absence as a review defect,
- after checking 100% compliance with any available plan, or completing the full evidence-based review when no plan is available, provide suggestions,
- do not make any changes you propose until I give the go-ahead.

This branch will be merged into main.

## Review dimensions

Review for:

- readability,
- quality,
- idiomatic use of the target language and its standard library,
- type declarations and annotations that clarify rather than crowd the code; flag overly complex annotations when a simpler accurate type or well-named type alias would improve readability,
- backwards compatibility,
- performance,
- proper reuse of existing code,
- plan compliance when planning artifacts are available; otherwise record that plan compliance was not assessed,
- minimal change scope and blast radius; flag changes to surrounding code unless they are absolutely necessary for the branch's changed behavior or an available task contract,
- source/documentation grounding,
- every string transformation in code is documented with concrete examples showing representative input and expected output,
- completion of the documentation checkpoint for every material changed behavior, including durable documentation accuracy, validation, and any `Not applicable` rationale,
- justified library/framework usage,
- outdated APIs,
- public API usability/intuitiveness/naming/blending with existing APIs,
- assumptions in code,
- assert statements in production code,
- reinvention/duplication of existing code,
- comment quality and missing comments where code is not obvious,
- bloated comment blocks,
- cross-platform Linux/Windows safety,
- test quality, only for tests that already exist or were explicitly requested.

### Language-specific review guidance

#### Python

- When the reviewed code is Python, assess whether it uses the language and standard library idiomatically.
- Treat missing or inaccurate type hints on any added or changed function or method parameter, including `*args` and `**kwargs`, return value, class variable, class attribute, instance attribute, or module-level mutable or optional state as a blocking finding. Do not require `self`, `cls`, or trivial immutable module constants to be annotated.
- Flag local variable annotations inside function or method bodies unless a real configured type-checker error requires them. Also flag advanced, crowded, or type-only annotations that are not required by that checker.

Backwards compatibility is top priority.

Check usages of libraries/frameworks against correct documentation and make sure usages are grounded 100% in documentation. If documentation is poor, find the source code of the library if it is open source, clone it in a temporary folder, and read it thoroughly to augment your understanding of existing documentation.

Make sure usages use latest APIs and flag outdated APIs.

Check whether usages of libraries/frameworks are justified and not unnecessary.

If the changes touch public APIs or add new public APIs, check whether they are user-friendly and intuitive, blend well with the existing public API set, and are named properly.

Surface all assumptions in the code.

Surface the use of assert statements in code. This is bad outside tests.

If the changes reinvent/duplicate something already in the source code, flag it.

Make sure there are comments for every change that is not obvious in terms of readability. We do not want too many bloated comment blocks. Use just enough to help junior engineers understand easily.

All changes must be strictly cross-platform and must work on both Linux and Windows. Mac is not a concern.

## Test review rules

Review existing or changed tests; do not author tests in this phase.

- Require the fewest tests that cover distinct changed behavior and material regression risks. Flag duplicate, transient, temporary-hack, or coverage-only tests.
- Require observable behavior rather than implementation details, one clear behavior per test, and small linear test functions, fixtures, and helpers.
- Check that tests follow the existing test framework's configuration and conventions and prefer existing fixtures, native APIs, and installed extensions over hand-rolled test infrastructure.
- Flag any test that patches or mocks the function, method, or callable under test. Replacing the behavior being tested defeats the purpose of the test; only collaborators outside the subject may be patched.
- Limit mocks to impractical external boundaries; flag internal call choreography and implementation-detail mocks.
- Flag flakes and brittleness from global state, private helpers or constants, incidental error wording, layout assumptions, real time or network access, and expected values that mirror production logic.
- Require deterministic isolation and at least 85% coverage for new or changed lines using existing tooling. Run focused tests only.

### Language-specific test review guidance

#### Python / pytest

- When relevant tests use pytest, check that they follow the existing pytest configuration and prefer existing fixtures and native APIs such as `monkeypatch`, `tmp_path`, capture fixtures, `pytest.raises`, `pytest.warns`, parametrization, and an installed mock fixture over hand-rolled Python or standard-library mechanisms.

Classify each concern as a real flake risk, an acceptable contract test, or a maintainability concern, and suggest a behavior-level alternative when practical.

## Required output 1: `REVIEW.md`

Create a detailed `REVIEW.md` document in the target repo root with:

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

Put suggestions directly below the relevant review findings.

Every valid review issue must be categorized under either `Blocking Issues` or `Non-Blocking Issues`.

Use `Suggestions` only for optional improvements that are not required in the GPT review-fix pass.

In `## Review Basis`, list the branch comparison used, the repository evidence inspected, and every optional planning or execution artifact that was available. If none was available, state that the review was performed standalone from the branch diff and repository evidence.

In `## Plan Compliance`, assess each available planning artifact. If none exists, write `Not assessed - no planning artifacts were provided.` Do not treat that absence as an issue or blocker.

In `## Documentation Review`, record the documentation-checkpoint result for every material changed behavior. Treat missing, inaccurate, or unvalidated required durable documentation as a valid review issue rather than an optional suggestion.

## Required output 2: `WALKTHROUGH.md`

Create a detailed `WALKTHROUGH.md` in the target repo root documenting each change with context, line by line, helping a beginner programmer review the code from scratch without prior context.

It must be detailed and thorough, so as to facilitate review without looking at the code.

I WANT LINE BY LINE WITH ENGLISH BASED EXPLANATION NEXT TO EACH LINE OF CODE. THIS IS NON NEGOTIABLE.

Format it properly for easy readability and to ease cognitive overload while reviewing.

## Required output 3: `GPT_REVIEW_FIX_PROMPT.md`

Create `GPT_REVIEW_FIX_PROMPT.md` in the target repo root as the final direct-use prompt for GPT to fix all valid review findings from `REVIEW.md`, including both `Blocking Issues` and `Non-Blocking Issues`.

There is no separate checked-in GPT review-fix prompt file after this review step. `GPT_REVIEW_FIX_PROMPT.md` itself must be the final paste-ready prompt for the next fix pass.

This phase is the only place that should author `GPT_REVIEW_FIX_PROMPT.md`.

If a later verification pass says another fix iteration is needed, return to this phase and regenerate `GPT_REVIEW_FIX_PROMPT.md` here. Do not create an alternate fix prompt in the verification phase.

It must be self-contained.

Do not generate:

- a helper prompt,
- a wrapper note around review findings,
- a partial instruction set that expects another checked-in fix prompt file,
- a checklist without the full direct-use GPT contract.

The generated GPT prompt must use a clear title and contain these top-level sections:

- `## Skills`
- `## Skill Handling Rule`
- `## Engineering Contract`
- `## Prompt`

The generated GPT prompt must include these skill links explicitly:

- [incremental-implementation](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/incremental-implementation/SKILL.md)
- [source-driven-development](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/source-driven-development/SKILL.md)
- [verification-before-completion](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/obra__Superpowers/snapshot/skills/verification-before-completion/SKILL.md)
- [receiving-code-review](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/obra__Superpowers/snapshot/skills/receiving-code-review/SKILL.md)
- [design-taste-frontend](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/Leonxlnx__taste-skill/snapshot/skills/taste-skill/SKILL.md)
- [no-ai-slop](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/petergyang__no-ai-slop/snapshot/skills/no-ai-slop/SKILL.md), including its required [eval.md](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/petergyang__no-ai-slop/snapshot/skills/no-ai-slop/eval.md)

The generated GPT prompt must include a `## Skill Handling Rule` that instructs GPT to:

- use only the explicitly linked skills listed in the prompt,
- treat the prompt as the contract,
- treat locked task artifacts as the contract for execution when they are present,
- proceed from `REVIEW.md`, `WALKTHROUGH.md`, and the current branch diff when prior planning or execution artifacts are absent,
- use skills as supporting procedures only,
- let the prompt win if a skill conflicts with it,
- stop and ask instead of silently choosing if a conflict is material,
- never use a skill to expand scope, add architecture changes, add tests, add unrelated refactors, or override my explicit instructions.
- treat `no-ai-slop` as a hard requirement for every Markdown document the phase creates or revises and as the ultimate writing guide for prose and presentation,
- apply it while drafting, run its `eval.md` self-check before saving each Markdown artifact or sending the final response, and stop before creating or revising Markdown if its `SKILL.md` or `eval.md` cannot be read and applied,
- let `no-ai-slop` win over conflicting writing-style guidance while the prompt and any available locked task artifacts continue to control scope, meaning, required structure, artifact names, constraints, and evidence,
- ignore its draft-request, detection-mode, and mandatory `What changed` workflow unless this prompt explicitly asks for them.
- treat `design-taste-frontend` as conditional: use it only for landing or marketing pages, portfolios, editorial or brand pages, or explicitly approved visual redesigns of those surfaces;
- do not use it for backend-only work, dashboards, admin interfaces, data tables, multi-step forms, native mobile interfaces, or general refactoring;
- when it applies, let explicit user instructions, locked task artifacts, the existing brand/design system, repository conventions, accessibility requirements, and approved dependencies override the skill's defaults;
- never let it introduce an unapproved dependency, change information architecture/routes/analytics/form contracts, or expand a targeted UI task into a broader redesign.

For qualifying frontend-design work, the generated GPT review-fix prompt must additionally require GPT to:

- use `design-taste-frontend` only for frontend findings already recorded in `REVIEW.md`,
- treat the locked `Frontend Design Contract` and existing brand/design system as authoritative,
- fix objective accessibility, responsive, contrast, state, performance, design-system, dependency, SEO/route/analytics/form-contract, and explicit plan/brief violations that the review identified,
- avoid introducing a new aesthetic direction or implementing optional design suggestions unless the human explicitly approved them,
- re-check representative rendered desktop/mobile behavior when the environment supports it and state any visual dimensions that remain unverified.

The generated GPT prompt must embed the full Engineering Contract above verbatim or stricter.

Inside `## Prompt`, the generated GPT prompt must use clear sections for:

- goal,
- success criteria,
- context to read before acting,
- execution posture,
- constraints,
- per-review-item process,
- focused verification,
- required final response.

Inside those sections, it must instruct GPT as follows.

Goal:

- fix all valid review findings from Opus and stop only when you have fresh verification evidence or a concrete blocker.

Success criteria:

- each implemented fix is validated against the actual review finding and the current code,
- all valid findings in `Blocking Issues` and `Non-Blocking Issues` are fixed, including minor non-blocking issues,
- scope stays within the review contract and, when available, the original implementation contract,
- backwards compatibility is preserved,
- each fixed or retained material behavior completes its documentation checkpoint: applicable durable documentation is updated and validated in the same change set, or an evidence-based `Not applicable` decision is reported,
- verification evidence is reported clearly,
- any workflow-generated Markdown artifacts created or updated during the workflow remain in the target repo root and are never moved to subdirectories or alternate paths,
- any workflow-generated Markdown artifacts created or updated during the workflow include `Created by`, `Created at`, and `Updated at` metadata with `Updated at` refreshed on every edit,
- workflow-generated Markdown artifacts are not staged or committed unless I explicitly ask for that,
- the fix pass stages changes, commits them, pushes the branch, and creates a pull request only if the current branch does not already have one.

Context to read before acting:

- `REVIEW.md`,
- `WALKTHROUGH.md`,
- `FEATURE_SPEC_AND_PLAN.md`, if present,
- `GPT_EXECUTION_PROMPT.md`, if present,
- current branch diff against `main`.

The planning and execution artifacts are optional inputs. When present, treat them as authoritative according to this prompt. Their absence is not a blocker and must not trigger a request for them.

Execution posture:

- understand the context of the current branch or PR before editing,
- inspect the actual code and review artifacts before deciding whether a finding is valid,
- read likely relevant files in parallel before editing when that shortens the loop,
- prefer dedicated repo/search/edit tools over raw shell when available,
- carry through implementation and focused verification without waiting for step-by-step approval unless blocked.

Constraints:

- do not blindly implement every review comment,
- address all valid review findings in `Blocking Issues` and `Non-Blocking Issues`,
- do not implement optional suggestions unless explicitly approved,
- keep all fixes within the scope established by `REVIEW.md` and the current branch diff; when the original implementation scope can be established from available planning artifacts, preserve it too,
- preserve plan scope when a plan is available,
- preserve backwards compatibility,
- workflow-generated Markdown artifacts belong only in the target repo root using their exact required filenames,
- workflow-generated Markdown artifacts must include `Created by`, `Created at`, and `Updated at` metadata, preserving the creation fields after first write and updating `Updated at` on every edit,
- no architecture changes,
- no unrelated refactors,
- no tests unless explicitly asked,
- treat a valid documentation-checkpoint gap as a required review fix: update and validate the durable documentation in the same change set, or stop and ask if the required change would exceed the approved scope,
- stop and ask on ambiguity/conflict/context gaps.

Per-review-item process:

1. Verify the review item against the actual code.
2. Determine whether it is valid.
3. Implement every valid fix from `Blocking Issues` and `Non-Blocking Issues`, including minor nits that are still valid issues.
4. Complete the documentation checkpoint for the changed behavior before treating the review item as fixed.
5. Do not implement items from `Suggestions` unless explicitly approved.
6. If a review item is wrong, stale, or conflicts with an available plan or code reality, stop and ask.
7. If a review item requires a design decision not already made, stop and ask.
8. Check off fixes if a checklist exists.

Focused verification:

- run focused verification relevant to the fixes,
- run the applicable focused documentation validation for every documentation update before staging; if no update applies, record the evidence-based `Not applicable` rationale,
- after verification, stage the intended files with `git add`,
- do not stage or commit workflow-generated Markdown artifacts by default, including `DRAFT_PLAN.md`, `INITIAL_OPUS_PLANNING_PROMPT.md`, `FEATURE_SPEC_AND_PLAN.md`, `GPT_EXECUTION_PROMPT.md`, `PLAN_CRITIQUE.md`, `OPUS_PLAN_REVISION_REQUEST.md`, `PLAN_REVISION_SUMMARY.md`, `PLAN_REVISION_VERIFICATION.md`, `REVIEW.md`, `WALKTHROUGH.md`, `GPT_REVIEW_FIX_PROMPT.md`, `REVIEW_FIX_VERIFICATION.md`, and `FOLLOWUP.md`, unless I explicitly ask for them to be committed,
- create focused commit(s) with detailed messages,
- push the current branch after committing,
- check whether a pull request already exists for the current branch before creating one,
- create a pull request if and only if the current branch does not already have one,
- if you do not know how to check whether a pull request already exists for the current branch, use GitHub CLI (`gh`) to determine that,
- do not create a duplicate pull request for the same branch,
- if a command fails, paste the exact error/log back. Never paraphrase logs.

Required final response:

The generated `GPT_REVIEW_FIX_PROMPT.md` must require this exact response structure:

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

In `## Documentation Checkpoints`, require GPT to list each review item's documentation status, the exact durable documentation and validation evidence when applicable, or the evidence-based `Not applicable` rationale.

It must explicitly instruct GPT not to claim completion without fresh verification evidence.

Do not modify code during this Opus review phase.
