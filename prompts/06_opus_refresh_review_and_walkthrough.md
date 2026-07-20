# 06 - Opus Refreshes Final Review + Walkthrough Files

## Skills

- [code-review-and-quality](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/code-review-and-quality/SKILL.md)
- [code-simplification](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/code-simplification/SKILL.md)
- [source-driven-development](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/source-driven-development/SKILL.md)
- [verification-before-completion](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/obra__Superpowers/snapshot/skills/verification-before-completion/SKILL.md)

## Skill Handling Rule

Use only the explicitly linked skills listed in this prompt.

The prompt is the contract. The locked task artifact is the contract for execution. Skills are supporting procedures only.

If a skill conflicts with this prompt, this prompt wins.

If a conflict is material, stop and ask instead of silently choosing.

Do not use any skill to expand scope, add architecture changes, add tests, add unrelated refactors, or override my explicit instructions.


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

- Do not create, modify, or delete tests while refreshing review artifacts.
- Run only focused existing tests or checks needed to support the refreshed review; do not manually run the entire suite.
- Review tests for the smallest nonduplicative behavior-focused set, one clear behavior per test, small readable functions and helpers, existing pytest fixtures and APIs instead of hand-rolled Python or standard-library mechanisms, limited boundary mocking, deterministic isolation, and at least 85% coverage for new or changed lines.
- Flag implementation coupling, patching or mocking the subject under test itself, unscoped global-state mutation, fragile message or layout assertions, mirrored production logic, and coverage-only tests.
- Defer new test authoring and the detailed pytest contract to the final model-agnostic `09_write_focused_tests_any_model.md` phase.

## Prompt

Role:

- You are Claude Opus refreshing the final review artifacts after the AI review/fix loop is complete.
- Read before answering. Do not speculate about files or code you have not inspected.

Task:

- your job is to update the review and walkthrough documents so they accurately reflect the final code state,
- preserve the existing review trail while clearly marking what was fixed during the review loop.

Artifact location rule:

- `REVIEW.md`, `WALKTHROUGH.md`, and any other workflow-generated Markdown artifacts must stay in the target repo root using their exact required filenames,
- every workflow-generated Markdown artifact must include `Created by`, `Created at`, and `Updated at` metadata, preserving the creation fields and refreshing `Updated at` whenever the artifact is updated,
- do not move or recreate them in subdirectories or alternate paths.

Context to review:

- current branch diff against `main`,
- final current code,
- `FEATURE_SPEC_AND_PLAN.md`, if present,
- `REVIEW.md`,
- `WALKTHROUGH.md`,
- `REVIEW_FIX_VERIFICATION.md`, if present.

Success criteria:

- `REVIEW.md` matches the final code and clearly distinguishes resolved findings from any remaining suggestions,
- `WALKTHROUGH.md` matches the final code state and remains useful for a beginner human reviewer,
- the refreshed artifacts are detailed, grounded, and internally consistent.

Constraints:

- do not modify production code,
- do not modify tests,
- do not make new review findings unless you discover something severe that was missed,
- if you discover a severe missed issue, stop and ask before proceeding.

## Required output 1: refreshed `REVIEW.md`

Update `REVIEW.md` in the target repo root so it reflects the final code.

It must include:

- final verdict,
- plan compliance,
- backwards compatibility review,
- public API review,
- performance/complexity review,
- source documentation grounding,
- code quality/readability,
- reuse/DRY/duplication,
- assumptions surfaced,
- assert usage,
- cross-platform review,
- test review, if applicable,
- documentation review,
- any remaining suggestions.

Clearly mark review findings that were fixed during the review loop.

## Required output 2: refreshed `WALKTHROUGH.md`

Update `WALKTHROUGH.md` in the target repo root so it reflects the final code, not the old pre-fix code.

Document each change with context, line by line, helping a beginner programmer review the code from scratch without prior context.

It must be detailed and thorough, so as to facilitate review without looking at the code.

I WANT LINE BY LINE WITH ENGLISH BASED EXPLANATION NEXT TO EACH LINE OF CODE. THIS IS NON NEGOTIABLE.

Format it properly for easy readability and to ease cognitive overload while reviewing.

The walkthrough must be suitable as a supplement for my human review and potentially as PR-description source material.

Before finishing, verify that `REVIEW.md` and `WALKTHROUGH.md` match the final code state.
