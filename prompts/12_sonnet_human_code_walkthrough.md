# 12 — Sonnet Human Code Walkthrough + FOLLOWUP.md Creation

Use this with Claude Sonnet when I enter the loop for final human review. This is not the AI review/fix loop. This is the human walkthrough phase.

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

Look at the code review document: `REVIEW.md`.

Let me know if you agree with all points or why you do not.

There is also a `WALKTHROUGH.md` document that we will use as a detailed supplement for the review.

Our first goal is to use `REVIEW.md` and `WALKTHROUGH.md` as supplements for our own review and review the changes in the PR, basically the diff of this branch against the main branch.

Let us review the PR one small change at a time.

Also create a follow-up list markdown file to track a checklist of the changes that are necessary.

Do not add anything yet.

Walk through each section of the review one by one.

For each section:

1. Read the relevant `REVIEW.md` section.
2. Use `WALKTHROUGH.md` only as supplemental context.
3. Inspect the corresponding actual code and actual diff against main.
4. Show me no more than 5 lines of code at a time.
5. Make sure each shown code block is split into logical chunks.
6. Explain what the code does.
7. Explain the review concern, if any.
8. Tell me if you agree with the review finding or why you do not.
9. Discuss and propose exact next steps.
10. Wait for my explicit approval before recording any follow-up item.

“Agreed” means I must explicitly type `AGREE` in all-caps.

Do not ever add anything to the follow-up list unless we have agreed on the exact changes that need to be implemented, fleshed out to the T.

After each agreed addition, proceed automatically to the next review item.

If you have questions, cannot make a decision, do not have enough context, or hit conflicts, DO NOT MAKE ASSUMPTIONS. STOP. ASK. GET CONFIRMATION. THEN PROCEED.

Once we are done reviewing, wait for my final go-ahead before implementation.

Do not implement changes during this Sonnet walkthrough phase.

## FOLLOWUP.md rules

Create/update `FOLLOWUP.md` only with explicitly agreed items.

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
