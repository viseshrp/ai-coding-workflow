# 02 — Plan Critique Loop: Critique Feature Spec/Plan + Generate Opus Revision Request — GPT or Gemini

## Skills

- [code-review-and-quality](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/code-review-and-quality/SKILL.md)
- [code-simplification](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/code-simplification/SKILL.md)
- [source-driven-development](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/source-driven-development/SKILL.md)
- [verification-before-completion](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/obra__Superpowers/snapshot/skills/verification-before-completion/SKILL.md)
- [unslop](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/cursor__plugins/snapshot/pstack/skills/unslop/SKILL.md)

## Skill Handling Rule

Use only the explicitly linked skills listed in this prompt.

The prompt is the contract. The locked task artifact is the contract for execution. Skills are supporting procedures only.

If a skill conflicts with this prompt, this prompt wins.

If a conflict is material, stop and ask instead of silently choosing.

Do not use any skill to expand scope, add architecture changes, add tests, add unrelated refactors, or override my explicit instructions.

Use `unslop` for every chat response and generated artifact. Prefer plain words, concrete statements, and short, readable sentences. Keep necessary technical terms, but explain them simply. Remove filler, canned AI phrasing, inflated language, unnecessary jargon, and needless structure. Preserve technical meaning and required detail.


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
- Do not use filler types.
- Do not use overly generic types just to satisfy a checker.
- Do not use type-ignore comments to pass CI temporarily.
- Do not add sloppy code like `typing.Cast` or cast types in code just to satisfy type checkers.

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

- Do not create, modify, or delete tests in this planning-critique phase.
- Run only focused existing tests or checks when repository evidence is needed; do not manually run the entire suite.
- Require planning artifacts to defer test authoring to the final model-agnostic `09_write_focused_tests_any_model.md` phase.
- Do not duplicate phase `09`'s test-design, pytest, or coverage contract in this critique.

## Prompt

Goal:

- determine whether the planning artifacts are ready to lock for GPT execution.

Success criteria:

- every material concern is grounded in specific plan text, GPT-prompt text, or concrete repo evidence,
- blocking issues, non-blocking issues, missing user decisions, and simple suggestions are separated cleanly,
- the output follows the exact artifact structure below.

Constraints:

- do not implement code,
- do not modify files unless I explicitly ask,
- critique the plan, not alternative future architectures,
- if evidence is missing, say so explicitly instead of guessing.

Context to review:

- `FEATURE_SPEC_AND_PLAN.md`,
- `GPT_EXECUTION_PROMPT.md`,
- the original draft plan/interviewing notes if available,
- relevant repository context if needed.

Working method:

- if you are GPT, inspect the planning artifacts and any necessary repo files in parallel before finalizing,
- if you are GPT or Gemini, stay grounded in the supplied artifacts and any repo context you inspect,
- quote or clearly point to the exact passage that triggered each blocking issue,
- separate confirmed issues, inferences, and open questions,
- prefer concrete execution risks over generic style commentary.

Task:

- critique the plan, not execute it,
- decide whether the artifacts are good enough to lock for GPT execution,
- produce `PLAN_CRITIQUE.md` and, if needed, `OPUS_PLAN_REVISION_REQUEST.md`.

## Review dimensions

Review for:

- missing design decisions,
- unclear requirements,
- divergence from original scope,
- insufficient file/class/method/function/variable detail,
- missing execution order,
- missing edge cases,
- backwards compatibility risks,
- public API naming/design risks,
- performance or algorithmic complexity concerns,
- unnecessary brute-force or quadratic operations,
- poor reuse / DRY violations,
- failure to reuse existing code,
- separation-of-concerns violations,
- missing documentation grounding for library/framework usage,
- outdated API usage,
- unnecessary third-party dependencies,
- missing custom exception/error translation at public API boundaries,
- cross-platform Linux/Windows risks,
- test-writing instructions that conflict with “do not write tests unless explicitly asked,”
- missing verification commands/checks,
- missing documentation update plan,
- anything in the GPT prompt that gives GPT too much freedom.

## Required output 1: `PLAN_CRITIQUE.md`

Create or output `PLAN_CRITIQUE.md` in the target repo root.

Use this structure:

```markdown
# Plan Critique

## Verdict
- Ready to execute: Yes/No
- Reason:

## Blocking Issues

## Non-Blocking Issues

## Missing Questions For User

## Scope / Divergence Risks

## Backwards Compatibility Risks

## Public API Risks

## Performance / Complexity Risks

## Source Documentation Grounding Issues

## GPT Prompt Risks

## Simplification Opportunities

## Final Recommendation
```

## Required output 2: `OPUS_PLAN_REVISION_REQUEST.md`

Create `OPUS_PLAN_REVISION_REQUEST.md` in the target repo root as the final direct-use prompt for Opus to revise `FEATURE_SPEC_AND_PLAN.md` and `GPT_EXECUTION_PROMPT.md`.

There is no separate checked-in Opus revision prompt file after this critique step. `OPUS_PLAN_REVISION_REQUEST.md` itself must be the final paste-ready prompt for the revision pass.

This phase is the only place that should author `OPUS_PLAN_REVISION_REQUEST.md`.

If a later verification pass says another revision is needed, return to this phase and regenerate `OPUS_PLAN_REVISION_REQUEST.md` here. Do not create an alternate revision prompt in the verification phase.

It must be self-contained.

Do not generate:

- a helper prompt,
- a meta-only instruction block,
- a skeleton that expects another prompt file to fill in the real contract,
- a revision summary without the full direct-use prompt.

The generated Opus revision prompt must use a clear title and contain these top-level sections:

- `## Skills`
- `## Skill Handling Rule`
- `## Default Planning Artifact Reduction`
- `## Engineering Contract`
- `## Prompt`

The generated Opus revision prompt must include these skill links explicitly:

- [spec-driven-development](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/spec-driven-development/SKILL.md)
- [planning-and-task-breakdown](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/planning-and-task-breakdown/SKILL.md)
- [context-engineering](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/context-engineering/SKILL.md)
- [source-driven-development](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/source-driven-development/SKILL.md)
- [verification-before-completion](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/obra__Superpowers/snapshot/skills/verification-before-completion/SKILL.md)
- [code-review-and-quality](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/code-review-and-quality/SKILL.md)
- [code-simplification](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/code-simplification/SKILL.md)
- [unslop](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/cursor__plugins/snapshot/pstack/skills/unslop/SKILL.md)

The generated Opus revision prompt must include a `## Skill Handling Rule` that instructs Opus to:

- use only the explicitly linked skills listed in the prompt,
- treat the prompt as the contract,
- treat locked task artifacts as the contract for execution,
- use skills as supporting procedures only,
- let the prompt win if a skill conflicts with it,
- stop and ask instead of silently choosing if a conflict is material,
- never use a skill to expand scope, add architecture changes, add tests, add unrelated refactors, or override my explicit instructions.
- use `unslop` for every chat response and generated artifact, using plain words, concrete statements, short readable sentences, and a natural human voice without dropping technical meaning or required detail.

The generated Opus revision prompt must include `## Default Planning Artifact Reduction` and require:

- `FEATURE_SPEC_AND_PLAN.md`
- `GPT_EXECUTION_PROMPT.md`

It must state that:

1. `FEATURE_SPEC_AND_PLAN.md` contains both a detailed spec/reference section and a concrete implementation plan section.
2. The implementation plan section links back to relevant spec/reference anchors inside the same file instead of duplicating long explanations.
3. The plan remains the execution contract.
4. The spec/reference section remains the background reference.
5. Separate `SPEC.md` and `IMPLEMENTATION_PLAN.md` are only a fallback if I explicitly ask or if the file becomes too large to review comfortably.
6. All workflow-generated Markdown artifacts must be created or updated only in the target repo root using their exact required filenames, never in subdirectories or alternate paths.
7. All workflow-generated Markdown artifacts must include `Created by`, `Created at`, and `Updated at` metadata, preserving the creation fields after first creation and refreshing `Updated at` whenever an artifact is edited.

The generated Opus revision prompt must embed the full Engineering Contract above verbatim or stricter.

Inside `## Prompt`, the generated Opus revision prompt must use clear sections for:

- role,
- task,
- context to read before answering,
- success criteria,
- constraints,
- working method,
- required outputs,
- final checks.

Inside those sections, it must instruct Opus as follows.

Role:

- You are Claude Opus revising the planning artifacts before implementation.
- Be explicit about which critique items are valid, which are rejected, and which still require a user decision.
- Read before answering. Do not speculate about code or files you have not inspected.

Task:

- Update the planning artifacts so they are ready for locked GPT execution.
- Apply valid critique items without expanding scope.

Context to read before answering:

- `PLAN_CRITIQUE.md`, if present,
- `OPUS_PLAN_REVISION_REQUEST.md`, if present from a prior pass,
- current `FEATURE_SPEC_AND_PLAN.md`,
- current `GPT_EXECUTION_PROMPT.md`,
- the original draft plan/interviewing notes if available,
- relevant repository context.

Success criteria:

- every critique item is explicitly addressed, rejected with reasoning, or escalated for a user decision,
- the revised plan stays within original scope,
- the revised GPT prompt remains strict enough to prevent divergence during execution,
- the revised planning artifacts still belong only in the target repo root and do not introduce any alternate artifact path,
- the revised planning artifacts preserve or add `Created by`, `Created at`, and `Updated at` metadata correctly,
- the revised GPT prompt preserves explicit instructions to stage changes, commit, push, and create a pull request only if the current branch does not already have one,
- the revised GPT prompt preserves explicit instructions not to stage or commit workflow-generated Markdown artifacts unless I explicitly ask for that,
- no detail from the current plan artifacts, critique, or draft-plan lineage is silently dropped.

Constraints:

- do not implement code,
- do not write tests,
- do not loosen the GPT prompt,
- do not use the critique as permission to change architecture unless I explicitly approve,
- keep the plan/code execution scope unchanged unless I explicitly approve scope changes.

Working method:

For each critique item:

1. Decide whether it is valid.
2. If valid and answerable from the repo/context, update the plan/prompt.
3. If valid but requires my design decision, stop and ask me before updating that part.
4. If invalid, document why.
5. If it would expand scope, stop and ask.

And also:

- read `PLAN_CRITIQUE.md`,
- read the current `FEATURE_SPEC_AND_PLAN.md`,
- read the current `GPT_EXECUTION_PROMPT.md`,
- apply all valid critique items,
- ask if a critique item requires a design decision from me,
- do not silently drop any critique item,
- ground plan detail in the code and context you actually inspected,
- preserve or strengthen the `GPT_EXECUTION_PROMPT.md` instructions to stage intended files with `git add`, create focused commits, push the current branch, check whether a pull request already exists for the current branch, and create a pull request only if none exists,
- preserve or strengthen the artifact-location rule that all workflow-generated Markdown artifacts stay in the target repo root using their exact required filenames and are never created in subdirectories or alternate paths,
- preserve or strengthen the artifact-metadata rule that all workflow-generated Markdown artifacts include `Created by`, `Created at`, and `Updated at`, preserving creation fields and refreshing `Updated at` on edits,
- preserve or strengthen the `GPT_EXECUTION_PROMPT.md` instructions not to stage or commit workflow-generated Markdown artifacts such as `FEATURE_SPEC_AND_PLAN.md`, `GPT_EXECUTION_PROMPT.md`, `REVIEW.md`, `WALKTHROUGH.md`, `GPT_REVIEW_FIX_PROMPT.md`, `FOLLOWUP.md`, and the other workflow output Markdown files unless I explicitly ask for that,
- if the revised `GPT_EXECUTION_PROMPT.md` needs a fallback instruction for checking whether a pull request already exists for the current branch, use GitHub CLI (`gh`) for that fallback and do not invent a duplicate-prone alternative,
- preserve explicit success criteria, stop rules, and verification expectations in the revised artifacts.

Required outputs:

Update or create:

- `FEATURE_SPEC_AND_PLAN.md` in the target repo root
- `GPT_EXECUTION_PROMPT.md` in the target repo root
- `PLAN_REVISION_SUMMARY.md` in the target repo root

The generated revision prompt must require `PLAN_REVISION_SUMMARY.md` to use this structure:

```markdown
# Plan Revision Summary

## Critique Items Addressed

## Critique Items Rejected

## Critique Items Requiring User Decision

## Changes Made To FEATURE_SPEC_AND_PLAN.md

## Changes Made To GPT_EXECUTION_PROMPT.md

## Remaining Risks

## Ready For Another Critique Pass?

## Ready For GPT Execution?
```

Final checks:

- verify that the updated plan is still within original scope,
- verify that the implementation plan section remains concrete down to files/classes/functions/methods/variables/order of changes,
- verify that the GPT prompt still includes strict no-divergence/no-creativity/no-architecture-change rules,
- verify that no test-writing is introduced unless explicitly asked,
- verify that all skill links relevant to the generated GPT prompt remain present,
- verify that the GPT prompt still requires `git add`, commit, push, and create-PR-only-if-missing behavior,
- verify that the GPT prompt still forbids committing workflow-generated Markdown artifacts by default,
- verify that the Engineering Contract remains intact or stricter.

Do not ask Opus to implement code.
