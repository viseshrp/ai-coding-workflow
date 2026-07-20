# Agentic Coding Prompt Pack — Refactored by Workflow Phase

This is a strict reorganization/refactor of the attached prompt pack. The original details are preserved, and the prompts are separated by the workflow phases you described:

```text
Initial exploration / grilling / interviewing
→ Draft plan + initial Opus prompt
→ Opus spec + implementation plan + Codex execution prompt
→ Plan critique loop
→ Locked plan
→ Codex execution
→ Opus implementation review
→ Review-fix loop
→ Final review/walkthrough refresh
→ Sonnet human walkthrough/follow-up
→ Codex human follow-up execution
→ Human final review
```

## Global rule

Do not use a skill router.

Skills are included directly in the specific prompts where they fit. If a prompt is a meta prompt that generates another prompt, it explicitly instructs the model to include the relevant skills and links in the generated output prompt.

---

# Canonical skill links used in this pack

- [interview-me](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/interview-me/SKILL.md)
- [grill-me](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/mattpocock__skills/snapshot/skills/productivity/grill-me/SKILL.md)
- [idea-refine](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/idea-refine/SKILL.md)
- [spec-driven-development](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/spec-driven-development/SKILL.md)
- [planning-and-task-breakdown](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/planning-and-task-breakdown/SKILL.md)
- [context-engineering](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/context-engineering/SKILL.md)
- [source-driven-development](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/source-driven-development/SKILL.md)
- [incremental-implementation](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/incremental-implementation/SKILL.md)
- [verification-before-completion](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/obra__Superpowers/snapshot/skills/verification-before-completion/SKILL.md)
- [code-review-and-quality](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/code-review-and-quality/SKILL.md)
- [code-simplification](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/code-simplification/SKILL.md)
- [receiving-code-review](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/obra__Superpowers/snapshot/skills/receiving-code-review/SKILL.md)

---

# 0. Shared skill policy block

Paste this inside any prompt that includes skills.

```markdown
## Skill handling rule for this prompt

Use only the explicitly linked skills listed inside this prompt.

The prompt is the contract. The locked plan/spec/request file is the contract for execution. Skills are supporting procedures only.

If a skill conflicts with this prompt, this prompt wins.

If a conflict is material, stop and ask instead of silently choosing.

Do not use any skill to expand scope, add architecture changes, add tests, add unrelated refactors, or override my explicit instructions.
```

---

# 1. Initial Exploration / Grilling / Interviewing — GPT/Codex

## Purpose

Use this before Opus planning. This phase turns a vague or partially formed idea into:

- `DRAFT_PLAN.md`
- `INITIAL_OPUS_PLANNING_PROMPT.md`
- a list of unresolved design decisions, if any

## Skills to include in this prompt

- [interview-me](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/interview-me/SKILL.md)
- [grill-me](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/mattpocock__skills/snapshot/skills/productivity/grill-me/SKILL.md)
- [idea-refine](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/idea-refine/SKILL.md)
- [context-engineering](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/context-engineering/SKILL.md)

## Prompt

```markdown
You are helping me perform the initial exploration phase for an agentic coding workflow.

## Skill handling rule for this prompt

Use only the explicitly linked skills listed inside this prompt.

The prompt is the contract. The locked plan/spec/request file is the contract for execution. Skills are supporting procedures only.

If a skill conflicts with this prompt, this prompt wins.

If a conflict is material, stop and ask instead of silently choosing.

Do not use any skill to expand scope, add architecture changes, add tests, add unrelated refactors, or override my explicit instructions.

Use these skills as supporting procedures:

- [interview-me](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/interview-me/SKILL.md)
- [grill-me](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/mattpocock__skills/snapshot/skills/productivity/grill-me/SKILL.md)
- [idea-refine](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/idea-refine/SKILL.md)
- [context-engineering](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/context-engineering/SKILL.md)

My workflow is:

1. GPT/Codex helps me think, interview, grill, and clarify the idea.
2. This produces a draft plan file.
3. This also produces an initial Claude Opus planning prompt file.
4. Opus later uses the draft plan plus repo context as seed context to create:
   - a detailed `SPEC.md`
   - a detailed `IMPLEMENTATION_PLAN.md`
   - an end-to-end `CODEX_EXECUTION_PROMPT.md`

Your job in this phase is NOT to implement code.

Your job is to interview/grill/clarify the idea until the goal, constraints, non-goals, and definition of done are clear enough to seed Opus.

Work interactively first.

Ask one question at a time when clarification is needed.

For each question:
- ask the question,
- include your best guess,
- explain briefly why the question matters.

If a question can be answered by exploring the codebase, explore the codebase instead of asking me.

Do not produce the final draft plan until the exploration is complete or I explicitly ask you to stop and generate the draft.

When ready, create or output:

## `DRAFT_PLAN.md`

Include:
- problem statement
- goals
- non-goals
- user-visible behavior
- constraints
- technical assumptions
- open questions
- decisions already made
- likely files/modules involved, if known
- risks
- definition of done
- anything that Opus must not lose

## `INITIAL_OPUS_PLANNING_PROMPT.md`

This prompt must tell Claude Opus to:
- read the draft plan,
- inspect the repository/codebase again,
- critique the draft plan,
- ask all remaining design questions together in one batch,
- after my answers, independently flesh out the plan to the T,
- produce `SPEC.md`, `IMPLEMENTATION_PLAN.md`, and `CODEX_EXECUTION_PROMPT.md`.

The generated Opus prompt must include the relevant skill links explicitly:
- [spec-driven-development](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/spec-driven-development/SKILL.md)
- [planning-and-task-breakdown](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/planning-and-task-breakdown/SKILL.md)
- [context-engineering](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/context-engineering/SKILL.md)
- [source-driven-development](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/source-driven-development/SKILL.md)
- [verification-before-completion](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/obra__Superpowers/snapshot/skills/verification-before-completion/SKILL.md)

The generated Opus prompt must also tell Opus that any generated Codex execution prompt must include the relevant Codex execution skill links explicitly:
- [incremental-implementation](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/incremental-implementation/SKILL.md)
- [source-driven-development](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/source-driven-development/SKILL.md)
- [verification-before-completion](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/obra__Superpowers/snapshot/skills/verification-before-completion/SKILL.md)

Do not implement code.
Do not write tests.
Do not create unrelated files.
If the task is still ambiguous, keep interviewing instead of pretending the plan is ready.
```

---

# 2. Meta Prompt — Codex/GPT Creates the Opus Planning Prompt

## Purpose

Use this when you already have an interviewing/grilling output or `DRAFT_PLAN.md`, and you want Codex/GPT to create the Opus planning prompt.

This refactors your existing “codex prompt to feed OPUS PLANNING” while preserving the original requirements.

## Skills to include in this meta prompt

- [spec-driven-development](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/spec-driven-development/SKILL.md)
- [planning-and-task-breakdown](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/planning-and-task-breakdown/SKILL.md)
- [context-engineering](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/context-engineering/SKILL.md)
- [source-driven-development](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/source-driven-development/SKILL.md)
- [verification-before-completion](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/obra__Superpowers/snapshot/skills/verification-before-completion/SKILL.md)

## Prompt

```markdown
Create a prompt for Claude Opus to perform the planning phase for this coding task.

This is a meta prompt. Your output is the prompt that I will paste into Claude Opus.

## Skill handling rule for this prompt

Use only the explicitly linked skills listed inside this prompt.

The prompt is the contract. The locked plan/spec/request file is the contract for execution. Skills are supporting procedures only.

If a skill conflicts with this prompt, this prompt wins.

If a conflict is material, stop and ask instead of silently choosing.

Do not use any skill to expand scope, add architecture changes, add tests, add unrelated refactors, or override my explicit instructions.

The Opus prompt you generate must explicitly include these skill links and instruct Opus to use them only as supporting procedures:

- [spec-driven-development](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/spec-driven-development/SKILL.md)
- [planning-and-task-breakdown](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/planning-and-task-breakdown/SKILL.md)
- [context-engineering](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/context-engineering/SKILL.md)
- [source-driven-development](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/source-driven-development/SKILL.md)
- [verification-before-completion](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/obra__Superpowers/snapshot/skills/verification-before-completion/SKILL.md)

The Opus prompt you generate must also instruct Opus that the final `CODEX_EXECUTION_PROMPT.md` it produces must explicitly include these Codex execution skill links:

- [incremental-implementation](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/incremental-implementation/SKILL.md)
- [source-driven-development](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/source-driven-development/SKILL.md)
- [verification-before-completion](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/obra__Superpowers/snapshot/skills/verification-before-completion/SKILL.md)

Seed context:
- Use the interviewing/grilling output and/or `DRAFT_PLAN.md`.
- Use the repository context.
- Treat the draft plan as initial source material, not as a fully reliable final plan.

The generated Opus prompt must tell Claude Opus to:

1. Analyze the code one more time.
2. Take the plan file we have.
3. Read and critique it.
4. Ask more questions to me about the design all at one go.
5. Flesh out the remaining details to the T after gathering my design decisions.
6. Include concrete files, classes, methods, variables, where these changes should go, and order of changes.
7. Be independent.
8. Do not constrain itself to the existing plan file except for the scope of the plan/changes.
9. Use the existing plan file as an initial source to get started.
10. Ignore devops/packaging/building and test related work and only focus on the code, unless otherwise specified in the plan.

The generated Opus prompt must require Opus to produce these markdown files:

1. `SPEC.md`
   - This is the detailed reference spec.
   - It should be more detailed than the implementation plan.
   - It should contain the deeper rationale, constraints, behavioral details, edge cases, and reference material.

2. `IMPLEMENTATION_PLAN.md`
   - This is the execution contract.
   - It must be concrete and absolutely thorough.
   - It must link back to relevant sections of `SPEC.md` for reference.
   - It must be detailed down to files, classes, methods, variables, and order of changes.

3. `CODEX_EXECUTION_PROMPT.md`
   - This is the end-to-end implementation prompt for Codex.
   - It must tell Codex to take the locked plan and spec and implement it end-to-end with no interruptions.
   - It must include all mandatory implementation requests below.
   - It must tell Codex to stop only when there is a conflict in decisions, a missing decision, insufficient context, or a blocking ambiguity.

The generated Opus prompt must include the following implementation requests inside the final `CODEX_EXECUTION_PROMPT.md` exactly in substance:

## Mandatory implementation requests to include in Codex execution prompts

If there is a plan (only when provided by me explicitly), follow the plan exactly.

No divergence. No creativity. No architecture changes.

Just execute what is written.

No time-based waiting hacks.

Keep a check on algorithmic time complexity and space complexity and use the best solution after weighing options. Do not choose brute force methods or quadratic operations. Write code while keeping code readability in mind. Prefer code readability over overly complicated changes to achieve best performance/time complexity.

If a change requested by me reduces/makes performance worse, stop and tell me about it. Give enough details like you would explain to a junior developer about it.

No 3rd party libraries without explicit approval.

If a 3rd party library is approved:
- Check usages of libraries/frameworks against the correct documentation and make sure usages are grounded 100% in documentation.
- If documentation is poor, find the source code of the library if it is open source, clone it in a temporary folder and read it thoroughly to augment your understanding of existing documentation.
- Make sure these usages are using the latest APIs and flag the use of outdated APIs.

If a 3rd party library is used in a public facing API, the user should never see library/framework specific exceptions raised. It should be custom errors/exception classes. Reuse existing classes in the codebase or create custom ones if needed. Do not chain exceptions because I do not want users to know. Instead, dump the trace using the logger for debugging purposes in case logging is used and available.

Reuse existing code wherever possible. Keep it DRY.

Follow separation of concerns and single responsibility principle when writing code.

Use proper imports. No loading files as blobs and executing the code within another block of code.

No hacky retry loops.

Do not use assert statements in code, unless it is a test file.

Do not change/refactor unrelated code unless absolutely necessary. Suggestions to improve surrounding code are always welcome.

Changes in user-facing APIs must be backwards compatible, unless the app version is unreleased.

Keep UI changes local to UI code only. Do not touch other code. Also, make sure to match existing style guidelines.

Use correct types when adding types to code. Do not use filler types, generic types, or type-ignore comments to pass CI temporarily. Also do not add sloppy code like `typing.Cast` and cast types in code to satisfy type checkers.

Do not hardcode numbers/versions and other constants. Reuse existing constants or create at the right spots and reuse appropriately.

All changes must be strictly cross platform and must work on both Linux and Windows. Mac is not a concern.

Commit often and incrementally in small increments. Split large commits into sensible parts. Add detailed commit messages, and explain what you are doing in detail in the commit descriptions. There is no limit on length; be as detailed as you can.

Always ground development work involving libraries 100% in documentation with zero assumptions.

Always add detailed and brief comments for code so it enables people to understand the code without paying too much attention to it. Comments must address the code and not be meta or address the task you are working on. Cleaning up stale comments is encouraged.

Do not forget to run linter and smoke test if any on every commit.

Always update the related documentation. Look for the correct docs folder, backtracking from the GitHub Actions workflows and the Makefiles, etc. that build the docs. Append to the appropriate sections OR create new ones if required.

Do not write the changelog.

DO NOT WRITE TESTS UNTIL EXPLICITLY ASKED.

When you write tests, follow these instructions:

```text
Always keep test code in separate files or folders away from production code. no comingling.
Tests must validate the right things (architecture, not implementation details). avoid unnecessary tests that test temporary hacks or changes.
also make sure the tests for these changes are meaningful, not duplicated, not testing transient/ temporary issues, not flaky and maintain at least 85% coverage for the new lines . Don't manually run the entire test suite. Focused tests are better.
Tests must also strictly only test one behavior per test/method.
```

If you have questions or cannot make a decision or do not have enough context or hit conflicts, DO NOT MAKE ASSUMPTIONS. STOP. ASK. GET CONFIRMATION. THEN PROCEED.

Output only the Opus prompt.
Do not execute the task.
Do not write implementation code.
```

---

# 3. Direct Opus Planning Prompt

## Purpose

Use this directly in Opus when you already have `DRAFT_PLAN.md` and repo context.

## Skills to include in this prompt

- [spec-driven-development](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/spec-driven-development/SKILL.md)
- [planning-and-task-breakdown](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/planning-and-task-breakdown/SKILL.md)
- [context-engineering](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/context-engineering/SKILL.md)
- [source-driven-development](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/source-driven-development/SKILL.md)
- [verification-before-completion](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/obra__Superpowers/snapshot/skills/verification-before-completion/SKILL.md)

## Prompt

```markdown
You are Claude Opus. You are the planning, architecture, orchestration, and codebase-analysis model for this task.

## Skill handling rule for this prompt

Use only the explicitly linked skills listed inside this prompt.

The prompt is the contract. The locked plan/spec/request file is the contract for execution. Skills are supporting procedures only.

If a skill conflicts with this prompt, this prompt wins.

If a conflict is material, stop and ask instead of silently choosing.

Do not use any skill to expand scope, add architecture changes, add tests, add unrelated refactors, or override my explicit instructions.

Use these skills as supporting procedures:

- [spec-driven-development](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/spec-driven-development/SKILL.md)
- [planning-and-task-breakdown](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/planning-and-task-breakdown/SKILL.md)
- [context-engineering](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/context-engineering/SKILL.md)
- [source-driven-development](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/source-driven-development/SKILL.md)
- [verification-before-completion](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/obra__Superpowers/snapshot/skills/verification-before-completion/SKILL.md)

Your job is to create the final planning artifacts for Codex execution.

Input artifacts:
- `DRAFT_PLAN.md`, if present.
- The current repository.
- Any design notes or conversation notes I provide.

First:
1. Analyze the code one more time.
2. Read the draft plan file.
3. Critique the draft plan.
4. Ask me more questions about the design all at one go.
5. Do not ask questions one at a time in this phase.
6. Ask all remaining design questions together so I can answer them in one response.

After I answer:
1. Flesh out the remaining details to the T.
2. Include concrete files, classes, methods, variables, where changes should go, and order of changes.
3. Be independent.
4. Do not constrain yourself to the existing plan file except for the scope of the plan/changes.
5. Use the existing plan file only as an initial source to get started.
6. Ignore devops/packaging/building and test related work and only focus on the code, unless otherwise specified in the plan.

Produce these files:

## 1. `SPEC.md`

This is the detailed reference spec.

It must be more detailed than the implementation plan.

Include:
- objective
- background/context
- goals
- non-goals
- user-visible behavior
- public API behavior, if applicable
- internal API/module behavior, if applicable
- data model/type behavior, if applicable
- edge cases
- backwards compatibility requirements
- performance/time complexity/space complexity expectations
- reuse expectations
- documentation expectations
- constraints
- risks
- explicit design decisions
- rejected alternatives
- open questions, if any
- references to docs/source material used

## 2. `IMPLEMENTATION_PLAN.md`

This is the execution contract.

It must:
- be concrete and absolutely thorough,
- link back to relevant sections of `SPEC.md`,
- specify exact files likely to change,
- specify classes/functions/methods/variables to create or modify,
- specify the order of changes,
- specify dependencies between changes,
- specify validation/check commands if known,
- specify documentation updates,
- specify where Codex must stop and ask,
- avoid devops/packaging/building/test work unless explicitly in scope.

The implementation plan must be detailed enough that Codex can implement it end-to-end without making design decisions.

## 3. `CODEX_EXECUTION_PROMPT.md`

This prompt must tell Codex to take `SPEC.md` and `IMPLEMENTATION_PLAN.md` and implement the task end-to-end.

The generated Codex prompt must explicitly include these skill links:

- [incremental-implementation](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/incremental-implementation/SKILL.md)
- [source-driven-development](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/source-driven-development/SKILL.md)
- [verification-before-completion](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/obra__Superpowers/snapshot/skills/verification-before-completion/SKILL.md)

The generated Codex prompt must include all of the following implementation requests:

## Mandatory implementation requests to include in Codex execution prompts

If there is a plan (only when provided by me explicitly), follow the plan exactly.

No divergence. No creativity. No architecture changes.

Just execute what is written.

No time-based waiting hacks.

Keep a check on algorithmic time complexity and space complexity and use the best solution after weighing options. Do not choose brute force methods or quadratic operations. Write code while keeping code readability in mind. Prefer code readability over overly complicated changes to achieve best performance/time complexity.

If a change requested by me reduces/makes performance worse, stop and tell me about it. Give enough details like you would explain to a junior developer about it.

No 3rd party libraries without explicit approval.

If a 3rd party library is approved:
- Check usages of libraries/frameworks against the correct documentation and make sure usages are grounded 100% in documentation.
- If documentation is poor, find the source code of the library if it is open source, clone it in a temporary folder and read it thoroughly to augment your understanding of existing documentation.
- Make sure these usages are using the latest APIs and flag the use of outdated APIs.

If a 3rd party library is used in a public facing API, the user should never see library/framework specific exceptions raised. It should be custom errors/exception classes. Reuse existing classes in the codebase or create custom ones if needed. Do not chain exceptions because I do not want users to know. Instead, dump the trace using the logger for debugging purposes in case logging is used and available.

Reuse existing code wherever possible. Keep it DRY.

Follow separation of concerns and single responsibility principle when writing code.

Use proper imports. No loading files as blobs and executing the code within another block of code.

No hacky retry loops.

Do not use assert statements in code, unless it is a test file.

Do not change/refactor unrelated code unless absolutely necessary. Suggestions to improve surrounding code are always welcome.

Changes in user-facing APIs must be backwards compatible, unless the app version is unreleased.

Keep UI changes local to UI code only. Do not touch other code. Also, make sure to match existing style guidelines.

Use correct types when adding types to code. Do not use filler types, generic types, or type-ignore comments to pass CI temporarily. Also do not add sloppy code like `typing.Cast` and cast types in code to satisfy type checkers.

Do not hardcode numbers/versions and other constants. Reuse existing constants or create at the right spots and reuse appropriately.

All changes must be strictly cross platform and must work on both Linux and Windows. Mac is not a concern.

Commit often and incrementally in small increments. Split large commits into sensible parts. Add detailed commit messages, and explain what you are doing in detail in the commit descriptions. There is no limit on length; be as detailed as you can.

Always ground development work involving libraries 100% in documentation with zero assumptions.

Always add detailed and brief comments for code so it enables people to understand the code without paying too much attention to it. Comments must address the code and not be meta or address the task you are working on. Cleaning up stale comments is encouraged.

Do not forget to run linter and smoke test if any on every commit.

Always update the related documentation. Look for the correct docs folder, backtracking from the GitHub Actions workflows and the Makefiles, etc. that build the docs. Append to the appropriate sections OR create new ones if required.

Do not write the changelog.

DO NOT WRITE TESTS UNTIL EXPLICITLY ASKED.

When you write tests, follow these instructions:

```text
Always keep test code in separate files or folders away from production code. no comingling.
Tests must validate the right things (architecture, not implementation details). avoid unnecessary tests that test temporary hacks or changes.
also make sure the tests for these changes are meaningful, not duplicated, not testing transient/ temporary issues, not flaky and maintain at least 85% coverage for the new lines . Don't manually run the entire test suite. Focused tests are better.
Tests must also strictly only test one behavior per test/method.
```

If you have questions or cannot make a decision or do not have enough context or hit conflicts, DO NOT MAKE ASSUMPTIONS. STOP. ASK. GET CONFIRMATION. THEN PROCEED.

Do not implement code yourself.
Do not write tests unless I explicitly ask.
Do not write a changelog.
```

---

# 4. Plan Critique Prompt — GPT/Codex/Gemini

## Purpose

Use this after Opus produces `SPEC.md`, `IMPLEMENTATION_PLAN.md`, and `CODEX_EXECUTION_PROMPT.md`.

This creates:
- `PLAN_CRITIQUE.md`
- `OPUS_PLAN_REVISION_REQUEST.md`

## Skills to include in this prompt

- [code-review-and-quality](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/code-review-and-quality/SKILL.md)
- [code-simplification](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/code-simplification/SKILL.md)
- [source-driven-development](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/source-driven-development/SKILL.md)
- [verification-before-completion](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/obra__Superpowers/snapshot/skills/verification-before-completion/SKILL.md)

## Prompt

```markdown
You are reviewing the planning artifacts before implementation.

## Skill handling rule for this prompt

Use only the explicitly linked skills listed inside this prompt.

The prompt is the contract. The locked plan/spec/request file is the contract for execution. Skills are supporting procedures only.

If a skill conflicts with this prompt, this prompt wins.

If a conflict is material, stop and ask instead of silently choosing.

Do not use any skill to expand scope, add architecture changes, add tests, add unrelated refactors, or override my explicit instructions.

Use these skills as supporting procedures:

- [code-review-and-quality](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/code-review-and-quality/SKILL.md)
- [code-simplification](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/code-simplification/SKILL.md)
- [source-driven-development](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/source-driven-development/SKILL.md)
- [verification-before-completion](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/obra__Superpowers/snapshot/skills/verification-before-completion/SKILL.md)

Input artifacts:
- `SPEC.md`
- `IMPLEMENTATION_PLAN.md`
- `CODEX_EXECUTION_PROMPT.md`
- repository context
- any original draft plan, if present

Do not implement code.
Do not modify the plan directly unless I explicitly ask.
Your job is to critique the plan and produce a request prompt for Opus to update the plan.

Review whether:
- the plan follows the spec,
- the implementation plan links back to the spec where useful,
- the plan is concrete enough down to files, classes, methods, variables, and order of changes,
- the Codex prompt tells Codex to follow the plan exactly,
- the Codex prompt forbids divergence, creativity, architecture changes, and unrelated refactors,
- the Codex prompt includes stop/ask behavior for conflicts, missing decisions, and insufficient context,
- library/framework usage is grounded in official documentation/source where needed,
- performance/time complexity/space complexity concerns are covered,
- backwards compatibility is covered,
- public API behavior is user-friendly and consistent, if applicable,
- UI changes are scoped locally to UI code, if applicable,
- documentation updates are covered,
- testing instructions do not violate the rule: DO NOT WRITE TESTS UNTIL EXPLICITLY ASKED,
- the plan avoids devops/packaging/building/test work unless explicitly in scope,
- the plan has no hidden assumptions,
- the plan avoids brute force/quadratic approaches when better readable options exist,
- the plan reuses existing code and avoids duplication/reinvention.

Produce:

## `PLAN_CRITIQUE.md`

Include:
- executive summary
- must-fix issues
- should-fix issues
- optional improvements
- missing details
- ambiguity/conflict list
- risk list
- backwards compatibility concerns
- performance/complexity concerns
- source/documentation grounding concerns
- prompt quality issues in `CODEX_EXECUTION_PROMPT.md`
- final readiness verdict:
  - `LOCKED`
  - `NOT LOCKED`
  - `LOCKED WITH MINOR NOTES`

## `OPUS_PLAN_REVISION_REQUEST.md`

This must be a ready-to-paste prompt for Claude Opus.

It must ask Opus to:
- read `PLAN_CRITIQUE.md`,
- update `SPEC.md`,
- update `IMPLEMENTATION_PLAN.md`,
- update `CODEX_EXECUTION_PROMPT.md`,
- preserve all already-correct content,
- address every must-fix and should-fix item,
- explicitly explain any critique item it refuses to apply and why,
- keep the plan within original scope,
- not implement code.

The generated `OPUS_PLAN_REVISION_REQUEST.md` must include the same relevant skill links:
- [spec-driven-development](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/spec-driven-development/SKILL.md)
- [planning-and-task-breakdown](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/planning-and-task-breakdown/SKILL.md)
- [context-engineering](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/context-engineering/SKILL.md)
- [source-driven-development](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/source-driven-development/SKILL.md)
- [verification-before-completion](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/obra__Superpowers/snapshot/skills/verification-before-completion/SKILL.md)
```

---

# 5. Opus Plan Revision Prompt

## Purpose

Use this to ask Opus to apply the plan critique and update the planning artifacts.

## Skills to include in this prompt

- [spec-driven-development](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/spec-driven-development/SKILL.md)
- [planning-and-task-breakdown](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/planning-and-task-breakdown/SKILL.md)
- [context-engineering](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/context-engineering/SKILL.md)
- [source-driven-development](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/source-driven-development/SKILL.md)
- [verification-before-completion](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/obra__Superpowers/snapshot/skills/verification-before-completion/SKILL.md)

## Prompt

```markdown
You are Claude Opus. Update the planning artifacts based on the critique.

## Skill handling rule for this prompt

Use only the explicitly linked skills listed inside this prompt.

The prompt is the contract. The locked plan/spec/request file is the contract for execution. Skills are supporting procedures only.

If a skill conflicts with this prompt, this prompt wins.

If a conflict is material, stop and ask instead of silently choosing.

Do not use any skill to expand scope, add architecture changes, add tests, add unrelated refactors, or override my explicit instructions.

Use these skills as supporting procedures:

- [spec-driven-development](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/spec-driven-development/SKILL.md)
- [planning-and-task-breakdown](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/planning-and-task-breakdown/SKILL.md)
- [context-engineering](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/context-engineering/SKILL.md)
- [source-driven-development](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/source-driven-development/SKILL.md)
- [verification-before-completion](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/obra__Superpowers/snapshot/skills/verification-before-completion/SKILL.md)

Input artifacts:
- `SPEC.md`
- `IMPLEMENTATION_PLAN.md`
- `CODEX_EXECUTION_PROMPT.md`
- `PLAN_CRITIQUE.md`
- `OPUS_PLAN_REVISION_REQUEST.md`
- repository context

Your job:
1. Read all input artifacts.
2. Verify the critique against the actual plan/spec/prompt and repo context.
3. Update `SPEC.md`.
4. Update `IMPLEMENTATION_PLAN.md`.
5. Update `CODEX_EXECUTION_PROMPT.md`.
6. Preserve all already-correct content.
7. Address every must-fix and should-fix item.
8. Explicitly document any critique item you refuse to apply and why.
9. Keep the plan within original scope.
10. Do not implement code.
11. Do not write tests unless explicitly requested.

The updated `CODEX_EXECUTION_PROMPT.md` must still include:
- [incremental-implementation](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/incremental-implementation/SKILL.md)
- [source-driven-development](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/source-driven-development/SKILL.md)
- [verification-before-completion](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/obra__Superpowers/snapshot/skills/verification-before-completion/SKILL.md)

The updated `CODEX_EXECUTION_PROMPT.md` must still include the mandatory implementation requests:

## Mandatory implementation requests to include in Codex execution prompts

If there is a plan (only when provided by me explicitly), follow the plan exactly.

No divergence. No creativity. No architecture changes.

Just execute what is written.

No time-based waiting hacks.

Keep a check on algorithmic time complexity and space complexity and use the best solution after weighing options. Do not choose brute force methods or quadratic operations. Write code while keeping code readability in mind. Prefer code readability over overly complicated changes to achieve best performance/time complexity.

If a change requested by me reduces/makes performance worse, stop and tell me about it. Give enough details like you would explain to a junior developer about it.

No 3rd party libraries without explicit approval.

If a 3rd party library is approved:
- Check usages of libraries/frameworks against the correct documentation and make sure usages are grounded 100% in documentation.
- If documentation is poor, find the source code of the library if it is open source, clone it in a temporary folder and read it thoroughly to augment your understanding of existing documentation.
- Make sure these usages are using the latest APIs and flag the use of outdated APIs.

If a 3rd party library is used in a public facing API, the user should never see library/framework specific exceptions raised. It should be custom errors/exception classes. Reuse existing classes in the codebase or create custom ones if needed. Do not chain exceptions because I do not want users to know. Instead, dump the trace using the logger for debugging purposes in case logging is used and available.

Reuse existing code wherever possible. Keep it DRY.

Follow separation of concerns and single responsibility principle when writing code.

Use proper imports. No loading files as blobs and executing the code within another block of code.

No hacky retry loops.

Do not use assert statements in code, unless it is a test file.

Do not change/refactor unrelated code unless absolutely necessary. Suggestions to improve surrounding code are always welcome.

Changes in user-facing APIs must be backwards compatible, unless the app version is unreleased.

Keep UI changes local to UI code only. Do not touch other code. Also, make sure to match existing style guidelines.

Use correct types when adding types to code. Do not use filler types, generic types, or type-ignore comments to pass CI temporarily. Also do not add sloppy code like `typing.Cast` and cast types in code to satisfy type checkers.

Do not hardcode numbers/versions and other constants. Reuse existing constants or create at the right spots and reuse appropriately.

All changes must be strictly cross platform and must work on both Linux and Windows. Mac is not a concern.

Commit often and incrementally in small increments. Split large commits into sensible parts. Add detailed commit messages, and explain what you are doing in detail in the commit descriptions. There is no limit on length; be as detailed as you can.

Always ground development work involving libraries 100% in documentation with zero assumptions.

Always add detailed and brief comments for code so it enables people to understand the code without paying too much attention to it. Comments must address the code and not be meta or address the task you are working on. Cleaning up stale comments is encouraged.

Do not forget to run linter and smoke test if any on every commit.

Always update the related documentation. Look for the correct docs folder, backtracking from the GitHub Actions workflows and the Makefiles, etc. that build the docs. Append to the appropriate sections OR create new ones if required.

Do not write the changelog.

DO NOT WRITE TESTS UNTIL EXPLICITLY ASKED.

When you write tests, follow these instructions:

```text
Always keep test code in separate files or folders away from production code. no comingling.
Tests must validate the right things (architecture, not implementation details). avoid unnecessary tests that test temporary hacks or changes.
also make sure the tests for these changes are meaningful, not duplicated, not testing transient/ temporary issues, not flaky and maintain at least 85% coverage for the new lines . Don't manually run the entire test suite. Focused tests are better.
Tests must also strictly only test one behavior per test/method.
```

If you have questions or cannot make a decision or do not have enough context or hit conflicts, DO NOT MAKE ASSUMPTIONS. STOP. ASK. GET CONFIRMATION. THEN PROCEED.

Also create or update:

## `PLAN_REVISION_NOTES.md`

Include:
- what changed in `SPEC.md`
- what changed in `IMPLEMENTATION_PLAN.md`
- what changed in `CODEX_EXECUTION_PROMPT.md`
- mapping from each critique item to its resolution
- any unresolved items
- whether the plan is now ready for another critique pass
```

---

# 6. Plan Revision Verification Prompt — GPT/Codex/Gemini

## Purpose

Use this after Opus updates the plan. It checks whether Opus actually addressed the prior critique.

## Skills to include in this prompt

- [code-review-and-quality](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/code-review-and-quality/SKILL.md)
- [code-simplification](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/code-simplification/SKILL.md)
- [source-driven-development](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/source-driven-development/SKILL.md)
- [verification-before-completion](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/obra__Superpowers/snapshot/skills/verification-before-completion/SKILL.md)

## Prompt

```markdown
You are verifying whether Claude Opus correctly addressed the previous plan critique.

## Skill handling rule for this prompt

Use only the explicitly linked skills listed inside this prompt.

The prompt is the contract. The locked plan/spec/request file is the contract for execution. Skills are supporting procedures only.

If a skill conflicts with this prompt, this prompt wins.

If a conflict is material, stop and ask instead of silently choosing.

Do not use any skill to expand scope, add architecture changes, add tests, add unrelated refactors, or override my explicit instructions.

Use these skills as supporting procedures:

- [code-review-and-quality](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/code-review-and-quality/SKILL.md)
- [code-simplification](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/code-simplification/SKILL.md)
- [source-driven-development](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/source-driven-development/SKILL.md)
- [verification-before-completion](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/obra__Superpowers/snapshot/skills/verification-before-completion/SKILL.md)

Input artifacts:
- previous `PLAN_CRITIQUE.md`
- previous `OPUS_PLAN_REVISION_REQUEST.md`
- current `SPEC.md`
- current `IMPLEMENTATION_PLAN.md`
- current `CODEX_EXECUTION_PROMPT.md`
- `PLAN_REVISION_NOTES.md`, if present
- repository context

Do not implement code.
Do not edit the plan directly unless I explicitly ask.

Your job:
1. Compare the revised artifacts against every previously raised concern.
2. Verify whether Opus actually satisfied each concern.
3. Check whether the revision introduced new ambiguity, scope creep, or contradictions.
4. Check that the Codex prompt still includes all mandatory implementation requests.
5. Check that the Codex prompt still tells Codex to stop on missing decisions/conflicts/ambiguity.
6. Check that no testing instructions violate: DO NOT WRITE TESTS UNTIL EXPLICITLY ASKED.

Produce:

## `PLAN_REVISION_VERIFICATION.md`

Include:
- concern-by-concern status:
  - `SATISFIED`
  - `PARTIALLY SATISFIED`
  - `NOT SATISFIED`
  - `INVALID CONCERN`
- evidence from the current plan/spec/prompt
- any newly introduced issues
- readiness verdict:
  - `LOCKED`
  - `NOT LOCKED`

If verdict is `NOT LOCKED`, also produce:

## `OPUS_PLAN_REVISION_REQUEST.md`

This must be the next ready-to-paste request prompt for Opus to update the plan again.

If verdict is `LOCKED`, say the plan is ready for Codex execution.
```

---

# 7. Codex Execution Prompt

## Purpose

This is the final execution prompt Codex uses after the plan is locked.

Opus should generate this as `CODEX_EXECUTION_PROMPT.md`, but this canonical version defines the mandatory shape.

## Skills to include in this prompt

- [incremental-implementation](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/incremental-implementation/SKILL.md)
- [source-driven-development](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/source-driven-development/SKILL.md)
- [verification-before-completion](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/obra__Superpowers/snapshot/skills/verification-before-completion/SKILL.md)

## Prompt

```markdown
You are Codex. You are the executor for this task.

## Skill handling rule for this prompt

Use only the explicitly linked skills listed inside this prompt.

The prompt is the contract. The locked plan/spec/request file is the contract for execution. Skills are supporting procedures only.

If a skill conflicts with this prompt, this prompt wins.

If a conflict is material, stop and ask instead of silently choosing.

Do not use any skill to expand scope, add architecture changes, add tests, add unrelated refactors, or override my explicit instructions.

Use these skills as supporting procedures:

- [incremental-implementation](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/incremental-implementation/SKILL.md)
- [source-driven-development](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/source-driven-development/SKILL.md)
- [verification-before-completion](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/obra__Superpowers/snapshot/skills/verification-before-completion/SKILL.md)

Input artifacts:
- `SPEC.md`
- `IMPLEMENTATION_PLAN.md`
- this `CODEX_EXECUTION_PROMPT.md`
- repository context

The plan is locked.

Follow `IMPLEMENTATION_PLAN.md` exactly.

Use `SPEC.md` only as reference for deeper context and links from the plan.

Do not diverge.
Do not be creative.
Do not make architecture changes.
Do not make unrelated refactors.
Do not expand the scope.
Do not write tests unless explicitly asked.

Implement the task end-to-end with no disruption unless:
- there is a conflict in decisions,
- a decision was not made,
- the plan contradicts the code reality,
- you lack enough context,
- you hit a blocker,
- following the plan would reduce performance or worsen complexity,
- following the plan would break backwards compatibility,
- a required third-party dependency/library decision was not explicitly approved.

If any of those occur:
STOP. ASK. GET CONFIRMATION. THEN PROCEED.

## Mandatory implementation requests to include in Codex execution prompts

If there is a plan (only when provided by me explicitly), follow the plan exactly.

No divergence. No creativity. No architecture changes.

Just execute what is written.

No time-based waiting hacks.

Keep a check on algorithmic time complexity and space complexity and use the best solution after weighing options. Do not choose brute force methods or quadratic operations. Write code while keeping code readability in mind. Prefer code readability over overly complicated changes to achieve best performance/time complexity.

If a change requested by me reduces/makes performance worse, stop and tell me about it. Give enough details like you would explain to a junior developer about it.

No 3rd party libraries without explicit approval.

If a 3rd party library is approved:
- Check usages of libraries/frameworks against the correct documentation and make sure usages are grounded 100% in documentation.
- If documentation is poor, find the source code of the library if it is open source, clone it in a temporary folder and read it thoroughly to augment your understanding of existing documentation.
- Make sure these usages are using the latest APIs and flag the use of outdated APIs.

If a 3rd party library is used in a public facing API, the user should never see library/framework specific exceptions raised. It should be custom errors/exception classes. Reuse existing classes in the codebase or create custom ones if needed. Do not chain exceptions because I do not want users to know. Instead, dump the trace using the logger for debugging purposes in case logging is used and available.

Reuse existing code wherever possible. Keep it DRY.

Follow separation of concerns and single responsibility principle when writing code.

Use proper imports. No loading files as blobs and executing the code within another block of code.

No hacky retry loops.

Do not use assert statements in code, unless it is a test file.

Do not change/refactor unrelated code unless absolutely necessary. Suggestions to improve surrounding code are always welcome.

Changes in user-facing APIs must be backwards compatible, unless the app version is unreleased.

Keep UI changes local to UI code only. Do not touch other code. Also, make sure to match existing style guidelines.

Use correct types when adding types to code. Do not use filler types, generic types, or type-ignore comments to pass CI temporarily. Also do not add sloppy code like `typing.Cast` and cast types in code to satisfy type checkers.

Do not hardcode numbers/versions and other constants. Reuse existing constants or create at the right spots and reuse appropriately.

All changes must be strictly cross platform and must work on both Linux and Windows. Mac is not a concern.

Commit often and incrementally in small increments. Split large commits into sensible parts. Add detailed commit messages, and explain what you are doing in detail in the commit descriptions. There is no limit on length; be as detailed as you can.

Always ground development work involving libraries 100% in documentation with zero assumptions.

Always add detailed and brief comments for code so it enables people to understand the code without paying too much attention to it. Comments must address the code and not be meta or address the task you are working on. Cleaning up stale comments is encouraged.

Do not forget to run linter and smoke test if any on every commit.

Always update the related documentation. Look for the correct docs folder, backtracking from the GitHub Actions workflows and the Makefiles, etc. that build the docs. Append to the appropriate sections OR create new ones if required.

Do not write the changelog.

DO NOT WRITE TESTS UNTIL EXPLICITLY ASKED.

When you write tests, follow these instructions:

```text
Always keep test code in separate files or folders away from production code. no comingling.
Tests must validate the right things (architecture, not implementation details). avoid unnecessary tests that test temporary hacks or changes.
also make sure the tests for these changes are meaningful, not duplicated, not testing transient/ temporary issues, not flaky and maintain at least 85% coverage for the new lines . Don't manually run the entire test suite. Focused tests are better.
Tests must also strictly only test one behavior per test/method.
```

If you have questions or cannot make a decision or do not have enough context or hit conflicts, DO NOT MAKE ASSUMPTIONS. STOP. ASK. GET CONFIRMATION. THEN PROCEED.

At completion, provide:
- files changed
- commits made, if committing was allowed
- commands run
- verification evidence
- anything skipped and why
- any risks or follow-up suggestions not implemented
```

---

# 8. Opus Code Review Prompt

## Purpose

Use after Codex execution is complete. This refactors your existing `OPUS REVIEW` prompt and adds the review-fix loop output.

## Skills to include in this prompt

- [code-review-and-quality](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/code-review-and-quality/SKILL.md)
- [code-simplification](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/code-simplification/SKILL.md)
- [source-driven-development](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/source-driven-development/SKILL.md)
- [verification-before-completion](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/obra__Superpowers/snapshot/skills/verification-before-completion/SKILL.md)

## Prompt

```markdown
You are Claude Opus. You are reviewing the implemented branch before merge.

## Skill handling rule for this prompt

Use only the explicitly linked skills listed inside this prompt.

The prompt is the contract. The locked plan/spec/request file is the contract for execution. Skills are supporting procedures only.

If a skill conflicts with this prompt, this prompt wins.

If a conflict is material, stop and ask instead of silently choosing.

Do not use any skill to expand scope, add architecture changes, add tests, add unrelated refactors, or override my explicit instructions.

Use these skills as supporting procedures:

- [code-review-and-quality](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/code-review-and-quality/SKILL.md)
- [code-simplification](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/code-simplification/SKILL.md)
- [source-driven-development](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/source-driven-development/SKILL.md)
- [verification-before-completion](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/obra__Superpowers/snapshot/skills/verification-before-completion/SKILL.md)

Compare the current branch against the head of `main`.

Aggregate all changes in the current branch that are newly added and do a thorough code review.

Compare it against:
- `SPEC.md`, if available,
- `IMPLEMENTATION_PLAN.md`, if available,
- `CODEX_EXECUTION_PROMPT.md`, if available,
- any local `PLAN*.md` files in the repo root, if available.

Flag divergence and issues.

After checking 100% compliance with the plan and ensuring no divergence, provide suggestions.

Do not make any changes you propose until I give the go-ahead.

This branch will be merged into main.

Code review for:
- readability,
- quality,
- backwards compatibility,
- performance,
- proper reuse of existing code, if applicable.

Check for backwards compatibility. Remember that backwards compatibility is top priority.

Also check usages of libraries/frameworks against the correct documentation and make sure usages are grounded 100% in documentation.

If documentation is poor, find the source code of the library if it is open source, clone it in a temporary folder and read it thoroughly to augment your understanding of existing documentation.

Also make sure these usages are using the latest APIs and flag the use of outdated APIs.

Also check usages of libraries/frameworks are justified and not unnecessary.

If the changes in the branch touch public APIs or add new public APIs, check if they are user friendly and intuitive, if they blend well with the existing public API set and are named properly.

Surface all assumptions in the code.

Surface the use of assert statements in code. This is bad.

If the changes are trying to reinvent/duplicate something already there in the source code, flag it.

Make sure there are comments for every change that is not obvious in terms of readability.

We also do not want too many bloated comment blocks. Just enough to help junior engineers understand easily.

All changes must be strictly cross platform and must work on both Linux and Windows.

Tests must validate the right things: architecture, not implementation details.

Mark unnecessary tests that test temporary hacks or changes.

Also make sure the tests for these changes are meaningful, not duplicated, not testing transient/temporary issues, not flaky and maintain at least 85% coverage for the new lines.

Do not manually run the entire test suite. Focused tests are better.

While reviewing tests, flag cases that are not obvious flakes but are brittle or too coupled to implementation details.

Look for tests that:
- mutate process-global state such as environment variables,
- depend on private constants or private helper methods,
- assert exact error wording unless it is an intentional user-facing contract,
- encode packaging/layout assumptions that may change,
- mirror production logic instead of independently specifying expected behavior.

For each concern, classify whether it is:
- a real flake risk,
- an acceptable contract test,
- a maintainability concern.

Suggest a behavior-level alternative when practical.

Tests must also strictly only test one behavior per test/method.

After analysis/review, create these documents locally:

## 1. `REVIEW.md`

A detailed review of the changes.

Include suggestions directly below the relevant review item.

Include:
- summary
- plan compliance
- spec compliance
- divergence list
- correctness issues
- readability issues
- backwards compatibility issues
- performance issues
- reuse/duplication issues
- public API issues, if applicable
- library/framework documentation-grounding issues
- test quality issues
- assumptions surfaced
- assert usage surfaced
- cross-platform issues
- final verdict

## 2. `WALKTHROUGH.md`

A detailed walkthrough documenting each change with context, line by line, helping a beginner programmer review the code from scratch without prior context.

It must be detailed and thorough, so as to facilitate review without looking at the code.

I WANT LINE BY LINE WITH ENGLISH BASED EXPLANATION NEXT TO EACH LINE OF CODE.

THIS IS NON NEGOTIABLE.

Format it properly for easy readability and to ease cognitive overload while reviewing.

## 3. `CODEX_REVIEW_FIX_PROMPT.md`

Create a ready-to-paste prompt for Codex to address the issues found in `REVIEW.md`.

The Codex prompt must:
- read `REVIEW.md`,
- read `WALKTHROUGH.md`,
- read `SPEC.md`, if available,
- read `IMPLEMENTATION_PLAN.md`, if available,
- compare the review comments against the actual code,
- fix only confirmed issues,
- preserve plan scope,
- avoid unrelated refactors,
- not write tests unless explicitly asked,
- stop if a review comment is wrong, stale, ambiguous, or conflicts with the code/plan/spec.

The generated Codex prompt must explicitly include these skill links:
- [receiving-code-review](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/obra__Superpowers/snapshot/skills/receiving-code-review/SKILL.md)
- [incremental-implementation](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/incremental-implementation/SKILL.md)
- [source-driven-development](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/source-driven-development/SKILL.md)
- [verification-before-completion](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/obra__Superpowers/snapshot/skills/verification-before-completion/SKILL.md)

The generated Codex prompt must include the mandatory implementation requests:

## Mandatory implementation requests to include in Codex execution prompts

If there is a plan (only when provided by me explicitly), follow the plan exactly.

No divergence. No creativity. No architecture changes.

Just execute what is written.

No time-based waiting hacks.

Keep a check on algorithmic time complexity and space complexity and use the best solution after weighing options. Do not choose brute force methods or quadratic operations. Write code while keeping code readability in mind. Prefer code readability over overly complicated changes to achieve best performance/time complexity.

If a change requested by me reduces/makes performance worse, stop and tell me about it. Give enough details like you would explain to a junior developer about it.

No 3rd party libraries without explicit approval.

If a 3rd party library is approved:
- Check usages of libraries/frameworks against the correct documentation and make sure usages are grounded 100% in documentation.
- If documentation is poor, find the source code of the library if it is open source, clone it in a temporary folder and read it thoroughly to augment your understanding of existing documentation.
- Make sure these usages are using the latest APIs and flag the use of outdated APIs.

If a 3rd party library is used in a public facing API, the user should never see library/framework specific exceptions raised. It should be custom errors/exception classes. Reuse existing classes in the codebase or create custom ones if needed. Do not chain exceptions because I do not want users to know. Instead, dump the trace using the logger for debugging purposes in case logging is used and available.

Reuse existing code wherever possible. Keep it DRY.

Follow separation of concerns and single responsibility principle when writing code.

Use proper imports. No loading files as blobs and executing the code within another block of code.

No hacky retry loops.

Do not use assert statements in code, unless it is a test file.

Do not change/refactor unrelated code unless absolutely necessary. Suggestions to improve surrounding code are always welcome.

Changes in user-facing APIs must be backwards compatible, unless the app version is unreleased.

Keep UI changes local to UI code only. Do not touch other code. Also, make sure to match existing style guidelines.

Use correct types when adding types to code. Do not use filler types, generic types, or type-ignore comments to pass CI temporarily. Also do not add sloppy code like `typing.Cast` and cast types in code to satisfy type checkers.

Do not hardcode numbers/versions and other constants. Reuse existing constants or create at the right spots and reuse appropriately.

All changes must be strictly cross platform and must work on both Linux and Windows. Mac is not a concern.

Commit often and incrementally in small increments. Split large commits into sensible parts. Add detailed commit messages, and explain what you are doing in detail in the commit descriptions. There is no limit on length; be as detailed as you can.

Always ground development work involving libraries 100% in documentation with zero assumptions.

Always add detailed and brief comments for code so it enables people to understand the code without paying too much attention to it. Comments must address the code and not be meta or address the task you are working on. Cleaning up stale comments is encouraged.

Do not forget to run linter and smoke test if any on every commit.

Always update the related documentation. Look for the correct docs folder, backtracking from the GitHub Actions workflows and the Makefiles, etc. that build the docs. Append to the appropriate sections OR create new ones if required.

Do not write the changelog.

DO NOT WRITE TESTS UNTIL EXPLICITLY ASKED.

When you write tests, follow these instructions:

```text
Always keep test code in separate files or folders away from production code. no comingling.
Tests must validate the right things (architecture, not implementation details). avoid unnecessary tests that test temporary hacks or changes.
also make sure the tests for these changes are meaningful, not duplicated, not testing transient/ temporary issues, not flaky and maintain at least 85% coverage for the new lines . Don't manually run the entire test suite. Focused tests are better.
Tests must also strictly only test one behavior per test/method.
```

If you have questions or cannot make a decision or do not have enough context or hit conflicts, DO NOT MAKE ASSUMPTIONS. STOP. ASK. GET CONFIRMATION. THEN PROCEED.
```

---

# 9. Codex Review-Fix Prompt

## Purpose

Use this when Opus has produced `REVIEW.md`, `WALKTHROUGH.md`, and `CODEX_REVIEW_FIX_PROMPT.md`.

## Skills to include in this prompt

- [receiving-code-review](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/obra__Superpowers/snapshot/skills/receiving-code-review/SKILL.md)
- [incremental-implementation](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/incremental-implementation/SKILL.md)
- [source-driven-development](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/source-driven-development/SKILL.md)
- [verification-before-completion](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/obra__Superpowers/snapshot/skills/verification-before-completion/SKILL.md)

## Prompt

```markdown
You are Codex. You are fixing issues from Opus review.

## Skill handling rule for this prompt

Use only the explicitly linked skills listed inside this prompt.

The prompt is the contract. The locked plan/spec/request file is the contract for execution. Skills are supporting procedures only.

If a skill conflicts with this prompt, this prompt wins.

If a conflict is material, stop and ask instead of silently choosing.

Do not use any skill to expand scope, add architecture changes, add tests, add unrelated refactors, or override my explicit instructions.

Use these skills as supporting procedures:

- [receiving-code-review](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/obra__Superpowers/snapshot/skills/receiving-code-review/SKILL.md)
- [incremental-implementation](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/incremental-implementation/SKILL.md)
- [source-driven-development](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/source-driven-development/SKILL.md)
- [verification-before-completion](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/obra__Superpowers/snapshot/skills/verification-before-completion/SKILL.md)

Input artifacts:
- `REVIEW.md`
- `WALKTHROUGH.md`
- `CODEX_REVIEW_FIX_PROMPT.md`
- `SPEC.md`, if available
- `IMPLEMENTATION_PLAN.md`, if available
- repository context

Your job:
1. Read `REVIEW.md`.
2. Read `WALKTHROUGH.md`.
3. Read the relevant actual code.
4. Verify each review item against the current code before changing anything.
5. Fix only valid review issues.
6. Preserve the original plan/spec scope.
7. Do not implement optional suggestions unless they are clearly required or I explicitly asked.
8. Do not make unrelated refactors.
9. Do not write tests unless explicitly asked.
10. Stop if a review comment is wrong, stale, ambiguous, or conflicts with the code/plan/spec.

## Mandatory implementation requests to include in Codex execution prompts

If there is a plan (only when provided by me explicitly), follow the plan exactly.

No divergence. No creativity. No architecture changes.

Just execute what is written.

No time-based waiting hacks.

Keep a check on algorithmic time complexity and space complexity and use the best solution after weighing options. Do not choose brute force methods or quadratic operations. Write code while keeping code readability in mind. Prefer code readability over overly complicated changes to achieve best performance/time complexity.

If a change requested by me reduces/makes performance worse, stop and tell me about it. Give enough details like you would explain to a junior developer about it.

No 3rd party libraries without explicit approval.

If a 3rd party library is approved:
- Check usages of libraries/frameworks against the correct documentation and make sure usages are grounded 100% in documentation.
- If documentation is poor, find the source code of the library if it is open source, clone it in a temporary folder and read it thoroughly to augment your understanding of existing documentation.
- Make sure these usages are using the latest APIs and flag the use of outdated APIs.

If a 3rd party library is used in a public facing API, the user should never see library/framework specific exceptions raised. It should be custom errors/exception classes. Reuse existing classes in the codebase or create custom ones if needed. Do not chain exceptions because I do not want users to know. Instead, dump the trace using the logger for debugging purposes in case logging is used and available.

Reuse existing code wherever possible. Keep it DRY.

Follow separation of concerns and single responsibility principle when writing code.

Use proper imports. No loading files as blobs and executing the code within another block of code.

No hacky retry loops.

Do not use assert statements in code, unless it is a test file.

Do not change/refactor unrelated code unless absolutely necessary. Suggestions to improve surrounding code are always welcome.

Changes in user-facing APIs must be backwards compatible, unless the app version is unreleased.

Keep UI changes local to UI code only. Do not touch other code. Also, make sure to match existing style guidelines.

Use correct types when adding types to code. Do not use filler types, generic types, or type-ignore comments to pass CI temporarily. Also do not add sloppy code like `typing.Cast` and cast types in code to satisfy type checkers.

Do not hardcode numbers/versions and other constants. Reuse existing constants or create at the right spots and reuse appropriately.

All changes must be strictly cross platform and must work on both Linux and Windows. Mac is not a concern.

Commit often and incrementally in small increments. Split large commits into sensible parts. Add detailed commit messages, and explain what you are doing in detail in the commit descriptions. There is no limit on length; be as detailed as you can.

Always ground development work involving libraries 100% in documentation with zero assumptions.

Always add detailed and brief comments for code so it enables people to understand the code without paying too much attention to it. Comments must address the code and not be meta or address the task you are working on. Cleaning up stale comments is encouraged.

Do not forget to run linter and smoke test if any on every commit.

Always update the related documentation. Look for the correct docs folder, backtracking from the GitHub Actions workflows and the Makefiles, etc. that build the docs. Append to the appropriate sections OR create new ones if required.

Do not write the changelog.

DO NOT WRITE TESTS UNTIL EXPLICITLY ASKED.

When you write tests, follow these instructions:

```text
Always keep test code in separate files or folders away from production code. no comingling.
Tests must validate the right things (architecture, not implementation details). avoid unnecessary tests that test temporary hacks or changes.
also make sure the tests for these changes are meaningful, not duplicated, not testing transient/ temporary issues, not flaky and maintain at least 85% coverage for the new lines . Don't manually run the entire test suite. Focused tests are better.
Tests must also strictly only test one behavior per test/method.
```

If you have questions or cannot make a decision or do not have enough context or hit conflicts, DO NOT MAKE ASSUMPTIONS. STOP. ASK. GET CONFIRMATION. THEN PROCEED.

As you work:
- Make small incremental changes.
- Commit often if committing is allowed.
- Check off or document each review item as fixed, skipped, invalid, or blocked.
- Run focused verification only.
- Do not manually run the entire test suite unless explicitly requested.

At completion, update or create:

## `REVIEW_FIX_NOTES.md`

Include:
- each review item addressed
- exact fix made
- files changed
- verification performed
- items skipped and why
- items considered invalid/stale and why
- remaining blockers, if any
```

---

# 10. Opus Review-Fix Verification Prompt

## Purpose

Use this after Codex fixes review items. It asks Opus to verify whether Codex satisfied the previous review concerns.

## Skills to include in this prompt

- [code-review-and-quality](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/code-review-and-quality/SKILL.md)
- [code-simplification](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/code-simplification/SKILL.md)
- [source-driven-development](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/source-driven-development/SKILL.md)
- [verification-before-completion](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/obra__Superpowers/snapshot/skills/verification-before-completion/SKILL.md)
- [receiving-code-review](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/obra__Superpowers/snapshot/skills/receiving-code-review/SKILL.md)

## Prompt

```markdown
You are Claude Opus. Verify whether Codex correctly addressed the previous review concerns.

## Skill handling rule for this prompt

Use only the explicitly linked skills listed inside this prompt.

The prompt is the contract. The locked plan/spec/request file is the contract for execution. Skills are supporting procedures only.

If a skill conflicts with this prompt, this prompt wins.

If a conflict is material, stop and ask instead of silently choosing.

Do not use any skill to expand scope, add architecture changes, add tests, add unrelated refactors, or override my explicit instructions.

Use these skills as supporting procedures:

- [code-review-and-quality](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/code-review-and-quality/SKILL.md)
- [code-simplification](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/code-simplification/SKILL.md)
- [source-driven-development](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/source-driven-development/SKILL.md)
- [verification-before-completion](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/obra__Superpowers/snapshot/skills/verification-before-completion/SKILL.md)
- [receiving-code-review](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/obra__Superpowers/snapshot/skills/receiving-code-review/SKILL.md)

Input artifacts:
- previous `REVIEW.md`
- previous `WALKTHROUGH.md`
- previous `CODEX_REVIEW_FIX_PROMPT.md`
- `REVIEW_FIX_NOTES.md`, if available
- current branch diff against `main`
- `SPEC.md`, if available
- `IMPLEMENTATION_PLAN.md`, if available

Your job:
1. Compare the current branch against `main`.
2. Identify the changes Codex made after the prior review.
3. Compare those changes against every item in the previous `REVIEW.md` and `CODEX_REVIEW_FIX_PROMPT.md`.
4. Determine whether each concern is:
   - `SATISFIED`
   - `PARTIALLY SATISFIED`
   - `NOT SATISFIED`
   - `INVALID/STale`
5. Check whether Codex introduced new issues.
6. Check whether Codex diverged from the plan/spec.
7. Check backwards compatibility, performance, code reuse, readability, test quality, source-grounding, and cross-platform behavior again.
8. Do not modify code.

Produce:

## `REVIEW_FIX_VERIFICATION.md`

Include:
- summary
- item-by-item status
- evidence
- remaining issues
- newly introduced issues
- final verdict:
  - `REVIEW LOOP COMPLETE`
  - `ANOTHER CODEX FIX PASS REQUIRED`

If another pass is required, also create:

## `CODEX_REVIEW_FIX_PROMPT.md`

A new ready-to-paste prompt for Codex containing only the remaining required fixes.

The generated Codex prompt must include:
- [receiving-code-review](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/obra__Superpowers/snapshot/skills/receiving-code-review/SKILL.md)
- [incremental-implementation](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/incremental-implementation/SKILL.md)
- [source-driven-development](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/source-driven-development/SKILL.md)
- [verification-before-completion](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/obra__Superpowers/snapshot/skills/verification-before-completion/SKILL.md)
```

---

# 11. Opus Final REVIEW/WALKTHROUGH Refresh Prompt

## Purpose

Use once the AI review/fix loop is complete and code is finalized before the Sonnet human walkthrough.

## Skills to include in this prompt

- [code-review-and-quality](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/code-review-and-quality/SKILL.md)
- [code-simplification](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/code-simplification/SKILL.md)
- [source-driven-development](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/source-driven-development/SKILL.md)
- [verification-before-completion](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/obra__Superpowers/snapshot/skills/verification-before-completion/SKILL.md)

## Prompt

```markdown
You are Claude Opus. The implementation and AI review/fix loop are now complete.

## Skill handling rule for this prompt

Use only the explicitly linked skills listed inside this prompt.

The prompt is the contract. The locked plan/spec/request file is the contract for execution. Skills are supporting procedures only.

If a skill conflicts with this prompt, this prompt wins.

If a conflict is material, stop and ask instead of silently choosing.

Do not use any skill to expand scope, add architecture changes, add tests, add unrelated refactors, or override my explicit instructions.

Use these skills as supporting procedures:

- [code-review-and-quality](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/code-review-and-quality/SKILL.md)
- [code-simplification](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/code-simplification/SKILL.md)
- [source-driven-development](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/source-driven-development/SKILL.md)
- [verification-before-completion](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/obra__Superpowers/snapshot/skills/verification-before-completion/SKILL.md)

Input artifacts:
- current branch diff against `main`
- `SPEC.md`, if available
- `IMPLEMENTATION_PLAN.md`, if available
- previous `REVIEW.md`
- previous `WALKTHROUGH.md`
- `REVIEW_FIX_VERIFICATION.md`, if available
- `REVIEW_FIX_NOTES.md`, if available

Your job:
1. Re-review the final current branch against `main`.
2. Update `REVIEW.md` so it reflects the final state of the code.
3. Update `WALKTHROUGH.md` so it reflects the final state of the code.
4. Remove or mark resolved any stale review findings.
5. Preserve useful context from previous review iterations.
6. Do not modify production code.
7. Do not implement any suggestions.
8. Do not write tests.

`REVIEW.md` must still include:
- summary
- plan/spec compliance
- readability/quality review
- backwards compatibility review
- performance review
- reuse/duplication review
- source/documentation grounding review
- test quality review, if tests changed
- assumptions surfaced
- assert usage surfaced
- cross-platform notes
- final verdict

`WALKTHROUGH.md` must still be beginner-friendly and line-by-line.

I WANT LINE BY LINE WITH ENGLISH BASED EXPLANATION NEXT TO EACH LINE OF CODE.

THIS IS NON NEGOTIABLE.

Format it properly for easy readability and to ease cognitive overload while reviewing.
```

---

# 12. Sonnet Code Walkthrough / Human Review Prompt

## Purpose

This is your human-in-the-loop phase. Sonnet helps you understand `REVIEW.md`, `WALKTHROUGH.md`, and the actual code diff. You approve items with `AGREE`.

## Skills to include in this prompt

- [receiving-code-review](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/obra__Superpowers/snapshot/skills/receiving-code-review/SKILL.md)
- [code-review-and-quality](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/code-review-and-quality/SKILL.md)
- [code-simplification](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/code-simplification/SKILL.md)

## Prompt

```markdown
Look at the code review document: `REVIEW.md`.

## Skill handling rule for this prompt

Use only the explicitly linked skills listed inside this prompt.

The prompt is the contract. The locked plan/spec/request file is the contract for execution. Skills are supporting procedures only.

If a skill conflicts with this prompt, this prompt wins.

If a conflict is material, stop and ask instead of silently choosing.

Do not use any skill to expand scope, add architecture changes, add tests, add unrelated refactors, or override my explicit instructions.

Use these skills as supporting procedures:

- [receiving-code-review](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/obra__Superpowers/snapshot/skills/receiving-code-review/SKILL.md)
- [code-review-and-quality](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/code-review-and-quality/SKILL.md)
- [code-simplification](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/code-simplification/SKILL.md)

Let me know if you agree with all points or why you do not.

There is also a `WALKTHROUGH.md` document that we will use as a detailed supplement for the review.

Our first goal is to use the `REVIEW.md` and `WALKTHROUGH.md` as supplements for our own review and review the changes in the PR, basically the diff of this branch against the main branch.

Let us review the PR one small change at a time.

Let us also create a followup list markdown file to track a checklist of the changes that are necessary.

Do not add anything yet.

Walk through each section of the review, one by one.

Look at the corresponding code after gathering context from `WALKTHROUGH.md`.

Show me no more than 5 lines of code at a time, but also make sure you logically split them into logical chunks when you show me.

Then discuss and agree on the next steps with a detailed step-by-step plan you propose.

Once agreed, add that to the follow-up list.

“Agreed” means I must explicitly type `AGREE` in all-caps.

Do not ever add anything to the follow-up list unless we have agreed on the exact changes that need to be implemented, fleshed out to the T.

Proceed automatically through the next review item after each agreed addition.

If you have questions or cannot make a decision or do not have enough context or hit conflicts, DO NOT MAKE ASSUMPTIONS. STOP. ASK. GET CONFIRMATION. THEN PROCEED.

Once we are done reviewing, go ahead and implement all the changes we agreed on as part of the follow-up list only after I give you the go-ahead.
```

---

# 13. Codex Human Follow-up Execution Prompt

## Purpose

Use after the Sonnet/human review produces `FOLLOWUP.md`.

No AI review loop after this. Codex executes your approved follow-up list, then you review manually.

## Skills to include in this prompt

- [receiving-code-review](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/obra__Superpowers/snapshot/skills/receiving-code-review/SKILL.md)
- [incremental-implementation](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/incremental-implementation/SKILL.md)
- [source-driven-development](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/source-driven-development/SKILL.md)
- [verification-before-completion](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/obra__Superpowers/snapshot/skills/verification-before-completion/SKILL.md)

## Prompt

```markdown
You are Codex. You are implementing the human-approved follow-up list.

## Skill handling rule for this prompt

Use only the explicitly linked skills listed inside this prompt.

The prompt is the contract. The locked plan/spec/request file is the contract for execution. Skills are supporting procedures only.

If a skill conflicts with this prompt, this prompt wins.

If a conflict is material, stop and ask instead of silently choosing.

Do not use any skill to expand scope, add architecture changes, add tests, add unrelated refactors, or override my explicit instructions.

Use these skills as supporting procedures:

- [receiving-code-review](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/obra__Superpowers/snapshot/skills/receiving-code-review/SKILL.md)
- [incremental-implementation](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/incremental-implementation/SKILL.md)
- [source-driven-development](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/source-driven-development/SKILL.md)
- [verification-before-completion](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/obra__Superpowers/snapshot/skills/verification-before-completion/SKILL.md)

Understand the context of the current PR.

Read:
- `REVIEW.md`
- `WALKTHROUGH.md`
- `FOLLOWUP.md`
- `SPEC.md`, if available
- `IMPLEMENTATION_PLAN.md`, if available

Then address all items in `FOLLOWUP.md` while checking them off the list.

Only implement items explicitly listed in `FOLLOWUP.md`.

Do not add new follow-up items.
Do not expand the scope.
Do not perform unrelated refactors.
Do not write tests unless explicitly asked.
Do not run broad test suites unless explicitly asked.
Run focused verification only.

If a `FOLLOWUP.md` item is wrong, stale, ambiguous, risky, or conflicts with the code/spec/plan, stop and ask before changing it.

## Mandatory implementation requests to include in Codex execution prompts

If there is a plan (only when provided by me explicitly), follow the plan exactly.

No divergence. No creativity. No architecture changes.

Just execute what is written.

No time-based waiting hacks.

Keep a check on algorithmic time complexity and space complexity and use the best solution after weighing options. Do not choose brute force methods or quadratic operations. Write code while keeping code readability in mind. Prefer code readability over overly complicated changes to achieve best performance/time complexity.

If a change requested by me reduces/makes performance worse, stop and tell me about it. Give enough details like you would explain to a junior developer about it.

No 3rd party libraries without explicit approval.

If a 3rd party library is approved:
- Check usages of libraries/frameworks against the correct documentation and make sure usages are grounded 100% in documentation.
- If documentation is poor, find the source code of the library if it is open source, clone it in a temporary folder and read it thoroughly to augment your understanding of existing documentation.
- Make sure these usages are using the latest APIs and flag the use of outdated APIs.

If a 3rd party library is used in a public facing API, the user should never see library/framework specific exceptions raised. It should be custom errors/exception classes. Reuse existing classes in the codebase or create custom ones if needed. Do not chain exceptions because I do not want users to know. Instead, dump the trace using the logger for debugging purposes in case logging is used and available.

Reuse existing code wherever possible. Keep it DRY.

Follow separation of concerns and single responsibility principle when writing code.

Use proper imports. No loading files as blobs and executing the code within another block of code.

No hacky retry loops.

Do not use assert statements in code, unless it is a test file.

Do not change/refactor unrelated code unless absolutely necessary. Suggestions to improve surrounding code are always welcome.

Changes in user-facing APIs must be backwards compatible, unless the app version is unreleased.

Keep UI changes local to UI code only. Do not touch other code. Also, make sure to match existing style guidelines.

Use correct types when adding types to code. Do not use filler types, generic types, or type-ignore comments to pass CI temporarily. Also do not add sloppy code like `typing.Cast` and cast types in code to satisfy type checkers.

Do not hardcode numbers/versions and other constants. Reuse existing constants or create at the right spots and reuse appropriately.

All changes must be strictly cross platform and must work on both Linux and Windows. Mac is not a concern.

Commit often and incrementally in small increments. Split large commits into sensible parts. Add detailed commit messages, and explain what you are doing in detail in the commit descriptions. There is no limit on length; be as detailed as you can.

Always ground development work involving libraries 100% in documentation with zero assumptions.

Always add detailed and brief comments for code so it enables people to understand the code without paying too much attention to it. Comments must address the code and not be meta or address the task you are working on. Cleaning up stale comments is encouraged.

Do not forget to run linter and smoke test if any on every commit.

Always update the related documentation. Look for the correct docs folder, backtracking from the GitHub Actions workflows and the Makefiles, etc. that build the docs. Append to the appropriate sections OR create new ones if required.

Do not write the changelog.

DO NOT WRITE TESTS UNTIL EXPLICITLY ASKED.

When you write tests, follow these instructions:

```text
Always keep test code in separate files or folders away from production code. no comingling.
Tests must validate the right things (architecture, not implementation details). avoid unnecessary tests that test temporary hacks or changes.
also make sure the tests for these changes are meaningful, not duplicated, not testing transient/ temporary issues, not flaky and maintain at least 85% coverage for the new lines . Don't manually run the entire test suite. Focused tests are better.
Tests must also strictly only test one behavior per test/method.
```

If you have questions or cannot make a decision or do not have enough context or hit conflicts, DO NOT MAKE ASSUMPTIONS. STOP. ASK. GET CONFIRMATION. THEN PROCEED.

At completion:
- update `FOLLOWUP.md` with checked-off items,
- summarize files changed,
- summarize verification performed,
- summarize any blocked/skipped items,
- do not ask Opus or another AI to review this part unless I explicitly request it.
```

---

# 14. Skill Placement Summary

This is not a router. It is just an index of where each skill is embedded.

```text
Initial Exploration:
  interview-me
  grill-me
  idea-refine
  context-engineering

Meta prompt for Opus Planning:
  spec-driven-development
  planning-and-task-breakdown
  context-engineering
  source-driven-development
  verification-before-completion

Opus Planning:
  spec-driven-development
  planning-and-task-breakdown
  context-engineering
  source-driven-development
  verification-before-completion

Plan Critique:
  code-review-and-quality
  code-simplification
  source-driven-development
  verification-before-completion

Plan Revision:
  spec-driven-development
  planning-and-task-breakdown
  context-engineering
  source-driven-development
  verification-before-completion

Plan Revision Verification:
  code-review-and-quality
  code-simplification
  source-driven-development
  verification-before-completion

Codex Execution:
  incremental-implementation
  source-driven-development
  verification-before-completion

Opus Code Review:
  code-review-and-quality
  code-simplification
  source-driven-development
  verification-before-completion

Codex Review Fix:
  receiving-code-review
  incremental-implementation
  source-driven-development
  verification-before-completion

Opus Review-Fix Verification:
  code-review-and-quality
  code-simplification
  source-driven-development
  verification-before-completion
  receiving-code-review

Opus Final REVIEW/WALKTHROUGH Refresh:
  code-review-and-quality
  code-simplification
  source-driven-development
  verification-before-completion

Sonnet Human Walkthrough:
  receiving-code-review
  code-review-and-quality
  code-simplification

Codex Human Follow-up:
  receiving-code-review
  incremental-implementation
  source-driven-development
  verification-before-completion
```

---

# 15. Source Preservation Appendix

The current prompt pack text below is preserved verbatim for audit purposes.

```text
------------------------------------
codex prompt to feed OPUS PLANNING: (a meta prompt to ask codex to create the planning prompt for opus, seeded by the interviewing/grilling output)

create a prompt for claude opus to first analyze the code one more time, take this plan file we have, read and critique it, ask more questions to me about the design (all at one go), and flesh out the remaining details to the T (as in concrete files, classes, methods, variables, where these changes should go etc) independently by itself after gathering my design decisions. so the initial interviewing output plan must be made into a more detailed implementation plan. allow opus to be independent and ask it not to constrain itself to the existing plan file (except for the scope of the plan/changes of course), but use it as an initial source to get started. 
it must ignore devops/packaging/building and test related work and only focus on the code, unless otherwise specified in the plan.
 it must produce two results in the end as md files:
1. a concrete implementation plan with every minor detail fleshed out absolutely thoroughly
2. a prompt for codex to take this plan and implement it end-to-end with no interruptions.

also ask opus to add these requests below to the final prompt for codex execution phases:
-----------------------------
IMPLEMENTATION requests :

if there is a plan (only when provided by me explicitly), follow the plan exactly
No divergence. No creativity. No architecture changes
Just execute what is written

no time-based waiting hacks

keep a check on algorithmic time complexity and space complexity and use the best solution after weighing options. dont choose brute force methods or quadratic operations. write code while keeping code readibility in mind. prefer code readability over overly complicated changes to achieve best performance/time complexity.

if a change requested by me reduces/makes performance worse, stop and tell me about it. give enough details like you would explain to a junior developer about it.

no 3rd party libraries without explicit approval.
if approved:
check usages of libraries/frameworks against the correct documentation and make sure usages are grounded 100% in documentation. if documentation is poor, find the source code of the library if it is open source, clone it in a temporary folder and read it thoroughly to augment your understanding of existing documentation.  Also make sure these usages are using the latest APIs and flag the use of outdated APIs.

if a 3rd party library is used in a public facing API, the user should never see library/framework specific exceptions raised. it should be custom errors/exception classes  (reuse existing classes in the codebase or create custom ones if needed), and dont chain exceptions because again, i dont want users to know. instead you can dump the trace using the logger for debugging purposes in case logging is used and available. 

reuse existing code wherever possible. keep it DRY.

follow separation of concerns and single responsibility principle when writing code.

use proper imports. no loading files as blobs and executing the code within another block of code.

no hacky retry loops.

do not use assert statements in code, unless it is a test file.

no changing/refactoring unrelated code unless absolutely necessary. suggestions to improve surrounding code is always welcome.

changes in user-facing APIs must be backwards compatible, unless the app version is unreleased.

keep ui changes local to ui code only. dont touch other code. Also, make sure to match existing style guidelines.

use correct types when adding types to code. dont use 'filler' types or generic types or type-ignore comments to pass ci temporarily. Also do not add sloppy code like typing.Cast and cast types in code to satisfy type checkers

do not hardcode numbers/versions and other constants. reuse existing constants or create at the right spots and reuse appropriately.

All changes must be strictly cross platform and must work on both Linux and Windows. Mac is not a concern.

commit often and incrementally in small increments. split large commits into sensible parts. add detailed commit messages, and explain what you are doing in detail in the commit descriptions (no limit on length - so be as detailed as you can)

Always ground development work involving libraries 100% in documentation with zero assumptions.

always add detailed and brief comments for code - so it enables people to understand the code without paying too much attention to it. comments must address the code and not be "meta" or address the task you are working on. cleaning up stale comments is encouraged. 

Don't forget to run linter and smoke test if any on every commit. 

always update the related documentation - look for the correct docs folder, back tracking from the Github Actions workflows and the Makefiles, etc. that build the docs. append to the appropriate sections OR create new ones if required. 

dont write the changelog.

DO NOT WRITE TESTS UNTIL EXPLICITLY ASKED.
When you write tests, follow these instructions:
```
Always keep test code in separate files or folders away from production code. no comingling.
Tests must validate the right things (architecture, not implementation details). avoid unnecessary tests that test temporary hacks or changes.
also make sure the tests for these changes are meaningful, not duplicated, not testing transient/ temporary issues, not flaky and maintain at least 85% coverage for the new lines . Don't manually run the entire test suite. Focused tests are better.
Tests must also strictly only test one behavior per test/method.
```

 if you have questions or can't make a decision or don't have enough context or hit conflicts, DO NOT MAKE ASSUMPTIONS. STOP. ASK. GET CONFIRMATION. THEN PROCEED.

--------------------------------

OPUS REVIEW:

compare the current branch against the head of main, aggregate all changes in the current branch that are newly added and do a thorough code review. compare it against any local PLAN md files in the repo root, if available,  and flag divergence and issues. After checking 100% compliance with the plan and ensuring no divergence, provide suggestions. dont make any changes you propose until i give the go ahead. this branch will be merged into main. Code review for readability, quality, backwards compatibility, performance and proper reuse of existing code, if applicable. Check for backwards compatibility. Remember that that is top priority. Also check usages of libraries/frameworks against the correct documentation and make sure usages are grounded 100% in documentation. if documentation is poor, find the source code of the library if it is open source, clone it in a temporary folder and read it thoroughly to augment your understanding of existing documentation.  Also make sure these usages are using the latest APIs and flag the use of outdated APIs. Also check usages of libraries/frameworks are justified and not unnecessary.

 If the  changes in the branch touch public APIs or add new public APIs, check if they are user friendly and intuitive, if they blend well with the existing public API set and are named properly. 

Surface all assumptions in the code. 

surface the use of assert statements in code. this is bad.

If the changes are trying to reinvent/duplicate something already there in the source code, flag it.

make sure there are comments for every change that is not obvious in terms of readability. we also dont want too many bloated comment blocks. just enough  to help junior engineers understand easily.

All changes must be strictly cross platform and must work on both Linux and Windows. 

Tests must validate the right things (architecture, not implementation details). mark unnecessary tests that test temporary hacks or changes.
also make sure the tests for these changes are meaningful, not duplicated, not testing transient/ temporary issues, not flaky and maintain at least 85% coverage for the new lines (don't manually run the entire test suite. Focused tests are better)
While reviewing tests, flag cases that are not obvious flakes but are brittle or too coupled to implementation details. Look for tests that mutate process-global state such as environment variables, depend on private constants or private helper methods, assert exact error wording unless it is an intentional user-facing contract, encode packaging/layout assumptions that may change, or mirror production logic instead of independently specifying expected behavior. For each concern, classify whether it is a real flake risk, an acceptable contract test, or a maintainability concern, and suggest a behavior-level alternative when practical.
Tests must also strictly only test one behavior per test/method.

after analysis/review,  create 2 documents locally:
#1 a detailed REVIEW.md doc with a review of the changes and also your suggestions right below the review.
#2 also write a detailed WALKTHROUGH.md documenting each change with context, line by line, helping a beginner programmer review the code from scratch(without prior context). it must be detailed and thorough, so as to facilitate review without looking at the code. 
I WANT LINE BY LINE WITH ENGLISH BASED EXPLANATION NEXT TO EACH LINE OF CODE. THIS IS NON NEGOTIABLE. FORMAT IT PROPERLY FOR EASY READABILITY AND TO EASE COGNITIVE OVERLOAD WHILE REVIEWING.




-----------------------------


SONNET CODE WALKTHROUGH:

Look at the code review document. REVIEW.md
let me know if you agree with all points or why you don't.  There is also a  WALKTHROUGH.md  document that we will use  as  a detailed supplement for the review.

Our first goal is to use the REVIEW and WALKTHROUGH as supplements for our own review and review the changes in the PR (basically the diff of this branch against the main branch)
let us review the PR one small change at a time.
let us also create a followup list md to track a checklist of the changes that are neccessary. dont add anything yet.
 let us walk through each section of the review, one by one, look at the corresponding code after gathering context from the WALKTHROUGH,
Show me no-more than 5 lines of code at a time, but also make sure you logically split them into logical chunks when you show me.

 then discuss and agree on the next steps with a detailed step by step plan you propose, once agreed, lets then add that to the follow-up list. 
"Agreed" means I must explicitly type "AGREE" in all-caps.
dont ever add anything to the followup list unless we have agreed on the exact changes that need to be implemented, fleshed out to the T.
proceed automatically through the next review item after each agreed addition 
if you have questions or can't make a decision or don't have enough context or hit conflicts, DO NOT MAKE ASSUMPTIONS. STOP. ASK. GET CONFIRMATION. THEN PROCEED. 
Once we are done reviewing, go ahead and implement all the changes we agreed on as part of the follow-up list after I give you the go-ahead.

---------------------------------
CODEX FOLLOWUP:

understand the context of the current PR. Read REVIEW.md WALKTHROUGH.md for context. then go on and address all items in FOLLOWUP.md while checking them off the list.



```
