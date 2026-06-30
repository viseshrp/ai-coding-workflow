# 01 — Initial Exploration / Grilling / Interviewing — GPT or Codex

Use this prompt before Opus planning. This phase turns a vague or partially formed idea into a draft plan and an initial Opus planning prompt.

## Skills

- [interview-me](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/interview-me/SKILL.md)
- [grill-me](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/mattpocock__skills/snapshot/skills/productivity/grill-me/SKILL.md)
- [idea-refine](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/idea-refine/SKILL.md)
- [context-engineering](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/context-engineering/SKILL.md)

## Skill Handling Rule

Use only the explicitly linked skills listed in this prompt.

The prompt is the contract. The locked task artifact is the contract for execution. Skills are supporting procedures only.

If a skill conflicts with this prompt, this prompt wins.

If a conflict is material, stop and ask instead of silently choosing.

Do not use any skill to expand scope, add architecture changes, add tests, add unrelated refactors, or override my explicit instructions.


## Prompt

You are helping me perform the initial exploration phase for an agentic coding workflow.

My workflow is:

1. GPT/Codex helps me think, interview, grill, and clarify the idea.
2. This produces `DRAFT_PLAN.md`.
3. This also produces `INITIAL_OPUS_PLANNING_PROMPT.md`.
4. Opus later uses the draft plan plus repo context as seed context to create:
   - `FEATURE_SPEC_AND_PLAN.md`
   - `CODEX_EXECUTION_PROMPT.md`

Do not implement code.

Do not write tests.

Do not create unrelated files.

Work interactively first.

Use the linked skills as supporting procedures:

- Use `interview-me` to extract what I actually want.
- Use `grill-me` to stress-test the plan/design.
- Use `idea-refine` to move from rough concept to concrete proposal.
- Use `context-engineering` to identify what repo context matters and avoid context flooding.

Ask one question at a time when clarification is needed.

For each question:

- ask the question,
- include your best guess,
- explain briefly why the question matters.

If a question can be answered by exploring the codebase, explore the codebase instead of asking me.

Keep going until the goal, constraints, non-goals, and definition of done are clear enough to seed Opus.

Do not produce final artifacts until exploration is complete or I explicitly ask you to stop and generate them.

## Output artifact 1: `DRAFT_PLAN.md`

Create `DRAFT_PLAN.md` with:

- problem statement,
- goals,
- non-goals,
- user-visible behavior,
- constraints,
- technical assumptions,
- open questions,
- decisions already made,
- likely files/modules involved, if known,
- risks,
- definition of done,
- anything that Opus must not lose.

## Output artifact 2: `INITIAL_OPUS_PLANNING_PROMPT.md`

Create `INITIAL_OPUS_PLANNING_PROMPT.md` as a prompt for Claude Opus.

The Opus prompt you generate must tell Opus to:

- read `DRAFT_PLAN.md`,
- inspect the repository/codebase again,
- critique the draft plan,
- ask all remaining design questions together in one batch,
- after my answers, independently flesh out the plan to the T,
- default to a combined `FEATURE_SPEC_AND_PLAN.md`,
- create `CODEX_EXECUTION_PROMPT.md`,
- ignore DevOps/packaging/building and test-related work unless otherwise specified in the plan,
- include the full Engineering Contract inside the generated Codex prompt,
- preserve all constraints and details from the draft plan.

The prompt you generate must explicitly include these skill links and instruct the target agent to use them only as supporting procedures:

- [spec-driven-development](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/spec-driven-development/SKILL.md)
- [planning-and-task-breakdown](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/planning-and-task-breakdown/SKILL.md)
- [context-engineering](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/context-engineering/SKILL.md)
- [source-driven-development](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/source-driven-development/SKILL.md)
- [verification-before-completion](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/obra__Superpowers/snapshot/skills/verification-before-completion/SKILL.md)


The Opus prompt you generate must also tell Opus that any generated `CODEX_EXECUTION_PROMPT.md` must explicitly include these skill links:

- [incremental-implementation](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/incremental-implementation/SKILL.md)
- [source-driven-development](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/source-driven-development/SKILL.md)
- [verification-before-completion](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/obra__Superpowers/snapshot/skills/verification-before-completion/SKILL.md)

If the task is still ambiguous, keep interviewing instead of pretending the plan is ready.
