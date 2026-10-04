# 11 - Optional Repository Complexity Audit - Any Model

Run this independent phase only when I explicitly request a repository complexity audit. Its number identifies the prompt; it is not a step after phase `10` and is not a prerequisite for the main workflow. Audit backend and UI repositories alike. Remain read-only and report findings in chat.

## Skills

- [ponytail-audit](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/DietrichGebert__ponytail/snapshot/skills/ponytail-audit/SKILL.md).
- [ponytail-review](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/DietrichGebert__ponytail/snapshot/skills/ponytail-review/SKILL.md), the review procedure referenced by `ponytail-audit`.
- [no-ai-slop](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/petergyang__no-ai-slop/snapshot/skills/no-ai-slop/SKILL.md), including its required [eval.md](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/petergyang__no-ai-slop/snapshot/skills/no-ai-slop/eval.md).

## Skill Handling Rule

Use only this prompt's explicitly linked skills. Fetch and read each applicable skill and required companion completely from its GitHub URL before use. Do not depend on local skill repositories, installed slash commands, or earlier prompt text. If a required file cannot be fetched and read completely, stop and report the blocker.

Apply the activation rules in `## UI work only` to conditional UI skill links. Skip those links when UI work is out of scope. Keep all other required skill loading unchanged.

The prompt is the contract. Skills are supporting procedures only. If a skill conflicts with this prompt, this prompt wins. If a conflict is material, stop and ask instead of silently choosing. Do not invoke unlisted skills or let a skill expand the phase's write permissions, outputs, or approval scope.

`no-ai-slop` is mandatory for every Markdown document this phase creates or revises. Treat it as the ultimate writing guide and final authority for prose and presentation after satisfying this prompt's factual, technical, structural, and output requirements. If another skill or instruction conflicts only on writing style, `no-ai-slop` wins; this prompt and approved task artifacts still control scope, meaning, required structure, artifact names, constraints, and evidence.

Apply `no-ai-slop` while drafting and run its `eval.md` self-check before saving each Markdown artifact or sending the final response. If its `SKILL.md` or `eval.md` cannot be read and applied, stop before creating or revising Markdown and report the blocker. Ignore its draft-request, detection-mode, and mandatory `What changed` workflow unless this prompt explicitly asks for them.

Use the Ponytail skills for evidence-based complexity findings only. Ignore line-count scoring, automatic single-caller or single-implementation findings, persistent modes, and the prescribed one-line output. Do not copy examples that weaken validation, correctness, compatibility, or test requirements. Rank findings by maintenance benefit, confidence, and change risk.

## Engineering Contract

### Scope

- Inspect the requested repository and any explicit scope limits. A whole-repository audit is permitted when requested; report excluded, unreadable, generated, vendored, or unexamined areas rather than claiming complete coverage.
- Do not create, edit, delete, format, or regenerate files. Do not create a report file, plan, prompt, debt ledger, or code comment. Do not stage, commit, push, switch branches, create or update a pull request, resolve review threads, or merge.
- Use read-only inspection and existing evidence. Do not run commands that install dependencies, write caches or reports, update snapshots, modify databases, or change remote state. If verification needs a write, record the missing evidence and defer it.
- Audit complexity and maintenance cost. Do not turn this into a correctness, security, performance, test, or visual audit. Report an incidentally discovered material issue separately with its evidence and route it to an authorized review; do not fix it here.
- Findings are suggestions for human selection. Do not infer authorization to implement them or overwrite an existing locked plan or `FOLLOWUP.md`.

### Simplicity and reuse

Apply this procedure to backend and UI work within this phase's existing permissions. In review-only phases, assess proposed or existing changes without implementing them:

- Before proposing or adding custom code, inspect relevant existing helpers, types, and patterns, then standard-library capabilities, native platform features, and already-installed dependencies. Prefer a compatible existing solution when it preserves behavior and readability; name the concrete alternative when flagging duplication.
- Justify a new abstraction or dependency by a current requirement, meaningful duplication, or a necessary ownership boundary. A single implementation or caller is not by itself a defect. Preserve dependency approval and source-documentation grounding.
- For a bug fix, trace the relevant callers, data flow, and error flow before choosing the repair location. Address the root cause within approved scope; if a shared fix would exceed that scope or alter compatibility, stop and ask.
- Before proposing deletion, inspect direct callers, dynamic or string references, public contracts, configuration, and relevant tests. Fewer lines or files are not acceptance criteria; preserve validation, security, accessibility, error handling, and verification.
- Do not substitute a simpler interpretation for an explicit requirement or locked plan. Put out-of-scope simplifications in the phase's permitted suggestions or chat; implementation still requires its existing authorization. Preserve the test-authoring boundary, native test-framework rules, and coverage gate; do not introduce production assertion demos, one-test quotas, persistent modes, debt markers, or new ledgers.

### Simplification limits and improvement claims

- During planning, record each deliberate simplification with a material limit: why it meets current requirements, its known limit, and the evidence that would trigger revisiting it. Do not invent thresholds or weaken explicit requirements. Carry applicable limits and revisit triggers into existing durable documentation during authorized implementation or fixes. In review, verification, and audit phases, check these decisions and route gaps through the existing documentation checkpoint; do not exceed the phase's write permissions. Use existing planning and documentation sections without adding comment markers, a debt ledger, or another artifact.
- In reviews and handoffs, distinguish measured improvements from expectations. Claims of reduced latency, memory use, or cost require comparable before-and-after evidence identifying the baseline, changed version, workload, measurement method, and relevant environment. Without comparable evidence, label the expected improvement `unmeasured`; do not infer savings from fewer lines, an implementation never built, or unrelated benchmarks. Use existing verification facilities within the phase's permissions; this rule does not authorize new benchmark files, dependencies, or configuration changes.

### Documentation checkpoint

- Identify the durable documentation files and sections that each proposed change would affect, along with the validation it would need, or record an evidence-based `Not applicable` decision.
- Report existing documentation gaps relevant to a finding. Do not edit documentation or require a prior workflow artifact to run this independent audit.

### Finding bar

- Name the concrete maintenance cost, affected file and symbol, callers or consumers, and proposed replacement. For reuse, identify the existing path; for standard-library or native alternatives, identify the exact API and verify relevant version and semantic compatibility.
- Before proposing deletion, inspect direct callers, exports, configuration, tests, fixtures, and dynamic or string references. Lack of a text match alone does not prove dead code; identify unresolved runtime or external consumers.
- Preserve validation, security, accessibility, error handling, public contracts, and behavior. A layer with one caller, one implementation, or few lines is not automatically unnecessary; explain why its ownership or compatibility role is not needed.
- Distinguish supported findings from candidates lacking evidence. Reject changes whose only benefit is fewer lines or that trade readable code for clever expressions. State material limits and revisit triggers for proposed simplifications.
- Use `delete`, `stdlib`, `native`, `reuse`, `yagni`, or `shrink` as finding labels when useful. Do not impose a finding quota or report hypothetical code, time, or cost savings as measured results.

## UI work only

Enable this section only when the audit scope includes UI code. A backend service having UI consumers does not by itself enable it. For backend-only work, skip this section and its UI-specific checks and reporting.

Apply the same complexity evidence bar to UI helpers, wrappers, dependencies, and components. Preserve component contracts, design tokens, accessibility behavior, and platform support. Do not judge visual taste or introduce animations, prototypes, or browser interactions. No additional UI skill downloads are required for this audit.

## Prompt

Goal:
Find supported opportunities to reduce maintenance cost in the requested repository without changing its behavior or files.

1. Read repository instructions, identify the requested scope, and record the current revision and any existing uncommitted changes without modifying them.
2. Inspect relevant entry points, dependency manifests, configuration, and module boundaries. Trace candidate duplication or unnecessary layers through their actual consumers before drawing conclusions.
3. Evaluate each candidate against the finding bar. Rank supported findings by maintenance benefit, confidence, and risk; keep uncertain candidates separate.
4. Complete the documentation checkpoint and verify that repository files and Git state remain unchanged by this phase.
5. Present the report in chat and stop. If I select findings for implementation, carry the exact selected findings into phase `01` as user-supplied context. For an active human walkthrough, each follow-up still requires `AGREE` and the final go-ahead before phase `08`.

## Required final response

Include:

- Scope and evidence: revision, areas inspected, exclusions, and limits on completeness.
- Ranked findings: location, concrete cost, replacement, caller and contract evidence, expected benefit, risk, and required verification.
- Unresolved candidates or rejected candidates when they explain a material limit in the audit.
- Documentation checkpoint: affected durable files and validation needed, or evidence-based `Not applicable` decisions.
- Handoff: no changes made; any selected work still needs the applicable planning or human-approval path. If no supported findings remain, say so without treating this audit as production approval.
