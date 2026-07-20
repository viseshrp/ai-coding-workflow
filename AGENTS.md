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
- `prompts/01_...md` through `prompts/09_...md`
  - Canonical phase prompts.
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

- No skill router. Skills are listed directly inside the relevant prompts.
- Prompts are intentionally self-contained, even when that creates duplication.
- The prompt is the contract for the target model in that phase.
- Each workflow phase should have exactly one prompt input. If the previous phase generates that prompt, the generated artifact is the only prompt for the next phase and should replace any separate checked-in prompt for that same step.
- Repeated policy blocks are duplicated on purpose; do not replace them with references like "same as prompt 07".
- The workflow uses explicit model-role boundaries:
  - Any capable repo-aware model for the initial exploration/grilling and final test-writing phases.
  - GPT or Gemini for meta critique/verification in some phases.
  - Claude Opus for planning/review/revision phases.
  - GPT or Claude Sonnet for the human walkthrough gate.
  - GPT for execution, fix, and follow-up phases.
- The default planning artifact is a combined `FEATURE_SPEC_AND_PLAN.md` plus a separate `GPT_EXECUTION_PROMPT.md`.
- `SPEC.md` plus `IMPLEMENTATION_PLAN.md` is not the default in the current pack; it is only a fallback or special case.
- The main Opus planning pass, Opus plan-revision pass, GPT execution pass, and GPT review-fix pass are driven by generated artifact prompts, not by separate checked-in prompt files.
- Execution phases must require the model to stage changes with `git add`, create commit(s), push the current branch, and create a pull request only if the current branch does not already have one.
- If an execution prompt needs a fallback way to check whether a pull request already exists for the current branch, it should use GitHub CLI (`gh`) only for that fallback rather than inventing duplicate-prone behavior.
- Execution phases must also require the model not to stage or commit workflow-generated Markdown artifacts such as `DRAFT_PLAN.md`, `FEATURE_SPEC_AND_PLAN.md`, `GPT_EXECUTION_PROMPT.md`, `REVIEW.md`, `WALKTHROUGH.md`, `GPT_REVIEW_FIX_PROMPT.md`, `REVIEW_FIX_VERIFICATION.md`, and `FOLLOWUP.md` unless the user explicitly asks for that.
- The final test-writing phase must require the fewest meaningful tests, small readable test functions/helpers, pytest-native APIs where available, and at least 85% coverage for new or changed lines.
- Before using its skills, phase `09` must enter `../ai-skills-archive`, pull `origin/main` with `--ff-only`, read each listed local `SKILL.md` completely, and return to the target repository.
- Phase `09` may change test files only. It must not generate another prompt, plan, review, walkthrough, summary, or workflow artifact, and it must not retain, stage, or commit generated coverage output.
- Human review of the phase-`09` test diff is the terminal workflow step. Do not add another AI phase after it.
- Runtime artifacts such as `DRAFT_PLAN.md`, `FEATURE_SPEC_AND_PLAN.md`, `REVIEW.md`, `FOLLOWUP.md`, and similar files are outputs described by prompts. They are not part of the default checked-in source set for this repo.

## Canonical Workflow Phases

The numbered prompt files define the workflow order and should stay in sequence.

1. `01_initial_exploration_any_model.md`
   - Clarifies a vague idea.
   - Produces `DRAFT_PLAN.md` and `INITIAL_OPUS_PLANNING_PROMPT.md`.
   - The Opus prompt produced here is the final paste-ready prompt for the main planning pass.
   - The main Opus planning phase is driven by that generated artifact rather than by a separate checked-in prompt file.
2. `02_plan_critique_gpt_gemini.md`
   - Critiques the locked planning artifacts.
   - Produces `PLAN_CRITIQUE.md` and `OPUS_PLAN_REVISION_REQUEST.md`.
   - The generated `OPUS_PLAN_REVISION_REQUEST.md` is the final paste-ready prompt for the Opus revision pass.
3. `03_plan_revision_verification_gpt_gemini.md`
   - Verifies that the revision addressed the critique.
   - Produces `PLAN_REVISION_VERIFICATION.md`.
   - If issues remain, the workflow returns to `02`; this phase does not author an alternate `OPUS_PLAN_REVISION_REQUEST.md`.
   - Locked execution is then driven by the generated `GPT_EXECUTION_PROMPT.md` plus `FEATURE_SPEC_AND_PLAN.md`; there is no separate checked-in execution prompt file.
4. `04_opus_review_branch.md`
   - Reviews implemented changes.
   - Produces `REVIEW.md`, `WALKTHROUGH.md`, and `GPT_REVIEW_FIX_PROMPT.md`.
   - The generated `GPT_REVIEW_FIX_PROMPT.md` is the final paste-ready prompt for the GPT review-fix pass.
5. `05_opus_verify_review_fixes.md`
   - Verifies the review-fix pass.
   - Produces `REVIEW_FIX_VERIFICATION.md`.
   - If issues remain, the workflow returns to `04`; this phase does not author an alternate `GPT_REVIEW_FIX_PROMPT.md`.
6. `06_opus_refresh_review_and_walkthrough.md`
   - Refreshes final `REVIEW.md` and `WALKTHROUGH.md` after fixes.
7. `07_human_code_walkthrough.md`
   - Human review gate.
   - Creates `FOLLOWUP.md` only from explicitly agreed items.
8. `08_gpt_implement_human_followup.md`
   - Implements only human-approved `FOLLOWUP.md` items.
9. `09_write_focused_tests_any_model.md`
   - Writes the smallest meaningful focused pytest test set for the final branch state.
   - Is explicitly model-agnostic and must not rely on vendor-specific behavior or tooling.
   - Pulls and reads its relevant skills from the sibling `../ai-skills-archive` repository before using them.
   - Requires at least 85% coverage for new or changed lines.
   - Changes test files only and generates no downstream prompt or workflow artifact.
   - Hands the resulting test diff directly to a human reviewer, which ends the workflow.

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

Present in all prompt files `01` through `09`.

Expectation:

- Keep the rule semantically aligned everywhere.
- The exact phrasing can vary slightly only if the phase genuinely requires it.
- Do not weaken the rule in one phase without a deliberate reason.

### `## Engineering Contract`

Present in:

- `prompts/02_plan_critique_gpt_gemini.md`
- `prompts/03_plan_revision_verification_gpt_gemini.md`
- `prompts/04_opus_review_branch.md`
- `prompts/05_opus_verify_review_fixes.md`
- `prompts/06_opus_refresh_review_and_walkthrough.md`
- `prompts/08_gpt_implement_human_followup.md`
- `prompts/09_write_focused_tests_any_model.md`

Expectation:

- This is the main cross-phase policy block.
- Changes here are high-impact and must be propagated deliberately.
- If you change policy semantics, review every copy before finishing.
- `01` does not contain the contract directly, but it instructs generated planning prompts to preserve constraints; keep that relationship in mind.
- `09` uses a test-focused Engineering Contract; keep its shared scope, verification, artifact, and Git rules aligned while preserving its explicit authorization to write tests.

The `### Tests` subsection is deliberately phase-specific:

- phases `01`, `02`, `03`, `05`, and `08` state only the no-authoring boundary and defer detailed test policy to `09`,
- phases `04` and `06` carry concise review-only test criteria,
- phase `09` owns the complete test-authoring contract,
- do not copy phase `09`'s detailed pytest rules back into every Engineering Contract.

### Combined planning artifact policy

Current default:

- `FEATURE_SPEC_AND_PLAN.md`
- `GPT_EXECUTION_PROMPT.md`

This policy is reflected in `README.md`, `01`, `02`, `03`, and downstream prompts that reference the combined artifact.

Do not casually reintroduce separate `SPEC.md` plus `IMPLEMENTATION_PLAN.md` as the default.

### Review artifact chain

The review/fix/human-review portion relies on a stable artifact chain:

- `REVIEW.md`
- `WALKTHROUGH.md`
- `GPT_REVIEW_FIX_PROMPT.md`
- `REVIEW_FIX_VERIFICATION.md`
- `FOLLOWUP.md`

If you rename or materially redefine one of these, update every downstream consumer prompt.

### Human approval gate

The explicit `AGREE` gate in `07_human_code_walkthrough.md` is intentional and high-value.

`FOLLOWUP.md` must remain human-approved only. Do not weaken this gate accidentally.

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
- Preserve explicit skill links or local skill paths.
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

- Keep wording direct and imperative.
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
- Do not add a generated prompt, review loop, or workflow artifact after phase `09`; only human review of its tests follows.
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
- `08_gpt_implement_human_followup.md`,
- `09_write_focused_tests_any_model.md`,
- references to `FOLLOWUP.md`,
- explicit approval wording around `AGREE`.

## Verification Checklist For Prompt-Pack Changes

Before finishing a change, verify:

- the repo has the expected `01` through `09` prompt set,
- filenames referenced in docs actually exist,
- artifact names are spelled consistently across producer and consumer prompts,
- skill references are consistent where intended,
- repeated policy blocks are updated everywhere they should be,
- `README.md` matches the actual prompt set and workflow,
- no file under `sources/` was modified, added, renamed, moved, or deleted,
- any new wording did not accidentally add scope or remove guardrails,
- Markdown remains readable and copy-paste ready.

## Suggested Search Targets When Maintaining This Repo

When making non-trivial changes, search for these strings before finalizing:

- `## Skill Handling Rule`
- `## Engineering Contract`
- `FEATURE_SPEC_AND_PLAN.md`
- `GPT_EXECUTION_PROMPT.md`
- `REVIEW.md`
- `WALKTHROUGH.md`
- `FOLLOWUP.md`
- `DO NOT MAKE ASSUMPTIONS`
- `Do not write tests`
- `85% coverage`
- `Use only the explicitly linked skills`
- `Use only the local skills`

## Default Agent Posture In This Repo

Be conservative.

Prefer exactness over creativity.

Preserve intentional duplication when it supports self-contained prompt usage.

Make the smallest change that keeps the workflow internally consistent.
