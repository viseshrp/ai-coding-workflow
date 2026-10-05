# 12 - Optional UI Prototyping - Any Model

Run this independent phase only when I explicitly request UI prototypes before planning or ask to explore alternative UI directions. Its number identifies the prompt; it does not follow phase `10`. Selection is a design decision for a later planning pass, not authorization to implement production changes.

## Skills

- [no-ai-slop](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/petergyang__no-ai-slop/snapshot/skills/no-ai-slop/SKILL.md), including its required [eval.md](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/petergyang__no-ai-slop/snapshot/skills/no-ai-slop/eval.md).
- [prototype](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/emilkowalski__skills/snapshot/skills/prototype/SKILL.md), including its required [PICKER.md](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/emilkowalski__skills/snapshot/skills/prototype/PICKER.md).
- [emil-design-eng](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/emilkowalski__skills/snapshot/skills/emil-design-eng/SKILL.md).

These procedures describe web UI. For a native UI request, resolve a compatible prototype approach before building; do not impose HTML, CSS, or browser conventions on the production stack or silently substitute a web implementation.

## Skill Handling Rule

Fetch skill procedures and their required companions only from `https://github.com/viseshrp/ai-skills-archive`. Resolve relative resource references to the explicitly linked archive copies; do not follow upstream skill URLs, install a skill package, or substitute an official-source copy. If a required archive resource is absent or unreadable, stop and report its exact missing path. Keep optional related-skill mentions and provenance links inactive unless this prompt explicitly authorizes the procedure. Target-library API and version documentation remains governed by the Engineering Contract; it is not a substitute source for skill material.

Use linked companions within this phase's scope. Preserve the test-authoring boundary and named outputs, and do not run optional bootstrap scripts.

Use only this prompt's explicitly linked skills. Fetch and read each applicable skill and required companion completely from its GitHub URL before use. Do not depend on local skill repositories, installed slash commands, or earlier prompt text. If a required file cannot be fetched and read completely, stop and report the blocker.

The prompt is the contract. Skills are supporting procedures only. If a skill conflicts with this prompt, this prompt wins. If a conflict is material, stop and ask instead of silently choosing. Do not invoke unlisted skills or let a skill expand the phase's write permissions, outputs, or approval scope.

`no-ai-slop` is mandatory for every Markdown document this phase creates or revises. Treat it as the ultimate writing guide and final authority for prose and presentation after satisfying this prompt's factual, technical, structural, and output requirements. If another skill or instruction conflicts only on writing style, `no-ai-slop` wins; this prompt and approved task artifacts still control scope, meaning, required structure, artifact names, constraints, and evidence.

Apply `no-ai-slop` while drafting and run its `eval.md` self-check before saving each Markdown artifact or sending the final response. If its `SKILL.md` or `eval.md` cannot be read and applied, stop before creating or revising Markdown and report the blocker. Ignore its draft-request, detection-mode, and mandatory `What changed` workflow unless this prompt explicitly asks for them.

Ignore skill greeting and pause routines. Follow the prototype skill through variant construction, verification, and human selection; do not follow its automatic production-promotion step. This phase's isolated output boundary overrides any skill instruction to modify application routes, integrate a winner, delete pre-existing files, or create additional reports.

## Engineering Contract

### Scope

- Work on one UI surface per run. If the request spans unrelated surfaces, resolve which one to explore before writing files. Inspect repository instructions, existing components, tokens, supported platforms, and the current Git status.
- Create or revise only files owned by this prototype run under `.ui-prototypes/<slug>/` and `UI_PROTOTYPE.md` in the target repository root. Choose an unused slug for new work. Do not overwrite existing prototypes or an unrelated `UI_PROTOTYPE.md`; resolve ownership or resume scope first.
- Do not modify production code, application routes, shared assets, tests, durable documentation, dependency manifests, lockfiles, build configuration, or deployment configuration. Do not install dependencies, add production feature flags, call mutating service endpoints, or write real user data. Use prototype-local synthetic sample data and isolated state.
- Use a self-contained HTML preview or existing tooling that can serve the isolated directory without changing application files or configuration. Verify that the preview is outside production imports, routes, builds, and deployment inputs. If safe isolation cannot be established, stop and report the blocker instead of placing the prototype in the application.
- Do not stage, commit, push, create or update a pull request, or deploy. This is an exploration phase, not an execution phase. Keep prototype files and `UI_PROTOTYPE.md` out of later commits unless explicitly requested. Do not author tests; later implementation follows the main workflow's test phases.

### Simplicity and reuse

Apply this procedure within the prototype's scope and output boundaries:

- Before proposing or adding custom code, inspect relevant existing helpers, types, and patterns, then standard-library capabilities, native platform features, and already-installed dependencies. Prefer a compatible existing solution when it preserves behavior and readability; name the concrete alternative when flagging duplication.
- Justify a new abstraction or dependency by a current requirement, meaningful duplication, or a necessary ownership boundary. A single implementation or caller is not by itself a defect. Preserve dependency approval and source-documentation grounding.
- For a bug fix, trace the relevant callers, data flow, and error flow before choosing the repair location. Address the root cause within approved scope; if a shared fix would exceed that scope or alter compatibility, stop and ask.
- Before proposing deletion, inspect direct callers, dynamic or string references, public contracts, configuration, and relevant tests. Fewer lines or files are not acceptance criteria; preserve validation, security, accessibility, error handling, and verification.
- Do not substitute a simpler interpretation for an explicit requirement or locked plan. Put out-of-scope simplifications in the phase's permitted suggestions or chat; implementation still requires its existing authorization. Preserve existing tests and validation requirements; do not author tests in this phase or introduce production assertion demos, one-test quotas, persistent modes, debt markers, or new ledgers.

### Simplification limits and improvement claims

- Record each deliberate prototype simplification with a material limit in `UI_PROTOTYPE.md`: why it is sufficient for the design decision, its known limit, and the evidence that would trigger revisiting it during planning. Do not invent thresholds or weaken explicit requirements. Carry relevant limits into the planning handoff; durable documentation changes wait for authorized implementation. Do not add comment markers, a debt ledger, or another artifact.
- In reviews and handoffs, distinguish measured improvements from expectations. Claims of reduced latency, memory use, or cost require comparable before-and-after evidence identifying the baseline, changed version, workload, measurement method, and relevant environment. Without comparable evidence, label the expected improvement `unmeasured`; do not infer savings from fewer lines, an implementation never built, or unrelated benchmarks. Use existing verification facilities within the phase's permissions; this rule does not authorize new benchmark files, dependencies, or configuration changes.

### Documentation checkpoint

- In `UI_PROTOTYPE.md`, record the durable documentation files and sections a selected design would affect, the planned validation, or an evidence-based `Not applicable` decision. Do not edit those durable files in this phase.
- Record prototype limitations, simulated behavior, and material simplification limits with revisit triggers. The prototype is evidence for planning, not proof of production readiness.

## Prototype requirements

### Skill limits

- This phase alone permits isolated prototype files and a picker. It does not enable prototypes, development toggles, or additional artifacts in phases `01` through `10` or the complexity audit.
- Reuse the project's visual language and component conventions where the isolation boundary permits. Existing tokens, approved behavior, accessibility, and supported platforms take precedence over generic aesthetic preferences or recipe values. Do not add motion solely to distinguish variants or introduce a dependency to satisfy a skill recipe.
- Follow `PICKER.md` for picker structure, appearance, and keyboard behavior. Preserve its accessible controls, instant variant switching, conditional replay, and input-focus exclusions. Check reload selection and invalid selection parameters; correct functional or accessibility defects within the isolated preview rather than copying a broken edge case verbatim.
- Distinguish observed behavior, code-only conclusions, and browser or device checks still pending. Do not claim visual verification from static inspection. Record unavailable required checks as pending or blocked in `UI_PROTOTYPE.md`.
- Preserve explicit human selection. Neither a default picker state nor a model recommendation counts as my choice. A request to keep a variant records the chosen direction; production integration requires a separate authorized planning and execution pass.

### Phase requirements

- Build three distinct variants by default, fewer if only fewer meaningful alternatives exist, and at most five when requested. Name each variant and its design difference before construction. Do not pad the set with color or copy changes alone.
- Render one full-size variant at a time in realistic surrounding context. Use representative long and missing values and applicable loading, error, and empty states. Demonstrate each requested interaction with local state; identify simulated service behavior explicitly.
- Verify every variant and picker control with available browser tooling. Check applicable keyboard and focus behavior, supported sizes, reduced motion, repeat interactions, reload selection, and console errors. Use existing tools only and keep any screenshots within this run's prototype directory.
- Present the variants with their tradeoffs and a working preview URL or file path. Wait for my choice or revision request. Keep the prototype available while selection is pending; do not promote or delete it automatically.
- After selection, update `UI_PROTOTYPE.md` with my exact choice and any constraints. Hand the artifact and selected prototype path to phase `01` as context when I request planning. Plan production integration and later cleanup explicitly; remove only this run's files when cleanup is authorized.

## Prompt

Goal:
Explore distinct UI directions in an isolated preview so I can choose one before locking a production plan.

1. Confirm the requested surface, required interactions, existing design constraints, and permitted preview approach from the task and repository. Resolve material gaps before construction.
2. Read the applicable linked skills and companions, inspect the target code, and establish the isolated output path. Build the variants and picker within that boundary.
3. Run the available preview checks. Record exact evidence and remaining uncertainty; do not mark the phase verified while required checks are pending.
4. Create or update `UI_PROTOTYPE.md`, present the comparison in chat, and wait for my explicit selection. If I request another round, revise only the owned preview files and update the comparison and verification evidence.
5. Record the selected direction and hand off to planning. Do not generate a planning prompt, change locked planning artifacts, or implement the selected design in production.

## Required output: `UI_PROTOTYPE.md`

Create or update this artifact only in the target repository root. Include `Created by`, `Created at`, and `Updated at`; preserve creation fields on updates.

Use this structure:

```markdown
# UI Prototype

Created by:
Created at:
Updated at:

## Scope and Constraints

## Preview Files and Run Instructions

## Variant Comparison

## Verification Evidence and Pending Checks

## Human Selection

## Documentation Checkpoint

## Planning Handoff and Cleanup
```

Record exact owned file paths, preview instructions, named variants and their tradeoffs, simulated behavior, verification commands or interactions and outcomes, and any required checks still pending. Set `Human Selection` to `Pending` until I explicitly choose. Include the rationale, known limits, and revisit triggers for material simplifications. The handoff must state that production integration has not occurred and preserve the main workflow's planning, review, and human-approval gates.

## Required final response

Include:

- The preview URL or file path and how to switch variants.
- A compact comparison of each variant's design difference, benefit, and cost.
- Verification results and any required checks still pending.
- The selection status and link to `UI_PROTOTYPE.md`.
- The next authorized step: wait for my choice, revise the requested variants, or hand the selected direction to planning. Do not treat selection as production implementation approval.
