# Agentic Coding Prompt Pack - Independent Phase Prompts

This folder contains separate self-contained Markdown prompts. Each checked-in prompt can be pasted directly into its own workflow phase without needing to reference another checked-in prompt file.

The generated prompt artifacts are different: when one phase creates the prompt for the next phase, that generated artifact is the real next prompt and should be used directly.

## Before You Start In Cursor / Copilot / Similar Agent UIs

- Run this workflow inside the target code repository, not inside this prompt-pack repository.
- Keep generated workflow artifacts strictly in the target repo root using the exact required filenames. Do not place them in subdirectories or alternate paths.
- Require every generated workflow artifact to include `Created by`, `Created at`, and `Updated at`. Preserve the creation fields after first creation and refresh `Updated at` on every edit.
- Use the exact artifact names required by the prompts, such as `DRAFT_PLAN.md`, `FEATURE_SPEC_AND_PLAN.md`, and `GPT_EXECUTION_PROMPT.md`.
- Prefer a fresh chat for each major phase or each model handoff so the session stays clean and the artifact boundary stays explicit.
- When a phase generates the next prompt, paste that generated artifact into the next model. Do not substitute a different checked-in prompt for that same step.
- In execution phases, expect the model to verify, `git add`, commit, push, and create a pull request only if the current branch does not already have one.
- If an execution phase needs a fallback way to check whether the current branch already has a pull request, use GitHub CLI (`gh`) only for that fallback.
- In execution phases, do not stage or commit workflow-generated Markdown artifacts unless you explicitly want that.

## Design Decisions In This Version

- The repeated GPT implementation rules and Opus review checks were consolidated into one internal `Engineering Contract` section that is embedded inside the prompts that need it.
- Each checked-in phase prompt is tuned to the target model family: GPT phases are outcome-first and operational, Opus/Sonnet phases use explicit sectioning and evidence-grounded output contracts, and GPT/Gemini critique phases keep verdicts and schemas explicit.
- Prompt files are written to be pasted directly into the target model session. Phase-orientation notes live in repo docs rather than as non-prompt blurbs above the prompt body.
- Each workflow phase should have exactly one prompt input. When the previous phase generates that prompt, the generated artifact is the only prompt for the next phase and replaces any separate checked-in prompt for that same step.
- The default planning output is reduced from separate `SPEC.md` + `IMPLEMENTATION_PLAN.md` into one combined `FEATURE_SPEC_AND_PLAN.md`.
- `FEATURE_SPEC_AND_PLAN.md` still preserves the intended split: the spec/reference section is the detailed reference, and the implementation plan section is the strict execution contract with links back to the spec/reference anchors.
- `GPT_EXECUTION_PROMPT.md` remains separate because it is the generated artifact pasted into GPT for execution.
- No skill router is used. Skill links are included directly in the relevant prompt files and in the generated downstream artifact prompts.
- Every prompt is intentionally self-contained, so some duplication remains across files.
- Prompt `01` creates the exploration outputs and the final paste-ready Opus planning prompt artifact, `INITIAL_OPUS_PLANNING_PROMPT.md`.
- The main Opus planning pass is driven by that generated artifact, not by a separate checked-in prompt file.
- Prompt `02` critiques the planning artifacts and generates `OPUS_PLAN_REVISION_REQUEST.md` as the final direct-use Opus revision prompt when changes are needed.
- Prompt `03` verifies the latest revision and, if it fails, sends the workflow back to `02` rather than generating an alternate revision prompt.
- There is no separate checked-in Opus plan-revision prompt file after the fold; the generated `OPUS_PLAN_REVISION_REQUEST.md` is the real revision-phase prompt.
- Locked execution is driven by the generated `GPT_EXECUTION_PROMPT.md` plus `FEATURE_SPEC_AND_PLAN.md`, not by a separate checked-in execution prompt file.
- Prompt `04` reviews the implemented branch and generates `GPT_REVIEW_FIX_PROMPT.md` as the final direct-use GPT fix prompt when review findings need action.
- Prompt `05` verifies the fix pass and, if it fails, sends the workflow back to `04` rather than generating an alternate fix prompt.
- There is no separate checked-in GPT review-fix prompt file after the fold; the generated `GPT_REVIEW_FIX_PROMPT.md` is the real review-fix prompt.
- Skill links point to the `viseshrp/ai-skills-archive` repository.

## Files In This Folder

- `README.md`
  - The pack-local guide you are reading now.
- `01_initial_exploration_gpt.md`
- `02_plan_critique_gpt_gemini.md`
- `03_plan_revision_verification_gpt_gemini.md`
- `04_opus_review_branch.md`
- `05_opus_verify_review_fixes.md`
- `06_opus_refresh_review_and_walkthrough.md`
- `07_sonnet_human_code_walkthrough.md`
- `08_gpt_implement_human_followup.md`

## Generated Workflow Artifacts That Replace Removed Checked-In Prompts

- `INITIAL_OPUS_PLANNING_PROMPT.md`
  - The direct-use Opus planning prompt generated by `01`.
- `OPUS_PLAN_REVISION_REQUEST.md`
  - The direct-use Opus plan-revision prompt generated by `02`.
- `GPT_EXECUTION_PROMPT.md`
  - The direct-use GPT execution prompt generated by the Opus planning phase.
- `GPT_REVIEW_FIX_PROMPT.md`
  - The direct-use GPT review-fix prompt generated by `04`.

## Step-By-Step Usage In Cursor / Copilot Agent Windows

1. Open the target code repository in Cursor, VS Code with Copilot agent mode, or another editor that gives the model live access to the repo files.
2. Keep this prompt-pack repo open in another window or side tab so you can copy the phase prompts from `prompts/`.
3. Run the workflow in the target code repo window, not in this repo. The prompt pack is the instruction source; the target repo is where the real work and runtime artifacts live.
4. Save every generated workflow artifact in the target repo root using the exact required filename. Do not place them in subdirectories or alternate paths. Make sure each artifact includes `Created by`, `Created at`, and `Updated at`; preserve the creation fields after first creation and refresh `Updated at` on every edit. If your UI does not auto-create files from model output, create the file manually and paste the output in.
5. Start a fresh GPT agent chat and paste `01_initial_exploration_gpt.md`. Add your task request below it and let that phase produce `DRAFT_PLAN.md` and `INITIAL_OPUS_PLANNING_PROMPT.md`.
6. Start a fresh Claude Opus chat and paste the generated `INITIAL_OPUS_PLANNING_PROMPT.md`. Let Opus create `FEATURE_SPEC_AND_PLAN.md` and `GPT_EXECUTION_PROMPT.md`.
7. Start a fresh GPT or Gemini critique chat and paste `02_plan_critique_gpt_gemini.md`. That phase should read the planning artifacts and produce `PLAN_CRITIQUE.md` and, when needed, `OPUS_PLAN_REVISION_REQUEST.md`.
8. If `02` says the plan needs revision, return to Opus and paste the generated `OPUS_PLAN_REVISION_REQUEST.md`. Save the updated `FEATURE_SPEC_AND_PLAN.md`, the updated `GPT_EXECUTION_PROMPT.md`, and `PLAN_REVISION_SUMMARY.md`.
9. Run `03_plan_revision_verification_gpt_gemini.md` in GPT or Gemini to verify the revision. If it still fails, go back to `02`. Repeat until the plan is actually locked.
10. Once the plan is locked, start a fresh GPT execution chat and paste the generated `GPT_EXECUTION_PROMPT.md`. GPT should implement against the locked `FEATURE_SPEC_AND_PLAN.md`.
    That execution pass should verify, `git add`, commit, push, and create a pull request only if the current branch does not already have one.
    It should not stage or commit workflow-generated Markdown artifacts such as `FEATURE_SPEC_AND_PLAN.md` or `GPT_EXECUTION_PROMPT.md` unless you explicitly ask for that.
11. After implementation, start a fresh Claude Opus review chat and paste `04_opus_review_branch.md`. Save `REVIEW.md`, `WALKTHROUGH.md`, and, if fixes are needed, `GPT_REVIEW_FIX_PROMPT.md`.
12. If Opus produced `GPT_REVIEW_FIX_PROMPT.md`, start a fresh GPT fix chat and paste that generated prompt. Let GPT fix all valid review findings, including non-blocking issues and minor nits, but not purely optional suggestions unless you explicitly approve them. That fix pass should also verify, `git add`, commit, push, and create a pull request only if the current branch does not already have one.
    It should not stage or commit workflow-generated Markdown artifacts such as `REVIEW.md`, `WALKTHROUGH.md`, or `GPT_REVIEW_FIX_PROMPT.md` unless you explicitly ask for that.
13. Run `05_opus_verify_review_fixes.md` in Opus to verify the fixes. If verification fails, go back to `04`. Repeat `04` -> generated `GPT_REVIEW_FIX_PROMPT.md` -> `05` until the AI review loop is complete.
14. Run `06_opus_refresh_review_and_walkthrough.md` in Opus so the final `REVIEW.md` and `WALKTHROUGH.md` reflect the post-fix code rather than a stale snapshot.
15. Run `07_sonnet_human_code_walkthrough.md` in Claude Sonnet with you present. Only items you explicitly approve should go into `FOLLOWUP.md`.
16. If `FOLLOWUP.md` exists, start a fresh GPT chat and paste `08_gpt_implement_human_followup.md`. GPT should implement only the human-approved follow-up items, then verify, `git add`, commit, push, and create a pull request only if the current branch does not already have one.
    It should not stage or commit workflow-generated Markdown artifacts such as `FOLLOWUP.md` unless you explicitly ask for that.
17. Do the final manual review yourself. The workflow does not replace that last human check.

## Worked Example

Example task:

`Add a CSV export button to the orders table in an existing React + Node repository without changing the current API contract or adding tests unless explicitly requested.`

Example operator flow:

1. Open the real product repo in Cursor or Copilot agent mode.
2. In the GPT chat for phase `01`, paste `01_initial_exploration_gpt.md`, then add a short operator note such as:

```text
We are working in the repo currently open in this editor.
Store generated workflow artifacts in the repo root.
Task: add a CSV export button to the orders table without changing the current API contract.
Do not write tests unless they become explicitly approved later.
```

3. Save the outputs from phase `01` as `DRAFT_PLAN.md` and `INITIAL_OPUS_PLANNING_PROMPT.md` in the target repo root.
4. Open an Opus chat, paste `INITIAL_OPUS_PLANNING_PROMPT.md`, and let Opus produce `FEATURE_SPEC_AND_PLAN.md` plus `GPT_EXECUTION_PROMPT.md`.
5. Open a GPT or Gemini critique chat, paste `02_plan_critique_gpt_gemini.md`, and let it critique whether the CSV export plan is actually complete. Save `PLAN_CRITIQUE.md` and `OPUS_PLAN_REVISION_REQUEST.md` if produced.
6. If the critique says the plan missed edge cases such as large export size, existing permissions, or table-filter behavior, paste `OPUS_PLAN_REVISION_REQUEST.md` into Opus and save the revised planning artifacts.
7. Paste `03_plan_revision_verification_gpt_gemini.md` into GPT or Gemini and confirm the revised plan now handles those issues. If it still fails, loop back to `02`.
8. When the plan is locked, paste `GPT_EXECUTION_PROMPT.md` into GPT in the target repo window and let it implement the CSV export change. That pass should also verify, `git add`, commit, push, and create a pull request only if the branch does not already have one.
   It should not commit workflow-generated Markdown artifacts unless you explicitly ask for that.
9. Paste `04_opus_review_branch.md` into Opus to review the implementation. If Opus generates `GPT_REVIEW_FIX_PROMPT.md`, paste that into a fresh GPT chat and fix every valid issue from `Blocking Issues` and `Non-Blocking Issues`, including minor nits.
10. Paste `05_opus_verify_review_fixes.md` into Opus to confirm the fix pass really addressed the findings. Repeat the review loop if needed.
11. Paste `06_opus_refresh_review_and_walkthrough.md` into Opus, then paste `07_sonnet_human_code_walkthrough.md` into Sonnet to walk yourself through the final diff.
12. If you explicitly approve any final cleanup item, save it in `FOLLOWUP.md`, then paste `08_gpt_implement_human_followup.md` into GPT to apply only that approved follow-up work. That pass should also verify, `git add`, commit, push, and create a pull request only if the branch does not already have one.
   It should not commit workflow-generated Markdown artifacts unless you explicitly ask for that.

## Skill Links Used

- [interview-me](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/interview-me/SKILL.md)
- [grill-me](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/mattpocock__skills/snapshot/skills/productivity/grill-me/SKILL.md)
- [idea-refine](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/idea-refine/SKILL.md)
- [spec-driven-development](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/spec-driven-development/SKILL.md)
- [planning-and-task-breakdown](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/planning-and-task-breakdown/SKILL.md)
- [context-engineering](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/context-engineering/SKILL.md)
- [source-driven-development](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/source-driven-development/SKILL.md)
- [incremental-implementation](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/incremental-implementation/SKILL.md)
- [verification-before-completion](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/obra__Superpowers/snapshot/skills/verification-before-completion/SKILL.md)
- [code-review-and-quality](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/code-review-and-quality/SKILL.md)
- [code-simplification](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/code-simplification/SKILL.md)
- [receiving-code-review](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/obra__Superpowers/snapshot/skills/receiving-code-review/SKILL.md)
