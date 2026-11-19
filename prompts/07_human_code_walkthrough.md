# 07 - Human Code Walkthrough + FOLLOWUP.md Creation - Any Model

## Skills

- [receiving-code-review](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/obra__Superpowers/snapshot/skills/receiving-code-review/SKILL.md)
- [code-review-and-quality](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/code-review-and-quality/SKILL.md)
- [code-simplification](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/code-simplification/SKILL.md)
- [no-ai-slop](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/petergyang__no-ai-slop/snapshot/skills/no-ai-slop/SKILL.md), including its required [eval.md](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/petergyang__no-ai-slop/snapshot/skills/no-ai-slop/eval.md)
- [show-me](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/humanlayer__skills/snapshot/plugins/show-me/skills/show-me/SKILL.md)
- For the security checks and threat-model guidance referenced by the linked procedures: [security-and-hardening](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/security-and-hardening/SKILL.md), with [hardening-patterns.md](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/security-and-hardening/references/hardening-patterns.md) and [security-checklist.md](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/references/security-checklist.md). Use only the applicable analysis within this phase's permissions; do not start a separate hardening or incident-response task.
- For the performance checks referenced by `code-review-and-quality`: [performance-optimization](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/performance-optimization/SKILL.md), with [optimization-patterns.md](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/performance-optimization/references/optimization-patterns.md) and [performance-checklist.md](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/references/performance-checklist.md). Use only applicable review guidance; do not start an optimization task, impose example thresholds, or create `PERF.md`.

## Skill Handling Rule

Fetch skill procedures and their required companions only from `https://github.com/viseshrp/ai-skills-archive`. Resolve relative resource references to the explicitly linked archive copies; do not follow upstream skill URLs, install a skill package, or substitute an official-source copy. If a required archive resource is absent or unreadable, stop and report its exact missing path. Keep optional related-skill mentions and provenance links inactive unless this prompt explicitly authorizes the procedure. Verify uncertain target-library APIs and versions against authoritative documentation; that documentation is not a substitute source for skill material.

Use linked companions within this phase's scope. Skip UI-only sections for backend work, preserve the test-authoring boundary and named outputs, and do not run optional bootstrap scripts.

Apply the activation and skill-loading rules in `## UI work only` to all UI skill links. Skip those links when UI work is out of scope. Keep all other required skill loading unchanged.

Use only this prompt's explicitly linked skills.

Fetch and read each linked skill and required companion completely from its GitHub URL before use. Follow the linked procedures directly; do not depend on local skill repositories, installed slash commands, or earlier prompt text.

The prompt is the contract. The locked task artifact is the contract for execution. Skills are supporting procedures only.

If a skill conflicts with this prompt, this prompt wins.

If a conflict is material, stop and ask instead of silently choosing.

The linked skills come from different authors and were written for other workflows, so they can disagree with each other as well as with this prompt. No linked skill outranks another. Use this prompt and any locked or approved task artifacts to settle a disagreement between skills. Where those are silent, take the option that stays inside the approved scope and requires the smaller change; if the choice is material, stop and ask.

A skill's named tools, slash commands, sub-agents, MCP servers, hooks, modes, personas, output templates, file-saving steps, and approval, pause, or stop-turn routines apply only where this prompt adopts them. Otherwise use this prompt's method, outputs, and gates with the tools your environment provides. A skill's instruction to read a companion only in part, or only when needed, does not relax this prompt's complete-read rule.

Resolve these known conflicts as follows:

- Each skill has one role here. `code-review-and-quality` and `code-simplification` supply the checks behind the concerns you raise. `receiving-code-review` applies when I propose a change or disagree with you: check my point against the code, and say plainly when the evidence does not support it, before we agree an item.
- None of these skills may change anything. Skip `receiving-code-review`'s implementation steps, `code-simplification`'s change, test, and commit loop, and `code-review-and-quality`'s mutation check, and do not post or reply to GitHub review comments.
- Review judgments are mine. Do not issue `code-review-and-quality`'s `Approve` or `Request changes` verdict or use its comment labels; state each concern with its evidence under the rules below.
- Do not raise a concern from a skill's size threshold alone, and do not call a compatibility path dead code without evidence in the code.
- `show-me`'s instruction to keep prose brief does not shorten the required explanations or the plain-language rules.

Do not use any skill to expand scope, add architecture changes, add tests, add unrelated refactors, or override my explicit instructions.

`no-ai-slop` is mandatory for every Markdown document this phase creates or revises. Treat it as the ultimate writing guide and final authority for prose and presentation after satisfying this prompt's factual, technical, structural, and output requirements. If another skill or instruction conflicts only on writing style, `no-ai-slop` wins; this prompt and locked task artifacts still control scope, meaning, required structure, artifact names, constraints, and evidence.

Apply `no-ai-slop` while drafting and run its `eval.md` self-check before saving each Markdown artifact or sending the final response. If its `SKILL.md` or `eval.md` cannot be read and applied, stop before creating or revising Markdown and report the blocker. Ignore its draft-request, detection-mode, and mandatory `What changed` workflow unless this prompt explicitly asks for them.

## Documentation checkpoint

Complete a documentation checkpoint during human review. For every material changed behavior, use the primary PR checklist to record the exact durable documentation update and its validation, or an evidence-based `Not applicable` decision. This phase must not implement documentation changes; a required documentation change becomes a `FOLLOWUP.md` item only after I explicitly type `AGREE`.

## Language-specific review guidance

### Python

When the current PR's changed code uses Python, add an explicit typing-compliance check to the primary checklist:

- Every parameter, including `*args` and `**kwargs`, and return value of an added or changed function or method must have an explicit, accurate type hint. Treat `self` and `cls` as implicit; do not require annotations for them.
- Every added or changed class variable, class attribute, instance attribute, and module-level mutable or optional state must have an explicit, accurate type hint. A trivial immutable module constant may remain inferred unless the configured type checker needs an annotation.
- Instance-attribute types should be declared at class scope where feasible. Do not require local-variable or `self.attribute: Type` annotations inside function or method bodies unless a real configured type-checker error requires one.
- Required annotations must stay simple and accurate; do not accept advanced type constructs or type-only refactors that the configured type checker does not require.

## Simplicity and reuse

Apply this procedure to backend and UI work within this phase's existing permissions. In review-only phases, assess proposed or existing changes without implementing them:

- Before proposing or adding custom code, inspect relevant existing helpers, types, and patterns, then standard-library capabilities, native platform features, and already-installed dependencies. Prefer a compatible existing solution when it preserves behavior and readability; name the concrete alternative when flagging duplication.
- Before adding new behavior, trace how the repository already handles comparable behavior: component responsibilities, dependency direction, shared services, and extension points. Build on those established flows instead of creating a parallel flow, duplicate infrastructure, or a path that bypasses an existing layer. If the approved scope appears to need a parallel path, or the established path cannot support the change without an architecture decision, stop and ask. In review-only phases, flag an unapproved parallel flow with concrete repository evidence and name the established path the code should use.
- Explicitly review duplication, excess abstractions, unused paths, and avoidable complexity across every file and change in scope, not a sample. Check for repeated work; checks already guaranteed elsewhere, such as by a caller or constructor; unreachable branches; assertions that cannot fail; duplicate tests; duplicated or stale text in code, comments, and documentation; leftovers from removed code; and single-use indirection. Justify a new abstraction or dependency by a current requirement, meaningful duplication, or a necessary ownership boundary. A single implementation or caller is not by itself a defect; flag single-use indirection only when it adds no contract, ownership boundary, or test seam. Whenever code is removed or proposed for removal, recheck the code, tests, comments, and documentation that depended on it, because a removal can leave new leftovers. When reporting that no further instances remain, name the files and checks covered; do not claim more. Preserve dependency approval and source-documentation grounding.
- For a bug fix, trace the relevant callers, data flow, and error flow before choosing the repair location. When a defect is found, search throughout the codebase for the same failure pattern and inspect candidate matches. Record the search scope, confirmed occurrences, and unexamined areas in the phase's existing output. For authorized fixes, address the root cause within this phase's permissions and approved scope; report other occurrences without changing them. If a shared fix would exceed scope or alter compatibility, stop and ask.
- Before proposing deletion, inspect direct callers, dynamic or string references, public contracts, configuration, and relevant tests. Fewer lines or files are not acceptance criteria; preserve validation, security, accessibility, error handling, and verification.
- Do not substitute a simpler interpretation for an explicit requirement or locked plan. Put out-of-scope simplifications in the phase's permitted suggestions or chat; implementation still requires its existing authorization. Preserve the test-authoring boundary, native test-framework rules, and coverage gate; do not introduce production assertion demos, one-test quotas, persistent modes, debt markers, or new ledgers.

## Simplification limits and improvement claims

- During planning, record each deliberate simplification with a material limit: why it meets current requirements, its known limit, and the evidence that would trigger revisiting it. Do not invent thresholds or weaken explicit requirements. Carry applicable limits and revisit triggers into existing durable documentation during authorized implementation or fixes. In review, verification, and audit phases, check these decisions and route gaps through the existing documentation checkpoint; do not exceed the phase's write permissions. Use existing planning and documentation sections without adding comment markers, a debt ledger, or another artifact.
- In reviews and handoffs, distinguish measured improvements from expectations. Claims of reduced latency, memory use, or cost require comparable before-and-after evidence identifying the baseline, changed version, workload, measurement method, and relevant environment. Without comparable evidence, label the expected improvement `unmeasured`; do not infer savings from fewer lines, an implementation never built, or unrelated benchmarks. Use existing verification facilities within the phase's permissions; this rule does not authorize new benchmark files, dependencies, or configuration changes.

## UI work only

Enable this section only when the approved task or reviewed change includes UI behavior, layout, presentation, or interaction. A backend service having UI consumers does not by itself enable this section. For backend-only work, skip this entire section and its skill downloads, questions, checks, and reporting.

Fetch and completely read only the applicable skills and companions explicitly linked in this section from GitHub before using them. These conditional links are exempt from unconditional skill-fetch instructions elsewhere in the prompt. If an applicable required file cannot be read completely, stop and report the blocker. Apply web-specific guidance only to web UI; do not impose CSS, React, browser, or mobile-web conventions on another UI stack.

### Conditional UI skills

- For applicable UI data and state cases: [break-ui](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/emilkowalski__skills/snapshot/skills/break-ui/SKILL.md) and its required [CATALOG.md](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/emilkowalski__skills/snapshot/skills/break-ui/CATALOG.md). Use the analysis and catalog only, subject to the limits below.
- When reviewing changed web motion: [review-animations](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/emilkowalski__skills/snapshot/skills/review-animations/SKILL.md) and its required [STANDARDS.md](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/emilkowalski__skills/snapshot/skills/review-animations/STANDARDS.md).
- When mobile-web behavior is in scope: [mobile-native](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/emilkowalski__skills/snapshot/skills/mobile-native/SKILL.md). Use it for planning or review only in phases that prohibit implementation.

### UI skill limits

- Preserve the approved scope, existing design system, component conventions, platform support, and dependency-approval rules. These skills do not authorize new UI features, animations, dependencies, framework changes, or redesigns.
- Ignore skill greeting and pause routines. Do not invoke unlisted skills or create prototype pages, development toggles, separate plans or reports, or retained fixtures through `break-ui`. Test-local fixtures may be authored only in phase `09` under its test contract. All other writes remain subject to this phase's permissions and named outputs.
- Treat recipe values and aesthetic preferences as defaults, not automatic defects. Existing tokens and approved behavior take precedence. Verify version-sensitive APIs and performance claims against the target stack's documentation and evidence. Resolve material conflicts before changing behavior; do not enforce blanket duration, easing, pure-fade, or keyboard-animation bans from a skill.
- The UI skills disagree with each other on points such as hover and looping motion, scroll reveals, stagger, reduced-motion behavior, durations and easing, and library choice. Approved UI decisions and existing tokens and components decide. Where they are silent, do not add or remove motion or add a dependency because one skill says so: in planning phases, record the choice as a decision for me; in implementation phases, stop and ask; in every other phase, treat a disagreement between skills as a suggestion at most. A skill's own gate or make-the-call rule does not cancel approved behavior or replace stop-and-ask, and a skill's report table, severity words, or `Block` or `Approve` verdict does not replace this phase's output format.
- Distinguish observed UI behavior, conclusions inferred from code, and checks awaiting a browser or real device. Use available running UI and existing tooling within the phase's permissions; do not claim visual or device verification from static inspection. Record an unavailable required check as pending or blocked in the existing artifact or chat handoff, not as passed. Do not add a new artifact or override `no-ai-slop` and its evaluator.

### Phase requirements

- Review UI behavior independently from the actual PR changes and inspected code; continue to discard `REVIEW.md`. Connect applicable data and state, keyboard and focus, touch, and motion paths to the prose overview and semantic blocks.
- Where available, inspect the running interaction using existing facilities. Discuss observed behavior separately from inferred behavior and pending browser or device checks. Do not create HTML, prototype pages, toggles, fixtures, or additional visual artifacts.
- Record documentation and required pending UI checks in the primary checklist. Preserve `AGREE` for each exact follow-up item, renewed review on changed code, `RESOLVE` plus verified GitHub Viewed state for file completion, and the final go-ahead before implementation.

## Prompt

Help me review the current PR from the actual code and PR changes. Start by showing how the code fits together and where each flow ends, then discuss one small semantic block at a time. Keep explanations concise without losing detail, and follow my questions about the code before moving on. Review judgments, `FOLLOWUP.md` approvals, and file completions in this phase remain my decisions.

Use ISO-style plain language and ASD-STE100-inspired technical writing as guidance, without claiming formal compliance. Write complete sentences with explicit subjects, actions, and outcomes. Define technical terms and abbreviations on first use. Explain each symbol's role, required background, and cause-and-effect relationships without assuming knowledge of earlier chats, the implementation session, or repository-specific concepts. Keep identifiers and technical meaning exact. These writing guidelines remain subordinate to `no-ai-slop` and do not replace required code excerpts, line-by-line coverage, or the example run.

### Read the PR and code

- At the start of each session, and whenever I say the PR changed, pull the current PR changed-file list and per-file changes from GitHub CLI (`gh`). Use them as the source of truth for the review checklist and changed blocks. The `RESOLVE` rule below refreshes the current file again. If `gh` cannot provide either, stop and ask; do not substitute the manual diff against `main`.
- Maintain a primary checklist with one item per changed file and statuses such as pending, in review, and resolved. Track reviewed blocks and documentation results; show progress when a file is completed or I ask for it.
- Re-read available original requirements and approved scope changes at the start, after long sessions or handoffs, and before completion to check for drift.
- Read the actual code, referenced declarations and definitions, and relevant `WALKTHROUGH.md` sections. Use the manual diff against `main` only for verification/reference.
- Discard `REVIEW.md` completely. Do not agree with, disagree with, summarize, import, or otherwise use its findings. Base review judgments on inspected code and PR changes.
- Use `WALKTHROUGH.md` only for supplemental context. Check it against actual code and the PR changes from `gh`, which take precedence. Do not let it replace or reorder the changed-file checklist, and do not use `FOLLOWUP.md` as that checklist.

Use `show-me` only for focused diffs and pseudocode alongside the required code context. Keep presentation diffs, pseudocode, and example runs in chat only; do not save them in `WALKTHROUGH.md` or other files. Do not create diagrams, mindmaps, HTML, or additional visual artifacts, or require skill installation.

### Explain the code context first

Open the first review response with a brief prose overview of the code under review: entry points, affected files and symbols, dependencies, shared state, and their relationships. Use concrete file and symbol names from inspected code.

Explain every reachable control-flow branch and data/state transition alongside the relevant semantic block. Identify branch conditions, inputs, calls, side effects, and terminal success or error states. Include early returns, skipped work, exception propagation and handling, retries, and cleanup wherever they exist. Explain loop conditions and exits instead of repeating cycles. Mark paths or outcomes that cannot be verified; do not invent behavior.

Base the overview and flow explanations on inspected code and PR changes, checking relevant `WALKTHROUGH.md` context against them. Show the overview in chat and pause for my questions or choice of where to start. Correct an explanation if later inspection changes a relationship, path, or outcome.

### Review a semantic block

Review one primary file at a time and one small semantic block per response. Choose a coherent operation or decision, such as input validation, a state update, or an error handler. Keep related declarations and definitions alongside that block, even when they come from other files. Track any blocks left to review when my questions change the order.

Show the block as a focused source diff with file/line locations and a few relevant surrounding lines. Show the complete block when most of it is new or omitted context would obscure ownership, order, or behavior. Identify before/after source locations where they differ. For every variable, constant, parameter, attribute, function, or method referenced but not defined in the displayed block, show its declaration or definition in a separate short excerpt with its file/line location. Show the relevant binding or initialization for values and enough of a called function or method to explain the call. For imported symbols, identify the source and use its verified declaration or definition; never invent one.

After the code, explain the block in this order:

1. Overview: in a few sentences, state what the block does, the inputs and state it depends on, the branch conditions, and how its outputs, side effects, returns, or errors connect to the surrounding code.
2. Line by line: go through the displayed block in source order. For each line, cite its file/line location and state what it does: the value it reads or sets, the condition it tests, the call it makes, and the branch, return, or error that follows. Cover every changed line and each unchanged line needed to follow them. Group lines only when they form one statement.
3. Example run: step through the block once with concrete values, the way a debugger steps over each line.

Build the example run as follows:

- Start with the starting values: every argument, constant, attribute, and other value that the block reads but does not define. Take constant and configuration values from their verified declarations or definitions. Take argument and state values from a real call site, an existing fixture, or a requirement example when one exists; otherwise choose a realistic value. Label each starting value `from code`, with its file/line location, or `example`. Never use a real secret, credential, or personal data; use an obviously fake value.
- Choose values that follow the block's main path. List each executed line in order with its file/line location, the values it reads, the value it sets or returns, and the branch it takes. Name the lines that this run skips and the condition that skips them. For a loop, step through the first pass and the pass that exits instead of repeating cycles.
- Step over each call: state its arguments and the value it returns for them, taken from its inspected code or documented behavior, without tracing its body. If you cannot determine the returned value, say so and continue with a value labeled `example`.
- End with the block's result for this run: the returned value, raised error, or changed state, and where control goes next.
- Derive the run from inspected code and label it as a code-derived trace. It is not observed behavior and does not satisfy a required runtime check. Do not create or modify a file to produce it.
- Give one run per block. Add a run with other values when I ask for one, or when a reachable error or alternate branch stays unclear after the line-by-line explanation.
- For a formatting-only change or a simple rename, state the change in one sentence and skip the line-by-line explanation and the example run. When the block has no executable statement, such as a type declaration, a configuration value, or documentation text, state that no example run applies.

For material logic changes, include brief before/after pseudocode after the overview, covering the relevant conditions, side effects, and error handling. Label it as pseudocode and keep the actual code visible. Skip pseudocode for formatting and simple renames.

Include relevant context from `WALKTHROUGH.md` beside the block. Point out a review concern only when the code supports it, explain your judgment, and state where evidence is missing. Discuss my questions about the displayed code before continuing to the next block.

Independently derive scenarios that could disprove the block's claimed behavior. Ground acceptance criteria and expected outcomes in product requirements, approved clarifications, or public contracts; do not treat the implementation or its tests as the specification. Check focused integration proof for material component or API interactions. Apply the Simplicity and reuse checks to duplication, excess abstractions, unused paths, and complexity, and assess incident diagnostics for changed failure paths. Search for the same defect pattern when a supported issue is found; inspect candidate matches, distinguish confirmed occurrences from false positives, record search limits, and discuss supported occurrences without expanding implementation authority. Missing test authoring remains work for phase `09`, subject to the existing `AGREE` gate when recording it in `FOLLOWUP.md`.

For runtime changes, use available running applications and real APIs through existing tools in an authorized environment. Remote requests remain read-only unless their side effects are authorized. Record observed behavior, code-only conclusions, and required pending checks in the primary checklist; required runtime verification gaps keep the relevant item pending.

For each material changed behavior, identify affected durable user-, operator-, API-, configuration-, or developer-facing documentation. Record the exact documentation update and validation evidence, or an evidence-based `Not applicable` decision, in the primary checklist. Discuss a missing or inaccurate documentation result alongside the relevant code; do not implement the documentation change here.

### Re-entry from the test audit

Phase `10` routes production, documentation, dependency, build, configuration, and environment findings to this phase, plus test-only findings that phase `09` reported as unsupported with evidence and the audit still holds, and test-only findings that are still `Open` after three phase-`09` correction attempts. When I start this walkthrough for those findings:

- Read `TEST_AUDIT.md` and list each `Open` finding whose destination is phase `07` by its identifier. Unlike `REVIEW.md`, these findings are input for our discussion. Check each one against the actual code and PR changes, show the code it cites, and explain whether the evidence supports it. The audit's conclusion is not my decision.
- Limit the checklist to the files those findings cite and the non-test files whose `viewerViewedState` is `DISMISSED` (changed since viewed) or `UNVIEWED` (added or not yet reviewed). Test files changed only by phase `09` stay with phase `10` and the final human review unless a routed finding cites them. Confirm this file list with me before starting. Another file leaves the review only when I confirm it.
- Record an agreed correction in `FOLLOWUP.md` only after `AGREE`, as a new item that cites the audit finding's identifier. Keep existing items and their checkboxes unchanged.
- When I explicitly decline a routed finding by its identifier, keep it out of the implementation items. Record an entry with its identifier and my reason in the `## Declined Audit Findings` section of `FOLLOWUP.md`.
- If this re-entry adds no new `FOLLOWUP.md` item because I declined every routed finding, state that phases `08` and `09` are skipped and that the workflow goes to the next phase-`10` pass.
- The existing block review, documentation checkpoint, `RESOLVE`, Viewed-state verification, and final go-ahead rules apply unchanged.

### Approve follow-up work and finish a file

- Discuss each proposed change and agree on its exact step-by-step implementation plan, including all details needed to implement it, before recording it. Leave `FOLLOWUP.md` unchanged until I explicitly type `AGREE` in all caps for that specific item. Add only that item; `AGREE` does not advance the review to the next file. The only other `FOLLOWUP.md` write is a `## Declined Audit Findings` entry, recorded when I explicitly decline a routed `TEST_AUDIT.md` finding by its identifier.
- Ask for `RESOLVE` only after every changed block in the current file is reviewed and each material changed behavior has a documentation-checkpoint result. Required documentation work may enter `FOLLOWUP.md` only after `AGREE`; otherwise keep it as a concern in the primary checklist.
- Only when I type `RESOLVE` in all caps, refresh the current file's PR changes with `gh` and compare them with the reviewed version. If they changed, review the new changes, refresh the documentation checkpoint, and obtain `RESOLVE` again before marking the file complete.
- For an unchanged, fully reviewed file, use `gh api graphql` to call `markFileAsViewed` with the current PR's node ID and exact repository-relative file path. Query the file's `viewerViewedState` and verify `VIEWED` before marking the primary checklist item resolved and advancing. If the file is already viewed, verify that state; it does not replace the review or `RESOLVE` gate.
- If the GitHub update or verification fails, report the failure and keep completion pending. Do not silently skip it, claim success, or advance to another file. File completion must not resolve review conversations or submit PR approval.
- After verified file completion, show the next file's first semantic block and explain how it connects to the surrounding code. When every file is resolved, tell me so and wait for my final go-ahead. The final go-ahead is my explicit statement in chat that the walkthrough is complete; `AGREE`, `RESOLVE`, and silence are not a final go-ahead. After it, name the next step under the `FOLLOWUP.md` rules. Implementation happens only in that next phase.

Do not modify code, tests, or durable documentation during this walkthrough. If evidence is insufficient or a review point is ambiguous, stop and ask. If you have questions, cannot make a decision, do not have enough context, or hit conflicts, DO NOT MAKE ASSUMPTIONS. STOP. ASK. GET CONFIRMATION. THEN PROCEED.

Keep every workflow-generated Markdown artifact in the target repo root under its exact required filename. Include `Created by`, `Created at`, and `Updated at` metadata; preserve the creation fields and refresh `Updated at` on each edit. Create or update `FOLLOWUP.md` only in that root and only for explicitly agreed changes and explicitly declined audit findings.

## FOLLOWUP.md rules

Track approved implementation work in `FOLLOWUP.md`. Keep the primary PR review checklist separate.

Each item must include:

- checkbox,
- item type: `implementation` for phase `08` or `test-authoring` for phase `09`; record production and test work as separate items,
- exact file(s),
- exact symbol(s)/location(s),
- exact change to make,
- why we agreed to it,
- acceptance criteria tied to product requirements or approved clarifications, with independent expected outcomes and applicable integration/API checks,
- verification needed,
- documentation checkpoint: exact durable documentation file/section, update, and validation, or the evidence-based `Not applicable` rationale,
- the `TEST_AUDIT.md` finding identifier, when the item comes from a routed audit finding,
- any risks or constraints.

Do not include speculative items.

Do not include optional suggestions unless I explicitly agree.

Do not include an item from `REVIEW.md`. Discard the AI review completely in this phase.

Do not add placeholder, draft, or "to discuss" items to `FOLLOWUP.md`.

Keep a `## Declined Audit Findings` section in `FOLLOWUP.md` only for routed `TEST_AUDIT.md` findings that I explicitly decline by identifier. Each entry records the finding identifier and my reason. These entries are not implementation work: give them no checkbox, and do not convert them into items. Keep earlier entries unchanged.

Hand the human-approved `FOLLOWUP.md` to the next implementation phase, or to the next phase-`10` pass when a test-audit re-entry added no new item. When the first walkthrough agrees no item, create no `FOLLOWUP.md`, skip phase `08`, and state that the next step is `09_write_focused_tests_any_model.md`. Do not implement its changes during this walkthrough.
