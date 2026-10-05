# AGENTS.md

## Purpose

This repository is a prompt-pack and workflow repository, not an application codebase.

Its primary job is to store and maintain a multi-phase AI coding workflow as copy-paste-ready Markdown prompts. Most work here is prompt curation, wording maintenance, workflow consistency, artifact naming consistency, and source-material preservation.

Future agents should optimize for:

- preserving workflow semantics,
- preserving phase boundaries,
- preserving self-contained prompts,
- keeping repeated policy blocks synchronized when intentionally duplicated,
- making only narrowly scoped, reviewable documentation changes.

## What This Repo Is

- A canonical set of phase-specific prompts under `prompts/`.
- A small source-material archive under `sources/`.
- A historical/refactored archive document under `archived/`.
- A repository whose main outputs are Markdown prompt artifacts, not runnable code.

## What This Repo Is Not

- Not an app or library.
- Not a place to generate runtime workflow artifacts by default.
- Not a place for speculative architecture changes.
- Not a place to introduce automation, codegen, or prompt indirection unless explicitly requested.

## Primary Rule For Agents

Treat the prompt pack as a product. The prompt wording, artifact names, review gates, and model-role boundaries are the behavior.

If you change wording that changes behavior, you are changing product logic.

## Repository Map

- `README.md`
  - User-facing workflow and prompt-pack guide.
- `AGENTS.md`
  - This repository-level maintenance guide.
- `.gitattributes`
  - Text normalization; preserve LF-friendly text files.
- `prompts/01_...md` through `prompts/10_...md`
  - Canonical main-workflow phase prompts.
- `prompts/11_optional_complexity_audit_any_model.md` and `prompts/12_optional_ui_prototyping_any_model.md`
  - Independent opt-in phases; their numbers do not extend the main workflow after phase `10`.
- `sources/current_skill_set.txt`
  - Preserved historical skill inventory. Its name does not make it a current synchronization target.
- `sources/original_scrappy_prompts.txt`
  - Earlier/raw source material.
- `sources/*.pdf`
  - Reference material that informed the workflow.
- `sources/chat_exports/`
  - Preserved chat/export context.
- `archived/agentic_coding_prompt_pack_refactored.md`
  - Historical consolidated/refactored prompt-pack document for reference/audit, not the main editable surface.
- `.agents/`
  - Present but currently empty.
- `.codex/`
  - Present but currently empty.

## Canonical Editing Surface

Default to editing only:

- `prompts/*.md`
- `README.md`
- `AGENTS.md`

Never edit, rename, or rewrite anything under `archived/` unless the user explicitly asks for archive work.

Do not populate `.agents/` or `.codex/` unless explicitly asked.

## Immutable Source Material - Hard Rule

Everything under `sources/` is immutable original or reference input. NEVER create, edit, rewrite, rename, move, format, normalize, regenerate, or delete a file under `sources/`.

This prohibition includes:

- `sources/original_scrappy_prompts.txt`,
- `sources/current_skill_set.txt`, despite its name,
- every file under `sources/chat_exports/`,
- every PDF and any future file placed under `sources/`.

Do not include `sources/` in repository-wide replacements, threshold updates, formatting passes, skill synchronization, archive refreshes, or wording cleanup. Read these files when provenance is needed, but apply derived changes only to canonical prompts, `README.md`, or `AGENTS.md`.

If a task appears to require changing a source file, stop and ask instead of modifying it. A broad request such as "change all mentions" does not override this rule.

## Core Product Constraints

These are the main design constraints that define this repo:

- No skill router. Each prompt lists its skills with explicit GitHub links, including required skill dependencies. Generated prompts must embed their complete skill links and handling rules. Fetch linked skills and required companions from GitHub; do not depend on local skill repositories, installed slash commands, or earlier prompt text.
- Prompts are intentionally self-contained, even when that creates duplication.
- Prompts are language-agnostic by default. Put language-specific guidance in clearly labeled subsections organized by language, and apply it only when the target repository uses that language or framework.
- Every checked-in phase prompt and every generated downstream prompt must include `no-ai-slop` and its `eval.md`. For every Markdown document a phase creates or revises, make them a hard requirement and the ultimate writing guide. They are the final authority for prose and presentation after the prompt's factual, technical, structural, and output requirements are satisfied. Require the model to apply the skill while drafting, run the evaluator before saving each Markdown artifact, and stop before writing Markdown if either file cannot be read and applied. Let `no-ai-slop` win over conflicting writing-style guidance, but never let it change scope, meaning, required structure, artifact names, constraints, or evidence. Ignore its draft-request, detection-mode, and mandatory `What changed` workflow unless the phase explicitly asks for them.
- The prompt is the contract for the target model in that phase.
- Each workflow phase should have exactly one prompt input. If the previous phase generates that prompt, the generated artifact is the only prompt for the next phase and should replace any separate checked-in prompt for that same step.
- Repeated policy blocks are duplicated on purpose; do not replace them with references like "same as prompt 07".
- The workflow uses explicit model-role boundaries:
  - Any capable repo-aware model or agent for exploration, critique, verification, execution, review fixes, the human walkthrough, follow-up implementation, test writing, and the independent test audit.
  - Claude Opus for planning, plan revision, and implemented-branch review.
- The default planning artifact is a combined `FEATURE_SPEC_AND_PLAN.md` plus a separate `EXECUTION_PROMPT.md`.
- `SPEC.md` plus `IMPLEMENTATION_PLAN.md` is not the default in the current pack; it is only a fallback or special case.
- The main Opus planning pass, Opus plan-revision pass, implementation pass, and review-fix pass are driven by generated artifact prompts, not by separate checked-in prompt files.
- Execution phases must require the model to stage changes with `git add`, create commit(s), push the current branch, and create a pull request only if the current branch does not already have one.
- If an execution prompt needs a fallback way to check whether a pull request already exists for the current branch, it should use GitHub CLI (`gh`) only for that fallback rather than inventing duplicate-prone behavior.
- Execution phases must also require the model not to stage or commit workflow-generated Markdown artifacts such as `DRAFT_PLAN.md`, `FEATURE_SPEC_AND_PLAN.md`, `EXECUTION_PROMPT.md`, `REVIEW.md`, `WALKTHROUGH.md`, `REVIEW_FIX_PROMPT.md`, `REVIEW_FIX_VERIFICATION.md`, `FOLLOWUP.md`, and `TEST_AUDIT.md` unless the user explicitly asks for that.
- Documentation is a required checkpoint at every planning, implementation, review, verification, and handoff stage. Each checkpoint must explicitly record either the durable documentation files/sections updated and their validation evidence, or an evidence-based `Not applicable` decision. Implementation and fix phases must complete applicable documentation in the same change set; phases `09` and `10` may only verify and escalate a gap because their scopes forbid documentation edits.
- The final test-writing phase must require the fewest meaningful tests, small readable test functions/helpers, the repository's native test-framework APIs where available, and at least 85% coverage for new or changed lines.
- Before using its skills, phase `09` must fetch and completely read each shared and applicable language-specific `SKILL.md` and the required `no-ai-slop` evaluator from their GitHub links.
- Phase `09` may change test files only. It must not generate another prompt, plan, review, walkthrough, summary, or workflow artifact, and it must not retain, stage, or commit generated coverage output.
- Phase `10` is a read-only independent test audit by any capable repository-aware agent. It must fetch and completely read the generic `test-audit` skill, its applicable Python or JavaScript/TypeScript sections, the other explicitly linked skills, and the required `no-ai-slop` evaluator.
- Phase `10` may create or update only `TEST_AUDIT.md`. It must not edit code, tests, documentation, configuration, dependencies, Git state, or pull-request state.
- Phase `10` routes test-only findings back to `09` and other findings to an authorized implementation or human-follow-up phase. Human review of the audited test diff is the terminal workflow step after phase `10` passes.
- Runtime artifacts such as `DRAFT_PLAN.md`, `FEATURE_SPEC_AND_PLAN.md`, `REVIEW.md`, `FOLLOWUP.md`, `TEST_AUDIT.md`, and similar files are outputs described by prompts. They are not part of the default checked-in source set for this repo.

## Canonical Workflow Phases

The numbered prompt files define the workflow order and should stay in sequence.

1. `01_initial_exploration_any_model.md`
   - Clarifies a vague idea.
   - Produces `DRAFT_PLAN.md` and `INITIAL_OPUS_PLANNING_PROMPT.md`.
   - The Opus prompt produced here is the final paste-ready prompt for the main planning pass.
   - The main Opus planning phase is driven by that generated artifact rather than by a separate checked-in prompt file.
2. `02_plan_critique_any_model.md`
   - Critiques the locked planning artifacts.
   - Produces `PLAN_CRITIQUE.md` and `OPUS_PLAN_REVISION_REQUEST.md`.
   - The generated `OPUS_PLAN_REVISION_REQUEST.md` is the final paste-ready prompt for the Opus revision pass.
3. `03_plan_revision_verification_any_model.md`
   - Verifies that the revision addressed the critique.
   - Produces `PLAN_REVISION_VERIFICATION.md`.
   - If issues remain, the workflow returns to `02`; this phase does not author an alternate `OPUS_PLAN_REVISION_REQUEST.md`.
   - Locked execution is then driven by the generated `EXECUTION_PROMPT.md` plus `FEATURE_SPEC_AND_PLAN.md`; there is no separate checked-in execution prompt file.
4. `04_opus_review_branch.md`
   - Reviews implemented changes.
   - Produces `REVIEW.md`, `WALKTHROUGH.md`, and `REVIEW_FIX_PROMPT.md`.
   - The generated `REVIEW_FIX_PROMPT.md` is the final paste-ready prompt for the review-fix pass.
5. `05_opus_verify_review_fixes.md`
   - Verifies the review-fix pass.
   - Produces `REVIEW_FIX_VERIFICATION.md`.
   - If issues remain, the workflow returns to `04`; this phase does not author an alternate `REVIEW_FIX_PROMPT.md`.
6. `06_opus_refresh_review_and_walkthrough.md`
   - Refreshes final `REVIEW.md` and `WALKTHROUGH.md` after fixes.
7. `07_human_code_walkthrough.md`
   - Starts human review with a code mindmap and all reachable success/error flows.
   - Reviews small semantic blocks with excerpts for references defined outside the block.
   - Creates `FOLLOWUP.md` only from explicitly agreed items.
8. `08_implement_human_followup_any_model.md`
   - Implements only human-approved `FOLLOWUP.md` items.
9. `09_write_focused_tests_any_model.md`
   - Writes the smallest meaningful focused test set for the final branch state.
   - Is explicitly model- and language-agnostic and must not rely on vendor-specific behavior, tooling, or a language-specific framework outside its labeled guidance.
   - Fetches and completely reads its relevant skills and required evaluator from their GitHub links before using them.
   - Requires at least 85% coverage for new or changed lines.
   - Changes test files only and generates no downstream prompt or workflow artifact.
   - Hands the resulting test diff to phase `10` for independent audit.
10. `10_test_audit_any_model.md`
   - Reviews the final test diff and the production seams it requires.
   - Is explicitly model- and language-agnostic, with Python and JavaScript/TypeScript guidance supplied by the linked generic `test-audit` skill.
   - Remains read-only except for creating or updating `TEST_AUDIT.md`.
   - Routes supported findings to the correct earlier phase and hands a passing audit to the human reviewer, which ends the workflow.

### Optional independent phases

11. `11_optional_complexity_audit_any_model.md`
    - Runs only on an explicit repository complexity-audit request, including backend work.
    - Uses `ponytail-audit` and its `ponytail-review` companion to produce evidence-backed findings in chat.
    - Remains read-only, including files, documentation, Git, and pull-request state. Creates no report artifact or downstream prompt.
    - Ranks findings by maintenance benefit, confidence, and risk; selected findings return to `01` or the existing human-approval path before implementation.
12. `12_optional_ui_prototyping_any_model.md`
    - Runs only on an explicit UI-prototyping request before planning; does not follow phase `10`.
    - Uses `prototype`, its required `PICKER.md`, and `emil-design-eng` for isolated web UI variants. Resolve a compatible approach before building native UI prototypes.
    - May write only owned preview files under `.ui-prototypes/<slug>/` and `UI_PROTOTYPE.md` in the target repository root. Does not change production code, tests, durable documentation, dependencies, configuration, Git, or pull-request state.
    - Requires browser evidence and explicit human selection. Keeps selection pending when no choice was made, and verification pending when required checks could not run.
    - Hands the selected direction and `UI_PROTOTYPE.md` to `01` when planning is requested. Selection does not authorize production integration or automatic cleanup.

These phases are optional entry points, not a continuation of the main workflow. Human review after a passing phase `10` remains terminal. Keep the two independent phases out of the main workflow's sequential diagram and required run instructions. Phase `12` is exploration, so the execution-phase commit, push, and PR requirements do not apply to it. Keep prototype files and `UI_PROTOTYPE.md` out of later commits unless explicitly requested.

Do not renumber these files casually.

If a new phase is added, preserve the numbered sequence and update all places that enumerate the prompt list.

## Prompt Anatomy

Most phase prompts follow a predictable structure:

1. Title and any copy-paste-safe phase context that belongs inside the prompt artifact itself.
2. `## Skills`
3. `## Skill Handling Rule`
4. Optional `## Engineering Contract`
5. Optional artifact-policy sections such as default planning artifact reduction.
6. `## Prompt`
7. Required outputs or required final response sections.

When editing a prompt:

- preserve the structure unless the task explicitly changes the prompt format,
- preserve copy-paste friendliness,
- keep non-prompt repo-usage notes out of the prompt body unless they are part of the actual contract for the target model,
- keep instructions concrete,
- keep artifact names exact,
- avoid hidden dependencies on other files beyond what the prompt explicitly names.

## Synchronization Map

Several sections are intentionally repeated across prompts. If you edit one, search for all copies and decide whether all copies must change in the same patch.

### `## Skill Handling Rule`

Present in all prompt files `01` through `12`.

Expectation:

- Keep the rule semantically aligned everywhere.
- The exact phrasing can vary slightly only if the phase genuinely requires it.
- Do not weaken the rule in one phase without a deliberate reason.

### Archive-only skill dependencies

Every skill mentioned in the workflow must be sourced from `viseshrp/ai-skills-archive`. Before using an applicable skill, fetch and completely read its `SKILL.md`, all required evaluators (including `eval.md`), and all required dependencies and companion resources recursively from that archive repository. Include explicit archive links for those resources in every prompt that uses the skill, including generated prompts. Do not load skill material from upstream or official repositories, installed local copies, or memory. Preserve conditional activation rules, including skipping UI-only skills for backend-only work.

All executable skill references and required companions must use explicit links into `https://github.com/viseshrp/ai-skills-archive`, including evaluators, checklists, patterns, examples, and procedures referenced by another skill. Verify archived paths and dependency links before handoff; resolve relative resource references to their archive copies. If a required resource is missing, report the exact path and stop rather than fetching an upstream or official-source replacement. Keep source metadata and optional related-skill mentions inactive. This source rule governs skill material, not the target-library API/version documentation already required by the Engineering Contract.

Keep dependency loading separate from permission to act: companions do not authorize test writing outside `09`, implementation during review, optional bootstrap scripts, new artifacts, or unrelated hardening or optimization work. Apply UI-only reference sections only when UI work is active. Generated prompts must carry the complete applicable archive links, dependency scope limits, and archive-only handling rule.

### Universal plain-language skill

`no-ai-slop` is required in:

- every checked-in phase prompt from `01` through `12`,
- the generated Opus planning prompt specified by `01`,
- the generated execution prompt specified by `01`,
- the generated Opus revision prompt specified by `02`,
- the generated review-fix prompt specified by `04`.

Each phase must link both `SKILL.md` and `eval.md`. For every Markdown document the phase creates or revises, `no-ai-slop` is a hard requirement and the ultimate writing guide. It is the final authority for prose and presentation after the prompt's factual, technical, structural, and output requirements are satisfied. Apply its editing principles while drafting, run its evaluator before saving each Markdown artifact or sending the final response, and stop before creating or revising Markdown if either file cannot be read and applied. Let it win over conflicting writing-style guidance, but preserve the prompt's control over scope, meaning, required structure, artifact names, constraints, and evidence. Ignore the draft-request, detection-mode, and mandatory `What changed` workflow unless the phase explicitly asks for them.

### `## Engineering Contract`

Present in:

- `prompts/01_initial_exploration_any_model.md` (downstream contract to embed)
- `prompts/02_plan_critique_any_model.md`
- `prompts/03_plan_revision_verification_any_model.md`
- `prompts/04_opus_review_branch.md`
- `prompts/05_opus_verify_review_fixes.md`
- `prompts/06_opus_refresh_review_and_walkthrough.md`
- `prompts/08_implement_human_followup_any_model.md`
- `prompts/09_write_focused_tests_any_model.md`
- `prompts/10_test_audit_any_model.md`
- `prompts/11_optional_complexity_audit_any_model.md`
- `prompts/12_optional_ui_prototyping_any_model.md`

Expectation:

- This is the main cross-phase policy block.
- Changes here are high-impact and must be propagated deliberately.
- If you change policy semantics, review every copy before finishing.
- Keep implementation requirements aligned with review criteria: compatibility priority, justified dependencies, idiomatic code, readable types, string-transformation examples, and scope-limited regression and meta-content checks. Embed applicable requirements in generated execution/fix prompts and phase `08`; preserve the existing exceptions and test-authoring boundaries. Verify the actual generated contracts before handoff rather than relying on the producer instructions alone.
- `01` includes the downstream Engineering Contract for the generated planning prompt to embed in `EXECUTION_PROMPT.md`; keep that complete contract synchronized too.
- `09` uses a test-focused Engineering Contract; keep its shared scope, verification, artifact, and Git rules aligned while preserving its explicit authorization to write tests.
- `10` uses a read-only audit contract; preserve its prohibition on code, test, documentation, configuration, dependency, Git, and pull-request mutations.
- `11` uses a fully read-only complexity-audit contract with chat-only output. `12` uses an isolated exploration contract with only its named preview files and `UI_PROTOTYPE.md` writable; preserve the production, test, dependency, configuration, and Git boundaries.

The `### Tests` subsection is deliberately phase-specific:

- phases `01`, `02`, `03`, `05`, and `08` state only the no-authoring boundary and defer detailed test policy to `09`,
- phases `04` and `06` carry concise review-only test criteria,
- phase `09` owns the complete test-authoring contract,
- phase `10` owns the independent test-value audit and finding-routing contract,
- do not copy phase `09`'s detailed test-framework or language-specific rules back into every Engineering Contract.

### Documentation checkpoint

Documentation is a cross-phase completion gate. Keep a named documentation-checkpoint rule in every checked-in prompt and every generated downstream prompt. Planning, critique, review, verification, and the human walkthrough must identify the documentation impact and require an explicit update-or-not-applicable result; implementation, fix, and follow-up phases must complete and validate applicable durable documentation in the same change set. Phases `09` and `10` must verify that prior documentation checkpoints passed and stop/escalate if they did not, without editing documentation.

### Simplicity and reuse

Keep the general Simplicity and reuse procedure aligned across all phases and generated planning, revision, execution, and review-fix prompts. Apply it to backend and UI work within each phase's permissions. Require inspection of existing code, standard-library capabilities, native features, and installed dependencies; justification for new abstractions; caller tracing for bug fixes; and reference and contract checks before deletion.

Preserve readability, compatibility, validation, security, and verification over line-count reductions. These are embedded rules derived from Ponytail, not authorization to activate its persistent mode, weaken test requirements, add production assertion demos, or create debt markers or ledgers. Keep provenance in `README.md`.

### Simplification limits and improvement claims

Keep these rules aligned across all phases and generated downstream prompts. Planning must record the rationale, known material limit, and evidence-based revisit trigger for a deliberate simplification. Authorized implementation carries applicable limits into existing durable documentation; review, verification, and audit phases check them through the documentation checkpoint without expanding write permissions. Require comparable before-and-after evidence for latency, memory, or cost improvement claims, identifying the baseline, changed version, workload, measurement method, and relevant environment. Label unsupported expectations `unmeasured`. Do not add comment markers, ledgers, benchmark infrastructure, or workflow artifacts to satisfy these rules.

### UI work only

Keep UI guidance in a separate `## UI work only` section in phases `01` through `11` and every generated downstream prompt. Enable it only for tasks or reviewed changes involving UI behavior, layout, presentation, or interaction. Backend-only work must skip the section and its skill downloads, questions, checks, and reporting. UI consumers of a backend service do not by themselves activate it.

- Keep conditional skill links and required companions explicit and self-contained. Apply the same activation rules to UI links in generated-prompt templates; unconditional skill-loading rules must not force UI downloads for backend-only work.
- Preserve phase-specific UI responsibilities: planning acceptance criteria, scoped construction, evidence-based review and verification, independent human walkthrough, minimal test authoring in `09`, and read-only test audit in `10`.
- Preserve existing design decisions, tokens, platform support, dependency approval, and output formats. Apply web guidance only to web UI. Do not promote recipe values or aesthetic preferences to automatic blockers; verify version-sensitive APIs and performance claims.
- Override upstream prototype, development-toggle, fixture-retention, separate-report, and alternate-plan workflows. Phase `09` alone may author test-local fixtures; UI guidance must not expand another phase's write permissions or bypass `AGREE`, `RESOLVE`, or the final go-ahead.
- Verify that generated planning, revision, execution, and review-fix prompts carry complete conditional UI sections, including activation, links, companions, limits, and verification requirements. Record observed behavior separately from code-only conclusions and required browser or device checks still pending.

Optional phase `12` is entirely UI prototyping and the only exception to the prototype prohibition. List its skills directly under `## Skills`; do not add a conditional UI section or backend-only skip rule. Keep its explicit opt-in entry point, isolated directory, synthetic sample data, named `UI_PROTOTYPE.md` artifact, browser verification, selection gate, and planning handoff self-contained. Do not copy this write permission into `01` through `10` or `11`. Prototype sample data is not authorization to author shared test fixtures. Override the upstream prototype skill's automatic promotion and cleanup steps: user selection records a design choice, and production integration remains subject to planning and execution gates. Phase `11` has no UI skill downloads and applies only its complexity evidence bar to in-scope UI code.

### Combined planning artifact policy

Current default:

- `FEATURE_SPEC_AND_PLAN.md`
- `EXECUTION_PROMPT.md`

This policy is reflected in `README.md`, `01`, `02`, `03`, and downstream prompts that reference the combined artifact.

Do not casually reintroduce separate `SPEC.md` plus `IMPLEMENTATION_PLAN.md` as the default.

### Review artifact chain

The review/fix/human-review portion relies on a stable artifact chain:

- `REVIEW.md`
- `WALKTHROUGH.md`
- `REVIEW_FIX_PROMPT.md`
- `REVIEW_FIX_VERIFICATION.md`
- `FOLLOWUP.md`
- `TEST_AUDIT.md`

If you rename or materially redefine one of these, update every downstream consumer prompt.

### Human approval gate

The explicit `AGREE` gate in `07_human_code_walkthrough.md` is intentional and high-value.

`FOLLOWUP.md` must remain human-approved only. Do not weaken this gate accidentally.

Phase `07` uses the explicitly linked `show-me` skill for chat-only walkthrough visuals. Start with a code mindmap and diagrams of all reachable flows and success/error states, then review small semantic blocks with focused source diffs, pseudocode for material logic changes, and the declarations and definitions needed to understand their references. Preserve `AGREE`, `RESOLVE`, and the documentation checkpoint without imposing a fixed per-response template. Keep diagrams, presentation diffs, and pseudocode in chat only; create no HTML or additional visual artifacts. The `WALKTHROUGH.md` producers `04` and `06` retain equivalent relationship/flow coverage in prose, semantic grouping, source excerpts, and adjacent line-by-line explanations.

On `RESOLVE`, phase `07` refreshes the file's PR changes. Changes since review require further review and renewed `RESOLVE`. Otherwise, use `gh api graphql` with `markFileAsViewed` and verify the file's `viewerViewedState` is `VIEWED` before resolving the checklist item and advancing. Already-viewed status does not bypass review or approval. Update or verification failures keep completion pending; do not silently skip them. File completion must not resolve review conversations or submit PR approval. Preserve the final go-ahead gate before implementation.

### Skill inventory

If you change the canonical skill set:

- update every affected prompt file,
- update `README.md`,
- do not update the preserved `sources/current_skill_set.txt` snapshot.

## Directory-Specific Rules

### `prompts/`

This is the canonical product surface.

Rules:

- Keep phase prompt filenames zero-padded and phase-ordered.
- Keep the consolidated pack guide at the repository-root `README.md`.
- Keep prompts self-contained.
- Preserve explicit GitHub skill links and require every phase to fetch its skills and required companions from them without a local skill repository prerequisite.
- Preserve explicit artifact filenames.
- Preserve the intended target model for each phase.
- Avoid style-only rewrites that create diff noise without workflow benefit.

### `README.md`

This is the consolidated repository and prompt-pack overview. Update it when:

- prompt filenames change,
- phase count changes,
- the default planning artifact policy changes,
- the canonical skill inventory changes,
- the high-level design decisions change.

### `sources/`

Treat every file here as immutable reference input.

Rules:

- Never modify, add, rename, move, normalize, regenerate, or delete anything in this directory.
- Never use this directory as a synchronization target.
- Do not assume the source files and prompt pack are one-to-one mirrors.
- Read them for provenance or rationale only when needed.

### `archived/`

Treat `archived/agentic_coding_prompt_pack_refactored.md` as historical/reference material.

Rules:

- Do not assume it is the primary source of truth.
- Do not refresh it unless the task explicitly asks for archive parity, audit refresh, or consolidation.
- If you do update it, verify it still matches the current prompt-pack philosophy and artifact naming.

## Style Guidance For Prompt Edits

- Keep wording direct and imperative. State the action; omit commentary describing the prompt's style or presentation.
- Prefer concrete file names over vague placeholders.
- Preserve strong constraints where they are clearly intentional.
- Preserve explicit stop-and-ask behavior on ambiguity/conflict.
- Preserve "do not write tests unless explicitly asked" semantics where present; prompt `09` is the explicit final authorization.
- Preserve backwards-compatibility emphasis where present.
- Preserve the separation between required actions and optional suggestions.
- Avoid adding tool/vendor assumptions not already part of the workflow.

## Encoding And Formatting Guidance

- Keep Markdown files UTF-8 friendly.
- If terminal output shows mojibake for existing title punctuation, verify with explicit UTF-8 reading before "fixing" text.
- Prefer simple Markdown that copies cleanly into model chats.
- Preserve fenced code blocks and exact artifact names inside them.
- Keep line endings text-friendly and compatible with `.gitattributes`.

## What Not To Do

- Do not replace shared safety-policy blocks with "see other file" references. Phase-owned detail, such as test authoring, may stay centralized in its owning phase with a concise boundary elsewhere.
- Do not invent a skill router.
- Do not silently change the default artifact flow.
- Do not collapse human approval gates.
- Do not weaken scope-control instructions accidentally.
- Do not generate runtime workflow artifacts in the repo unless the user explicitly asks for them.
- Do not add a generated prompt after phase `09`. Phase `10` uses its checked-in prompt and may create only `TEST_AUDIT.md`; only human review follows a passing audit.
- Do not treat `archived/` as the primary editable surface.
- Do not rename prompts just for aesthetics.

## Change Playbooks

### If you change a skill reference

Also check:

- the prompt file that uses it,
- other prompts that should stay aligned by phase,
- `README.md`.

### If you change the Engineering Contract

Also check:

- every prompt that contains `## Engineering Contract`,
- prompts that describe generated prompts embedding that contract,
- whether the change alters downstream review expectations,
- whether the change alters artifact expectations.

### If you change generated artifact names

Also check:

- upstream producer prompts,
- downstream consumer prompts,
- `README.md`,
- any explicit required-output headings that mention the artifact.

### If you add a new workflow phase

Also check:

- numbering and filename ordering,
- `README.md`,
- any text that enumerates the workflow end-to-end,
- whether the new phase should contain `## Skill Handling Rule`,
- whether it should contain `## Engineering Contract`.

### If you revise the human walkthrough/follow-up flow

Also check:

- `07_human_code_walkthrough.md`,
- `08_implement_human_followup_any_model.md`,
- `09_write_focused_tests_any_model.md`,
- `10_test_audit_any_model.md`,
- references to `FOLLOWUP.md`,
- explicit approval wording around `AGREE`.

## Verification Checklist For Prompt-Pack Changes

Before finishing a change, verify:

- the repo has the expected `01` through `10` prompt set,
- independent prompts `11` and `12` are present, explicitly optional, and do not extend the terminal phase-10 workflow,
- filenames referenced in docs actually exist,
- artifact names are spelled consistently across producer and consumer prompts,
- skill references are consistent where intended,
- repeated policy blocks are updated everywhere they should be,
- `README.md` matches the actual prompt set and workflow,
- no file under `sources/` was modified, added, renamed, moved, or deleted,
- any new wording did not accidentally add scope or remove guardrails,
- every phase has an explicit documentation checkpoint appropriate to its write permissions,
- Markdown remains readable and copy-paste ready.

## Suggested Search Targets When Maintaining This Repo

When making non-trivial changes, search for these strings before finalizing:

- `## Skill Handling Rule`
- `## Engineering Contract`
- `FEATURE_SPEC_AND_PLAN.md`
- `EXECUTION_PROMPT.md`
- `REVIEW.md`
- `WALKTHROUGH.md`
- `FOLLOWUP.md`
- `TEST_AUDIT.md`
- `DO NOT MAKE ASSUMPTIONS`
- `Do not write tests`
- `85% coverage`
- `Use only the explicitly linked skills`
- `Fetch and read`
- `no-ai-slop`
- `test-audit`
- `Documentation checkpoint`

## Default Agent Posture In This Repo

Be conservative.

Prefer exactness over creativity.

Preserve intentional duplication when it supports self-contained prompt usage.

Make the smallest change that keeps the workflow internally consistent.
