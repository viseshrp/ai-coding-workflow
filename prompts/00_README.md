# Agentic Coding Prompt Pack — Independent Phase Prompts

This zip contains separate self-contained Markdown prompts. Each prompt can be dropped directly into its own phase/session without needing to reference another prompt file.

## Design decisions in this version

- The repeated Codex implementation rules and Opus review checks were consolidated into one internal **Engineering Contract** section that is embedded inside the prompts that need it.
- Each phase prompt is tuned to the target model family: GPT/Codex phases are outcome-first and operational, Opus/Sonnet phases use explicit sectioning and evidence-grounded output contracts, and GPT/Gemini/Codex critique phases keep verdicts and schemas explicit.
- Prompt files are written to be pasted directly into the target model session. Phase-orientation notes live in the repo docs rather than as non-prompt blurbs above the prompt body.
- The default planning output is reduced from separate `SPEC.md` + `IMPLEMENTATION_PLAN.md` into one combined `FEATURE_SPEC_AND_PLAN.md`.
- `FEATURE_SPEC_AND_PLAN.md` still preserves your intended split: the spec/reference section is the detailed reference, and the implementation plan section is the strict execution contract with links to the spec/reference anchors.
- `CODEX_EXECUTION_PROMPT.md` remains separate because it is the artifact pasted into Codex for implementation.
- Skill links point to your `viseshrp/ai-skills-archive` repository.
- No skill router is used. Skill links are included directly in the relevant prompt files.
- Every prompt is intentionally self-contained, so some duplication remains across files.
- Prompt `01` creates the exploration outputs and a seed Opus planning prompt, prompt `02` is the optional helper that refines that seed into the final paste-ready Opus planning prompt, and prompt `03` is the direct Opus planning prompt itself.

## Prompt files

1. `01_initial_exploration_gpt_codex.md`
2. `02_meta_create_opus_planning_prompt.md`
3. `03_opus_planning_create_feature_spec_plan_and_codex_prompt.md`
4. `04_plan_critique_gpt_gemini_codex.md`
5. `05_opus_apply_plan_critique.md`
6. `06_plan_revision_verification_gpt_gemini_codex.md`
7. `07_codex_execute_locked_plan.md`
8. `08_opus_review_branch.md`
9. `09_codex_fix_opus_review_findings.md`
10. `10_opus_verify_review_fixes.md`
11. `11_opus_refresh_review_and_walkthrough.md`
12. `12_sonnet_human_code_walkthrough.md`
13. `13_codex_implement_human_followup.md`

## Skill links used

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
