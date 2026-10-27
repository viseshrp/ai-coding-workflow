# 04 - Review Implemented Branch - Any Model

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

Use linked companions within this phase's scope. Skip UI-only sections for backend work, preserve the test-authoring boundary and named outputs, and do not run optional bootstrap scripts. When this phase generates a downstream prompt, embed this archive-only rule, every applicable explicit skill and companion link, and the same scope limits.

Apply the activation and skill-loading rules in `## UI work only` to all UI skill links, including generated-prompt templates. Skip those links when UI work is out of scope. Keep all other required skill loading unchanged.

Use only this prompt's explicitly linked skills.

Fetch and read each linked skill and required companion completely from its GitHub URL before use. Follow the linked procedures directly; do not depend on local skill repositories, installed slash commands, or earlier prompt text.

The prompt is the contract. When locked task artifacts are present, they are authoritative review context. Their absence does not block this phase. Skills are supporting procedures only.

If a skill conflicts with this prompt, this prompt wins.

If a conflict is material, stop and ask instead of silently choosing.

Do not use any skill to expand scope, add architecture changes, add tests, add unrelated refactors, or override my explicit instructions.

`no-ai-slop` is mandatory for every Markdown document this phase creates or revises. Treat it as the ultimate writing guide and final authority for prose and presentation after satisfying this prompt's factual, technical, structural, and output requirements. If another skill or instruction conflicts only on writing style, `no-ai-slop` wins; this prompt and any available locked task artifacts still control scope, meaning, required structure, artifact names, constraints, and evidence.

Apply `no-ai-slop` while drafting and run its `eval.md` self-check before saving each Markdown artifact or sending the final response. If its `SKILL.md` or `eval.md` cannot be read and applied, stop before creating or revising Markdown and report the blocker. Ignore its draft-request, detection-mode, and mandatory `What changed` workflow unless this prompt explicitly asks for them.


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
- Identify the installed or explicitly approved library/framework version and use documentation and source for that version. Do not treat an unapproved version upgrade as an implementation detail.
- If documentation is poor and the library is open source, find its source code, clone it in a temporary folder, and read it thoroughly to supplement the documentation.
- Ensure usage follows the latest APIs.
- Flag outdated APIs, including deprecated or unsupported usage.
- If using the latest API would require an unapproved dependency upgrade, conflict with the approved version, or break backwards compatibility, stop and ask. Do not upgrade the dependency or silently relax the latest-API requirement.
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
- Before adding new behavior, trace how the repository already handles comparable behavior: component responsibilities, dependency direction, shared services, and extension points. Build on those established flows instead of creating a parallel flow, duplicate infrastructure, or a path that bypasses an existing layer. If the approved scope appears to need a parallel path, or the established path cannot support the change without an architecture decision, stop and ask. In review-only phases, flag an unapproved parallel flow with concrete repository evidence and name the established path the code should use.
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
- Always update related documentation during authorized implementation and fix passes. Planning, review, and verification phases must identify required updates and require their completion through the documentation checkpoint; they must not edit durable documentation when their scope forbids it.
- Do not mark documentation `Not applicable` merely because the current phase has no permission to edit it.
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
- If repository support or an explicitly approved task requirement conflicts with this platform rule, stop and ask. Do not silently waive Linux/Windows support, drop existing required platform support, or expand the platform scope.

### Git and verification

- Commit often in small increments when committing is allowed.
- Split large commits into sensible parts.
- Add detailed commit messages.
- Explain the work in commit descriptions with as much detail as needed; no length limit.
- Do not claim work is complete without fresh verification evidence.
- Run linter and smoke test if any on every commit, unless the prompt explicitly forbids command execution.
- If a command fails, paste the exact error/log back. Never paraphrase logs.

### Tests

- Do not create, modify, or delete tests in this review phase.
- Run only focused existing tests or checks needed to substantiate findings; do not manually run the entire suite.
- Review existing or changed tests for the smallest nonduplicative behavior-focused set, one clear behavior per test, small readable functions, fixtures, and helpers, native APIs from the existing test framework, limited external-boundary mocking, deterministic isolation, and the full 85% changed-line coverage requirement. Flag mocking the subject itself, hidden global state, private implementation coupling, fragile message/layout assertions, mirrored expected values, and coverage-only tests.
- Defer all test authoring to the dedicated model-agnostic `09_write_focused_tests_any_model.md` phase. These review criteria do not authorize writing test files, scripts, fixtures, or instrumentation.
- Assess existing tests against independent requirements. Assign findings that require only test changes or final coverage proof to `09` with status `Deferred to 09`; do not require their implementation during review fixes.
- Phase `09` owns test authoring, focused integration tests, and the final 85% changed-line coverage gate; phase `10` audits them. Deferred test work does not block the earlier review handoff, but production defects, failed acceptance behavior, and missing required runtime verification do.

## UI work only

Enable this section only when the approved task or reviewed change includes UI behavior, layout, presentation, or interaction. A backend service having UI consumers does not by itself enable this section. For backend-only work, skip this entire section and its skill downloads, questions, checks, and reporting.

Fetch and completely read only the applicable skills and companions explicitly linked in this section from GitHub before using them. These conditional links are exempt from unconditional skill-fetch instructions elsewhere in the prompt. If an applicable required file cannot be read completely, stop and report the blocker. Apply web-specific guidance only to web UI; do not impose CSS, React, browser, or mobile-web conventions on another UI stack.

### Conditional UI skills

- Only for eligible visual web surfaces under the frontend design gate: [design-taste-frontend](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/Leonxlnx__taste-skill/snapshot/skills/taste-skill/SKILL.md).
- For web UI design decisions: [emil-design-eng](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/emilkowalski__skills/snapshot/skills/emil-design-eng/SKILL.md).
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
- Distinguish observed UI behavior, conclusions inferred from code, and checks awaiting a browser or real device. Use available running UI and existing tooling within the phase's permissions; do not claim visual or device verification from static inspection. Record an unavailable required check as pending or blocked in the existing artifact or chat handoff, not as passed. Do not add a new artifact or override `no-ai-slop` and its evaluator.

### Phase requirements

- For an eligible surface, establish the baseline from the locked `Frontend Design Contract` when present. If planning artifacts are absent, use the user brief, repository contracts, existing brand/design system, and branch evidence; do not invent a missing contract or block direct-entry review merely because it is absent.
- Inspect the eligible rendered UI at representative desktop/mobile viewports with existing tooling when available. In `REVIEW.md`, record the baseline, viewports, tooling, responsive and accessibility evidence, protected SEO/routes/forms/analytics behavior, objective failures, and pending checks. Require measured evidence for performance regressions; keep uncontracted aesthetic alternatives in `Suggestions`.
- Inspect the changed UI and relevant existing behavior against approved requirements or, if planning artifacts are absent, repository contracts and the branch diff. Check applicable data and state cases, container widths, zoom, keyboard and focus, touch access, reduced motion, and mobile-web behavior.
- Review changed motion for purpose, frequency, interruption, exit, token reuse, and supported accessibility behavior. Reproduce material issues with existing tooling where available; cite the location, triggering case, expected behavior, and evidence. Treat unsupported aesthetic preferences as optional suggestions, not blocking or non-blocking defects that require fixes.
- Record UI evidence, pending browser or device checks, and documentation results inside the existing review artifacts. Do not create fixtures, toggles, prototypes, or a separate UI report; do not change production code or tests.

## Prompt

Role:

- You are a capable repository-aware model or agent performing post-implementation review in an existing codebase.
- Run this review in a fresh session or agent that does not carry the implementation or review-fix context. If you implemented or fixed these changes in this session, stop and ask for a fresh reviewer.
- Read before answering. Do not speculate about files or code you have not inspected.

Task:

- Independently review the changes selected for this pass against available requirements and public contracts, the existing architecture, and any available locked planning artifacts.
- On the first pass, review all changes introduced by the current branch. On later passes, review only changes since the last independently reviewed or verified state recorded in `REVIEW.md` or `REVIEW_FIX_VERIFICATION.md`, whichever is later, and the paths they affect; carry forward earlier conclusions unless those changes invalidate them.
- Identify real defects, plan divergence when a plan is available, and high-value follow-up suggestions without expanding scope.
- Identify all possible regressions caused by the selected changes, including indirect effects on existing callers, behavior, compatibility, and error paths.
- Identify meta content in the selected changes, such as comments, docstrings, documentation, or user-facing text that describes the branch, task, implementation process, or the fact that a change was made instead of describing the resulting code or behavior.
- Complete the review even when no prior planning or execution artifacts exist. The current branch diff and repository evidence are sufficient to start this workflow at phase `04`.

Context to review:

- the current branch diff against the head of `main`, plus the diff since the last independently reviewed or verified state on later passes. Record exact base and head revisions and the comparison used; include newly affected integration paths if `main` changed since the earlier review,
- affected code, callers, public interfaces, configuration, durable documentation, and existing tests,
- existing `REVIEW.md` and `REVIEW_FIX_VERIFICATION.md`, if present, for the last independently reviewed or verified state, finding identifiers, statuses, pending checks, and the new issues recorded under `New Issues Introduced`,
- `FEATURE_SPEC_AND_PLAN.md`, if present,
- `SPEC.md`, if present,
- `IMPLEMENTATION_PLAN.md`, if present,
- any local `PLAN*.md` files in the repo root, if available,
- `EXECUTION_PROMPT.md`, if present,
- the pull-request description, plus the implementation or review-fix pass's final response if it is supplied, for existing-test failures it reported as caused by an intended behavior change.

The named planning and execution artifacts are optional. Do not require, recreate, or ask for them merely because they are absent.

Success criteria:

- every reported issue is actionable and grounded in inspected repository evidence and applicable requirements, contracts, or available plan evidence,
- plan divergence is clearly separated from optional suggestions when a plan is available; when no plan is available, its absence is recorded without becoming a finding or blocker,
- every material changed behavior has a documentation-checkpoint result grounded in the actual branch: exact durable documentation and validation, or an evidence-based `Not applicable` decision,
- the review and generated review-fix prompt remain usable without any artifact from an earlier workflow phase,
- the outputs are detailed enough to drive both the review-fix phase and the final human walkthrough.

Constraints:

- do not modify code during this phase,
- create or update only `REVIEW.md`, `WALKTHROUGH.md`, and `REVIEW_FIX_PROMPT.md`. Do not edit production code, tests, durable documentation, configuration, dependencies, Git state, or pull-request state,
- give `REVIEW.md`, `WALKTHROUGH.md`, and `REVIEW_FIX_PROMPT.md` `Created by`, `Created at`, and `Updated at` metadata. On later passes, preserve the creation fields and refresh `Updated at`,
- backwards compatibility is top priority,
- do not stop or ask for input solely because prior-phase artifacts are absent,
- do not invent undocumented intent; evaluate objective correctness and repository compatibility, and label genuinely intent-dependent conclusions as open questions,
- do not report preferences, speculative risks, or unverified assumptions as findings; require evidence of a defect or contract mismatch.

Working method:

- compare the current branch against the current head of `main` to establish scope. Review that full branch change on the first pass. For later passes, establish the last independently reviewed or verified base, head, and working-tree state from `REVIEW.md` `## Review Basis` or `REVIEW_FIX_VERIFICATION.md` `## Verification Basis`, whichever is later, or from Git/PR evidence; review only new changes and paths newly affected by changes to the branch, `main`, requirements, or repository contracts. Account for previously reviewed uncommitted changes as well as commits; do not treat an unchanged working-tree diff as new. If the prior baseline cannot be recovered, review only identifiable new changes and keep the remaining scope pending; do not silently restart a full review,
- establish the review basis from the diff and repository evidence before judging. Confirm that prior evidence belongs to this branch and change; ignore unrelated review artifacts and treat a branch with no prior review as an initial pass. Reuse evidence only when the relevant behavior, contracts, dependencies, configuration, and environment are unchanged,
- inspect actual code, affected callers, existing contracts, durable documentation, and actual diff before judging,
- trace how comparable behavior fits into the existing architecture: component responsibilities, dependency direction, shared services, and extension points. Verify that changed code uses those paths and preserves ownership boundaries. Flag unapproved parallel abstractions, duplicate infrastructure, or bypassed architectural layers with concrete repository evidence,
- give architecture and other high-impact changes deeper scrutiny, including changes to shared behavior, public contracts, persistent data, security boundaries, or concurrency. Assess impact from affected consumers and failure consequences, even for small diffs. Trace the relevant compatibility, migration, and failure/recovery paths and prioritize independent verification of those risks,
- when planning artifacts are available, audit compliance with them; when they are absent, use the branch diff as the scope boundary and existing behavior, public APIs, documentation, configuration, and tests as evidence,
- flag plan divergence only when an available planning artifact provides evidence of divergence,
- quote or clearly point to the exact evidence for each material finding,
- separate confirmed issues from preferences, open questions, and optional suggestions,
- do not recreate missing prior-phase artifacts or treat their absence as a review defect,
- assess 100% of the requirements in every available plan during the initial review, or complete the full evidence-based branch review when no plan is available, before reporting applicable suggestions. On later passes, update the affected requirement-to-evidence entries and carry the unchanged entries forward with their original evidence; do not silently drop a requirement, unresolved finding, or pending check because it is outside the new diff. Use `None.` when no concrete optional suggestion is supported,
- do not make any changes you propose until I give the go-ahead.

This branch will be merged into main.

## Review dimensions

Review for:

- readability,
- quality,
- correctness, including missing edge cases, regressions, incorrect assumptions, and integration failures,
- idiomatic use of the target language and its standard library,
- type declarations and annotations that clarify rather than crowd the code; flag overly complex annotations when a simpler accurate type or well-named type alias would improve readability,
- backwards compatibility,
- performance,
- alignment with the existing architecture and reuse of established components, services, abstractions, and extension points,
- plan compliance when planning artifacts are available; otherwise record that plan compliance was not assessed,
- minimal change scope and blast radius; flag changes to surrounding code unless they are absolutely necessary for the branch's changed behavior or an available task contract,
- source/documentation grounding,
- every string transformation in code is documented with concrete examples showing representative input and expected output,
- completion of the documentation checkpoint for every material changed behavior, including durable documentation accuracy, validation, and any `Not applicable` rationale,
- justified library/framework usage,
- outdated APIs, including deprecated or unsupported usage and version conflicts that require an explicit decision,
- public API usability/intuitiveness/naming/blending with existing APIs,
- assumptions in code,
- assert statements in production code,
- reinvention/duplication of existing code,
- excess abstractions, unused paths, and avoidable complexity, with caller and contract evidence before recommending removal,
- incident diagnostics for changed failure paths,
- comment quality and missing comments where code is not obvious,
- bloated comment blocks,
- cross-platform Linux/Windows safety, including explicit escalation of conflicts with repository or approved platform requirements,
- test quality for tests that already exist or were explicitly requested, plus missing tests for material acceptance criteria. Identify the missing test work without authoring it in this phase.

### Language-specific review guidance

#### Python

- When the reviewed code is Python, assess whether it uses the language and standard library idiomatically.
- Treat missing or inaccurate type hints on any added or changed function or method parameter, including `*args` and `**kwargs`, return value, class variable, class attribute, instance attribute, or module-level mutable or optional state as a blocking finding. Do not require `self`, `cls`, or trivial immutable module constants to be annotated solely for this requirement; preserve configured-checker requirements.
- Flag local variable annotations inside function or method bodies unless a real configured type-checker error requires them. Also flag advanced, crowded, or type-only annotations that are not required by that checker.

Verify library/framework usage against the correct documentation; ground 100% of usage in those docs. If documentation is poor and the library is open source, find its source code, clone it in a temporary folder, and read it thoroughly to supplement the documentation. Use documentation and source for the installed or explicitly approved version.

Ensure usage follows the latest APIs and flag outdated APIs. If that conflicts with the approved version, dependency approval, or backwards compatibility, stop and ask instead of upgrading or relaxing the requirement.

If the changes touch public APIs or add new public APIs, check whether they are user-friendly and intuitive, blend well with the existing public API set, and have appropriate names.

Surface all assumptions in the code.

Report assert usage and flag any assertions outside test files.

If the changes reinvent/duplicate something already in the source code, flag it.

Ensure every non-obvious change has an explanatory comment. Avoid bloated comment blocks. Include enough detail for junior engineers to understand easily.

All changes must be strictly cross-platform and must work on both Linux and Windows. Mac is not a concern. Escalate any conflict with existing required platform support; do not silently waive either requirement.


## Independent verification and incident diagnostics

Independently challenge the author's completion claims using the procedure below. Tests can reinforce the same unsupported assumptions as the implementation. Judge both against acceptance criteria grounded in product requirements and public contracts; passing author-written tests alone do not establish correct running behavior.

1. Re-read the original requirements and approved scope changes, when available. Map each material requirement and completion claim affected by the selected changes to the current code and evidence. Look for omitted behavior, unintended additions, and drift after long coding sessions. If intent is unavailable, identify that limit rather than inventing requirements.
2. Establish independent acceptance criteria and expected outcomes from the available requirements, approved clarifications, and public contracts before adopting the author's test cases or expected results. Use inspected code to identify paths to exercise, and try to disprove completion claims with relevant boundary, failure, recovery, and regression scenarios. Describe and exercise the scenarios with existing tools; do not author test files, scripts, or fixtures in this phase.
3. For changed runtime behavior, exercise the running application through its real entry points and call the relevant real APIs. Use an authorized local or test environment and existing tools. Remote requests must be read-only unless the user has authorized their side effects. Do not install dependencies or change configuration to enable a review. Record the revision, environment, scenario, expected result, observed result, command or interaction, and evidence. Keep observed behavior, code-only conclusions, and pending checks distinct. Missing access or an unavailable environment leaves the required check pending and prevents a passing verdict; explain `Not applicable` for changes with no runnable behavior.
4. When one defect is found, identify its root cause or defect category and search throughout the codebase for the same failure pattern, including sibling implementations and other callers. Inspect candidate matches and distinguish confirmed occurrences from false positives. Group confirmed occurrences only when the same failure mechanism and corrective rule apply, with evidence for each location and a correction that addresses the category. Record search scope and unexamined areas. On later passes, reuse that inventory and inspect new or affected occurrences rather than repeating an unchanged scan. Report occurrences outside the approved scope separately; discovery does not authorize broader fixes.
5. Inspect logs and error handling for the changed failure paths as if diagnosing an incident. Check whether an engineer could identify the failing operation, correlate a request or job, understand the cause and trace, and determine retry or recovery outcomes where applicable. Use captured runtime evidence when available and identify gaps in existing logging, while checking for secrets, sensitive payloads, or excessive noise. Do not add instrumentation during review.

## Test review rules

Review existing or changed tests; do not author tests in this phase.

- Require the fewest tests that cover distinct changed behavior and material regression risks. Flag duplicate, transient, temporary-hack, or coverage-only tests.
- Require observable behavior tied to an independent acceptance criterion and its requirement source, one clear behavior per test, and small linear test functions, fixtures, and helpers. Flag tests that validate an implementation assumption instead of the product requirement.
- For material component or API interactions, require focused integration proof through the actual public entry point and relevant components. Use existing integration checks and authorized running-application and real-API checks to verify current behavior; mocked unit tests alone do not prove those interactions. Record missing required automated integration tests as `Deferred to 09`; that does not defer current runtime verification or permit a passing claim without the required proof.
- Check that tests follow the existing test framework's configuration and conventions and prefer existing fixtures, native APIs, and installed extensions over hand-rolled test infrastructure.
- Flag any test that patches or mocks the function, method, or callable under test. Replacing the behavior being tested defeats the purpose of the test; only collaborators outside the subject may be patched.
- Limit mocks to impractical external boundaries; flag internal call choreography and implementation-detail mocks.
- Treat an existing test that fails only because it asserts behavior that a cited locked requirement or approved scope change explicitly replaces as a test-only finding with status `Deferred to 09`. Treat a failure caused by unintended behavior as a regression assigned to `Review fix`.
- Flag flakes and brittleness from global state, private helpers or constants, incidental error wording, layout assumptions, real time or uncontrolled network access, and expected values that mirror production logic.
- Require deterministic isolation and at least 85% coverage for new or changed lines using existing tooling. Run focused tests only, including every existing test that a reported intended behavior change affects. Record the measured coverage and its scope when available; missing test authoring or final coverage proof remains explicitly `Deferred to 09`, never passed or waived. The complete coverage gate must pass in `09` and be independently verified in `10`.

### Language-specific test review guidance

#### Python / pytest

- When relevant tests use pytest, check that they follow the existing pytest configuration and prefer existing fixtures and native APIs such as `monkeypatch`, `tmp_path`, capture fixtures, `pytest.raises`, `pytest.warns`, parametrization, and an installed mock fixture over hand-rolled Python or standard-library mechanisms.

Classify each concern as a real flake risk, an acceptable contract test, or a maintainability concern, and suggest a behavior-level alternative when practical.

## Required output 1: `REVIEW.md`

Create or update a detailed `REVIEW.md` document in the target repo root with:

```markdown
# Review

## Verdict

## Review Basis

## Plan Compliance

## Blocking Issues

## Non-Blocking Issues

## Backwards Compatibility

## Public API Review

## Performance / Complexity Review

## Source Documentation Grounding

## Code Quality / Readability

## Python Typing Review

## Reuse / DRY / Duplication

## Assumptions Surfaced

## Assert Usage

## Cross-Platform Review

## Test Review

## Independent Verification

## Repeated Defect Search

## Incident Diagnostics

## Documentation Review

## Suggestions
```

Report only actionable, evidence-backed findings under `Blocking Issues` or `Non-Blocking Issues`, ordered by severity within each section. For each finding, include:

- a stable finding identifier, status, destination (`Review fix` or `09`), severity, and a concise description of the defect category or root cause,
- the exact inspected file path and a narrow line range,
- the affected requirement or existing contract and the concrete impact,
- minimal reproduction steps with prerequisites, inputs, expected behavior, and the observed failure or failure shown by the code,
- the smallest justified correction or the acceptance check needed to demonstrate resolution.

Use exactly one of these finding statuses: `Open` (confirmed and not yet fixed), `Partially Resolved` (fixed for some, but not all, confirmed occurrences or acceptance checks), `Resolved` (fixed and verified with fresh evidence), `Invalid Finding` (disproved by inspected evidence, which the entry records), or `Deferred to 09` (test-only work assigned to phase `09`). Do not use other status values.

For static issues, provide repeatable inspection or call-trace steps that demonstrate the mismatch. Label unexecuted reproduction scenarios `Not run`; never invent observations. Keep unanswered intent questions and pending verification in the existing review-basis and evidence sections, separate from confirmed defects.

Every valid review issue must remain categorized under either `Blocking Issues` or `Non-Blocking Issues`, including test-only findings assigned to `09`. Put each finding's corrective suggestion directly below its evidence and reproduction steps. Keep broader optional improvements in `Suggestions` and reference the related finding identifier without reposting the finding.

Mark test-only findings `Deferred to 09`, retaining their identifiers, severity, evidence, and required scenarios in the issue list and `Test Review`. In `Verdict`, explicitly report whether all valid blocking and non-blocking findings are resolved, and keep that overall result `No` while any valid finding is deferred or unresolved. Separately report readiness for phase `06` and human code review, without implying completion of phases `09` and `10`. Deferral applies only to test work; it cannot excuse a production defect, failed acceptance behavior, or a required runtime check that has not passed.

Use `None.` under either issue heading when no actionable findings exist. Keep optional improvements in `Suggestions`; include only concrete, evidence-backed actions and write `None.` when there are none. Suggestions are not required in the review-fix pass.

Never repost the same finding. Match against existing findings by failure pattern and affected contract, even if wording or line numbers change. Preserve its identifier and original evidence in `REVIEW.md`, update its status and remaining occurrences in place, and reference that identifier in later responses and handoffs. Add new evidence or newly found occurrences of the same defect category to that entry; create a new finding only for a distinct defect. On a later pass, adopt each new issue recorded in `REVIEW_FIX_VERIFICATION.md` under `New Issues Introduced` into `REVIEW.md` under its assigned identifier, with its status, destination, severity, evidence, reproduction steps, and correction; do not repost it under a new identifier. Treat findings that phase `06` recorded in `REVIEW.md` as existing findings. Keep resolved entries as clearly marked review history outside active issue lists, without requiring unchanged fixes again.

In `## Review Basis`, record the initial comparison against `main`, exact base and head revisions, the previous reviewed or verified state and the current reviewed revision, any uncommitted changes included, and the scope of this pass. Record enough evidence to identify the reviewed working-tree state on a later pass; a commit SHA alone does not identify uncommitted content. List the repository evidence inspected and every optional planning or execution artifact that was available. If none was available, state that the review was performed standalone from the branch diff and repository evidence. Identify architecture and high-impact changes that warranted deeper scrutiny, their affected consumers and failure consequences, and the additional evidence gathered or still required.

In `## Plan Compliance`, assess requirements affected by the selected changes against the available planning artifacts and retain prior conclusions for unchanged requirements. If none exists, write `Not assessed - no planning artifacts were provided.` Do not treat that absence as an issue or blocker.

In `## Code Quality / Readability` and `## Reuse / DRY / Duplication`, explain how the new code fits the existing architecture. Cite the relevant components, callers, and established paths it reuses or bypasses. Distinguish justified additions within the approved design from unapproved parallel architecture; for each supported mismatch, identify the existing path the code should use and the concrete compatibility or maintenance impact.

In `## Independent Verification`, record the independently derived scenarios, claims challenged, runtime/API evidence, and any pending checks or evidence-based `Not applicable` decision. In `## Repeated Defect Search`, record the pattern, search scope, confirmed occurrences, and limits, or state that no defect triggered a search. In `## Incident Diagnostics`, record the relevant failure paths, available diagnostic evidence, and supported gaps, or explain why logging does not apply. Categorize supported defects under the issue headings; keep evidence gaps explicit and do not report pending required verification as passed.

In `## Documentation Review`, record the documentation-checkpoint result for every material changed behavior. Treat missing, inaccurate, or unvalidated required durable documentation as a valid review issue rather than an optional suggestion.

## Required output 2: `WALKTHROUGH.md`

Create a detailed `WALKTHROUGH.md` in the target repo root documenting each change with context, line by line, helping a beginner programmer review the code from scratch without prior context.

On later passes, update only coverage affected by new changes and retain accurate unchanged explanations. Do not restart a review of untouched code to regenerate the walkthrough.

Use ISO-style plain language and ASD-STE100-inspired technical writing as guidance, without claiming formal compliance. Write complete sentences with explicit subjects, actions, and outcomes. Define technical terms and abbreviations on first use. Explain each symbol's role, required background, and cause-and-effect relationships without assuming knowledge of earlier chats, the implementation session, or repository-specific concepts. Keep identifiers and technical meaning exact. These writing guidelines remain subordinate to `no-ai-slop` and do not replace required code excerpts or line-by-line coverage.

Begin with a prose overview of the code under review: entry points, affected files and symbols, dependencies, shared state, and their relationships. Use concrete file and symbol names from inspected code.

Describe every reachable control-flow branch and data/state transition through that code in prose. Identify branch conditions, inputs, calls, side effects, and terminal success or error states. Include early returns, skipped work, exception propagation and handling, retries, and cleanup wherever they exist. Explain loop conditions and exits instead of repeating cycles. Mark paths or outcomes that cannot be verified; do not invent behavior.

Keep presentation diffs and pseudocode out of `WALKTHROUGH.md`; phase `07` presents them in chat from freshly inspected code and PR changes. Preserve source excerpts and prose coverage of relationships and flows here. Do not create diagrams, HTML, or additional visual artifacts.

Group the code into small semantic blocks, each covering one coherent operation or decision. Include relevant surrounding lines and file/line locations. For every variable, constant, parameter, attribute, function, or method referenced but not defined in the displayed block, show its declaration or definition in a separate short excerpt with its file/line location. Show the relevant binding or initialization for values and enough of a called function or method to explain the call. For imported symbols, identify the source and use its verified declaration or definition; never invent one.

Include enough detail for a thorough review without opening the source code.

Every line of code must have an English explanation beside it.

Use short, readable excerpts and keep each explanation beside the code it describes.

## UI section in the generated review-fix prompt

Always embed the following complete, isolated section in `REVIEW_FIX_PROMPT.md`, including its explicit skill links and companions. Use accepted `REVIEW.md` findings and the current branch as the UI contract when planning artifacts are absent. Retain the general Simplicity and reuse procedure in the full Engineering Contract for all work. Do not replace either contract with a reference to this phase.

```markdown
## UI work only

Enable this section only when the approved task or reviewed change includes UI behavior, layout, presentation, or interaction. A backend service having UI consumers does not by itself enable this section. For backend-only work, skip this entire section and its skill downloads, questions, checks, and reporting.

Fetch and completely read only the applicable skills and companions explicitly linked in this section from GitHub before using them. These conditional links are exempt from unconditional skill-fetch instructions elsewhere in the prompt. If an applicable required file cannot be read completely, stop and report the blocker. Apply web-specific guidance only to web UI; do not impose CSS, React, browser, or mobile-web conventions on another UI stack.

### Conditional UI skills

- Only for eligible visual web surfaces under the frontend design gate: [design-taste-frontend](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/Leonxlnx__taste-skill/snapshot/skills/taste-skill/SKILL.md).
- For web UI design decisions: [emil-design-eng](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/emilkowalski__skills/snapshot/skills/emil-design-eng/SKILL.md).
- For applicable UI data and state cases: [break-ui](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/emilkowalski__skills/snapshot/skills/break-ui/SKILL.md) and its required [CATALOG.md](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/emilkowalski__skills/snapshot/skills/break-ui/CATALOG.md). Use the analysis and catalog only, subject to the limits below.
- When implementing web motion: [animate](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/emilkowalski__skills/snapshot/skills/animate/SKILL.md) and its required [RECIPES.md](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/emilkowalski__skills/snapshot/skills/animate/RECIPES.md).
- Only when motion work requires choosing a web UI primitive: [pick-ui-library](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/emilkowalski__skills/snapshot/skills/pick-ui-library/SKILL.md), the procedure referenced by `animate`. Use it to evaluate existing options; new dependencies still require explicit approval.
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
- Distinguish observed UI behavior, conclusions inferred from code, and checks awaiting a browser or real device. Use available running UI and existing tooling within the phase's permissions; do not claim visual or device verification from static inspection. Record an unavailable required check as pending or blocked in the existing artifact or chat handoff, not as passed. Do not add a new artifact or override `no-ai-slop` and its evaluator.

### Phase requirements

- Use `design-taste-frontend` only for accepted findings about eligible surfaces already recorded in `REVIEW.md`. The exact finding, existing brand/design system, and any locked `Frontend Design Contract` bound the fix; do not implement optional aesthetic suggestions or redesign adjacent sections.
- For eligible fixes, recheck the affected rendered desktop/mobile viewports with existing tooling. In the final response's `## Frontend Design Verification`, record the accepted finding or contract, viewports, tooling, rendered results, responsive and accessibility checks, protected behavior, and pending checks alongside the documentation checkpoint.
- Implement only the approved UI behavior using existing components and tokens. Complete applicable loading, error, and empty states, keyboard, focus, and touch behavior, and realistic data handling from the plan or accepted finding.
- For approved motion, implement its purpose and frequency decision, interruption and exit behavior, reduced-motion alternative, and hover capability gating where relevant. Use the simplest compatible existing tool; no library is required merely for a fade.
- Verify the changed UI with applicable realistic data, container widths, zoom, supported locale/direction, keyboard/touch interaction, and rapid interruption. Verify mobile viewport, safe-area, scrolling, and input behavior when in scope. Use existing preview/data facilities; do not create tests or a dev toggle. Report observed results and any required device checks still pending in the existing handoff, alongside the documentation checkpoint.
- Apply these requirements only to valid accepted review findings. Do not implement optional aesthetic suggestions without approval.
```

Verify that the actual generated fix prompt includes the complete UI activation gate, links, companions, limits, requirements, and documentation checkpoint before handoff.

## Required output 3: `REVIEW_FIX_PROMPT.md`

Only this phase may author `REVIEW_FIX_PROMPT.md`. Create it in the target repo root as the final direct-use, paste-ready prompt for any capable repository-aware coding model to fix all valid `REVIEW.md` findings assigned to `Review fix`, including both blocking and non-blocking issues. Carry test-only deferrals to `09` without authoring tests here. There is no separate checked-in review-fix prompt file after this review step.

If a later verification pass, or a severe missed issue recorded by phase `06`, requires another fix iteration, return to this phase and regenerate `REVIEW_FIX_PROMPT.md` here. Do not create an alternate fix prompt in the verification phase.

It must be self-contained.

Do not generate:

- a helper prompt,
- a wrapper note around review findings,
- a partial instruction set that expects another checked-in fix prompt file,
- a checklist without the full direct-use review-fix contract.

The generated review-fix prompt must have a clear title and these top-level sections:

- `## Skills`
- `## Skill Handling Rule`
- `## Engineering Contract`
- `## UI work only`
- `## Prompt`

The generated review-fix prompt must include these skill links explicitly:

- [incremental-implementation](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/incremental-implementation/SKILL.md)
- [source-driven-development](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/source-driven-development/SKILL.md)
- [verification-before-completion](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/obra__Superpowers/snapshot/skills/verification-before-completion/SKILL.md)
- [receiving-code-review](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/obra__Superpowers/snapshot/skills/receiving-code-review/SKILL.md)
- [no-ai-slop](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/petergyang__no-ai-slop/snapshot/skills/no-ai-slop/SKILL.md), including its required [eval.md](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/petergyang__no-ai-slop/snapshot/skills/no-ai-slop/eval.md)
- Required planning and incremental-verification companion: [definition-of-done.md](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/references/definition-of-done.md). Apply it within this phase's scope, artifact policy, and test-authoring boundary.
- For the security checks and threat-model guidance referenced by the linked procedures: [security-and-hardening](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/security-and-hardening/SKILL.md), with [hardening-patterns.md](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/security-and-hardening/references/hardening-patterns.md) and [security-checklist.md](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/references/security-checklist.md). Use only the applicable analysis within this phase's permissions; do not start a separate hardening or incident-response task.
- For the stack-discovery procedure referenced by `incremental-implementation`: [test-driven-development](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/test-driven-development/SKILL.md), including [testing-patterns.md](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/references/testing-patterns.md). Use only stack discovery and existing-test verification here; do not author tests or invoke its test-first implementation cycle. Apply JavaScript/TypeScript examples only to a matching stack.

The generated review-fix prompt must include a `## Skill Handling Rule` that instructs the review-fix model to:

- use only the prompt's explicitly linked skills,
- fetch and read every required skill and companion completely from its GitHub URL before use, subject to the generated prompt's isolated UI activation rules; skip UI-only links for backend-only work; do not depend on local skill repositories, installed slash commands, or earlier prompt text,
- fetch skill procedures and required companions only from `https://github.com/viseshrp/ai-skills-archive`; resolve relative resource references to the linked archive copies; do not follow upstream skill URLs, install a skill package, or substitute an official-source copy; if a required archive resource is absent or unreadable, stop and report its exact missing path; keep optional related-skill mentions and provenance links inactive,
- treat the prompt as the contract,
- treat locked task artifacts as the contract for execution when they are present,
- proceed from `REVIEW.md`, `WALKTHROUGH.md`, and the current branch diff when prior planning or execution artifacts are absent,
- use skills as supporting procedures only,
- let the prompt win if a skill conflicts with it,
- stop and ask instead of silently choosing if a conflict is material,
- never use a skill to expand scope, add architecture changes, add tests, add unrelated refactors, or override my explicit instructions.
- require `no-ai-slop` for every Markdown document the phase creates or revises; use it as the ultimate prose and presentation guide,
- apply it while drafting, run its `eval.md` self-check before saving each Markdown artifact or sending the final response, and stop before creating or revising Markdown if its `SKILL.md` or `eval.md` cannot be read and applied,
- let `no-ai-slop` win over conflicting writing-style guidance while the prompt and any available locked task artifacts continue to control scope, meaning, required structure, artifact names, constraints, and evidence,
- ignore its draft-request, detection-mode, and mandatory `What changed` workflow unless this prompt explicitly asks for them.

The generated review-fix prompt must embed the full Engineering Contract above verbatim or stricter.

Also embed the complete `Test review rules` and its Python/pytest guidance as direct, review-only criteria inside the generated prompt's Tests section. Preserve every behavior, framework, mocking, isolation, brittleness, coverage, and routing criterion; do not replace the list with a reference to rules in this producer or to a missing section below. These criteria permit only focused existing-test verification and do not authorize test authoring before `09`.

Preserve every existing review-fix instruction at its full level of detail, including conditions, exceptions, approval gates, stop rules, enumerated evidence fields, and all skill/evaluator/companion links. Do not substitute a short reference to the Engineering Contract for the operational steps or final-response structure. Verify the actual generated `REVIEW_FIX_PROMPT.md` independently against both the complete contract and each instruction below before handoff.

Inside `## Prompt`, the generated review-fix prompt must use clear sections for:

- goal,
- success criteria,
- context to read before acting,
- execution posture,
- constraints,
- per-review-item process,
- focused verification,
- required final response.

Inside those sections, it must instruct the review-fix model as follows.

Goal:

- fix all valid findings assigned to `Review fix` and stop only when you have fresh verification evidence or a concrete blocker.

Success criteria:

- each implemented fix is validated against the actual review finding and the current code,
- all valid findings assigned to `Review fix` in `Blocking Issues` and `Non-Blocking Issues` are fixed, including minor non-blocking issues; findings marked `Deferred to 09` remain tracked for that phase,
- scope stays within the review contract and, when available, the original implementation contract,
- backwards compatibility is preserved,
- each fixed or retained material behavior completes its documentation checkpoint: applicable durable documentation is updated and validated in the same change set, or an evidence-based `Not applicable` decision is reported,
- verification evidence is reported clearly,
- any workflow-generated Markdown artifacts created or updated during the workflow remain in the target repo root and are never moved to subdirectories or alternate paths,
- any workflow-generated Markdown artifacts created or updated during the workflow include `Created by`, `Created at`, and `Updated at` metadata with `Updated at` refreshed on every edit,
- workflow-generated artifacts are not staged or committed unless I explicitly ask for that,
- `WALKTHROUGH.html` is also an uncommitted workflow artifact unless I explicitly ask for it to be committed; only phase `06` generates or refreshes it,
- the fix pass stages changes, commits them, pushes the branch, and creates a pull request only if the current branch does not already have one.

Context to read before acting:

- `REVIEW.md`,
- `WALKTHROUGH.md`,
- `REVIEW_FIX_VERIFICATION.md`, if present, for finding statuses and remaining occurrences,
- `FEATURE_SPEC_AND_PLAN.md`, if present,
- `EXECUTION_PROMPT.md`, if present,
- current branch diff against `main`.

Planning and execution artifacts are optional. When present, treat them as authoritative under this prompt. Their absence must not block work or trigger a request for them.

Execution posture:

- understand the context of the current branch or PR before editing,
- inspect the actual code and review artifacts before deciding whether a finding is valid,
- read likely relevant files in parallel before editing when that shortens the loop,
- prefer dedicated repo/search/edit tools over raw shell when available,
- carry through implementation and focused verification without waiting for step-by-step approval unless blocked.

Constraints:

- do not blindly implement every review comment,
- address all valid findings assigned to `Review fix`; do not implement findings marked `Deferred to 09`,
- if a valid fix makes an existing test fail only because the test asserts the behavior the finding requires changing, do not modify the test. Keep the fix, report the test name, exact failure output, cause, and finding identifier in the final response and in the pull-request description as test-only work for phase `09`, and do not claim the suite passes. If the failure shows a regression or an incorrect fix, correct the fix instead,
- if no unresolved finding is assigned to this pass, report that no review-fix changes are needed; do not create an empty commit or change branch or pull-request state,
- do not implement optional suggestions unless explicitly approved,
- keep all fixes within the scope established by `REVIEW.md` and the current branch diff; when the original implementation scope can be established from available planning artifacts, preserve it too,
- preserve plan scope when a plan is available,
- preserve backwards compatibility,
- fix valid architectural mismatches by using the established components and extension points identified in the review. Do not create a replacement architecture or broaden the redesign; stop and ask if a compliant fix requires a new architecture decision,
- before adding new code in any fix, trace how the repository already handles comparable behavior and build on those established components, shared services, and extension points. Do not create a parallel flow, duplicate infrastructure, or a path that bypasses an existing layer; stop and ask if a fix appears to require one,
- workflow-generated Markdown artifacts belong only in the target repo root using their exact required filenames,
- workflow-generated Markdown artifacts must include `Created by`, `Created at`, and `Updated at` metadata, preserving the creation fields after first write and updating `Updated at` on every edit,
- no architecture changes,
- no unrelated refactors,
- no tests unless explicitly asked,
- treat a valid documentation-checkpoint gap as a required review fix: update and validate the durable documentation in the same change set, or stop and ask if the required change would exceed the approved scope,
- stop and ask on ambiguity/conflict/context gaps.

Per-review-item process:

1. Verify the review item against the actual code.
2. Determine whether it is valid.
3. Fix each unresolved valid defect category assigned to `Review fix`, including minor valid issues. Confirm its root cause, inspect the existing occurrence inventory, and correct every confirmed occurrence within the approved scope. Use the smallest coherent correction; avoid broad mechanical replacements, unrelated refactors, or abstractions without a current need. Preserve finding identifiers in the fix summary, including deferred test work, and do not redo resolved fixes whose behavior is unchanged.
4. Complete the documentation checkpoint for the changed behavior before treating the review item as fixed.
5. Do not implement items from `Suggestions` unless explicitly approved.
6. If a review item is wrong, stale, or conflicts with an available plan or code reality, stop and ask.
7. If a review item requires a design decision not already made, stop and ask.
8. Check off fixes if a checklist exists.

Focused verification:

- before completion, check the full diff of this implementation pass against the Engineering Contract and approved scope,
- inspect all changes made by this fix pass for possible regressions, including indirect effects on existing callers, behavior, compatibility, and error paths. Fix regressions within the approved review-fix scope; stop and ask if a fix would exceed it,
- inspect the changes made by this pass for added or changed meta content wherever it appears, including in comments, docstrings, durable documentation, or user-facing text: descriptions of the branch, task, implementation process, or the fact that a change was made instead of the resulting code or behavior. Remove or rewrite it within the approved scope,
- run focused verification relevant to the fixes,
- judge test and runtime results against the independent acceptance criteria. Investigate any disagreement between passing tests and failed real API checks; do not weaken expectations or claim completion until the required behavior is verified,
- derive verification scenarios from the accepted finding and independent acceptance criteria grounded in the available original requirements or public contracts, then replay the reviewer's independent scenarios against the changed behavior. Give fixes in architecture or other high-impact areas deeper verification of the affected consumers and risks recorded in `REVIEW.md`. For runtime changes, verify the running application and relevant real APIs in an authorized environment using existing tools; preserve the read-only remote-request boundary unless side effects are authorized. Record the finding identifier, requirement or claim, scenario, exact command or interaction, expected and observed results, environment and revision, and pending checks; do not claim completion from author-written tests alone,
- verify that the accepted defect category is resolved across every confirmed in-scope occurrence, not only the originally reported example. Update the existing search evidence for new or affected matches and assess incident diagnostics for changed failure paths. Report other supported occurrences and gaps by the existing finding identifier for the appropriate approval path; preserve the test-authoring boundary,
- run the applicable focused documentation validation for every documentation update before staging; if no update applies, record the evidence-based `Not applicable` rationale,
- after verification, stage the intended files with `git add`,
- do not stage or commit workflow-generated artifacts by default, including `DRAFT_PLAN.md`, `INITIAL_PLANNING_PROMPT.md`, `FEATURE_SPEC_AND_PLAN.md`, `EXECUTION_PROMPT.md`, `PLAN_CRITIQUE.md`, `PLAN_REVISION_REQUEST.md`, `PLAN_REVISION_SUMMARY.md`, `PLAN_REVISION_VERIFICATION.md`, `REVIEW.md`, `WALKTHROUGH.md`, `WALKTHROUGH.html`, `REVIEW_FIX_PROMPT.md`, `REVIEW_FIX_VERIFICATION.md`, `FOLLOWUP.md`, `TEST_AUDIT.md`, `UI_PROTOTYPE.md`, and files under `.ui-prototypes/`, unless I explicitly ask for them to be committed,
- create focused commit(s) with detailed messages,
- push the current branch after committing,
- check whether the current branch already has a pull request before creating one,
- create a pull request if and only if the current branch does not already have one,
- if unsure how to check whether the current branch already has a pull request, use GitHub CLI (`gh`) to determine that,
- do not create a duplicate pull request for the same branch,
- if a command fails, paste the exact error/log back. Never paraphrase logs.

Required final response:

The generated `REVIEW_FIX_PROMPT.md` must require the response structure below. For eligible frontend fixes, insert `## Frontend Design Verification` after `## Verification Evidence` and include the evidence required by the UI section. Omit that additional section for other work.

```markdown
# Review Fix Summary

## Review Items Fixed

## Review Items Not Fixed And Why

## Files Changed

## Verification Evidence

## Documentation Checkpoints

## Commits Created

## Push Status

## Pull Request

## Suggestions Not Implemented Because Out Of Scope

## Remaining Questions / Blockers
```

In `## Documentation Checkpoints`, require the review-fix model to list each review item's documentation status, the exact durable documentation and validation evidence when applicable, or the evidence-based `Not applicable` rationale.

It must explicitly instruct the review-fix model not to claim completion without fresh verification evidence.

Before handing off `REVIEW_FIX_PROMPT.md`, check that it embeds every Engineering Contract requirement and review-fix instruction above with its priority, scope, conditions, exceptions, and stop gates intact. Verify its explicit design-skill link, complete frontend design gate, accepted-finding boundary, and rendered-verification instructions. Repair omissions or weakened instructions before handoff.

Do not modify code during this review phase.
