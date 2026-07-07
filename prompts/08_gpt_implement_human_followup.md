# 08 - GPT Implements Human-Approved FOLLOWUP.md

## Skills

- [incremental-implementation](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/incremental-implementation/SKILL.md)
- [source-driven-development](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/source-driven-development/SKILL.md)
- [verification-before-completion](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/obra__Superpowers/snapshot/skills/verification-before-completion/SKILL.md)
- [receiving-code-review](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/obra__Superpowers/snapshot/skills/receiving-code-review/SKILL.md)

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

Goal:

- execute the human-approved `FOLLOWUP.md` items end-to-end and stop only when you have a verified result or a concrete blocker.

Success criteria:

- only approved `FOLLOWUP.md` items are implemented,
- each completed item is checked off only after the change and its verification are done,
- the smallest correct changes are made,
- required documentation updates are completed,
- focused verification is run and reported with fresh evidence,
- any workflow-generated Markdown artifacts created or updated during the workflow remain in the target repo root and are never moved to subdirectories or alternate paths,
- any workflow-generated Markdown artifacts created or updated during the workflow include `Created by`, `Created at`, and `Updated at` metadata with `Updated at` refreshed on every edit,
- workflow-generated Markdown artifacts are not staged or committed unless I explicitly ask for that,
- if committing is allowed, each commit strictly corresponds to one approved `FOLLOWUP.md` item and does not mix work from multiple follow-up items,
- if committing is allowed, commits are small, focused, and split into sensible parts rather than bundled into one broad commit,
- the final execution flow stages changes, commits them, pushes the branch, and creates a pull request only if the current branch does not already have one,
- no AI review loop is restarted after this phase; the workflow returns to manual review.

Context to read before acting:

- `REVIEW.md`,
- `WALKTHROUGH.md`,
- `FOLLOWUP.md`,
- `FEATURE_SPEC_AND_PLAN.md`, if present,
- current branch diff against `main`.

Execution posture:

- act like an autonomous engineer: gather context, implement, run the smallest relevant checks, refine, then report,
- understand the context of the current PR before editing,
- use `REVIEW.md` and `WALKTHROUGH.md` for context only,
- treat `FOLLOWUP.md` as the execution contract for this phase,
- read all likely relevant files in parallel before editing when that shortens the loop,
- prefer dedicated repo/search/edit tools over raw shell when available,
- keep progressing until you have a verified result or one of the stop conditions below.

Constraints:

- `FOLLOWUP.md` is the execution contract for this phase,
- `REVIEW.md` and `WALKTHROUGH.md` are reference context only,
- workflow-generated Markdown artifacts belong only in the target repo root using their exact required filenames,
- workflow-generated Markdown artifacts must include `Created by`, `Created at`, and `Updated at` metadata, preserving the creation fields after first write and updating `Updated at` on every edit,
- go on and address all items in `FOLLOWUP.md` while checking them off the list,
- only implement items that are explicitly present in `FOLLOWUP.md`,
- do not add new follow-up items,
- do not expand scope,
- do not implement optional suggestions unless they are explicitly in `FOLLOWUP.md`,
- follow the approved `FOLLOWUP.md` items exactly,
- no divergence,
- no creativity,
- no architecture changes,
- just execute what is written.

Stop rules:

- implement end-to-end with no interruptions unless one of the following conditions is true,
- stop and ask if there is a conflict in decisions,
- stop and ask if a required decision was never made,
- stop and ask if a `FOLLOWUP.md` item is wrong, stale, ambiguous, conflicts with the current code, or needs a design decision,
- stop and ask if following `FOLLOWUP.md` would create a performance, backwards-compatibility, security, or public-API problem,
- stop and ask if you do not have enough context,
- if a missing credential, external dependency, or environment precondition blocks verification, say exactly what blocked you,
- if any of those happens, stop and ask. Do not assume.
- otherwise do not stop at analysis.

Execution rules:

- read likely relevant files in parallel before editing when practical,
- prefer dedicated repo/file/edit/search tools over raw shell when available,
- carry through context gathering, implementation, focused verification, and refinement without waiting for step-by-step approval unless blocked,
- work in small increments,
- if committing is allowed, each commit must map to exactly one approved `FOLLOWUP.md` item,
- if committing is allowed, commit often in small focused increments,
- do not bundle multiple follow-up items, partial work for unrelated items, or unrelated cleanup into the same commit,
- split large commits into sensible smaller focused parts,
- use detailed commit messages and detailed commit descriptions,
- do not make unrelated refactors,
- do not write tests unless explicitly asked,
- run focused verification relevant to the approved follow-up items,
- run linter and smoke test if any on every commit, unless command execution is unavailable or explicitly disallowed,
- if a command fails, paste the exact error/log back. Never paraphrase logs.
- update related documentation as required by the approved follow-up items,
- do not write the changelog,
- after verification, stage the intended files with `git add`,
- do not stage or commit workflow-generated Markdown artifacts by default, including `DRAFT_PLAN.md`, `INITIAL_OPUS_PLANNING_PROMPT.md`, `FEATURE_SPEC_AND_PLAN.md`, `GPT_EXECUTION_PROMPT.md`, `PLAN_CRITIQUE.md`, `OPUS_PLAN_REVISION_REQUEST.md`, `PLAN_REVISION_SUMMARY.md`, `PLAN_REVISION_VERIFICATION.md`, `REVIEW.md`, `WALKTHROUGH.md`, `GPT_REVIEW_FIX_PROMPT.md`, `REVIEW_FIX_VERIFICATION.md`, and `FOLLOWUP.md`, unless I explicitly ask for them to be committed,
- create focused commit(s) with detailed messages,
- push the current branch after committing,
- check whether a pull request already exists for the current branch before creating one,
- create a pull request if and only if the current branch does not already have one,
- if you do not know how to check whether a pull request already exists for the current branch, use GitHub CLI (`gh`) to determine that,
- do not create a duplicate pull request for the same branch,
- do not create a new AI review prompt,
- do not ask Opus to review this phase,
- keep interim narration minimal and save the full report for the final response unless blocked.

I will do the final review manually.

## Required final response

```markdown
# Human Follow-Up Implementation Summary

## What Changed

## Files Changed

## FOLLOWUP.md Items Completed

## Verification Evidence

## Documentation Updated

## Commits Created

## Push Status

## Pull Request

## Not Done / Blocked

## Suggestions Not Implemented Because Out Of Scope

## Remaining Manual Review Notes
```

In `## Commits Created`, list each commit together with the exact `FOLLOWUP.md` item it corresponds to.

Do not claim completion without fresh verification evidence.
