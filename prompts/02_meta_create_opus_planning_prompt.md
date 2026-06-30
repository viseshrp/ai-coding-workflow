# 02 — Meta Prompt: Create the Opus Planning Prompt — GPT or Codex

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


## Prompt

Create a prompt for Claude Opus to perform the planning phase for this coding task. It must be the final paste-ready prompt for the main planning phase.

This is a meta prompt. Your output is the prompt that I will paste into Claude Opus.

Goal:

- turn the current exploration outputs into the final direct-use Opus planning prompt,
- refine and normalize the exploration-phase seed prompt when it exists,
- preserve scope and detail while improving direct paste readiness.

Success criteria:

- the generated Opus prompt is explicit about task, scope, success criteria, stop rules, and required artifacts,
- it is structured with clear sections for role, context to read, task, success criteria, constraints, required outputs, and final self-check,
- it tells Opus not to speculate about code or files it has not read,
- it preserves the current scope while letting Opus deepen detail inside that scope,
- it preserves all valid task-specific detail from `DRAFT_PLAN.md` and `INITIAL_OPUS_PLANNING_PROMPT.md`, if present,
- this phase outputs only the final Opus planning prompt text; it does not perform the planning work itself and it does not create `FEATURE_SPEC_AND_PLAN.md` or `CODEX_EXECUTION_PROMPT.md`.

Constraints:

- this is a meta phase; your output is the final prompt that I will paste into Claude Opus,
- the Opus prompt you generate must be self-contained,
- do not do the Opus planning work yourself,
- do not implement code,
- do not write tests,
- do not introduce unrelated files or workflow changes,
- if `INITIAL_OPUS_PLANNING_PROMPT.md` is present, treat it as the exploration-phase seed prompt and preserve its valid task-specific detail unless you are improving structure, clarity, or completeness.

Context to use when available:

- `DRAFT_PLAN.md`,
- `INITIAL_OPUS_PLANNING_PROMPT.md`,
- interviewing/grilling output,
- relevant repository context.

Required behavior for the generated Opus prompt:

- analyze the code one more time,
- take the draft plan file / interviewing output we have,
- read and critique it,
- ask more questions to me about the design all at one go,
- independently flesh out the remaining details to the T after gathering my design decisions,
- make the initial interviewing output plan into a more detailed implementation plan,
- be independent and not constrain itself to the existing plan file except for the scope of the plan/changes,
- use the existing plan file only as an initial source to get started,
- ignore DevOps/packaging/building and test-related work and focus only on the code, unless otherwise specified in the plan,
- use the existing plan file as a seed artifact, not the ceiling for detail,
- preserve all valid task-specific detail from `DRAFT_PLAN.md` and `INITIAL_OPUS_PLANNING_PROMPT.md`, if present,
- if those sources differ materially, keep the more scope-conservative interpretation and tell Opus to surface the conflict to the user instead of silently choosing,
- ask remaining design questions in one batch before finalizing artifacts,
- ground file/class/function details in actual repository context,
- separate confirmed facts from inferences and surface unresolved uncertainty plainly.

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


The Opus prompt must require these final outputs:

1. `FEATURE_SPEC_AND_PLAN.md` — a single combined artifact with:
   - a detailed spec/reference section,
   - a concrete implementation plan with every minor detail fleshed out absolutely thoroughly,
   - concrete files, classes, methods, variables, and where changes should go,
   - implementation plan links back to relevant spec/reference anchors inside the same file.
2. `CODEX_EXECUTION_PROMPT.md` — a prompt for Codex to take the locked feature spec/plan and implement it end-to-end with no interruptions unless a required decision was not made or a conflict appears.

The prompt you generate must explicitly include these skill links and instruct the target agent to use them only as supporting procedures:

- [spec-driven-development](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/spec-driven-development/SKILL.md)
- [planning-and-task-breakdown](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/planning-and-task-breakdown/SKILL.md)
- [context-engineering](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/context-engineering/SKILL.md)
- [source-driven-development](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/source-driven-development/SKILL.md)
- [verification-before-completion](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/obra__Superpowers/snapshot/skills/verification-before-completion/SKILL.md)


The Opus prompt must also require that the generated `CODEX_EXECUTION_PROMPT.md` include these skills explicitly:

- [incremental-implementation](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/incremental-implementation/SKILL.md)
- [source-driven-development](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/source-driven-development/SKILL.md)
- [verification-before-completion](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/obra__Superpowers/snapshot/skills/verification-before-completion/SKILL.md)

The Opus prompt must include the full Engineering Contract below and instruct Opus to embed the contract into `CODEX_EXECUTION_PROMPT.md`.

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


Do not implement code.

Do not write tests.

Only output the Claude Opus planning prompt.
