# 02 — Plan Critique Loop: Critique Feature Spec/Plan + Generate Opus Revision Request — Any Model

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

Use linked companions within this phase's scope. Skip UI-only sections for backend work, preserve the test-authoring boundary and named outputs, and do not run optional bootstrap scripts. When `spec-driven-development` is explicitly linked, use only its specification and planning procedures; do not invoke its implementation-stage skills. When this phase generates a downstream prompt, embed this archive-only rule, every applicable explicit skill and companion link, and the same scope limits.

Apply the activation and skill-loading rules in `## UI work only` to all UI skill links, including generated-prompt templates. Skip those links when UI work is out of scope. Keep all other required skill loading unchanged.

Use only this prompt's explicitly linked skills.

Fetch and read each linked skill and required companion completely from its GitHub URL before use. Follow the linked procedures directly; do not depend on local skill repositories, installed slash commands, or earlier prompt text.

The prompt is the contract. The locked task artifact is the contract for execution. Skills are supporting procedures only.

If a skill conflicts with this prompt, this prompt wins.

If a conflict is material, stop and ask instead of silently choosing.

Do not use any skill to expand scope, add architecture changes, add tests, add unrelated refactors, or override my explicit instructions.

`no-ai-slop` is mandatory for every Markdown document this phase creates or revises. Treat it as the ultimate writing guide and final authority for prose and presentation after satisfying this prompt's factual, technical, structural, and output requirements. If another skill or instruction conflicts only on writing style, `no-ai-slop` wins; this prompt and locked task artifacts still control scope, meaning, required structure, artifact names, constraints, and evidence.

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

- Do not create, modify, or delete tests in this planning-critique phase.
- Run only focused existing tests or checks when repository evidence is needed; do not manually run the entire suite.
- Require planning artifacts to defer test authoring to the dedicated model-agnostic `09_write_focused_tests_any_model.md` phase.
- Do not duplicate phase `09`'s test-design, test-framework-specific, or coverage contract in this critique.

## UI work only

Enable this section only when the requested or planned work includes UI behavior, layout, presentation, or interaction. A backend service having UI consumers does not by itself enable this section. For backend-only work, skip this entire section and its skill downloads, questions, checks, and reporting.

Fetch and completely read only the applicable skills and companions explicitly linked in this section from GitHub before using them. These conditional links are exempt from unconditional skill-fetch instructions elsewhere in the prompt. If an applicable required file cannot be read completely, stop and report the blocker. Apply web-specific guidance only to web UI; do not impose CSS, React, browser, or mobile-web conventions on another UI stack.

### Conditional UI skills

- Only for eligible visual web surfaces under the frontend design gate: [design-taste-frontend](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/Leonxlnx__taste-skill/snapshot/skills/taste-skill/SKILL.md).
- For web UI design decisions: [emil-design-eng](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/emilkowalski__skills/snapshot/skills/emil-design-eng/SKILL.md).
- For applicable UI data and state cases: [break-ui](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/emilkowalski__skills/snapshot/skills/break-ui/SKILL.md) and its required [CATALOG.md](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/emilkowalski__skills/snapshot/skills/break-ui/CATALOG.md). Use the analysis and catalog only, subject to the limits below.
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

- For an eligible surface, critique the `Frontend Design Contract` for missing objective decisions, protected behavior, approved dependencies, and rendered-validation viewports. Check that the actual `EXECUTION_PROMPT.md` retains the complete frontend design gate and enforces the contract. Record gaps in `PLAN_CRITIQUE.md`; alternative aesthetic preferences remain suggestions.
- Critique the applicable UI acceptance criteria and evidence plan: realistic data and state cases, keyboard and focus, touch, supported sizes/locales, and motion/reduced-motion behavior. Separate missing decisions from preferences.
- Verify that `EXECUTION_PROMPT.md` contains a complete conditional UI section with the applicable construction skills, companions, limits, and verification instructions. Put gaps in `PLAN_CRITIQUE.md` and preserve or repair the full section through `OPUS_PLAN_REVISION_REQUEST.md`; do not create separate UI plans.

## Prompt

Goal:

- determine whether the planning artifacts are ready to lock for implementation.

Success criteria:

- every material concern is grounded in specific plan text, execution-prompt text, or concrete repo evidence,
- blocking issues, non-blocking issues, missing user decisions, and simple suggestions are separated cleanly,
- the plan and generated execution prompt give every implementation step a documentation checkpoint with an update-and-validation action or an evidence-based `Not applicable` decision,
- the output follows the exact artifact structure below.

Constraints:

- do not implement code,
- do not modify any file other than `PLAN_CRITIQUE.md` and `OPUS_PLAN_REVISION_REQUEST.md`,
- this phase's only permitted repository writes are `PLAN_CRITIQUE.md` and `OPUS_PLAN_REVISION_REQUEST.md`. Do not edit the locked plan, execution prompt, production code, tests, durable documentation, configuration, dependencies, Git state, or pull-request state during critique,
- critique the plan, not alternative future architectures,
- if evidence is missing, say so explicitly instead of guessing.

Context to review:

- `FEATURE_SPEC_AND_PLAN.md`,
- `EXECUTION_PROMPT.md`,
- the original draft plan/interviewing notes if available,
- relevant repository context if needed,
- on a later pass, `PLAN_REVISION_VERIFICATION.md` from phase `03`, for every concern not marked `Resolved` or `Invalid Concern`, every remaining issue, and every new issue introduced by the revision,
- on a later pass, the prior `PLAN_CRITIQUE.md` and `PLAN_REVISION_SUMMARY.md`, for earlier critique items, their dispositions, and user decisions still pending.

Working method:

- inspect the planning artifacts and any necessary repository files before finalizing; inspect independent files in parallel when your available tools make that efficient,
- on a later pass, update `PLAN_CRITIQUE.md` instead of starting over. Carry every concern that `PLAN_REVISION_VERIFICATION.md` marks `Partially Resolved` or `Not Resolved`, every remaining issue, and every new issue introduced by the revision into the matching section under its identifier, and cite the verification entry for each. Carry user decisions that `PLAN_REVISION_SUMMARY.md` still lists as pending into `Missing Questions For User`. Do not reopen a concern marked `Resolved` or `Invalid Concern` unless the revised artifacts changed it again; then cite the new evidence. Preserve the `Created by` and `Created at` fields and refresh `Updated at`,
- give each critique item a stable identifier, such as `PC-1`, and use it wherever the item appears in `PLAN_CRITIQUE.md`. On a later pass, keep existing identifiers, update each item in place, and create a new identifier only for a distinct item, including each new issue `PLAN_REVISION_VERIFICATION.md` reports,
- stay grounded in the supplied artifacts and any repository context you inspect,
- quote or clearly point to the exact passage that triggered each blocking issue,
- check the actual `EXECUTION_PROMPT.md` against every applicable implementation requirement in the Engineering Contract, including its priority, scope, conditions, exceptions, and stop gates; report omissions or weaker instructions as blocking issues before declaring it ready for implementation,
- separate confirmed issues, inferences, and open questions,
- prefer concrete execution risks over generic style commentary.

Task:

- critique the plan, not execute it,
- decide whether the artifacts are good enough to lock for implementation,
- produce `PLAN_CRITIQUE.md`,
- produce `OPUS_PLAN_REVISION_REQUEST.md` only when `Ready to execute` is `No`, or when it is `Yes` and I ask to address non-blocking issues.

## Review dimensions

Review for:

- missing design decisions,
- unclear requirements,
- acceptance criteria or expected results that repeat implementation assumptions or test assertions without an independent product requirement or public contract,
- divergence from original scope,
- insufficient file/class/method/function/variable detail,
- missing execution order,
- missing edge cases,
- backwards compatibility risks,
- public API naming/design risks,
- performance or algorithmic complexity concerns,
- unnecessary brute-force or quadratic operations,
- poor reuse / DRY violations,
- failure to reuse existing code,
- excess abstractions, unused paths, and avoidable complexity without a current requirement,
- separation-of-concerns violations,
- missing documentation grounding for library/framework usage,
- outdated API usage, including deprecated or unsupported APIs. Apply the Engineering Contract's version and approval conflict rules rather than silently relaxing the requirement,
- unnecessary third-party dependencies,
- missing custom exception/error translation at public API boundaries,
- cross-platform Linux/Windows risks, plus conflicts with existing or explicitly required platform support that must be escalated rather than silently waived,
- test-writing instructions that conflict with “do not write tests unless explicitly asked,”
- missing verification commands/checks,
- missing independent scenarios and expected results, running-application and relevant real-API checks for runtime changes, or explicit handling of unavailable verification,
- a missing plan for focused integration proof of material component or API interactions; test authoring must remain deferred to `09`,
- missing incident diagnostic requirements for changed failure and recovery paths,
- missing per-implementation-step documentation checkpoints, durable documentation updates, validation, or evidence-based `Not applicable` decisions,
- anything in the execution prompt that gives the implementation model too much freedom.

## Required output 1: `PLAN_CRITIQUE.md`

Create or update `PLAN_CRITIQUE.md` in the target repo root. Do not deliver the critique only in chat; later phases read this file.

Use this structure:

```markdown
# Plan Critique

## Verdict
- Ready to execute: Yes/No
- Reason:

## Blocking Issues

## Non-Blocking Issues

## Missing Questions For User

## Scope / Divergence Risks

## Backwards Compatibility Risks

## Public API Risks

## Performance / Complexity Risks

## Source Documentation Grounding Issues

## Documentation Checkpoint Gaps

## Execution Prompt Risks

## Simplification Opportunities

## Final Recommendation
```

Set `Ready to execute: Yes` only when no blocking issue and no missing user decision remains and, on a later pass, every carried-forward item is resolved or recorded with evidence as invalid. Otherwise set it to `No`.

When `Ready to execute` is `Yes` and I have not asked to address non-blocking issues:

- do not create `OPUS_PLAN_REVISION_REQUEST.md`,
- state in `## Final Recommendation` that the plan is locked and the next step is execution with `EXECUTION_PROMPT.md`,
- state that any existing `OPUS_PLAN_REVISION_REQUEST.md` from a prior pass is superseded and must not be used,
- state that phase `03` does not run because no revision pass ran.

When `Ready to execute` is `No`, create `OPUS_PLAN_REVISION_REQUEST.md` as required output 2.

## UI section in the generated revision prompt

Include a separate `## UI work only` section in `OPUS_PLAN_REVISION_REQUEST.md`. Embed this complete section as direct instructions to Opus, including its explicit links, companions, activation gate, and limits:

```markdown
## UI work only

Enable this section only when the requested or planned work includes UI behavior, layout, presentation, or interaction. A backend service having UI consumers does not by itself enable this section. For backend-only work, skip this entire section and its skill downloads, questions, checks, and reporting.

Fetch and completely read only the applicable skills and companions explicitly linked in this section from GitHub before using them. These conditional links are exempt from unconditional skill-fetch instructions elsewhere in the prompt. If an applicable required file cannot be read completely, stop and report the blocker. Apply web-specific guidance only to web UI; do not impose CSS, React, browser, or mobile-web conventions on another UI stack.

### Conditional UI skills

- Only for eligible visual web surfaces under the frontend design gate: [design-taste-frontend](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/Leonxlnx__taste-skill/snapshot/skills/taste-skill/SKILL.md).
- For web UI design decisions: [emil-design-eng](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/emilkowalski__skills/snapshot/skills/emil-design-eng/SKILL.md).
- For applicable UI data and state cases: [break-ui](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/emilkowalski__skills/snapshot/skills/break-ui/SKILL.md) and its required [CATALOG.md](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/emilkowalski__skills/snapshot/skills/break-ui/CATALOG.md). Use the analysis and catalog only, subject to the limits below.
- Only when a requested motion effect needs clarification: [animation-vocabulary](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/emilkowalski__skills/snapshot/skills/animation-vocabulary/SKILL.md).
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

- For an eligible surface, place the resolved UI decisions in a dedicated `## Frontend Design Contract` section of `FEATURE_SPEC_AND_PLAN.md`: page kind and audience; visual direction and references; existing brand, assets, and tokens; preserve-versus-overhaul mode; required layout, typography, spacing, color, motion, density, and supported themes; responsive, keyboard/focus, contrast, reduced-motion, and state behavior; asset policy; protected content, SEO, routes/navigation, forms, and analytics; approved dependencies; prohibited changes; and representative desktop/mobile viewports with objective acceptance checks.
- Separate locked requirements from optional aesthetic suggestions. Require the actual `EXECUTION_PROMPT.md` to retain the complete frontend design gate and implement this contract with existing tooling. Resolve required design decisions before execution and record unavailable rendered checks as pending rather than passed.
- Preserve the established applicability decision and repair the existing contract within approved scope. Carry its gate, accepted decisions, and rendered-verification requirements into the revised `EXECUTION_PROMPT.md`; do not introduce a new design direction.
- For each affected UI surface, specify applicable loading, error, empty, partial-data, and permission states; realistic or schema-backed long or missing values, Unicode, and zero, one, or many items; container widths, zoom, and supported locales. Resolve choices such as wrapping versus truncation before locking implementation. Do not require every catalog case for every component.
- Specify keyboard, focus, and touch behavior, existing components and tokens to reuse, and applicable mobile viewport, safe-area, scrolling, and input behavior. For motion, record its purpose, frequency, interruption and exit behavior, reduced-motion alternative, and acceptance checks. Preserve feedback and access without requiring animation.
- Put these decisions, verification steps, and documentation impact in the existing planning artifacts. Keep unresolved design decisions explicit. Do not build prototypes, change UI code, or author tests during planning.
```

Require the revision prompt to preserve or repair the complete isolated UI section already in `EXECUTION_PROMPT.md`, including its applicable construction skill links and companions, activation gate, accepted UI criteria, write limits, and verification instructions. Copy that execution section in full into the revision request as the contract to retain; do not use a reference to this phase or earlier chat.

Preserve or repair the complete frontend design gate and require eligible execution to follow the locked `Frontend Design Contract`, inspect the existing rendered surface when available, validate its desktop/mobile viewports, and report evidence or pending checks in the final response's `## Frontend Design Verification`.

If the execution UI section is absent, use the explicit execution skill links below and embed the complete activation gate, frontend design gate, and UI skill limits above. Require direct instructions to implement only approved UI behavior, reuse existing components and tokens, verify applicable data and state cases, keyboard and touch interaction, and reduced-motion behavior with existing tooling, report observed versus pending browser or device checks, and complete the documentation checkpoint. Do not authorize tests, prototypes, toggles, or extra reports.

- Only for eligible visual web surfaces under the frontend design gate: [design-taste-frontend](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/Leonxlnx__taste-skill/snapshot/skills/taste-skill/SKILL.md).
- For web UI design decisions: [emil-design-eng](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/emilkowalski__skills/snapshot/skills/emil-design-eng/SKILL.md).
- For applicable UI data and state cases: [break-ui](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/emilkowalski__skills/snapshot/skills/break-ui/SKILL.md) and its required [CATALOG.md](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/emilkowalski__skills/snapshot/skills/break-ui/CATALOG.md). Use the analysis and catalog only, subject to the UI skill limits above.
- When implementing web motion: [animate](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/emilkowalski__skills/snapshot/skills/animate/SKILL.md) and its required [RECIPES.md](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/emilkowalski__skills/snapshot/skills/animate/RECIPES.md).
- Only when motion work requires choosing a web UI primitive: [pick-ui-library](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/emilkowalski__skills/snapshot/skills/pick-ui-library/SKILL.md), the procedure referenced by `animate`. Use it to evaluate existing options; new dependencies still require explicit approval.
- When mobile-web behavior is in scope: [mobile-native](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/emilkowalski__skills/snapshot/skills/mobile-native/SKILL.md). Use it for planning or review only in phases that prohibit implementation.

Always embed the complete execution UI template below in `OPUS_PLAN_REVISION_REQUEST.md` as the downstream contract to preserve or repair. Carry it directly into the actual revised `EXECUTION_PROMPT.md`, retaining any additional approved task-specific requirements already present. Its implementation instructions apply only to the later execution pass; they do not authorize code, test, documentation, dependency, configuration, or Git changes during revision. Do not replace this template with a summary of its requirements.

```markdown
## UI work only

Enable this section only when the approved task includes UI behavior, layout, presentation, or interaction. A backend service having UI consumers does not by itself enable this section. For backend-only work, skip this entire section and its skill downloads, questions, checks, and reporting.

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

- For an eligible surface, implement only the locked `Frontend Design Contract`. If it is absent or leaves a required design choice unresolved, stop and return to planning; do not infer a new direction from skill defaults.
- For eligible changes, inspect the existing rendered surface before editing when available, then validate the final result at the contract's desktop/mobile viewports with existing repository tooling. In the final response's `## Frontend Design Verification`, record the contract, viewports, tooling, rendered results, responsive and accessibility checks, protected behavior, and pending checks alongside the documentation checkpoint. Do not claim rendered verification from code inspection.
- Implement only the approved UI behavior using existing components and tokens. Complete applicable loading, error, and empty states, keyboard, focus, and touch behavior, and realistic data handling from the plan or accepted finding.
- For approved motion, implement its purpose and frequency decision, interruption and exit behavior, reduced-motion alternative, and hover capability gating where relevant. Use the simplest compatible existing tool; no library is required merely for a fade.
- Verify the changed UI with applicable realistic data, container widths, zoom, supported locale/direction, keyboard/touch interaction, and rapid interruption. Verify mobile viewport, safe-area, scrolling, and input behavior when in scope. Use existing preview/data facilities; do not create tests or a dev toggle. Report observed results and any required device checks still pending in the existing handoff, alongside the documentation checkpoint.
```

Verify both generated sections before handoff, including the explicit design-skill link, complete frontend design gate, locked-contract requirements, and rendered-verification instructions in the actual revision and execution prompts. Keep the general Simplicity and reuse procedure in the revision prompt's Engineering Contract and the revised execution prompt for backend and UI tasks alike.

## Required output 2: `OPUS_PLAN_REVISION_REQUEST.md`

Create this output only when `PLAN_CRITIQUE.md` sets `Ready to execute: No`, or when it sets `Yes` and I ask to address non-blocking issues.

Only this phase may author `OPUS_PLAN_REVISION_REQUEST.md`. Create it in the target repo root as the final direct-use, paste-ready prompt for Opus to revise `FEATURE_SPEC_AND_PLAN.md` and `EXECUTION_PROMPT.md`. There is no separate checked-in Opus revision prompt file after this critique step.

If a later verification pass says another revision is needed, return to this phase and regenerate `OPUS_PLAN_REVISION_REQUEST.md` here. Do not create an alternate revision prompt in the verification phase.

It must be self-contained.

Do not generate:

- a helper prompt,
- a meta-only instruction block,
- a skeleton that expects another prompt file to fill in the real contract,
- a revision summary without the full direct-use prompt.

The generated Opus revision prompt must have a clear title and these top-level sections:

- `## Skills`
- `## Skill Handling Rule`
- `## Default Planning Artifact Reduction`
- `## Engineering Contract`
- `## UI work only`
- `## Prompt`

The generated Opus revision prompt must include these skill links explicitly:

- [spec-driven-development](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/spec-driven-development/SKILL.md)
- [planning-and-task-breakdown](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/planning-and-task-breakdown/SKILL.md)
- [context-engineering](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/context-engineering/SKILL.md)
- [source-driven-development](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/source-driven-development/SKILL.md)
- [verification-before-completion](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/obra__Superpowers/snapshot/skills/verification-before-completion/SKILL.md)
- [code-review-and-quality](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/code-review-and-quality/SKILL.md)
- [code-simplification](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/code-simplification/SKILL.md)
- [no-ai-slop](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/petergyang__no-ai-slop/snapshot/skills/no-ai-slop/SKILL.md), including its required [eval.md](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/petergyang__no-ai-slop/snapshot/skills/no-ai-slop/eval.md)
- Required planning and incremental-verification companion: [definition-of-done.md](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/references/definition-of-done.md). Apply it within this phase's scope, artifact policy, and test-authoring boundary.
- For the security checks and threat-model guidance referenced by the linked procedures: [security-and-hardening](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/security-and-hardening/SKILL.md), with [hardening-patterns.md](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/security-and-hardening/references/hardening-patterns.md) and [security-checklist.md](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/references/security-checklist.md). Use only the applicable analysis within this phase's permissions; do not start a separate hardening or incident-response task.
- For the performance checks referenced by `code-review-and-quality`: [performance-optimization](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/performance-optimization/SKILL.md), with [optimization-patterns.md](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/performance-optimization/references/optimization-patterns.md) and [performance-checklist.md](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/references/performance-checklist.md). Use only applicable review guidance; do not start an optimization task, impose example thresholds, or create `PERF.md`.

The generated Opus revision prompt must include a `## Skill Handling Rule` that instructs Opus to:

- use only the prompt's explicitly linked skills,
- fetch skill procedures and required companions only from `https://github.com/viseshrp/ai-skills-archive`; resolve relative resource references to the linked archive copies; do not follow upstream skill URLs, install a skill package, or substitute an official-source copy; if a required archive resource is absent or unreadable, stop and report its exact missing path; keep optional related-skill mentions and provenance links inactive,
- fetch and read every required skill and companion completely from its GitHub URL before use, subject to the generated prompt's isolated UI activation rules; skip UI-only links for backend-only work; embed full links and these handling rules in the generated prompt; do not depend on local skill repositories, installed slash commands, or earlier prompt text,
- treat the prompt as the contract,
- treat locked task artifacts as the contract for execution,
- use skills as supporting procedures only,
- let the prompt win if a skill conflicts with it,
- stop and ask instead of silently choosing if a conflict is material,
- never use a skill to expand scope, add architecture changes, add tests, add unrelated refactors, or override my explicit instructions.
- require `no-ai-slop` for every Markdown document the phase creates or revises; use it as the ultimate prose and presentation guide,
- apply it while drafting, run its `eval.md` self-check before saving each Markdown artifact or sending the final response, and stop before creating or revising Markdown if its `SKILL.md` or `eval.md` cannot be read and applied,
- let `no-ai-slop` win over conflicting writing-style guidance while the prompt and locked task artifacts continue to control scope, meaning, required structure, artifact names, constraints, and evidence,
- ignore its draft-request, detection-mode, and mandatory `What changed` workflow unless this prompt explicitly asks for them.

The generated Opus revision prompt must include `## Default Planning Artifact Reduction` and require:

- `FEATURE_SPEC_AND_PLAN.md`
- `EXECUTION_PROMPT.md`

It must state that:

1. `FEATURE_SPEC_AND_PLAN.md` contains both a detailed spec/reference section and a concrete implementation plan section.
2. The implementation plan section links back to relevant spec/reference anchors inside the same file instead of duplicating long explanations.
3. The plan remains the execution contract.
4. The spec/reference section remains the background reference.
5. Separate `SPEC.md` and `IMPLEMENTATION_PLAN.md` are only a fallback if I explicitly ask or if the file becomes too large to review comfortably.
6. All workflow-generated Markdown artifacts must be created or updated only in the target repo root using their exact required filenames, never in subdirectories or alternate paths.
7. All workflow-generated Markdown artifacts must include `Created by`, `Created at`, and `Updated at` metadata, preserving the creation fields after first creation and refreshing `Updated at` whenever an artifact is edited.

The generated Opus revision prompt must embed the full Engineering Contract above verbatim or stricter.

It must preserve every requirement in the existing planning and execution artifacts at its full level of detail. Do not replace explicit checklists, field lists, examples, conditions, exceptions, priorities, approval gates, or stop rules with compressed prose or a reference to another prompt. Carry every applicable requirement into the actual revised `EXECUTION_PROMPT.md`, not only into the revision request. A conflict must be surfaced and resolved explicitly; it is not permission to silently delete or weaken an instruction.

Inside `## Prompt`, the generated Opus revision prompt must use clear sections for:

- role,
- task,
- context to read before answering,
- success criteria,
- constraints,
- working method,
- required outputs,
- final checks.

Inside those sections, it must instruct Opus as follows.

Role:

- You are Claude Opus revising the planning artifacts before implementation.
- Be explicit about which critique items are valid, which are rejected, and which still require a user decision.
- Read before answering. Do not speculate about code or files you have not inspected.

Task:

- Update the planning artifacts so they are ready for locked implementation.
- Apply valid critique items without expanding scope.

Context to read before answering:

- `PLAN_CRITIQUE.md`, if present,
- `OPUS_PLAN_REVISION_REQUEST.md`, if present from a prior pass,
- `PLAN_REVISION_VERIFICATION.md`, if present from a prior pass,
- `PLAN_REVISION_SUMMARY.md`, if present from a prior pass,
- current `FEATURE_SPEC_AND_PLAN.md`,
- current `EXECUTION_PROMPT.md`,
- the original draft plan/interviewing notes if available,
- relevant repository context.

Success criteria:

- every critique item is explicitly addressed, rejected with reasoning, or escalated for a user decision, and `PLAN_REVISION_SUMMARY.md` refers to each item by its `PLAN_CRITIQUE.md` identifier,
- on a later pass, every concern that `PLAN_REVISION_VERIFICATION.md` reports as `Partially Resolved` or `Not Resolved`, every remaining issue, and every new issue introduced by the revision is addressed, rejected with reasoning, or escalated for a user decision, and the updated `PLAN_REVISION_SUMMARY.md` records the result for each one,
- the revised plan stays within original scope,
- the revised execution prompt remains strict enough to prevent divergence during execution,
- the revised plan and execution prompt preserve a documentation checkpoint for every implementation step, including exact durable documentation/validation or an evidence-based `Not applicable` decision,
- the revised planning artifacts still belong only in the target repo root and do not introduce any alternate artifact path,
- the revised planning artifacts preserve or add `Created by`, `Created at`, and `Updated at` metadata correctly,
- the revised execution prompt preserves explicit instructions to stage changes, commit, push, and create a pull request only if the current branch does not already have one,
- the revised execution prompt preserves explicit instructions not to stage or commit workflow-generated artifacts unless I explicitly ask for that,
- no detail from the current plan artifacts, critique, or draft-plan lineage is silently dropped.

Constraints:

- do not implement code,
- do not write tests,
- do not loosen the execution prompt,
- the generated revision pass may create or update only `FEATURE_SPEC_AND_PLAN.md`, `EXECUTION_PROMPT.md`, and `PLAN_REVISION_SUMMARY.md`. It must not edit production code, tests, durable documentation, configuration, dependencies, Git state, or pull-request state,
- do not use the critique as permission to change architecture unless I explicitly approve,
- keep the plan/code execution scope unchanged unless I explicitly approve scope changes.

Working method:

For each critique item:

1. Decide whether it is valid.
2. If valid and answerable from the repo/context, update the plan/prompt.
3. If valid but requires my design decision, stop and ask me before updating that part.
4. If invalid, document why.
5. If it would expand scope, stop and ask.

Also:

- read `PLAN_CRITIQUE.md`,
- read the current `FEATURE_SPEC_AND_PLAN.md`,
- read the current `EXECUTION_PROMPT.md`,
- apply all valid critique items,
- ask if a critique item requires a design decision from me,
- do not silently drop any critique item,
- ground plan detail in the code and context you inspected,
- preserve original requirements, approved clarifications, independent acceptance criteria and their requirement sources, explicit unnecessary-code checks, searches across the codebase for repeated defects, and incident diagnostics for changed failure paths in the revised plan and actual `EXECUTION_PROMPT.md`,
- preserve independent scenarios and expected results, focused integration proof for material component or API interactions, authorized running-application and relevant real-API checks for runtime changes, and evidence reporting with required unavailable checks pending. Keep remote requests read-only unless side effects are authorized, changes within approved scope, and test authoring deferred to `09`; do not implement during revision,
- preserve or strengthen the `EXECUTION_PROMPT.md` instructions to stage intended files with `git add`, create focused commits, push the current branch, check whether the current branch already has a pull request, and create a pull request only if none exists,
- preserve or strengthen the per-implementation-step documentation checkpoint: update and validate the exact durable documentation in the same change set, or record an evidence-based `Not applicable` decision,
- preserve or strengthen the artifact-location rule that all workflow-generated Markdown artifacts stay in the target repo root using their exact required filenames and are never created in subdirectories or alternate paths,
- preserve or strengthen the artifact-metadata rule that all workflow-generated Markdown artifacts include `Created by`, `Created at`, and `Updated at`, preserving creation fields and refreshing `Updated at` on edits,
- preserve or strengthen the `EXECUTION_PROMPT.md` instructions not to stage or commit workflow-generated artifacts such as `FEATURE_SPEC_AND_PLAN.md`, `EXECUTION_PROMPT.md`, `REVIEW.md`, `WALKTHROUGH.md`, `WALKTHROUGH.html`, `REVIEW_FIX_PROMPT.md`, `FOLLOWUP.md`, `TEST_AUDIT.md`, and the other workflow output Markdown files unless I explicitly ask for that,
- if the revised `EXECUTION_PROMPT.md` needs a fallback instruction for checking whether the current branch already has a pull request, use GitHub CLI (`gh`) for that fallback and do not invent a duplicate-prone alternative,
- preserve explicit success criteria, stop rules, and verification expectations in the revised artifacts.

Required outputs:

Update or create:

- `FEATURE_SPEC_AND_PLAN.md` in the target repo root
- `EXECUTION_PROMPT.md` in the target repo root
- `PLAN_REVISION_SUMMARY.md` in the target repo root

The generated revision prompt must require `PLAN_REVISION_SUMMARY.md` to use this structure:

```markdown
# Plan Revision Summary

## Critique Items Addressed

## Critique Items Rejected

## Critique Items Requiring User Decision

## Changes Made To FEATURE_SPEC_AND_PLAN.md

## Changes Made To EXECUTION_PROMPT.md

## Documentation Checkpoints Updated

## Remaining Risks

## Ready For Another Critique Pass?

## Ready For Implementation?
```

The generated revision prompt must require `## Changes Made To EXECUTION_PROMPT.md` to record, for every changed or removed `EXECUTION_PROMPT.md` instruction, its previous wording, its revised wording or `Removed`, and the critique item or approved decision that required the change. Copy the previous wording before editing `EXECUTION_PROMPT.md`, because the revision overwrites that file in place.

Final checks:

- verify that the updated plan is still within original scope,
- verify that the implementation plan section remains concrete down to files/classes/functions/methods/variables/order of changes,
- verify that the execution prompt still includes strict no-divergence/no-creativity/no-architecture-change rules,
- verify that every implementation step still has a documentation checkpoint with durable documentation validation or an evidence-based `Not applicable` decision,
- verify that no test-writing is introduced unless explicitly asked,
- verify that all skill links relevant to the generated execution prompt remain present,
- embed the following execution skill links in the revision request and require them in the revised `EXECUTION_PROMPT.md`, preserving any additional existing execution skills and its full skill-handling rules. Require the revised `EXECUTION_PROMPT.md` `## Skill Handling Rule` to retain or add this archive-only bullet: fetch skill procedures and required companions only from `https://github.com/viseshrp/ai-skills-archive`; resolve relative resource references to the linked archive copies; do not follow upstream skill URLs, install a skill package, or substitute an official-source copy; if a required archive resource is absent or unreadable, stop and report its exact missing path; keep optional related-skill mentions and provenance links inactive. Embed these execution skill links:
  - [incremental-implementation](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/incremental-implementation/SKILL.md),
  - [source-driven-development](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/source-driven-development/SKILL.md),
  - [verification-before-completion](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/obra__Superpowers/snapshot/skills/verification-before-completion/SKILL.md),
  - [no-ai-slop](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/petergyang__no-ai-slop/snapshot/skills/no-ai-slop/SKILL.md), including its required [eval.md](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/petergyang__no-ai-slop/snapshot/skills/no-ai-slop/eval.md),
  - Required planning and incremental-verification companion: [definition-of-done.md](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/references/definition-of-done.md), applied within the execution scope, artifact policy, and test-authoring boundary,
  - For applicable security checks: [security-and-hardening](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/security-and-hardening/SKILL.md), with [hardening-patterns.md](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/security-and-hardening/references/hardening-patterns.md) and [security-checklist.md](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/references/security-checklist.md). Use only applicable analysis; do not start a separate hardening or incident-response task,
  - For the stack-discovery procedure referenced by `incremental-implementation`: [test-driven-development](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/test-driven-development/SKILL.md), including [testing-patterns.md](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/references/testing-patterns.md). Use only stack discovery and existing-test verification during execution; do not author tests or invoke its test-first cycle. Apply JavaScript/TypeScript examples only to a matching stack,
- keep those downstream implementation resources and their scope limits explicit in the generated revision request so Opus can repair missing execution links. Their presence does not authorize implementation during revision,
- verify the actual execution prompt retains its goal, success criteria, context, execution posture, constraints, stop rules, execution rules, and required final response. Do not reduce the execution prompt to the shared Engineering Contract alone,
- preserve explicit full-diff checks for drift, omissions, unintended additions, duplication, excess abstractions, unused paths, and avoidable complexity. Require re-reading original requirements after long sessions or context handoffs and before completion,
- preserve the check for all possible regressions within the branch's change scope, including indirect effects on callers, existing behavior, backwards compatibility, and error paths. Fix only within the locked plan and stop and ask if a repair would exceed it,
- preserve the separate meta-content check across comments, docstrings, durable documentation, and user-facing text. Remove or rewrite descriptions of the branch, task, implementation process, or the fact that a change was made instead of descriptions of resulting behavior,
- preserve concrete input/output examples for every added or changed string transformation, full Python typing requirements and exceptions, readable types, public error translation, production-assert restrictions, dependency approval, latest-API conflict handling, and Linux/Windows requirements,
- preserve independent acceptance criteria and runtime scenarios, real application entry points and relevant real APIs, authorized environments, read-only remote requests unless effects are authorized, and evidence fields for the requirement or claim, scenario, command or interaction, revision, environment, expected result, observed result, and pending checks. Required unavailable checks must block completion,
- preserve codebase-wide searches for each discovered defect pattern, inspection of candidate matches, confirmed occurrences and false positives, unexamined areas, in-scope root-cause fixes, and incident diagnostics for operation, request/job context, cause/trace, retry/recovery, secrets, sensitive payloads, and duplicate noise,
- preserve focused existing-test/lint/smoke/build verification, no test authoring before `09`, no full suite unless explicitly requested, no patching or mocking the subject under test, existing tests broken only by a change that a locked requirement explicitly requires left unmodified and reported as test-only work for `09`, exact command failure logs, and fresh verification before a completion claim,
- preserve same-change-set durable documentation updates and validation for every implementation step, or an evidence-based `Not applicable` result. Code comments, commits, and workflow artifacts are not substitutes; do not update the changelog without explicit authorization,
- preserve the complete required final-response structure in the execution prompt: `# Implementation Summary`, `## What Changed`, `## Files Changed`, `## Plan Steps Completed`, `## Verification Evidence`, `## Documentation Checkpoints`, `## Commits Created`, `## Push Status`, `## Pull Request`, `## Not Done / Blocked`, and `## Suggestions Not Implemented Because Out Of Scope`. For eligible frontend work, retain `## Frontend Design Verification` immediately after `## Verification Evidence` with the complete required evidence; omit that additional section for other work. Preserve any additional required headings already present in the approved execution prompt,
- verify that the execution prompt still requires `git add`, commit, push, and create-PR-only-if-missing behavior,
- verify that the execution prompt still forbids committing workflow-generated artifacts by default,
- verify that the Engineering Contract remains intact or stricter.
- compare each applicable implementation requirement in the Engineering Contract with its wording in the revised `EXECUTION_PROMPT.md`, including priority, scope, conditions, exceptions, and stop gates; repair omissions or weakened instructions before handoff.
- compare every existing execution instruction and each detailed preservation check above with the actual revised artifact. Preserve its full wording unless an explicitly approved change requires revision, and record the previous and revised wording of each changed or removed instruction in `PLAN_REVISION_SUMMARY.md`; do not mark it ready while any required section, field, companion resource, or operational check is absent or weaker.

Do not ask Opus to implement code.
