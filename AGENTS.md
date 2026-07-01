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
  - Minimal root entrypoint.
- `AGENTS.md`
  - This repository-level maintenance guide.
- `.gitattributes`
  - Text normalization; preserve LF-friendly text files.
- `prompts/00_README.md`
  - User-facing overview of the independent prompt pack.
- `prompts/01_...md` through `prompts/11_...md`
  - Canonical phase prompts.
- `sources/current_skill_set.txt`
  - Condensed skill inventory by workflow phase.
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
- `prompts/00_README.md`
- `sources/current_skill_set.txt`
- `README.md`
- `AGENTS.md`

Do not edit `archived/` unless the task explicitly asks for the archive to be refreshed or kept in sync.

Do not populate `.agents/` or `.codex/` unless explicitly asked.

Do not edit PDFs or chat exports unless explicitly asked.

## Core Product Constraints

These are the main design constraints that define this repo:

- No skill router. Skills are linked directly inside the relevant prompts.
- Prompts are intentionally self-contained, even when that creates duplication.
- The prompt is the contract for the target model in that phase.
- Repeated policy blocks are duplicated on purpose; do not replace them with references like "same as prompt 07".
- The workflow uses explicit model-role boundaries:
  - GPT/Codex for exploration/meta critique in some phases.
  - Claude Opus for planning/review/revision phases.
  - Claude Sonnet for human walkthrough/follow-up gating.
  - Codex for execution/fix phases.
- The default planning artifact is a combined `FEATURE_SPEC_AND_PLAN.md` plus a separate `CODEX_EXECUTION_PROMPT.md`.
- `SPEC.md` plus `IMPLEMENTATION_PLAN.md` is not the default in the current pack; it is only a fallback or special case.
- Runtime artifacts such as `DRAFT_PLAN.md`, `FEATURE_SPEC_AND_PLAN.md`, `REVIEW.md`, `FOLLOWUP.md`, and similar files are outputs described by prompts. They are not part of the default checked-in source set for this repo.

## Canonical Workflow Phases

The numbered prompt files define the workflow order and should stay in sequence.

1. `01_initial_exploration_gpt_codex.md`
   - Clarifies a vague idea.
   - Produces `DRAFT_PLAN.md` and `INITIAL_OPUS_PLANNING_PROMPT.md`.
   - The Opus prompt produced here is the final paste-ready prompt for the main planning pass.
   - The main Opus planning phase is driven by that generated artifact rather than by a separate checked-in prompt file.
2. `02_plan_critique_gpt_gemini_codex.md`
   - Critiques the locked planning artifacts.
   - Produces `PLAN_CRITIQUE.md` and `OPUS_PLAN_REVISION_REQUEST.md`.
3. `03_opus_apply_plan_critique.md`
   - Revises the planning artifacts.
4. `04_plan_revision_verification_gpt_gemini_codex.md`
   - Verifies that the revision addressed the critique.
   - Produces `PLAN_REVISION_VERIFICATION.md`.
5. `05_codex_execute_locked_plan.md`
   - Executes the locked implementation plan.
6. `06_opus_review_branch.md`
   - Reviews implemented changes.
   - Produces `REVIEW.md`, `WALKTHROUGH.md`, and `CODEX_REVIEW_FIX_PROMPT.md`.
7. `07_codex_fix_opus_review_findings.md`
   - Fixes valid review findings from the Opus review.
8. `08_opus_verify_review_fixes.md`
   - Verifies the review-fix pass.
   - Produces `REVIEW_FIX_VERIFICATION.md`.
9. `09_opus_refresh_review_and_walkthrough.md`
   - Refreshes final `REVIEW.md` and `WALKTHROUGH.md` after fixes.
10. `10_sonnet_human_code_walkthrough.md`
   - Human review gate.
   - Creates `FOLLOWUP.md` only from explicitly agreed items.
11. `11_codex_implement_human_followup.md`
   - Implements only human-approved `FOLLOWUP.md` items.

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

Present in all prompt files `01` through `11`.

Expectation:

- Keep the rule semantically aligned everywhere.
- The exact phrasing can vary slightly only if the phase genuinely requires it.
- Do not weaken the rule in one phase without a deliberate reason.

### `## Engineering Contract`

Present in:

- `prompts/02_plan_critique_gpt_gemini_codex.md`
- `prompts/03_opus_apply_plan_critique.md`
- `prompts/04_plan_revision_verification_gpt_gemini_codex.md`
- `prompts/05_codex_execute_locked_plan.md`
- `prompts/06_opus_review_branch.md`
- `prompts/07_codex_fix_opus_review_findings.md`
- `prompts/08_opus_verify_review_fixes.md`
- `prompts/09_opus_refresh_review_and_walkthrough.md`
- `prompts/11_codex_implement_human_followup.md`

Expectation:

- This is the main cross-phase policy block.
- Changes here are high-impact and must be propagated deliberately.
- If you change policy semantics, review every copy before finishing.
- `01` does not contain the contract directly, but it instructs generated planning prompts to preserve constraints; keep that relationship in mind.

### Combined planning artifact policy

Current default:

- `FEATURE_SPEC_AND_PLAN.md`
- `CODEX_EXECUTION_PROMPT.md`

This policy is reflected in multiple files including `prompts/00_README.md`, `01`, and downstream prompts that reference the combined artifact.

Do not casually reintroduce separate `SPEC.md` plus `IMPLEMENTATION_PLAN.md` as the default.

### Review artifact chain

The review/fix/human-review portion relies on a stable artifact chain:

- `REVIEW.md`
- `WALKTHROUGH.md`
- `CODEX_REVIEW_FIX_PROMPT.md`
- `REVIEW_FIX_VERIFICATION.md`
- `FOLLOWUP.md`

If you rename or materially redefine one of these, update every downstream consumer prompt.

### Human approval gate

The explicit `AGREE` gate in `10_sonnet_human_code_walkthrough.md` is intentional and high-value.

`FOLLOWUP.md` must remain human-approved only. Do not weaken this gate accidentally.

### Skill inventory

If you change the canonical skill set:

- update every affected prompt file,
- update `prompts/00_README.md`,
- update `sources/current_skill_set.txt`.

## Directory-Specific Rules

### `prompts/`

This is the canonical product surface.

Rules:

- Keep filenames zero-padded and phase-ordered.
- Keep prompts self-contained.
- Preserve explicit skill links.
- Preserve explicit artifact filenames.
- Preserve the intended target model for each phase.
- Avoid style-only rewrites that create diff noise without workflow benefit.

### `prompts/00_README.md`

This is the pack overview. Update it when:

- prompt filenames change,
- phase count changes,
- the default planning artifact policy changes,
- the canonical skill inventory changes,
- the high-level design decisions change.

### `sources/current_skill_set.txt`

Treat this as a compact support manifest for the workflow's skill placement.

Update it when:

- a skill is added,
- a skill is removed,
- a skill moves to a different workflow phase,
- phase names materially change.

### `sources/`

Treat files here as reference inputs, not ordinary editable docs.

Rules:

- Do not rename or rewrite source PDFs casually.
- Do not assume the source files and prompt pack are one-to-one mirrors.
- Use them for rationale only when needed.

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
- Preserve "do not write tests unless explicitly asked" semantics where present.
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

- Do not replace repeated policy blocks with "see other file" references.
- Do not invent a skill router.
- Do not silently change the default artifact flow.
- Do not collapse human approval gates.
- Do not weaken scope-control instructions accidentally.
- Do not generate runtime workflow artifacts in the repo unless the user explicitly asks for them.
- Do not treat `archived/` as the primary editable surface.
- Do not rename prompts just for aesthetics.

## Change Playbooks

### If you change a skill link

Also check:

- the prompt file that uses it,
- other prompts that should stay aligned by phase,
- `prompts/00_README.md`,
- `sources/current_skill_set.txt`.

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
- `prompts/00_README.md`,
- any explicit required-output headings that mention the artifact.

### If you add a new workflow phase

Also check:

- numbering and filename ordering,
- `prompts/00_README.md`,
- `sources/current_skill_set.txt`,
- any text that enumerates the workflow end-to-end,
- whether the new phase should contain `## Skill Handling Rule`,
- whether it should contain `## Engineering Contract`.

### If you revise the human walkthrough/follow-up flow

Also check:

- `10_sonnet_human_code_walkthrough.md`,
- `11_codex_implement_human_followup.md`,
- references to `FOLLOWUP.md`,
- explicit approval wording around `AGREE`.

## Verification Checklist For Prompt-Pack Changes

Before finishing a change, verify:

- the repo still has the expected `00` through `11` prompt set unless the task intentionally changes it,
- filenames referenced in docs actually exist,
- artifact names are spelled consistently across producer and consumer prompts,
- skill links are consistent where intended,
- repeated policy blocks are updated everywhere they should be,
- `prompts/00_README.md` still matches the actual prompt set,
- `sources/current_skill_set.txt` still matches the actual prompt set,
- any new wording did not accidentally add scope or remove guardrails,
- Markdown remains readable and copy-paste ready.

## Suggested Search Targets When Maintaining This Repo

When making non-trivial changes, search for these strings before finalizing:

- `## Skill Handling Rule`
- `## Engineering Contract`
- `FEATURE_SPEC_AND_PLAN.md`
- `CODEX_EXECUTION_PROMPT.md`
- `REVIEW.md`
- `WALKTHROUGH.md`
- `FOLLOWUP.md`
- `DO NOT MAKE ASSUMPTIONS`
- `Do not write tests`
- `Use only the explicitly linked skills`

## Default Agent Posture In This Repo

Be conservative.

Prefer exactness over creativity.

Preserve intentional duplication when it supports self-contained prompt usage.

Make the smallest change that keeps the workflow internally consistent.
