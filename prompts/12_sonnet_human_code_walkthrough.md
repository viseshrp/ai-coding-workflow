# 12 — Sonnet Human Code Walkthrough + FOLLOWUP.md Creation

## Skills

- [receiving-code-review](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/obra__Superpowers/snapshot/skills/receiving-code-review/SKILL.md)
- [code-review-and-quality](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/code-review-and-quality/SKILL.md)
- [code-simplification](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/code-simplification/SKILL.md)

## Skill Handling Rule

Use only the explicitly linked skills listed in this prompt.

The prompt is the contract. The locked task artifact is the contract for execution. Skills are supporting procedures only.

If a skill conflicts with this prompt, this prompt wins.

If a conflict is material, stop and ask instead of silently choosing.

Do not use any skill to expand scope, add architecture changes, add tests, add unrelated refactors, or override my explicit instructions.


## Prompt

Role:

- You are Claude Sonnet helping me run the final human walkthrough of a PR.
- Be structured, explicit, and evidence-driven.
- If the code does not support a review point, say so plainly instead of guessing.

Goal:

- this is not the AI review/fix loop; this is the human walkthrough phase,
- look at the code review document: `REVIEW.md`,
- let me know if you agree with all points or why you do not,
- there is also a `WALKTHROUGH.md` document that we will use as a detailed supplement for the review,
- use `REVIEW.md`, `WALKTHROUGH.md`, the actual code, and the actual diff against `main` to help me review the PR one small change at a time,
- create or update `FOLLOWUP.md` only from items that I explicitly approve.

Context to read before starting:

- `REVIEW.md`,
- `WALKTHROUGH.md`,
- the current branch diff against `main`,
- the actual code referenced by the section under discussion.

Success criteria:

- each review point is checked against the real code and real diff,
- no more than 5 lines of code are shown at once,
- every proposed follow-up item is specific enough to implement directly,
- nothing is added to `FOLLOWUP.md` unless I type `AGREE` in all caps.

Constraints:

- do not add anything to `FOLLOWUP.md` yet,
- do not implement changes during this Sonnet walkthrough phase,
- use `WALKTHROUGH.md` as supplemental context only; actual code and actual diff win,
- prepare to create or update `FOLLOWUP.md`, but leave it unchanged until I explicitly approve a specific item,
- if evidence is insufficient or the review point is ambiguous, stop and ask instead of filling gaps with assumptions.

Review loop:

- let us review the PR one small change at a time,
- walk through each section of the review one by one,
- inspect the corresponding actual code and actual diff against `main`,
- show me no more than 5 lines of code at a time,
- split shown code into logical chunks,
- after each agreed addition, proceed automatically to the next review item.

Response format for each review step:

1. `Section Under Review`
2. `Code Excerpt`
3. `What The Code Does`
4. `Review Concern`
5. `Do You Agree With The Review Finding?`
6. `Exact Next Step`
7. `Waiting For Approval`

For each section:

1. Read the relevant `REVIEW.md` section.
2. Use `WALKTHROUGH.md` only as supplemental context.
3. Inspect the corresponding actual code and actual diff against `main`.
4. Show me no more than 5 lines of code at a time.
5. Make sure each shown code block is split into logical chunks.
6. Explain what the code does.
7. Explain the review concern, if any.
8. Tell me if you agree with the review finding or why you do not.
9. Discuss and propose exact next steps.
10. Wait for my explicit approval before recording any follow-up item.

“Agreed” means I must explicitly type `AGREE` in all-caps.

Do not ever add anything to the follow-up list unless we have agreed on the exact changes that need to be implemented, fleshed out to the T.

If you have questions, cannot make a decision, do not have enough context, or hit conflicts, DO NOT MAKE ASSUMPTIONS. STOP. ASK. GET CONFIRMATION. THEN PROCEED.

Once we are done reviewing, wait for my final go-ahead before implementation.

## FOLLOWUP.md rules

Create/update `FOLLOWUP.md` only with explicitly agreed items.

Also create a follow-up list markdown file to track a checklist of the changes that are necessary.

Each item must include:

- checkbox,
- exact file(s),
- exact symbol(s)/location(s),
- exact change to make,
- why we agreed to it,
- acceptance criteria,
- verification needed,
- any risks or constraints.

Do not include speculative items.

Do not include optional suggestions unless I explicitly agree.

Do not include an item just because `REVIEW.md` says it unless we inspected the code and I typed `AGREE`.
