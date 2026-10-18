# 06 - Opus Refreshes Final Review and Walkthrough, Then Generates Interactive HTML

## Skills

- [code-review-and-quality](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/code-review-and-quality/SKILL.md)
- [code-simplification](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/code-simplification/SKILL.md)
- [source-driven-development](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/source-driven-development/SKILL.md)
- [verification-before-completion](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/obra__Superpowers/snapshot/skills/verification-before-completion/SKILL.md)
- [no-ai-slop](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/petergyang__no-ai-slop/snapshot/skills/no-ai-slop/SKILL.md), including its required [eval.md](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/petergyang__no-ai-slop/snapshot/skills/no-ai-slop/eval.md)
- For the security checks and threat-model guidance referenced by the linked procedures: [security-and-hardening](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/security-and-hardening/SKILL.md), with [hardening-patterns.md](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/security-and-hardening/references/hardening-patterns.md) and [security-checklist.md](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/references/security-checklist.md). Use only the applicable analysis within this phase's permissions; do not start a separate hardening or incident-response task.
- For the performance checks referenced by `code-review-and-quality`: [performance-optimization](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/performance-optimization/SKILL.md), with [optimization-patterns.md](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/performance-optimization/references/optimization-patterns.md) and [performance-checklist.md](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/references/performance-checklist.md). Use only applicable review guidance; do not start an optimization task, impose example thresholds, or create `PERF.md`.

## Skill Handling Rule

Fetch skill procedures and their required companions only from `https://github.com/viseshrp/ai-skills-archive`. Resolve relative resource references to the explicitly linked archive copies; do not follow upstream skill URLs, install a skill package, or substitute an official-source copy. If a required archive resource is absent or unreadable, stop and report its exact missing path. Keep optional related-skill mentions and provenance links inactive unless this prompt explicitly authorizes the procedure. Target-library API and version documentation remains governed by the Engineering Contract; it is not a substitute source for skill material.

Use linked companions within this phase's scope. Skip UI-only sections for backend work, preserve the test-authoring boundary and named outputs, and do not run optional bootstrap scripts.

Apply the activation and skill-loading rules in `## UI work only` to all UI skill links. Skip those links when UI work is out of scope. Keep all other required skill loading unchanged.

Use only this prompt's explicitly linked skills.

Fetch and read each linked skill and required companion completely from its GitHub URL before use. Follow the linked procedures directly; do not depend on local skill repositories, installed slash commands, or earlier prompt text.

The prompt is the contract. The locked task artifact is the contract for execution. Skills are supporting procedures only.

If a skill conflicts with this prompt, this prompt wins.

If a conflict is material, stop and ask instead of silently choosing.

Do not use any skill to expand scope, add architecture changes, add tests, add unrelated refactors, or override my explicit instructions.

`no-ai-slop` is mandatory for every Markdown document this phase creates or revises. Treat it as the ultimate writing guide and final authority for prose and presentation after satisfying this prompt's factual, technical, structural, and output requirements. If another skill or instruction conflicts only on writing style, `no-ai-slop` wins; this prompt and locked task artifacts still control scope, meaning, required structure, artifact names, constraints, and evidence.

Apply `no-ai-slop` while drafting and run its `eval.md` self-check before saving each Markdown artifact or sending the final response. If its `SKILL.md` or `eval.md` cannot be read and applied, stop before creating or revising Markdown and report the blocker. Ignore its draft-request, detection-mode, and mandatory `What changed` workflow unless this prompt explicitly asks for them.

Apply the same writing guide and evaluator to the explanatory text in `WALKTHROUGH.html` before saving it. The HTML is a workflow explanation, so its generation does not activate UI implementation or design skills for backend-only changes.


## Engineering Contract

Apply this contract during planning, execution, review, and review fixes.

### Plan adherence

- If there is a plan, and only when a plan is provided by me explicitly, follow the plan exactly.
- No divergence.
- No creativity.
- No architecture changes.
- Just execute what is written.
- Re-read the original requirements and approved changes after long sessions or context handoffs and before sign-off. Compare them with the current plan or implementation to identify drift, omitted behavior, and unintended additions. Use the original artifacts when available; do not infer missing intent from an author's completion summary.
- Derive acceptance criteria and expected results from product requirements, approved clarifications, and public contracts independently of implementation details and agent-written tests. Do not change them merely to make the current code pass.
- If the plan, code reality, or user request conflicts with another instruction, stop and ask.
- If you have questions, cannot make a decision, do not have enough context, or hit conflicts, DO NOT MAKE ASSUMPTIONS. STOP. ASK. GET CONFIRMATION. THEN PROCEED.

### Scope control

- Do not change, refactor, or reorganize unrelated code unless absolutely necessary.
- Put suggestions to improve surrounding code in a separate “Not Doing / Suggestions” section; do not implement them.
- Ignore DevOps, packaging, building, and test-related work unless otherwise specified in the plan or prompt.
- Keep UI changes within UI code unless the plan explicitly requires changes elsewhere.
- Match existing style guidelines.
- Do not write the changelog.

### Performance and complexity

- No time-based waiting hacks.
- No hacky retry loops.
- Check algorithmic time and space complexity.
- Use the best solution after weighing options.
- Do not choose brute-force methods or quadratic operations unless the plan explicitly justifies them and the data size makes them safe.
- Write readable code.
- Prefer readable code over overcomplicated performance or time-complexity optimizations.
- If a change I request reduces performance, stop and tell me before implementing it.
- Explain performance concerns in enough detail for a junior developer to understand.

### Dependencies, frameworks, and documentation grounding

- No third-party libraries without explicit approval.
- If a third-party library is approved, verify library/framework usage against the correct documentation; ground 100% of usage in those docs.
- Always ground development work involving libraries 100% in documentation with zero assumptions.
- If documentation is poor and the library is open source, find its source code, clone it in a temporary folder, and read it thoroughly to supplement the documentation.
- Ensure usage follows the latest APIs.
- Flag outdated APIs.
- Check that library/framework usage is necessary and justified.

### Public APIs and exceptions

- Backwards compatibility is top priority.
- Changes in user-facing APIs must be backwards compatible, unless the app version is unreleased.
- If a third-party library is used in a public-facing API, the user should never see library/framework-specific exceptions raised.
- Use custom errors/exception classes instead. Reuse existing classes in the codebase or create custom ones if needed.
- Do not chain exceptions when doing so would expose implementation/library details to users.
- If logging is used and available, log the trace with the logger for debugging.
- For changed failure paths, assess whether incident logs identify the failed operation, relevant request or job context, error cause and trace, and retry or recovery outcome where applicable. Follow existing logging conventions and levels; avoid secrets, sensitive payloads, and duplicate noise. Identify diagnostic gaps within the approved change scope.
- If changes touch public APIs or add new public APIs, ensure they are user-friendly, intuitive, blend well with the existing public API set, and have appropriate names.

### Code quality and maintainability

- Use the target language and its standard library idiomatically.
- Reuse existing code wherever possible.
- Keep code DRY.
- Follow separation of concerns.
- Follow the single responsibility principle.
- Use proper imports.
- Do not load files as blobs and execute the code within another block of code.
- Use assert statements only in test files, never in production code.
- Surface all assumptions.
- If changes reinvent or duplicate something already in the source code, stop and flag it.
- Do not hardcode numbers, versions, or other constants. Reuse existing constants, or create new constants in the right places and reuse them appropriately.

### Simplicity and reuse

Apply this procedure to backend and UI work within this phase's existing permissions. In review-only phases, assess proposed or existing changes without implementing them:

- Before proposing or adding custom code, inspect relevant existing helpers, types, and patterns, then standard-library capabilities, native platform features, and already-installed dependencies. Prefer a compatible existing solution when it preserves behavior and readability; name the concrete alternative when flagging duplication.
- Explicitly review duplication, excess abstractions, unused paths, and avoidable complexity. Justify a new abstraction or dependency by a current requirement, meaningful duplication, or a necessary ownership boundary. A single implementation or caller is not by itself a defect. Preserve dependency approval and source-documentation grounding.
- For a bug fix, trace the relevant callers, data flow, and error flow before choosing the repair location. When a defect is found, search throughout the codebase for the same failure pattern and inspect candidate matches. Record the search scope, confirmed occurrences, and unexamined areas in the phase's existing output. For authorized fixes, address the root cause within this phase's permissions and approved scope; report other occurrences without changing them. If a shared fix would exceed scope or alter compatibility, stop and ask.
- Before proposing deletion, inspect direct callers, dynamic or string references, public contracts, configuration, and relevant tests. Fewer lines or files are not acceptance criteria; preserve validation, security, accessibility, error handling, and verification.
- Do not substitute a simpler interpretation for an explicit requirement or locked plan. Put out-of-scope simplifications in the phase's permitted suggestions or chat; implementation still requires its existing authorization. Preserve the test-authoring boundary, native test-framework rules, and coverage gate; do not introduce production assertion demos, one-test quotas, persistent modes, debt markers, or new ledgers.

### Simplification limits and improvement claims

- During planning, record each deliberate simplification with a material limit: why it meets current requirements, its known limit, and the evidence that would trigger revisiting it. Do not invent thresholds or weaken explicit requirements. Carry applicable limits and revisit triggers into existing durable documentation during authorized implementation or fixes. In review, verification, and audit phases, check these decisions and route gaps through the existing documentation checkpoint; do not exceed the phase's write permissions. Use existing planning and documentation sections without adding comment markers, a debt ledger, or another artifact.
- In reviews and handoffs, distinguish measured improvements from expectations. Claims of reduced latency, memory use, or cost require comparable before-and-after evidence identifying the baseline, changed version, workload, measurement method, and relevant environment. Without comparable evidence, label the expected improvement `unmeasured`; do not infer savings from fewer lines, an implementation never built, or unrelated benchmarks. Use existing verification facilities within the phase's permissions; this rule does not authorize new benchmark files, dependencies, or configuration changes.

### Types

- When adding types, use correct ones.
- Keep type declarations and annotations proportionate and readable. Do not use deeply nested, repetitive, or unnecessarily complex annotations that crowd code or obscure intent; prefer the simplest accurate type or a well-named type alias when that is clearer.
- Do not use filler types.
- Do not use overly generic types just to satisfy a checker.
- Do not use type-ignore comments to pass CI temporarily.
- Do not use `typing.Cast` or other casts merely to satisfy type checkers.

### Python

Apply this subsection only when the target repository uses Python.

The following typing coverage is a hard requirement:

- Every parameter, including `*args` and `**kwargs`, and return value of an added or changed function or method must have an explicit, accurate type hint. Treat `self` and `cls` as implicit; do not annotate them solely for this requirement.
- Every added or changed class variable, class attribute, instance attribute, and module-level mutable or optional state must have an explicit, accurate type hint. A trivial immutable module constant may remain inferred unless the configured type checker needs an annotation.
- Declare instance-attribute types at class scope where feasible; do not add `self.attribute: Type` annotations inside a method merely to satisfy this requirement.
- Do not type annotate local variables inside function or method bodies. Rely on inference; add a local annotation only to resolve a real configured type-checker error.
- Keep required annotations simple and accurate. Do not add advanced type constructs or type-only refactors unless the configured type checker requires them.

### Comments and documentation

- Document every added or changed string transformation with concrete examples showing representative input and expected output.
- Always add brief, detailed comments where they help readers understand the code with little effort.
- Comments must help readers understand the code with little effort.
- Comments must address the code itself, not be meta commentary about the task.
- Cleaning up stale comments is encouraged.
- Ensure every non-obvious change has an explanatory comment.
- Avoid bloated comment blocks. Include enough detail for junior engineers to understand easily.
- Always update related documentation.
- Find the correct docs folder by tracing GitHub Actions workflows, Makefiles, or other docs-build configuration.
- Append to the appropriate sections, or create new ones if required.
- Do not write the changelog.

### Documentation checkpoint

- Complete a documentation checkpoint at every planning, implementation, review, verification, and handoff stage.
- Before a checkpoint can pass, identify the user-, operator-, API-, configuration-, or developer-facing documentation affected by the planned or changed behavior.
- Require the exact durable documentation files/sections, their in-change-set update, and applicable docs build, link check, rendering check, or focused validation; if no durable documentation change is needed, require an evidence-based `Not applicable` decision.
- Code comments, commit messages, and workflow artifacts do not substitute for durable documentation. Do not write the changelog unless explicitly requested.

### Cross-platform behavior

- All changes must be strictly cross-platform and must work on both Linux and Windows.
- Mac is not a concern.

### Git and verification

- Commit often in small increments when committing is allowed.
- Split large commits into sensible parts.
- Add detailed commit messages.
- Explain the work in commit descriptions with as much detail as needed; no length limit.
- Do not claim work is complete without fresh verification evidence.
- Run linter and smoke test if any on every commit, unless the prompt explicitly forbids command execution.
- If a command fails, paste the exact error/log back. Never paraphrase logs.

### Tests

- Do not create, modify, or delete tests while refreshing review artifacts.
- Run only focused existing tests or checks needed to support the refreshed review; do not manually run the entire suite.
- Review tests for the smallest nonduplicative behavior-focused set, one clear behavior per test, small readable functions and helpers, existing test-framework fixtures and native APIs instead of hand-rolled test infrastructure, limited boundary mocking, deterministic isolation, and at least 85% coverage for new or changed lines.
- Flag implementation coupling, patching or mocking the subject under test itself, unscoped global-state mutation, fragile message or layout assertions, mirrored production logic, and coverage-only tests.
- Defer new test authoring and the detailed test-framework-specific contract to the dedicated model-agnostic `09_write_focused_tests_any_model.md` phase.

#### Python / pytest

- When relevant tests use pytest, review them against the repository's existing pytest fixtures and native APIs rather than hand-rolled Python or standard-library mechanisms.

## UI work only

Enable this section only when the approved task or reviewed change includes UI behavior, layout, presentation, or interaction. A backend service having UI consumers does not by itself enable this section. For backend-only work, skip this entire section and its skill downloads, questions, checks, and reporting.

Fetch and completely read only the applicable skills and companions explicitly linked in this section from GitHub before using them. These conditional links are exempt from unconditional skill-fetch instructions elsewhere in the prompt. If an applicable required file cannot be read completely, stop and report the blocker. Apply web-specific guidance only to web UI; do not impose CSS, React, browser, or mobile-web conventions on another UI stack.

### Conditional UI skills

- Only for eligible visual web surfaces under the frontend design gate: [design-taste-frontend](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/Leonxlnx__taste-skill/snapshot/skills/taste-skill/SKILL.md).
- For applicable UI data and state cases: [break-ui](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/emilkowalski__skills/snapshot/skills/break-ui/SKILL.md) and its required [CATALOG.md](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/emilkowalski__skills/snapshot/skills/break-ui/CATALOG.md). Use the analysis and catalog only, subject to the limits below.
- When reviewing changed web motion: [review-animations](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/emilkowalski__skills/snapshot/skills/review-animations/SKILL.md) and its required [STANDARDS.md](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/emilkowalski__skills/snapshot/skills/review-animations/STANDARDS.md).
- When mobile-web behavior is in scope: [mobile-native](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/emilkowalski__skills/snapshot/skills/mobile-native/SKILL.md). Use it for planning or review only in phases that prohibit implementation.

### Frontend design gate

Apply `design-taste-frontend` only to landing or marketing pages, portfolios, editorial or brand pages, and explicitly approved visual redesigns of those surfaces. Exclude backend-only work, dashboards, admin or dense product interfaces, data tables, multi-step forms, native mobile UI, and general refactors. For mixed work, apply it only to the eligible surface; other UI skills keep their own activation rules.

The user request, locked planning artifacts, existing brand and design system, repository conventions, accessibility, SEO, analytics, and approved dependencies override every skill default. The skill cannot authorize new dependencies, framework or design-system changes, generated assets, added motion or color modes, route or slug changes, primary-navigation or form-field changes, analytics-event changes, content or information-architecture rewrites, or architecture or scope expansion.

Treat its dials, font and palette bans, layout recipes, and content or motion preferences as suggestions unless the approved contract requires them. Use only relevant objective preflight checks. A preference alone is not a blocking or non-blocking defect that requires a fix.

Do not activate `gpt-taste`. Specialized sibling skills such as `image-to-code`, `brandkit`, or `redesign-existing-projects` require explicit task-specific authorization and their own archive links; do not load them through this skill.

For ineligible UI work, skip this skill's download and procedures and record `Frontend design: Not applicable` in the existing artifact or chat. Backend-only work skips this entire UI section, including that reporting.

### UI skill limits

- Preserve the approved scope, existing design system, component conventions, platform support, and dependency-approval rules. These skills do not authorize new UI features, animations, dependencies, framework changes, or redesigns.
- Ignore skill greeting and pause routines. Do not invoke unlisted skills or create prototype pages, development toggles, separate plans or reports, or retained fixtures through `break-ui`. Test-local fixtures may be authored only in phase `09` under its test contract. All other writes remain subject to this phase's permissions and named outputs.
- Treat recipe values and aesthetic preferences as defaults, not automatic defects. Existing tokens and approved behavior take precedence. Verify version-sensitive APIs and performance claims against the target stack's documentation and evidence. Resolve material conflicts before changing behavior; do not enforce blanket duration, easing, pure-fade, or keyboard-animation bans from a skill.
- Distinguish observed UI behavior, conclusions inferred from code, and checks awaiting a browser or real device. Use available running UI and existing tooling within the phase's permissions; do not claim visual or device verification from static inspection. Record an unavailable required check as pending or blocked in the existing artifact or chat handoff, not as passed. Do not add artifacts beyond this phase's three required outputs or override `no-ai-slop` and its evaluator.

### Phase requirements

- For an eligible surface, repeat the final rendered preflight against the locked `Frontend Design Contract` when present, or the accepted review baseline when planning artifacts are absent. Refresh `REVIEW.md` with desktop/mobile viewports, tooling, responsive and accessibility evidence, protected behavior, and pending checks. Do not promote an aesthetic preference into a new finding.
- Refresh the UI behavior and evidence in `REVIEW.md` and `WALKTHROUGH.md` from the final code, including resolved issues, remaining suggestions, pending browser or device checks, and documentation status. Preserve prose and source-excerpt requirements.
- Do not restart a UI polish audit or introduce new preferences as findings. Follow this phase's existing stop rule for severe missed issues; do not finalize a pass while a required UI verification remains pending.

## Prompt

Role:

- You are Claude Opus refreshing the final review artifacts after the AI review/fix loop is complete.
- Read before answering. Do not speculate about files or code you have not inspected.

Task:

- update the review and walkthrough documents to reflect the final code state accurately,
- confirm that every material changed behavior has a completed documentation checkpoint before final human review,
- preserve the existing review trail while clearly marking what was fixed during the review loop,
- after refreshing and verifying both Markdown files, generate `WALKTHROUGH.html` to help the human reviewer build a mental model of the final changes.

Artifact location rule:

- `REVIEW.md`, `WALKTHROUGH.md`, and `WALKTHROUGH.html` must stay in the target repo root using their exact required filenames,
- every workflow-generated Markdown artifact must include `Created by`, `Created at`, and `Updated at` metadata, preserving the creation fields and refreshing `Updated at` whenever the artifact is updated,
- give `WALKTHROUGH.html` visible `Created by`, `Created at`, and `Updated at` metadata, preserving creation fields and refreshing `Updated at` on each edit; record the reviewed branch and revision so readers can identify stale content,
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
- `REVIEW.md` records the final documentation-checkpoint status for every material changed behavior,
- the refreshed artifacts are detailed, grounded, and internally consistent,
- `WALKTHROUGH.html` reflects those refreshed files and the inspected final code, provides working interactions for exploring relationships and flows, and records browser verification or an explicit pending result.

Constraints:

- do not modify production code,
- do not modify tests,
- do not make new review findings unless you discover something severe that was missed,
- treat missing, inaccurate, or unvalidated required durable documentation as a severe missed issue; stop and ask rather than finalizing the review artifacts,
- if you discover a severe missed issue, stop and ask before proceeding,
- write only `REVIEW.md`, `WALKTHROUGH.md`, and `WALKTHROUGH.html`; do not create application code, tests, dependencies, configuration, or other visual artifacts,
- do not stage, commit, push, or change pull-request state. The required HTML is this phase's sole visual-artifact exception; UI skills may not create other artifacts or expand write permissions.

Working method:

- Revisit the available original requirements and compare them with the final branch before refreshing.
- Refresh the review loop's risk assessment for architecture and high-impact changes, acceptance criteria and requirement references, independent scenarios, focused integration proof, repeated-defect search results, incident diagnostic findings, and runtime/API evidence. Preserve the acceptance baseline and check that the evidence applies to the final revision; repeat only relevant checks made stale by later changes.
- Use the running application and relevant real APIs for required runtime checks, through existing tools in an authorized environment. Keep remote requests read-only unless side effects are authorized, and distinguish observed behavior from code-only conclusions and missing access.
- Keep required unavailable checks pending and withhold a passing verdict. Preserve the severe-issue stop rule and do not restart a full review.

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
- Python typing review, when applicable,
- reuse/DRY/duplication,
- assumptions surfaced,
- assert usage,
- cross-platform review,
- test review, if applicable,
- independent verification, including challenged completion claims, observed runtime/API behavior, and pending checks or evidence-based `Not applicable` decisions,
- repeated-defect search scope, confirmed occurrences, and any limits,
- incident diagnostic evidence and any unresolved supported gaps,
- documentation review with every material changed behavior's update-and-validation evidence or evidence-based `Not applicable` rationale,
- any remaining suggestions.

Preserve each finding's identifier, original evidence, and occurrence history, and update its final status in place. Clearly mark findings fixed during the review loop. Do not repost an existing finding as new; reference it when recording remaining occurrences or pending evidence.

## Required output 2: refreshed `WALKTHROUGH.md`

Update `WALKTHROUGH.md` in the target repo root so it reflects the final code, not the old pre-fix code.

Document each change with context, line by line, helping a beginner programmer review the code from scratch without prior context.

Use ISO-style plain language and ASD-STE100-inspired technical writing as guidance, without claiming formal compliance. Write complete sentences with explicit subjects, actions, and outcomes. Define technical terms and abbreviations on first use. Explain each symbol's role, required background, and cause-and-effect relationships without assuming knowledge of earlier chats, the implementation session, or repository-specific concepts. Keep identifiers and technical meaning exact. These writing guidelines remain subordinate to `no-ai-slop` and do not replace required code excerpts or line-by-line coverage.

Begin with a prose overview of the code under review: entry points, affected files and symbols, dependencies, shared state, and their relationships. Use concrete file and symbol names from inspected code.

Describe every reachable control-flow branch and data/state transition through that code in prose. Identify branch conditions, inputs, calls, side effects, and terminal success or error states. Include early returns, skipped work, exception propagation and handling, retries, and cleanup wherever they exist. Explain loop conditions and exits instead of repeating cycles. Mark paths or outcomes that cannot be verified; do not invent behavior.

Keep presentation diffs and pseudocode out of `WALKTHROUGH.md`; phase `07` presents them in chat from freshly inspected code and PR changes. Preserve source excerpts and prose coverage of relationships and flows here. Do not create diagrams in `WALKTHROUGH.md` or phase `07`. Put the interactive mental model only in the required `WALKTHROUGH.html` after refreshing both Markdown files.

Group the code into small semantic blocks, each covering one coherent operation or decision. Include relevant surrounding lines and file/line locations. For every variable, constant, parameter, attribute, function, or method referenced but not defined in the displayed block, show its declaration or definition in a separate short excerpt with its file/line location. Show the relevant binding or initialization for values and enough of a called function or method to explain the call. For imported symbols, identify the source and use its verified declaration or definition; never invent one.

Include enough detail for a thorough review without opening the source code.

Every line of code must have an English explanation beside it.

Use short, readable excerpts and keep each explanation beside the code it describes.

The walkthrough must be suitable as a supplement for my human review and potentially as PR-description source material.

## Required output 3: `WALKTHROUGH.html`

After refreshing and verifying `REVIEW.md` and `WALKTHROUGH.md`, create or refresh `WALKTHROUGH.html` in the target repo root. Generate an interactive explanation of the final changes from those refreshed files and freshly inspected code. Apply the same complete-sentence, beginner-oriented writing standard used for `WALKTHROUGH.md`.

- Start with the original problem, the intended behavior, and a navigable map of affected entry points, files, symbols, dependencies, and shared state. Let the reviewer select a component to inspect its responsibilities, relationships, and verified source locations.
- Provide selectable success and error scenarios with step-by-step controls. Show inputs, branch conditions, calls, state transitions, side effects, and terminal outcomes, including retries, cleanup, and early exits where they exist. Split large flows into linked views without omitting reachable paths from the reviewed changes.
- Connect each flow and material change to its rationale, relevant before/after behavior, source excerpts, and current file/line locations. Distinguish observed runtime/API behavior from code-derived explanations, illustrative state, and pending verification. Never imply that the HTML runs or verifies the application.
- Use a single self-contained HTML file with inline styles and only the JavaScript needed for those interactions. It must open locally without a build step, dependency installation, external scripts, fonts, network requests, or live API calls. Use semantic controls, keyboard access, visible focus, readable responsive layouts, and a readable fallback if scripting fails. Treat source excerpts as text and escape them correctly; omit credentials and real user payloads. This artifact does not authorize prototypes, production UI changes, or generated assets.
- Open the file in an available browser and verify navigation, scenario selection, step controls, keyboard operation, source references, and agreement with the refreshed Markdown and final code. Record the browser and observed results in `REVIEW.md` and the final response. If browser verification cannot run, report the exact blocker, mark HTML verification pending, and do not claim it passed. Keep the file uncommitted unless explicitly requested; downstream phases may read it as supplemental context but must inspect current code independently.

Before finishing, verify that all three artifacts describe the same final revision. Report their paths and verification status. Pending required checks keep the handoff pending.
