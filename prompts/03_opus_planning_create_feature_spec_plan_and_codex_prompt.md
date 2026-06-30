# 03 — Opus Planning: Create Feature Spec/Plan + Codex Execution Prompt

## Skills

- [spec-driven-development](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/spec-driven-development/SKILL.md)
- [planning-and-task-breakdown](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/planning-and-task-breakdown/SKILL.md)
- [context-engineering](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/context-engineering/SKILL.md)
- [source-driven-development](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/source-driven-development/SKILL.md)
- [verification-before-completion](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/obra__Superpowers/snapshot/skills/verification-before-completion/SKILL.md)

## Skill Handling Rule

Use only the explicitly linked skills listed in this prompt.

The prompt is the contract. The locked task artifact is the contract for execution. Skills are supporting procedures only.

If a skill conflicts with this prompt, this prompt wins.

If a conflict is material, stop and ask instead of silently choosing.

Do not use any skill to expand scope, add architecture changes, add tests, add unrelated refactors, or override my explicit instructions.


## Default Planning Artifact Reduction

Default to one combined planning artifact instead of separate spec and implementation plan files.

Create:

- `FEATURE_SPEC_AND_PLAN.md`
- `CODEX_EXECUTION_PROMPT.md`

`FEATURE_SPEC_AND_PLAN.md` must contain both:

1. a detailed spec/reference section, and
2. a concrete implementation plan section.

The implementation plan section must link to the relevant spec/reference anchors inside the same file instead of duplicating long explanations.

The plan remains the execution contract. The spec/reference section remains the background reference.

Only split into separate `SPEC.md` and `IMPLEMENTATION_PLAN.md` if I explicitly ask or if the file becomes too large to review comfortably.


## Prompt

Role:

- You are Claude Opus performing the planning phase for an agentic coding workflow.
- Be explicit, source-grounded, and conservative about assumptions.
- Read before answering. Do not speculate about code or files you have not inspected.

Task:

- Perform the main planning work itself. Do not generate a meta prompt for another model.
- Your job is to create the detailed planning artifacts that will become the contract for Codex execution.
- Critique the current draft plan, ask any remaining design questions in one batch, then produce the locked planning artifacts after my answers.
- The initial interviewing output plan must be made into a more detailed implementation plan.

Context to read before answering:

- Read the draft plan, prior interviewing/grilling notes, and relevant repository context.
- the draft plan,
- prior interviewing/grilling notes,
- relevant repository context.

Success criteria:

- `FEATURE_SPEC_AND_PLAN.md` is concrete enough that Codex can execute without inventing missing detail,
- `CODEX_EXECUTION_PROMPT.md` preserves the Engineering Contract and leaves Codex no ambiguity about scope, stop rules, or verification,
- no important detail from the draft plan is dropped,
- scope stays within the requested change.

Constraints:

- do not implement code,
- do not write tests,
- do not make unrelated files or unrelated changes,
- ignore DevOps/packaging/building and test-related work unless otherwise specified in the plan,
- prefer the minimum necessary design surface and do not overengineer or add speculative abstractions.

Working method:

- analyze the code one more time,
- you may be independent and should not constrain yourself to the existing plan file except for the scope of the plan/changes,
- use the existing plan file as an initial source to get started,
- use the existing plan as a seed artifact, not the ceiling for detail,
- ask remaining design questions together in one batch,
- after my answers, flesh out the remaining details thoroughly enough that Codex can execute without guessing,
- ground file/class/function details in code you actually inspected,
- if repo reality conflicts with the draft plan, surface the conflict explicitly instead of silently rewriting scope,
- separate confirmed facts from inferences and call out unresolved uncertainty plainly.

Final self-check:

- verify that the planning artifacts are explicit about success criteria, stop rules, and verification,
- verify that the implementation plan is detailed enough to drive end-to-end Codex execution,
- verify that the prompt and plan remain within the original requested scope.

## Required planning depth

The final plan must be concrete down to:

- files,
- classes,
- functions,
- methods,
- variables,
- constants,
- call flow,
- data flow,
- public API behavior,
- error behavior,
- backwards compatibility expectations,
- where each change should go,
- order of changes,
- verification commands/checks,
- documentation updates.

## Required design-question pass

Before finalizing artifacts, identify every remaining design decision that I need to make.

Ask all remaining questions together in one batch.

For each question:

- explain why it matters,
- give your recommended answer,
- explain the tradeoffs,
- identify what parts of the plan depend on the answer.

After I answer, update the artifacts accordingly.

If a question can be answered by reading the codebase, answer it from codebase exploration instead of asking me.

## Required output 1: `FEATURE_SPEC_AND_PLAN.md`

Create `FEATURE_SPEC_AND_PLAN.md`.

It must include:

### 1. Executive summary

- one-paragraph problem statement,
- goal,
- non-goals,
- definition of done.

### 2. Spec / reference section

This is the detailed reference section. Include:

- current behavior,
- desired behavior,
- user-visible behavior,
- public API behavior,
- backwards compatibility requirements,
- constraints,
- design decisions,
- edge cases,
- error handling,
- performance/complexity expectations,
- dependency/library documentation findings,
- source-code references,
- risks,
- non-goals,
- unresolved questions, if any.

### 3. Concrete implementation plan section

This is the execution contract.

It must be more direct than the spec/reference section but still extremely detailed.

For every step include:

- exact file(s),
- exact symbol(s),
- exact change to make,
- why the change is needed,
- link to relevant spec/reference anchor inside this same file,
- dependencies on previous steps,
- verification relevant to that step.

### 4. Source/documentation grounding section

For every library/framework/API involved:

- identify the version if possible,
- cite the official docs/source consulted,
- explain the pattern chosen,
- flag anything unverified,
- flag outdated APIs,
- explain if source code was used because docs were poor.

### 5. Verification plan

Include:

- focused lint/smoke/build commands, if available,
- exact checks to run,
- what successful output means,
- what failures should be pasted back without paraphrasing,
- no full test-suite run unless explicitly asked.

### 6. Documentation update plan

Include:

- likely docs folder/file(s),
- how you found them,
- exact sections to update or create,
- reminder not to write the changelog.

## Required output 2: `CODEX_EXECUTION_PROMPT.md`

Create `CODEX_EXECUTION_PROMPT.md`.

This must be a self-contained end-to-end prompt for Codex.

It must instruct Codex to:

- read `FEATURE_SPEC_AND_PLAN.md`,
- follow the implementation plan exactly,
- use the spec/reference section only as reference,
- make no architecture changes,
- make no unrelated changes,
- implement end-to-end with no interruptions unless a required decision was not made or a conflict appears,
- stop and ask on ambiguity/conflict/context gaps,
- use the full Engineering Contract below,
- include these skills explicitly:

- [incremental-implementation](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/incremental-implementation/SKILL.md)
- [source-driven-development](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/source-driven-development/SKILL.md)
- [verification-before-completion](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/obra__Superpowers/snapshot/skills/verification-before-completion/SKILL.md)

The generated Codex prompt must include the following Engineering Contract verbatim or stricter:

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


Before finishing, verify that:

- `FEATURE_SPEC_AND_PLAN.md` is sufficient for Codex execution,
- `CODEX_EXECUTION_PROMPT.md` contains every implementation rule above,
- no details from the draft plan were dropped.
