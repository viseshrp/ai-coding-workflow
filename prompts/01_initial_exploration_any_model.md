# 01 — Initial Exploration / Grilling / Interviewing + Opus Planning Prompt Generation — Any Model

## Skills

- [interview-me](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/interview-me/SKILL.md)
- [grill-me](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/mattpocock__skills/snapshot/skills/productivity/grill-me/SKILL.md)
- [idea-refine](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/idea-refine/SKILL.md)
- [context-engineering](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/context-engineering/SKILL.md)

## Skill Handling Rule

Use only the explicitly linked skills listed in this prompt.

The prompt is the contract. The locked task artifact is the contract for execution. Skills are supporting procedures only.

If a skill conflicts with this prompt, this prompt wins.

If a conflict is material, stop and ask instead of silently choosing.

Do not use any skill to expand scope, add architecture changes, add tests, add unrelated refactors, or override my explicit instructions.


## Prompt

You are helping me perform the initial exploration phase for an agentic coding workflow.

This exploration prompt is intentionally model-agnostic. Use the same interviewing, grilling, clarification, and artifact-generation contract regardless of whether the model is GPT, Claude, Gemini, or another capable repo-aware model.

Goal:

- turn a vague or partially formed idea into a solid draft plan and a strong Opus planning prompt,
- surface scope, constraints, non-goals, risks, and definition of done before planning is locked.

Success criteria:

- the intended outcome is concrete enough that Opus will not need to guess,
- the important constraints, risks, and non-goals are explicit,
- every material question is either answered from repo/context exploration or explicitly resolved with me before artifacts are finalized,
- `DRAFT_PLAN.md` preserves anything Opus must not lose,
- `INITIAL_OPUS_PLANNING_PROMPT.md` is the final paste-ready Opus planning prompt for the main planning phase,
- both generated artifacts are created in the target repo root using the exact required filenames and nowhere else,
- this phase stops at `DRAFT_PLAN.md` and `INITIAL_OPUS_PLANNING_PROMPT.md`; it does not perform the Opus planning phase itself.

Constraints:

- do not implement code,
- do not write tests,
- do not create unrelated files,
- create workflow-generated Markdown artifacts only in the target repo root using the exact required filenames,
- every workflow-generated Markdown artifact must include `Created by`, `Created at`, and `Updated at` fields,
- use only the linked skills as supporting procedures.

Working method:

- work interactively first,
- keep the collaboration style practical and outcome-first, but do not be shallow or overly terse when a decision needs real explanation,
- ask only when the answer would materially change the plan,
- if a question can be answered by exploring the codebase, explore the codebase instead of asking me,
- if a question can be answered by exploring the codebase or provided context, explore first instead of asking me,
- if your environment supports repo exploration and parallel context gathering, gather the most relevant repo context in parallel before asking repo-answerable questions,
- when clarification is needed, ask one question at a time and do not move on until that question is actually nailed down,
- keep grilling until every material scope, UX, behavior, technical, constraint, rollout, edge-case, backwards-compatibility, and documentation decision is either answered or explicitly marked as intentionally deferred,
- for each question, include:
  1. the question,
  2. why the answer matters,
  3. all reasonable answer options or decision paths you think I should consider,
  4. a proper detailed explanation of each option, including tradeoffs, risks, and downstream implications,
  5. your recommended option,
  6. the reasoning for why that option is recommended,
  7. your current best guess, if useful,
- after I answer, briefly confirm the decision, note any important consequences for the plan, and then ask the next highest-leverage unresolved question,
- do not accept vague answers at face value when they still leave important ambiguity; follow up until the answer is precise enough that Opus will not need to guess,
- keep going until the goal, constraints, non-goals, likely implementation surface, and definition of done are clear enough to seed Opus.

Stop rules:

- do not produce final artifacts until exploration is complete or I explicitly ask you to stop and generate them,
- if any material question is still unresolved, keep interviewing one question at a time instead of pretending the plan is ready,
- if the task is still ambiguous in a way that would change scope or behavior, keep interviewing instead of pretending the plan is ready.

Workflow context:

My workflow is:

1. A capable exploration model helps me think, interview, grill, and clarify the idea.
2. This produces `DRAFT_PLAN.md`.
3. This also produces `INITIAL_OPUS_PLANNING_PROMPT.md`.
4. I paste `INITIAL_OPUS_PLANNING_PROMPT.md` into Opus.
5. Opus then uses the draft plan plus repo context as seed context to create:
   - `FEATURE_SPEC_AND_PLAN.md`
   - `GPT_EXECUTION_PROMPT.md`

Use the linked skills as supporting procedures:

- Use `interview-me` to extract what I actually want.
- Use `grill-me` to stress-test the plan/design.
- Use `idea-refine` to move from rough concept to concrete proposal.
- Use `context-engineering` to identify what repo context matters and avoid context flooding.

## Output artifact 1: `DRAFT_PLAN.md`

Create `DRAFT_PLAN.md` in the target repo root with:

- problem statement,
- goals,
- non-goals,
- user-visible behavior,
- constraints,
- technical assumptions,
- open questions,
- decisions already made,
- likely files/modules involved, if known,
- risks,
- definition of done,
- anything that Opus must not lose.

## Output artifact 2: `INITIAL_OPUS_PLANNING_PROMPT.md`

Create `INITIAL_OPUS_PLANNING_PROMPT.md` in the target repo root as the final direct-use planning prompt for Claude Opus.

This generated artifact is the prompt that I will paste into Claude Opus for the main planning phase.

There is no separate checked-in planning prompt file after this exploration step. `INITIAL_OPUS_PLANNING_PROMPT.md` itself must be the final paste-ready prompt for the Opus planning phase.

It must be self-contained.

Do not generate:

- a helper prompt,
- a seed-only prompt that expects later normalization,
- a meta prompt for another model,
- planning artifacts such as `FEATURE_SPEC_AND_PLAN.md` or `GPT_EXECUTION_PROMPT.md` in this exploration phase.

The generated Opus prompt must use a clear title and contain these top-level sections:

- `## Skills`
- `## Skill Handling Rule`
- `## Default Planning Artifact Reduction`
- `## Prompt`

In `## Skills`, it must explicitly include these skill links:

- [spec-driven-development](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/spec-driven-development/SKILL.md)
- [planning-and-task-breakdown](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/planning-and-task-breakdown/SKILL.md)
- [context-engineering](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/context-engineering/SKILL.md)
- [source-driven-development](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/source-driven-development/SKILL.md)
- [verification-before-completion](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/obra__Superpowers/snapshot/skills/verification-before-completion/SKILL.md)

In `## Skill Handling Rule`, it must instruct the target agent to:

- use only the explicitly linked skills listed in the prompt,
- treat the prompt as the contract,
- treat locked task artifacts as the contract for execution,
- use skills as supporting procedures only,
- let the prompt win if a skill conflicts with it,
- stop and ask instead of silently choosing if a conflict is material,
- never use a skill to expand scope, add architecture changes, add tests, add unrelated refactors, or override my explicit instructions.

In `## Default Planning Artifact Reduction`, it must instruct Opus to default to one combined planning artifact instead of separate spec and implementation plan files.

It must also instruct Opus that every workflow-generated Markdown artifact belongs in the target repo root using the exact required filename and must never be created in a subdirectory or alternate path.

It must also instruct Opus that every workflow-generated Markdown artifact must include `Created by`, `Created at`, and `Updated at` metadata, preserving `Created by` and `Created at` after first creation and refreshing `Updated at` whenever the artifact is edited.

It must require:

- `FEATURE_SPEC_AND_PLAN.md`
- `GPT_EXECUTION_PROMPT.md`

It must state that:

1. `FEATURE_SPEC_AND_PLAN.md` contains both a detailed spec/reference section and a concrete implementation plan section.
2. The implementation plan section links back to relevant spec/reference anchors inside the same file instead of duplicating long explanations.
3. The plan remains the execution contract.
4. The spec/reference section remains the background reference.
5. Separate `SPEC.md` and `IMPLEMENTATION_PLAN.md` are only a fallback if I explicitly ask or if the file becomes too large to review comfortably.

Inside `## Prompt`, the generated Opus prompt must use clear sections for:

- role,
- task,
- context to read before answering,
- success criteria,
- constraints,
- working method,
- final self-check.

The generated Opus prompt must instruct Opus as follows.

Role:

- You are Claude Opus performing the planning phase for an agentic coding workflow.
- Be explicit, source-grounded, and conservative about assumptions.
- Read before answering. Do not speculate about code or files you have not inspected.

Task:

- Perform the main planning work itself. Do not generate a meta prompt for another model.
- Your job is to create the detailed planning artifacts that will become the contract for GPT execution.
- Critique the current draft plan, ask any remaining design questions in one batch, then produce the locked planning artifacts after my answers.
- The initial interviewing output plan must be made into a more detailed implementation plan.

Context to read before answering:

- Read `DRAFT_PLAN.md`, prior interviewing/grilling notes, and relevant repository context.
- Read the draft plan.
- Read prior interviewing/grilling notes.
- Read relevant repository context.

Success criteria:

- the generated Opus prompt is explicit about task, scope, success criteria, stop rules, and required artifacts,
- `FEATURE_SPEC_AND_PLAN.md` is concrete enough that GPT can execute without inventing missing detail,
- `GPT_EXECUTION_PROMPT.md` preserves the Engineering Contract and leaves GPT no ambiguity about scope, stop rules, or verification,
- no important detail from the draft plan is dropped,
- scope stays within the requested change,
- the prompt preserves the current scope while letting Opus deepen detail inside that scope.

Constraints:

- do not implement code,
- do not write tests,
- do not make unrelated files or unrelated changes,
- ignore DevOps/packaging/building and test-related work unless otherwise specified in the plan,
- prefer the minimum necessary design surface and do not overengineer or add speculative abstractions.

Working method:

- analyze the code one more time,
- take the draft plan file and interviewing output we have,
- read and critique that material,
- ask all remaining design questions together in one batch,
- independently flesh out the remaining details to the T after gathering my design decisions,
- make the initial interviewing output plan into a more detailed implementation plan,
- be independent and not constrain yourself to the existing plan file except for the scope of the plan/changes,
- use the existing plan file only as an initial source to get started,
- use the existing plan as a seed artifact, not the ceiling for detail,
- preserve all valid task-specific detail from `DRAFT_PLAN.md` and the exploration output,
- if exploration notes conflict materially with repo reality or with each other, keep the more scope-conservative interpretation and surface the conflict to the user instead of silently choosing,
- ground file/class/function details in actual repository context and never speculate about code you have not read,
- if repo reality conflicts with the draft plan, surface the conflict explicitly instead of silently rewriting scope,
- separate confirmed facts from inferences and surface unresolved uncertainty plainly,
- after my answers, update the artifacts accordingly.

Final self-check:

- verify that the planning artifacts are explicit about success criteria, stop rules, and verification,
- verify that the implementation plan is detailed enough to drive end-to-end GPT execution,
- verify that the prompt and plan remain within the original requested scope.

Inside `## Prompt`, after the core sections above, the generated Opus prompt must also include these requirement blocks in substance.

Required planning depth:

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

Required design-question pass:

- before finalizing artifacts, identify every remaining design decision that I need to make,
- ask all remaining questions together in one batch,
- for each question:
  1. explain why it matters,
  2. give your recommended answer,
  3. explain the tradeoffs,
  4. identify what parts of the plan depend on the answer,
- after I answer, update the artifacts accordingly,
- if a question can be answered by reading the codebase, answer it from codebase exploration instead of asking me.

Required output 1: `FEATURE_SPEC_AND_PLAN.md`

- create `FEATURE_SPEC_AND_PLAN.md` in the target repo root,
- make it a single combined artifact with:
  1. a detailed spec/reference section,
  2. a concrete implementation plan with every minor detail fleshed out absolutely thoroughly,
  3. concrete files, classes, methods, variables, and where changes should go,
  4. implementation plan links back to relevant spec/reference anchors inside the same file.

`FEATURE_SPEC_AND_PLAN.md` must include:

1. Executive summary:
   - one-paragraph problem statement,
   - goal,
   - non-goals,
   - definition of done.
2. Spec / reference section:
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
3. Concrete implementation plan section:
   - exact file(s),
   - exact symbol(s),
   - exact change to make,
   - why the change is needed,
   - link to relevant spec/reference anchor inside the same file,
   - dependencies on previous steps,
   - verification relevant to that step.
4. Source/documentation grounding section:
   - identify the version if possible,
   - cite the official docs/source consulted,
   - explain the pattern chosen,
   - flag anything unverified,
   - flag outdated APIs,
   - explain if source code was used because docs were poor.
5. Verification plan:
   - focused lint/smoke/build commands, if available,
   - exact checks to run,
   - what successful output means,
   - what failures should be pasted back without paraphrasing,
   - no full test-suite run unless explicitly asked.
6. Documentation update plan:
   - likely docs folder/file(s),
   - how you found them,
   - exact sections to update or create,
   - reminder not to write the changelog.

Required output 2: `GPT_EXECUTION_PROMPT.md`

- create `GPT_EXECUTION_PROMPT.md` in the target repo root,
- make it the final direct-use prompt that I will paste into GPT for locked execution,
- make it self-contained,
- do not generate a helper prompt, summary, wrapper note, partial contract, or any prompt that expects another checked-in execution prompt file,
- there is no separate checked-in GPT execution prompt file after this planning step,
- require it to instruct GPT to:
  1. read `FEATURE_SPEC_AND_PLAN.md`,
  2. treat the implementation plan section inside `FEATURE_SPEC_AND_PLAN.md` as the execution contract,
  3. treat the spec/reference section inside `FEATURE_SPEC_AND_PLAN.md` as reference context,
  4. follow the implementation plan exactly,
  5. make no architecture changes,
  6. make no unrelated changes,
  7. implement end-to-end with no interruptions unless a required decision was not made or a conflict appears,
  8. stop and ask on ambiguity/conflict/context gaps,
  9. use the full Engineering Contract below.

The generated `GPT_EXECUTION_PROMPT.md` must use a clear title and contain these top-level sections:

- `## Skills`
- `## Skill Handling Rule`
- `## Engineering Contract`
- `## Prompt`

The generated Opus prompt must also require that the generated `GPT_EXECUTION_PROMPT.md` explicitly include these skill links:

- [incremental-implementation](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/incremental-implementation/SKILL.md)
- [source-driven-development](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/source-driven-development/SKILL.md)
- [verification-before-completion](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/obra__Superpowers/snapshot/skills/verification-before-completion/SKILL.md)

The generated `GPT_EXECUTION_PROMPT.md` must include a `## Skill Handling Rule` that instructs GPT to:

- use only the explicitly linked skills listed in the prompt,
- treat the prompt as the contract,
- treat locked task artifacts as the contract for execution,
- use skills as supporting procedures only,
- let the prompt win if a skill conflicts with it,
- stop and ask instead of silently choosing if a conflict is material,
- never use a skill to expand scope, add architecture changes, add tests, add unrelated refactors, or override my explicit instructions.

The generated Opus prompt must include the full Engineering Contract below and instruct Opus to embed that contract into `GPT_EXECUTION_PROMPT.md`.

The generated GPT prompt must require the following Engineering Contract verbatim or stricter:

Inside `## Prompt`, the generated `GPT_EXECUTION_PROMPT.md` must use clear sections for:

- goal,
- success criteria,
- context to read before acting,
- execution posture,
- constraints,
- stop rules,
- execution rules,
- required final response.

Inside those sections, the generated Opus prompt must require `GPT_EXECUTION_PROMPT.md` to instruct GPT as follows.

Goal:

- execute the locked implementation plan end-to-end and stop only when you have a verified result or a concrete blocker.

Success criteria:

- only the planned changes are implemented,
- the smallest correct changes are made,
- required documentation updates are completed,
- focused verification is run and reported with fresh evidence,
- any workflow-generated Markdown artifacts created or updated during the workflow remain in the target repo root and are never moved to subdirectories or alternate paths,
- any workflow-generated Markdown artifacts created or updated during the workflow include `Created by`, `Created at`, and `Updated at` metadata with `Updated at` refreshed on every edit,
- workflow-generated Markdown artifacts are not staged or committed unless I explicitly ask for that,
- the final execution flow stages changes, commits them, pushes the branch, and creates a pull request only if the current branch does not already have one.

Context to read before acting:

- `FEATURE_SPEC_AND_PLAN.md`,
- `GPT_EXECUTION_PROMPT.md`, if present as saved artifact context,
- relevant repository context.

Execution posture:

- act like an autonomous engineer: gather context, implement, run the smallest relevant checks, refine, then report,
- read all likely relevant files in parallel before editing when that shortens the loop,
- prefer dedicated repo/search/edit tools over raw shell when available,
- keep progressing until you have a verified result or one of the stop conditions below.

Constraints:

- the implementation plan section inside `FEATURE_SPEC_AND_PLAN.md` is the execution contract,
- the spec/reference section inside `FEATURE_SPEC_AND_PLAN.md` is reference context,
- workflow-generated Markdown artifacts belong only in the target repo root using their exact required filenames,
- workflow-generated Markdown artifacts must include `Created by`, `Created at`, and `Updated at` metadata, preserving the creation fields after first write and updating `Updated at` on every edit,
- follow the plan exactly,
- no divergence,
- no creativity,
- no architecture changes,
- just execute what is written.

Stop rules:

- implement end-to-end with no interruptions unless one of the following conditions is true,
- stop and ask if there is a conflict in decisions,
- stop and ask if a required decision was never made,
- stop and ask if the plan contradicts code reality,
- stop and ask if following the plan would create a performance, backwards-compatibility, security, or public-API problem,
- stop and ask if you do not have enough context,
- if a missing credential, external dependency, or environment precondition blocks verification, say exactly what blocked you,
- if any of those happens, stop and ask. Do not assume.
- otherwise do not stop at analysis.

Execution rules:

- read likely relevant files in parallel before editing when practical,
- prefer dedicated repo/file/edit/search tools over raw shell when available,
- carry through context gathering, implementation, focused verification, and refinement without waiting for step-by-step approval unless blocked,
- work in small increments,
- commit often and incrementally in small increments if committing is allowed,
- split large commits into sensible parts,
- use detailed commit messages and detailed commit descriptions,
- do not make unrelated refactors,
- do not write tests unless explicitly asked,
- run focused linter/smoke/build checks described by the plan,
- run linter and smoke test if any on every commit, unless command execution is unavailable or explicitly disallowed,
- if a command fails, paste the exact error/log back. Never paraphrase logs.
- update related documentation as described in the plan,
- do not write the changelog,
- after verification, stage the intended files with `git add`,
- do not stage or commit workflow-generated Markdown artifacts by default, including `DRAFT_PLAN.md`, `INITIAL_OPUS_PLANNING_PROMPT.md`, `FEATURE_SPEC_AND_PLAN.md`, `GPT_EXECUTION_PROMPT.md`, `PLAN_CRITIQUE.md`, `OPUS_PLAN_REVISION_REQUEST.md`, `PLAN_REVISION_SUMMARY.md`, `PLAN_REVISION_VERIFICATION.md`, `REVIEW.md`, `WALKTHROUGH.md`, `GPT_REVIEW_FIX_PROMPT.md`, `REVIEW_FIX_VERIFICATION.md`, and `FOLLOWUP.md`, unless I explicitly ask for them to be committed,
- create focused commit(s) with detailed messages,
- push the current branch after committing,
- check whether a pull request already exists for the current branch before creating one,
- create a pull request if and only if the current branch does not already have one,
- if you do not know how to check whether a pull request already exists for the current branch, use GitHub CLI (`gh`) to determine that,
- do not create a duplicate pull request for the same branch,
- keep interim narration minimal and save the full report for the final response unless blocked.

Required final response:

The generated `GPT_EXECUTION_PROMPT.md` must require this exact response structure:

```markdown
# GPT Execution Summary

## What Changed

## Files Changed

## Plan Steps Completed

## Verification Evidence

## Documentation Updated

## Commits Created

## Push Status

## Pull Request

## Not Done / Blocked

## Suggestions Not Implemented Because Out Of Scope
```

It must explicitly instruct GPT not to claim completion without fresh verification evidence.

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
- Suggestions to improve surrounding code are always welcome, but put them in a separate "Not Doing / Suggestions" section instead of implementing them.
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

- Do not create, modify, or delete tests in this phase.
- Run only focused existing tests or checks when needed for verification; do not manually run the entire suite.
- The generated planning and execution prompts must defer test authoring to the final model-agnostic `09_write_focused_tests_any_model.md` phase.
- Do not duplicate phase `09`'s test-design, pytest, or coverage contract in generated prompts for earlier phases.

Before finishing, the generated prompt must instruct Opus to verify that:

- `FEATURE_SPEC_AND_PLAN.md` is sufficient for GPT execution,
- `GPT_EXECUTION_PROMPT.md` contains every implementation rule above,
- no details from the draft plan were dropped.

If the task is still ambiguous, keep interviewing instead of pretending the plan is ready.
