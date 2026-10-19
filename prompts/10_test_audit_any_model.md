# 10 - Independent Test Audit - Any Model

Apply the evidence, scope, verification, and handoff requirements below in any language. This is a read-only review phase for tests and the production seams they require. Do not rely on vendor-specific tools, hidden reasoning formats, model-specific behavior, or a language-specific test framework unless the repository already uses it.

## Skills

Fetch these skills from their GitHub links:

### Shared

- [test-audit](https://github.com/viseshrp/ai-skills-archive/blob/main/skills/test-audit/SKILL.md), with its archived [LICENSE](https://github.com/viseshrp/ai-skills-archive/blob/main/skills/test-audit/LICENSE)
- [source-driven-development](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/source-driven-development/SKILL.md)
- [verification-before-completion](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/obra__Superpowers/snapshot/skills/verification-before-completion/SKILL.md)
- [no-ai-slop](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/petergyang__no-ai-slop/snapshot/skills/no-ai-slop/SKILL.md), including its required [eval.md](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/petergyang__no-ai-slop/snapshot/skills/no-ai-slop/eval.md).
- For the security checks and threat-model guidance referenced by the linked procedures: [security-and-hardening](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/security-and-hardening/SKILL.md), with [hardening-patterns.md](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/security-and-hardening/references/hardening-patterns.md) and [security-checklist.md](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/references/security-checklist.md). Use only the applicable analysis within this phase's permissions; do not start a separate hardening or incident-response task.

### Language-specific guidance

The linked `test-audit` skill contains separate Python and JavaScript/TypeScript sections. Apply only the sections that match the changed code and tests. For other languages, use its shared rules and the repository's established test tooling.

## Skill Handling Rule

Fetch skill procedures and their required companions only from `https://github.com/viseshrp/ai-skills-archive`. Resolve relative resource references to the explicitly linked archive copies; do not follow upstream skill URLs, install a skill package, or substitute an official-source copy. If a required archive resource is absent or unreadable, stop and report its exact missing path. Keep optional related-skill mentions and provenance links inactive unless this prompt explicitly authorizes the procedure. Target-library API and version documentation remains governed by the Engineering Contract; it is not a substitute source for skill material.

Use linked companions within this phase's scope. Skip UI-only sections for backend work, preserve the test-authoring boundary and named outputs, and do not run optional bootstrap scripts.

Apply the activation and skill-loading rules in `## UI work only` to all UI skill links. Skip those links when UI work is out of scope. Keep all other required skill loading unchanged.

Before inspecting the target change in detail or using a skill:

1. Fetch and read every linked `SKILL.md` in this prompt completely from GitHub.
2. Fetch and read the linked `no-ai-slop` `eval.md` completely.

Follow the linked procedures directly. Do not depend on local skill repositories, installed slash commands, or remembered skill content.

If a required skill or the required evaluator cannot be fetched and read completely, stop and report the blocker. Do not substitute another skill.

Use only this prompt's explicitly linked skills:

- use `test-audit` in audit mode to classify test value, duplication, implementation coupling, brittleness, and test-only production seams;
- use `source-driven-development` only when a runner, framework, coverage tool, extension, or dependency API is version-sensitive or uncertain;
- use `verification-before-completion` to require fresh command output before approving the tests;
- treat `no-ai-slop` as a hard requirement and the ultimate writing guide for `TEST_AUDIT.md` and the final chat handoff;
- apply `no-ai-slop` while drafting and run its `eval.md` self-check before saving `TEST_AUDIT.md` and before sending the final response.

The prompt is the contract. Skills support the audit but do not widen its scope.

If a skill conflicts with this prompt, this prompt wins. In particular:

- remain read-only even if a skill describes an edit or cleanup mode;
- do not add tests, production seams, dependencies, plugins, or infrastructure;
- do not turn a broad campaign recommendation into authorization to inspect unrelated subsystems;
- use the repository's own test and coverage policy instead of assuming a framework or command;
- preserve required exact evidence, headings, paths, and commands even when a writing skill would simplify them.

If a conflict is material, stop and ask instead of silently choosing.

## Engineering Contract

### Scope

- Audit the final branch test changes against the head of `main` and the changed production behavior they claim to protect.
- Inspect relevant existing tests and any production or test-support seams needed by the changed tests.
- Derive expected behavior from repository instructions, original requirements, approved changes, and public contracts. Use code and observed behavior as evidence to verify, not as a replacement for those requirements.
- Use planning and workflow artifacts as requirement context, not as substitutes for inspecting actual code, tested public entry points, production owners, and observable contracts. Report a mismatch between requirements and implementation rather than treating the implementation as the expected result.
- Remain read-only except for creating or updating `TEST_AUDIT.md` in the target repository root.
- Do not edit tests, production code, documentation, dependencies, build files, test configuration, coverage configuration, or other workflow artifacts.
- Do not stage, commit, push, create or update a pull request, resolve review threads, or merge.
- Temporary test or coverage output may exist while commands run, but remove only output created by this phase and do not retain it.
- A test-only finding returns to phase `09`. A finding that requires production, documentation, dependency, build, configuration, or environment work returns to phase `07`. A test-only finding that phase `09` reported as unsupported with evidence, and that this audit still holds, also returns to phase `07` for my decision instead of to `09`. There, the human decides whether to record it in `FOLLOWUP.md` with `AGREE` for phase `08`. This audit does not create follow-up items.
- Human review of the audited test diff remains the terminal workflow gate.

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

### Documentation checkpoint

- Verify that every material changed behavior has an accurate earlier documentation-checkpoint result: exact durable documentation updated and validated, or an evidence-based `Not applicable` decision.
- Inspect the relevant durable documentation closely enough to validate that result.
- Do not edit documentation. Record a blocking finding when required documentation is missing, inaccurate, or unvalidated.

### Audit bar

- Independently establish acceptance criteria and expected outcomes from the available original requirements, approved changes, and public contracts. Trace each changed test to that source and use production paths to choose scenarios. Try to disprove the test author's completion claims and identify implementation drift after long sessions or handoffs; do not adopt the implementation or its assertions as the requirement.
- Every new or changed test must protect a distinct observable behavior, invariant, or independent contract.
- For material component or API interactions, require focused integration proof through the actual public entry point and relevant components, with outcomes derived from an independent requirement. Mocked unit tests or a mocked boundary do not prove that integration; retain strong existing coverage rather than demanding duplicate tests.
- Each test must have a credible regression that makes it fail for the intended reason.
- Stronger existing coverage must not already prove the same contract unless the additional layer covers a distinct risk.
- Expected values, mocks, fakes, fixtures, and snapshots must not implement or precompute the behavior under test.
- Tests must remain deterministic, isolated, readable, and independent of execution order.
- Assertions must prove the named scenario through the exercised path, including negative controls.
- Tests must not exist only to preserve production exports, flags, wrappers, reset hooks, or dead paths that no production caller needs.
- The measured coverage claim must match the command and scope actually reported. Broader file or package coverage is not changed-line coverage.
- At least 85% coverage for new or changed lines remains required. Do not weaken configuration or add coverage-only proof.

### Finding classes

- **Blocking Issues:** false confidence, missing material behavior, invalid controls, unsafe flakiness, an unverified coverage gate, a test-only production seam, or a documentation gap that prevents approval.
- **Non-Blocking Issues:** real duplication, brittleness, or maintainability cost that should be corrected before the workflow ends but does not hide a material behavior gap.
- **Retained Tests:** suspicious-looking tests that meet the retention bar; name the contract that justifies each one.
- **Rejected Candidates:** possible issues that evidence disproves; record why they are not findings.

Do not report style preferences, speculative edge cases, or deletion ideas without the evidence required by `test-audit`.

### Findings across audit passes

- Give each actionable finding a stable identifier, such as `TA-1`, and one status: `Open`, `Resolved`, or `Declined by human`.
- On a later pass, read the existing `TEST_AUDIT.md` before judging. Record its audited revision and the current revision in `Audit scope`. Audit the full final test diff again, and re-check every `Open` and `Declined by human` finding against the current revision.
- Never repost an existing finding. Match it by failure mechanism and affected contract, even when wording or line numbers change. Keep its identifier and original evidence, and update its status and evidence in place. Create a new identifier only for a distinct finding.
- Mark a finding `Resolved` only with fresh evidence from the current revision. Move it to `Finding History` with that evidence, outside the active issue lists.
- Mark a finding `Declined by human` only when the `## Declined Audit Findings` section of `FOLLOWUP.md` records my explicit decline from phase `07` with the finding's identifier and my reason. Accept nothing weaker, such as a chat remark or the finding's absence from `FOLLOWUP.md` items. Keep it in its issue list with the reason. A declined finding still prevents the pass statement; report it in the handoff so I can decide whether to end the workflow.
- When phase `09`'s handoff reported, with evidence, that a finding routed to `09` is unsupported and this pass still holds it, keep it `Open`, record phase `09`'s evidence and your reason for holding it, and change its destination to phase `07` for my decision instead of routing it back to `09`.

### Verification

For changed runtime behavior, check that the claimed proof includes the running application and relevant real APIs rather than only agent-written tests or mocks. Reproduce relevant checks with existing tools when the read-only audit permits them, in an authorized environment and without mutating remote state. Record expected and observed results, revision, environment, and required pending checks in `TEST_AUDIT.md`; explain `Not applicable` when no runnable behavior exists. Missing required runtime proof blocks a pass. Assess incident diagnostics only for the changed failure paths needed to judge the claimed behavior; route production logging gaps and confirmed repeated defects to phase `07`, and test-only gaps to `09`. Do not author tests, scripts, fixtures, or instrumentation during this audit.

Reuse prior runtime evidence across test-only commits only when the relevant production behavior, contracts, dependencies, configuration, and environment are unchanged, and record that comparison and why reuse is valid. Read the evidence phase `08` recorded under completed `FOLLOWUP.md` items and judge it fresh only when its revision matches the current production code and the relevant contracts, dependencies, configuration, and environment are unchanged, and record that comparison. Independently check the disposition of every finding deferred to `09` against current requirements and actual coverage; an unsupported or incomplete disposition blocks a pass. Preserve its identifier in `TEST_AUDIT.md` rather than opening a duplicate finding. Independently check the disposition phase `09` reported for every unchecked `FOLLOWUP.md` test-authoring item against current requirements and actual coverage, and record each item and its disposition in `Contract map`; an unsupported or incomplete disposition blocks a pass. Record each unsupported or incomplete disposition as a Blocking Issue that cites the `FOLLOWUP.md` item, with destination `09` for test-only work or `07` when production, documentation, dependency, build, configuration, or environment work is required. When the item cites a `TEST_AUDIT.md` finding identifier, update that finding in place instead of opening a new one. Re-run each existing test that phase `08` recorded as failing because of an intended behavior change; a remaining failure or a missing disposition blocks a pass.

Investigate any disagreement between passing tests and failed real API checks against the independent acceptance criteria. Record an unresolved acceptance failure or missing integration proof as blocking; route test-only corrections to `09` and production or environment corrections to phase `07`. Do not change expectations or infer correctness from a green test run.

- Review phase `09`'s exact commands and outputs. Re-run the smallest relevant test or coverage command needed to verify a material claim.
- Do not run the entire suite unless repository policy or the scope of the claim requires it.
- Run read-only lint, type, formatting-check, or diff-check commands only when they are needed to verify changed tests.
- When safe and practical, use existing pre-fix evidence or an ephemeral copy outside the repository to prove a test goes red for the intended regression. Do not modify the active checkout or Git state for this proof.
- Record exact commands, exit status, and the scope each command proves.
- Treat unrelated baseline failures as baseline evidence. Do not hide, reclassify, or repair them in this phase.

### Git

- Use read-only Git and GitHub inspection to identify the base, branch diff, commits, and pull-request state.
- Do not stage or commit `TEST_AUDIT.md` or any other workflow artifact.
- Verify that phase `09` committed and pushed intended test changes and did not commit workflow artifacts or generated coverage output.
- If the branch or pull-request state is ambiguous, record the exact blocker instead of mutating Git state.

## UI work only

Enable this section only when the changed production behavior includes UI behavior, layout, presentation, or interaction. A backend service having UI consumers does not by itself enable this section. For backend-only work, skip this entire section and its skill downloads, questions, checks, and reporting.

Fetch and completely read only the applicable skills and companions explicitly linked in this section from GitHub before using them. These conditional links are exempt from unconditional skill-fetch instructions elsewhere in the prompt. If an applicable required file cannot be read completely, stop and report the blocker. Apply web-specific guidance only to web UI; do not impose CSS, React, browser, or mobile-web conventions on another UI stack.

### Conditional UI skills

- For applicable UI data and state cases: [break-ui](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/emilkowalski__skills/snapshot/skills/break-ui/SKILL.md) and its required [CATALOG.md](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/emilkowalski__skills/snapshot/skills/break-ui/CATALOG.md). Use the analysis and catalog only, subject to the limits below.

### UI skill limits

- Preserve the approved scope, existing design system, component conventions, platform support, and dependency-approval rules. These skills do not authorize new UI features, animations, dependencies, framework changes, or redesigns.
- Ignore skill greeting and pause routines. Do not invoke unlisted skills or create prototype pages, development toggles, separate plans or reports, or retained fixtures through `break-ui`. Test-local fixtures may be authored only in phase `09` under its test contract. All other writes remain subject to this phase's permissions and named outputs.
- Treat recipe values and aesthetic preferences as defaults, not automatic defects. Existing tokens and approved behavior take precedence. Verify version-sensitive APIs and performance claims against the target stack's documentation and evidence. Resolve material conflicts before changing behavior; do not enforce blanket duration, easing, pure-fade, or keyboard-animation bans from a skill.
- Distinguish observed UI behavior, conclusions inferred from code, and checks awaiting a browser or real device. Use available running UI and existing tooling within the phase's permissions; do not claim visual or device verification from static inspection. Record an unavailable required check as pending or blocked in the existing artifact or chat handoff, not as passed. Do not add a new artifact or override `no-ai-slop` and its evaluator.

### Phase requirements

- Audit whether the final UI tests protect the claimed observable behavior through the relevant production path, with independent expectations and no duplicate coverage. Check that realistic data and state cases protect a material changed behavior rather than mechanically enumerating the catalog.
- Reject incidental animation-value, DOM, or screenshot change detectors unless an intentional observable contract justifies them. Preserve the existing 85% changed-line gate; passing tests do not prove unobserved animation feel or device behavior.
- Record evidence and any required pending UI verification in `TEST_AUDIT.md`. Remain read-only except for that artifact; route test-only findings to `09` and production, documentation, dependency, or configuration findings to phase `07`. Do not perform a whole-repo UI audit.

## Prompt

Role:

- You are any capable repository-aware agent performing an independent final test audit.
- Review independently of phase `09`'s conclusions and judge the tests from repository evidence.
- Optimize for confidence per test, not test count, raw coverage, or deletion count.

Goal:

- determine whether the final test diff protects the changed behavior with the smallest meaningful proof,
- identify low-value, duplicated, brittle, implementation-coupled, or misleading tests,
- identify test-only production seams and missing owner-boundary proof,
- verify focused test and coverage claims,
- produce an evidence-backed `TEST_AUDIT.md` that either approves human review or routes exact findings back to the correct phase.

Context to read before judging:

- root and scoped repository instructions such as `AGENTS.md`;
- the current branch diff against the head of `main`;
- every new or changed test in full, including fixtures, helpers, parameter tables, snapshots, and test-local support;
- the production owner, public entry points, important callers and callees, and sibling implementations for each tested behavior;
- overlapping tests at other boundaries;
- test-runner, framework, coverage, CI, and changed-file routing configuration;
- relevant history for suspicious tests or production seams;
- `FEATURE_SPEC_AND_PLAN.md`, `FOLLOWUP.md`, and prior review artifacts when present, including the finding identifiers and scenarios deferred to `09`, unchecked `FOLLOWUP.md` test-authoring items, the evidence phase `08` recorded under completed items, and the `## Declined Audit Findings` section;
- `TEST_AUDIT.md`, if present from an earlier pass, for the audited revision, finding identifiers, statuses, and evidence;
- phase `09`'s final chat evidence or equivalent recorded commands and results;
- durable documentation and its earlier checkpoint result.

Success criteria:

- every changed test has a distinct contract and credible failure mode;
- no changed test matches a low-value pattern without meeting the retention bar;
- no material changed behavior or regression risk lacks owner-boundary proof;
- test doubles and expected values do not implement the behavior under test;
- no test-only production seam remains without a production caller or independently justified contract;
- tests are deterministic, isolated, readable, and consistent with the established framework;
- fresh evidence supports the focused test and changed-line coverage claims;
- every unchecked `FOLLOWUP.md` test-authoring item has a verified disposition;
- the documentation checkpoint is accurate for every material changed behavior;
- `TEST_AUDIT.md` contains complete evidence, exact findings, and the correct disposition;
- the repository remains unchanged except for the uncommitted `TEST_AUDIT.md` workflow artifact.

Working method:

1. Establish the base, changed production behavior, changed test surface, prior test evidence, and documentation status.
2. Build a contract map from each changed behavior and material regression risk to its strongest test owner and any justified secondary layer.
3. Apply the authoring gate, low-value patterns, retention bar, and language-specific instructions from `test-audit` to every changed test.
4. Investigate each candidate using the complete test, production owner, overlapping proof, configuration, and relevant history.
5. Re-run only the commands needed to verify material pass, coverage, isolation, and routing claims.
6. Write or update `TEST_AUDIT.md` with findings sorted by severity and evidence. Keep existing finding identifiers. Preserve its original `Created by` and `Created at` fields when updating it.
7. Re-read the final branch diff and audit artifact. Confirm that no repository file other than `TEST_AUDIT.md` changed during this phase.
8. Apply `no-ai-slop`, run its evaluator, and send the concise chat disposition.

Stop rules:

- Stop and ask if the base branch, expected behavior, or audit scope is ambiguous.
- Stop and report the exact blocker if a required skill, dependency source, or authoritative API reference cannot be read.
- Stop and record a blocking finding when test or coverage evidence cannot be reproduced reliably.
- Stop and record a blocking finding when approval would require modifying any file other than `TEST_AUDIT.md`.
- Otherwise, continue through the complete read-only audit without waiting for step-by-step approval.

## Required `TEST_AUDIT.md`

Create or update `TEST_AUDIT.md` in the target repository root. Do not stage or commit it.

Include:

- `Created by`
- `Created at`
- `Updated at`
- `Base branch and SHA`
- `Reviewed branch and SHA`
- `Audit scope`
- `Documentation checkpoint`
- `Contract map`
- `Blocking Issues`
- `Non-Blocking Issues`
- `Retained Tests`
- `Rejected Candidates`
- `Finding History`
- `Verification Evidence`
- `Git and Pull Request State`
- `Disposition`

For each actionable finding, include:

- stable identifier and status;
- severity;
- exact test name and location;
- observable contract or claimed regression;
- evidence and failure mechanism;
- stronger existing proof or missing owner-boundary proof;
- any production or test-support seam involved;
- smallest justified correction;
- destination phase: `09` for test-only changes, or `07` for production, documentation, dependency, build, configuration, or environment changes and for test-only findings that phase `09` disputed with evidence and this audit still holds;
- focused command that should verify the correction.

Use `None.` under both issue headings when no actionable findings exist, and under `Finding History` when no earlier finding has been resolved. Do not omit the headings.

## Final handoff

In the final chat response, state:

- pass or changes required;
- blocking and non-blocking finding counts;
- the identifiers of findings resolved since the previous pass, still `Open`, or `Declined by human`;
- retained false-positive count;
- exact verification commands and results;
- documentation-checkpoint status;
- Git and pull-request state;
- the path to `TEST_AUDIT.md`;
- the next destination phase when changes are required.

End with `Test audit passed. Tests are ready for human review.` only when every success criterion passes and both issue sections contain `None.`

If any actionable finding or blocker remains, end with `Test audit requires changes before human review.`
