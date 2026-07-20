# 03 - Plan Revision Verification - GPT or Gemini

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

- Do not create, modify, or delete tests in this plan-verification phase.
- Run only focused existing tests or checks when repository evidence is needed; do not manually run the entire suite.
- Verify that the planning artifacts defer test authoring to the final model-agnostic `09_write_focused_tests_any_model.md` phase.
- Do not duplicate phase `09`'s test-design, pytest, or coverage contract in this verification.

## Prompt

Goal:

- determine whether Opus actually addressed the previous plan critique and whether the planning artifacts are now ready for GPT execution.

Success criteria:

- each prior concern is checked against the revised artifacts and linked to concrete evidence,
- the verdict is explicit about both readiness and remaining gaps,
- the output follows the exact structure below.

Constraints:

- do not implement code,
- do not modify files unless explicitly asked,
- if evidence is missing, say so explicitly instead of guessing.

Context to review:

- the previous `PLAN_CRITIQUE.md`,
- the previous `OPUS_PLAN_REVISION_REQUEST.md`, if present,
- `PLAN_REVISION_SUMMARY.md`,
- the updated `FEATURE_SPEC_AND_PLAN.md`,
- the updated `GPT_EXECUTION_PROMPT.md`,
- original draft plan/interviewing notes if available.

Working method:

- if you are GPT, inspect the revised artifacts and any needed repo files in parallel before finalizing,
- if you are GPT or Gemini, stay grounded in the supplied artifacts and any repo context you inspect,
- quote or clearly point to where each concern was addressed,
- distinguish resolved issues, partial fixes, missing fixes, and invalid original concerns,
- if the revision introduced a new problem, call it out explicitly instead of forcing a pass verdict.

Task:

- determine whether the revised plan and revised GPT prompt satisfy all previously raised concerns,
- produce `PLAN_REVISION_VERIFICATION.md`,
- if anything remains unresolved, do not author a new revision prompt here; instead make it explicit that the workflow must return to the critique phase so `02_plan_critique_gpt_gemini.md` can produce the next `OPUS_PLAN_REVISION_REQUEST.md`.

Artifact location rule:

- all workflow-generated Markdown artifacts for this workflow must live in the target repo root using the exact required filenames,
- do not normalize them into subdirectories or alternate paths,
- all workflow-generated Markdown artifacts must include `Created by`, `Created at`, and `Updated at` metadata, preserving creation fields and refreshing `Updated at` on edits,
- treat any artifact-path drift as a workflow failure to call out explicitly.

For each previously raised concern:

- quote or summarize the concern,
- identify where it was addressed,
- classify status as `Resolved`, `Partially Resolved`, `Not Resolved`, or `Invalid Concern`,
- explain your reasoning.

## Required output: `PLAN_REVISION_VERIFICATION.md`

Create `PLAN_REVISION_VERIFICATION.md` in the target repo root.

Use this structure:

```markdown
# Plan Revision Verification

## Verdict
- All previous concerns resolved: Yes/No
- Ready for GPT execution: Yes/No

## Concern-by-Concern Verification

| Concern | Status | Evidence | Remaining Action |
|---|---|---|---|

## Remaining Blocking Issues

## Remaining Non-Blocking Issues

## New Issues Introduced By Revision

## Required Next Action
```

If any issue remains:

- do not create `OPUS_PLAN_REVISION_REQUEST.md` in this phase,
- state explicitly that the workflow must return to `02_plan_critique_gpt_gemini.md`,
- state that `02` is the only phase that should author `OPUS_PLAN_REVISION_REQUEST.md`,
- if the existing `OPUS_PLAN_REVISION_REQUEST.md` was missing, weak, or failed to preserve the needed revision instructions, call that out as a failure in the upstream critique/request phase rather than compensating for it here.

If no issue remains, state clearly that the plan is ready for GPT execution.
