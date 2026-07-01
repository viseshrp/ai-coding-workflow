# 06 — Opus Reviews Implemented Branch

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

- DO NOT WRITE TESTS UNTIL EXPLICITLY ASKED.
- Do not create, modify, or delete tests unless I explicitly ask for test changes.
- Running existing focused tests/checks is allowed when the prompt asks for verification.
- Do not manually run the entire test suite unless I explicitly ask. Focused tests are better.

When I explicitly ask you to write tests, follow these rules:

```text
Always keep test code in separate files or folders away from production code. No comingling.
Tests must validate the right things: architecture and behavior, not implementation details.
Avoid unnecessary tests that test temporary hacks or changes.
Make sure tests for these changes are meaningful, not duplicated, not testing transient/temporary issues, not flaky, and maintain at least 95% coverage for the new lines.
Do not manually run the entire test suite unless explicitly asked. Focused tests are better.
Tests must strictly test one behavior per test/method.
```

When reviewing tests, flag cases that are not obvious flakes but are brittle or too coupled to implementation details. Look for tests that:

- mutate process-global state such as environment variables,
- depend on private constants or private helper methods,
- assert exact error wording unless it is an intentional user-facing contract,
- encode packaging/layout assumptions that may change,
- mirror production logic instead of independently specifying expected behavior.

For each test concern, classify whether it is:

- a real flake risk,
- an acceptable contract test,
- or a maintainability concern.

Suggest a behavior-level alternative when practical.


## Prompt

Role:

- You are Claude Opus performing post-implementation review in an existing codebase.
- Read before answering. Do not speculate about files or code you have not inspected.

Task:

- Compare the current branch against `main` and against the locked planning artifacts.
- Aggregate all changes in the current branch that are newly added and do a thorough code review.
- Identify real defects, plan divergence, and high-value follow-up suggestions without expanding scope.

Context to review:

- `FEATURE_SPEC_AND_PLAN.md`, if present,
- `SPEC.md`, if present,
- `IMPLEMENTATION_PLAN.md`, if present,
- any local `PLAN*.md` files in the repo root, if available,
- `CODEX_EXECUTION_PROMPT.md`, if present.

Success criteria:

- every blocking issue is grounded in specific diff, code, or plan evidence,
- plan divergence is clearly separated from optional suggestions,
- the outputs are detailed enough to drive both the review-fix phase and the final human walkthrough.

Constraints:

- do not modify code during this phase,
- backwards compatibility is top priority,
- do not turn preferences into blocking findings unless they are justified by real risk or contract mismatch.

Working method:

- compare the current branch against the head of `main`,
- inspect actual code and actual diff before judging,
- flag divergence and issues,
- quote or clearly point to the exact evidence for each material finding,
- separate confirmed issues from preferences, open questions, and optional suggestions,
- after checking 100% compliance with the plan and ensuring no divergence, provide suggestions.
- do not make any changes you propose until I give the go-ahead.

This branch will be merged into main.

## Review dimensions

Review for:

- readability,
- quality,
- backwards compatibility,
- performance,
- proper reuse of existing code,
- plan compliance,
- source/documentation grounding,
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

Tests must validate the right things: architecture and behavior, not implementation details.

Mark unnecessary tests that test temporary hacks or changes.

Make sure tests for these changes are meaningful, not duplicated, not testing transient/temporary issues, not flaky, and maintain at least 95% coverage for the new lines.

Do not manually run the entire test suite. Focused tests are better.

While reviewing tests, flag cases that are not obvious flakes but are brittle or too coupled to implementation details. Look for tests that:

- mutate process-global state such as environment variables,
- depend on private constants or private helper methods,
- assert exact error wording unless it is an intentional user-facing contract,
- encode packaging/layout assumptions that may change,
- mirror production logic instead of independently specifying expected behavior.

For each concern, classify whether it is:

- a real flake risk,
- an acceptable contract test,
- or a maintainability concern.

Suggest a behavior-level alternative when practical.

Tests must strictly test one behavior per test/method.

## Required output 1: `REVIEW.md`

Create a detailed `REVIEW.md` document with:

```markdown
# Review

## Verdict

## Plan Compliance

## Blocking Issues

## Non-Blocking Issues

## Backwards Compatibility

## Public API Review

## Performance / Complexity Review

## Source Documentation Grounding

## Code Quality / Readability

## Reuse / DRY / Duplication

## Assumptions Surfaced

## Assert Usage

## Cross-Platform Review

## Test Review

## Documentation Review

## Suggestions
```

Put suggestions directly below the relevant review findings.

## Required output 2: `WALKTHROUGH.md`

Create a detailed `WALKTHROUGH.md` documenting each change with context, line by line, helping a beginner programmer review the code from scratch without prior context.

It must be detailed and thorough, so as to facilitate review without looking at the code.

I WANT LINE BY LINE WITH ENGLISH BASED EXPLANATION NEXT TO EACH LINE OF CODE. THIS IS NON NEGOTIABLE.

Format it properly for easy readability and to ease cognitive overload while reviewing.

## Required output 3: `CODEX_REVIEW_FIX_PROMPT.md`

Create a self-contained prompt for Codex to fix the valid review findings.

The generated Codex prompt must include these skill links explicitly:

- [incremental-implementation](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/incremental-implementation/SKILL.md)
- [source-driven-development](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/source-driven-development/SKILL.md)
- [verification-before-completion](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/obra__Superpowers/snapshot/skills/verification-before-completion/SKILL.md)
- [receiving-code-review](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/obra__Superpowers/snapshot/skills/receiving-code-review/SKILL.md)

The generated Codex prompt must instruct Codex to:

- read `REVIEW.md`,
- read `WALKTHROUGH.md` for context,
- understand the current PR,
- address only the valid required review findings,
- not implement optional suggestions unless explicitly approved,
- preserve plan scope,
- preserve backwards compatibility,
- follow the Engineering Contract,
- check off fixes if a checklist exists,
- stop and ask on ambiguity/conflict/context gaps.

Do not modify code during this Opus review phase.
