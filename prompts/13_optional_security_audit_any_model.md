# 13 - Optional Repository Security Audit - Any Model

Run this independent phase only when I explicitly request a security audit or penetration-style review of a repository. Its number identifies the prompt; it is not a step after phase `10` and is not a prerequisite for the main workflow. Audit backend and UI repositories alike. Keep the target repository read-only and write the audit files only to an output directory outside it.

## Skills

- [security-audit](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/cloudflare__security-audit-skill/snapshot/skills/security-audit/SKILL.md), including its required companions:
  - [RECONNAISSANCE.md](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/cloudflare__security-audit-skill/snapshot/skills/security-audit/RECONNAISSANCE.md)
  - [HUNTING.md](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/cloudflare__security-audit-skill/snapshot/skills/security-audit/HUNTING.md)
  - [ATTACK-CLASSES.md](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/cloudflare__security-audit-skill/snapshot/skills/security-audit/ATTACK-CLASSES.md)
  - [VALIDATION-AND-REPORTING.md](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/cloudflare__security-audit-skill/snapshot/skills/security-audit/VALIDATION-AND-REPORTING.md)
  - [report-schema.json](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/cloudflare__security-audit-skill/snapshot/skills/security-audit/report-schema.json)
  - [validate-findings.cjs](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/cloudflare__security-audit-skill/snapshot/skills/security-audit/validate-findings.cjs)
  - [validate-coverage-ledger.cjs](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/cloudflare__security-audit-skill/snapshot/skills/security-audit/validate-coverage-ledger.cjs)
- The `security-audit` domain companions. Use one only when reconnaissance finds the trust boundary that its `When to use this file` section describes:
  - [WEB-PROTOCOL-AND-AUTH.md](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/cloudflare__security-audit-skill/snapshot/skills/security-audit/WEB-PROTOCOL-AND-AUTH.md)
  - [CLIENT-SIDE.md](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/cloudflare__security-audit-skill/snapshot/skills/security-audit/CLIENT-SIDE.md)
  - [PROTOCOLS-RPC-AND-MESSAGING.md](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/cloudflare__security-audit-skill/snapshot/skills/security-audit/PROTOCOLS-RPC-AND-MESSAGING.md)
  - [DATA-ISOLATION-AND-LIFECYCLE.md](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/cloudflare__security-audit-skill/snapshot/skills/security-audit/DATA-ISOLATION-AND-LIFECYCLE.md)
  - [RESOURCE-EXHAUSTION-AND-AVAILABILITY.md](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/cloudflare__security-audit-skill/snapshot/skills/security-audit/RESOURCE-EXHAUSTION-AND-AVAILABILITY.md)
  - [SUPPLY-CHAIN-AND-RELEASE.md](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/cloudflare__security-audit-skill/snapshot/skills/security-audit/SUPPLY-CHAIN-AND-RELEASE.md)
  - [CLOUD-AND-DEPLOYMENT.md](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/cloudflare__security-audit-skill/snapshot/skills/security-audit/CLOUD-AND-DEPLOYMENT.md)
  - [AI-AND-LLM.md](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/cloudflare__security-audit-skill/snapshot/skills/security-audit/AI-AND-LLM.md)
  - [MEMORY-SAFETY-AND-BINARY.md](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/cloudflare__security-audit-skill/snapshot/skills/security-audit/MEMORY-SAFETY-AND-BINARY.md)
  - [DESKTOP-MOBILE-AND-LOCAL-IPC.md](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/cloudflare__security-audit-skill/snapshot/skills/security-audit/DESKTOP-MOBILE-AND-LOCAL-IPC.md)
- [no-ai-slop](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/petergyang__no-ai-slop/snapshot/skills/no-ai-slop/SKILL.md), including its required [eval.md](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/petergyang__no-ai-slop/snapshot/skills/no-ai-slop/eval.md).

## Skill Handling Rule

Fetch skill procedures and their required companions only from `https://github.com/viseshrp/ai-skills-archive`. Resolve relative resource references to the explicitly linked archive copies; do not follow upstream skill URLs, install a skill package, or substitute an official-source copy. If a required archive resource is absent or unreadable, stop and report its exact missing path. Keep optional related-skill mentions and provenance links inactive unless this prompt explicitly authorizes the procedure. Target-library API and version documentation remains governed by the Engineering Contract; it is not a substitute source for skill material.

Use linked companions within this phase's scope. Skip UI-only sections for backend work, preserve the test-authoring boundary and named outputs, and do not run optional bootstrap scripts.

Use only this prompt's explicitly linked skills. Fetch and read each applicable skill and required companion completely from its GitHub URL before use. Do not depend on local skill repositories, installed slash commands, or earlier prompt text. If a required file cannot be fetched and read completely, stop and report the blocker.

The prompt is the contract. Skills are supporting procedures only. If a skill conflicts with this prompt, this prompt wins. If a conflict is material, stop and ask instead of silently choosing. Do not invoke unlisted skills or let a skill expand the phase's write permissions, outputs, or approval scope.

The linked skills come from different authors and were written for other workflows, so they can disagree with each other as well as with this prompt. No linked skill outranks another. Use this prompt and any locked or approved task artifacts to settle a disagreement between skills. Where those are silent, take the option that stays inside the approved scope and requires the smaller change; if the choice is material, stop and ask.

A skill's named tools, slash commands, sub-agents, MCP servers, hooks, modes, personas, output templates, file-saving steps, and approval, pause, or stop-turn routines apply only where this prompt adopts them. Otherwise use this prompt's method, outputs, and gates with the tools your environment provides. A skill's instruction to read a companion only in part, or only when needed, does not relax this prompt's complete-read rule.

`no-ai-slop` is mandatory for every Markdown document this phase creates or revises: `architecture.md`, `REPORT.md`, `FINDINGS-DETAIL.md`, `NEEDS-VALIDATION.md`, and the final response. Treat it as the ultimate writing guide and final authority for prose and presentation after satisfying this prompt's factual, technical, structural, and output requirements. If another skill or instruction conflicts only on writing style, `no-ai-slop` wins; this prompt and approved task artifacts still control scope, meaning, required structure, artifact names, constraints, and evidence.

Apply `no-ai-slop` while drafting and run its `eval.md` self-check before saving each Markdown artifact or sending the final response. If its `SKILL.md` or `eval.md` cannot be read and applied, stop before creating or revising Markdown and report the blocker. Ignore its draft-request, detection-mode, and mandatory `What changed` workflow unless this prompt explicitly asks for them. Do not use it to reword a block that `security-audit` requires copied verbatim into an agent prompt, a JSON record, a fingerprint, or a coverage identifier. It does not lift the 1,000-word cap on `architecture.md` or remove a section the skill requires in a report.

An explicit request for this phase selects `security-audit`'s full audit mode. Do not use its guidance mode or ask its mode question. Follow its six phases, run profiles, scoped runs, budget gate, prior-run rules, coverage ledger, candidate gate, verdict states, severity anchors, and `Universal execution safety` rules as written, inside this prompt's Engineering Contract. This prompt adopts the skill's delegated agents, hunter and verifier prompts, structured results, shared run files, per-agent `scratch/` and `artifacts/` directories, promotion procedure, and both validators. They are the only skill-owned files, sub-agents, and scripts this phase permits, and every file stays inside the output directory. Use your environment's delegation mechanism for the skill's `Task tool`, `research` agent, and `general` agent, and keep each role's write isolation and independence. A delegated agent does not see this prompt, so add the target read-only boundary and the execution safety rules of the Engineering Contract to every hunter, critic, and verifier prompt, after the parts the skill requires.

The skill reads its companions selectively; this prompt sets what the complete-read rule covers. Before reconnaissance, read `SKILL.md`, `RECONNAISSANCE.md`, `HUNTING.md`, `ATTACK-CLASSES.md`, `VALIDATION-AND-REPORTING.md`, and `report-schema.json` completely. After reconnaissance, read each domain companion's `When to use this file` section to decide whether it applies, then read every selected companion completely before copying its blocks into a hunter prompt. An unselected companion needs no further reading; record it in the ledger's `excluded_blocks` with the source fact that excludes it. The two validators are programs this phase runs, not procedures to apply. Fetch them unchanged and do not edit them.

The skill's `Skill directory` is a local path, and this prompt forbids an installed copy. Save unchanged copies of the linked archive files to `<output-dir>/skill/` and use that directory wherever the skill says `<skill-dir>`. `validate-findings.cjs` loads `report-schema.json` from its own directory, so keep them together.

The skill permits an output directory inside the target when I select one and version control ignores it. This phase does not: if I name a path inside the target repository, stop and ask for an external path. The skill's rule never to stop mid-phase does not override this prompt's stop-and-ask rules. When a stop interrupts a run that has started, first record `run_status: "incomplete"` with the exact reason in `run-metadata.json`.

The skill's harnesses, fixtures, and disposable source copies exist only in an agent's `scratch/` directory. They are local checks, not test authoring, and nothing from them enters the target repository. Its `remediation`, `code_changes`, and regression cases describe a fix for a later authorized phase; do not edit target source or write tests. Its `critical`, `high`, `medium`, `low`, and `informational` severities and its `confirmed`, `needs_validation`, and `rejected` verdicts are this phase's output. They are not phase `04`'s finding statuses or blocking levels, and no verdict or severity authorizes a fix. Where the skill's `Obvious things` class asks about known vulnerabilities in dependencies, use only advisory data already available locally or published documentation you can read without sending repository contents anywhere; otherwise record the question as `needs_validation`.

## Engineering Contract

### Scope

- Audit the requested repository at its current revision. Resolve the run profile, any scope paths, and any agent budget from my request before reconnaissance; when I name no profile, use `standard` and say so. A `quick`, scoped, budget-limited, or incomplete run is a partial pass and must say so.
- Keep the target repository read-only. Do not create, edit, delete, format, or regenerate any file in it, including a report, plan, prompt, test, fixture, ignore rule, or code comment. Do not stage, commit, push, switch branches, create or update a pull request, resolve review threads, or merge.
- Write only inside the output directory: a new directory outside the target repository, by default `~/security-audit-skill/<repo-name>/run-<N>` with the next unused `<N>`. Do not write anywhere else, including `/tmp` and other paths under the home directory. Earlier `run-<N>` directories for the same repository are prior-run input; read them and do not modify them.
- Before reconnaissance, confirm three preconditions and stop with the exact missing one if any fails: a delegation mechanism that starts an agent with a fresh context, which independent verification needs; a locally available Node.js runtime for the validators; and a writable output directory outside the target. Do not install anything to satisfy a precondition.
- Audit security only. Do not turn this into a correctness, complexity, performance, test, or visual audit. Report an incidentally discovered material issue of another kind separately in the final response with its evidence and route it to an authorized review; do not fix it here.
- Findings are evidence for human selection. Do not infer authorization to implement a fix or to overwrite an existing locked plan or `FOLLOWUP.md`.

### Execution safety

- Source inspection is read-only. Run target-controlled builds, tests, processes, browsers, emulators, fuzzers, and fixture processing only inside an OS-enforced sandbox that provides every control `security-audit` lists under `Universal execution safety`: no external network, an empty allowlisted environment, a read-only target and toolchain, writes confined to the agent's `scratch/` directory, and explicit low CPU, memory, process, file-size, disk, and wall-clock limits. If any control cannot be enforced, do not execute target code. Record the missing capability as a `needs_validation` blocker with a safe validation plan.
- Do not install dependencies or let a build fetch them. Do not contact deployed endpoints, external or shared services, registries, identity providers, cloud APIs, or live control planes. Use dummy principals, fixtures, and secrets only. Stop at the minimum local effect that establishes the defect.
- Do not copy a real secret, credential, token, or personal data value into any output file, agent prompt, or chat message. Report the file, line, and kind of value, and how to confirm it.

### Simplicity and reuse

Apply this procedure to every remediation the audit recommends, without implementing it:

- Before recommending new code, inspect relevant existing helpers, types, and patterns, then standard-library capabilities, native platform features, and already-installed dependencies. Prefer a compatible existing control when it enforces the invariant and preserves behavior and readability; name the concrete alternative.
- Trace how the repository already handles comparable behavior: component responsibilities, dependency direction, shared services, and extension points. Recommend the fix at the established control point, such as the existing authorization layer or validator, not a parallel flow, duplicate infrastructure, or a path that bypasses an existing layer. Name the established path the fix should use.
- Report duplicated, unreachable, or bypassed security controls only when they support a finding. Justify a recommended abstraction or dependency by the invariant it enforces. Whenever a remediation removes code, name the code, tests, comments, and documentation that depend on it. Preserve dependency approval and source-documentation grounding.
- Treat each mechanism a remediation would add to choose between behaviors, such as a mode, fallback, comparison, or special case, as a design decision to test, not a settled one. Check whether a path the code already requires can enforce the invariant for every case on its own. When repository evidence shows a simpler fix that meets the same requirement, recommend it with the code it would remove and its trade-off.
- For each fix, trace the relevant callers, data flow, and error flow before choosing the repair location. Before recommending a repair that adds code, check whether removing or simplifying the faulty path resolves the defect, and prefer that repair when it preserves behavior and contracts. Address the root cause; when a shared fix would alter compatibility, say so.
- Before recommending deletion, inspect direct callers, dynamic or string references, public contracts, configuration, and relevant tests. Fewer lines or files are not acceptance criteria; preserve validation, security, accessibility, error handling, and verification.
- Do not substitute a simpler interpretation for an explicit requirement or locked plan. Implementation still requires its existing authorization. Preserve existing tests and validation requirements; do not author tests in this phase or introduce production assertion demos, one-test quotas, persistent modes, debt markers, or new ledgers beyond the skill's coverage ledger in the output directory.

### Simplification limits and improvement claims

- For each recommended remediation with a material limit, report why it would enforce the invariant under current requirements, its known limit, and the evidence that would trigger revisiting it. Do not invent thresholds or weaken explicit requirements. Keep this in the finding's remediation text; do not create planning artifacts, comments, or a debt ledger.
- In reviews and handoffs, distinguish measured improvements from expectations. Claims of reduced latency, memory use, or cost require comparable before-and-after evidence identifying the baseline, changed version, workload, measurement method, and relevant environment. Without comparable evidence, label the expected improvement `unmeasured`; do not infer savings from fewer lines, an implementation never built, or unrelated benchmarks. Use existing verification facilities within the phase's permissions; this rule does not authorize new benchmark files, dependencies, or configuration changes.

### Documentation checkpoint

- For each confirmed finding, identify the durable documentation files and sections its fix would affect, along with the validation they would need, or record an evidence-based `Not applicable` decision.
- Report existing security-relevant documentation gaps that support a finding, such as a documented control the source does not enforce. Do not edit documentation or require a prior workflow artifact to run this independent audit.

### Finding bar

- A `confirmed` record names the lower-trust principal, the accepted input or action, the intended control, the crossed boundary, the affected principal or resource, and a bounded local observed result. Cite repository-relative files and lines for every trace and evidence entry.
- A missing best practice, guessed deployment behavior, generic parser crash, or self-impact is not a finding. Keep concrete non-finding observations as hardening notes.
- Use `needs_validation` only for a source-grounded boundary hypothesis blocked by a specific fact outside source or the sandboxed fixture. Name the blocker and a safe local or owner-observed check. Give it no severity.
- Ground a claim that depends on a third-party library, framework, or platform in the documentation of the installed or pinned version. When that behavior is decisive and cannot be established from source, local checks, or that documentation, use `needs_validation`.
- Only a record that a fresh, independent verifier has checked enters `findings.json`. Severity cannot exceed demonstrated impact. A clean run may confirm nothing; say so and state the coverage limits without inventing low-severity findings.

## UI work only

Enable this section only when the audit scope includes UI code. A backend service having UI consumers does not by itself enable it. For backend-only work, skip this section and its UI-specific checks and reporting.

Select `CLIENT-SIDE.md`, and the webview parts of `DESKTOP-MOBILE-AND-LOCAL-IPC.md`, only when reconnaissance finds the browser or webview trust boundary each describes. Run a local browser or emulator check only inside the required sandbox with dummy accounts. Do not judge visual taste, accessibility, or interaction quality, and do not create prototypes. No additional UI skill downloads are required for this audit.

## Prompt

Goal:
Find vulnerabilities in the requested repository that violate a real trust boundary, verify each one independently, and give me the source evidence, bounded reproduction, priority, and smallest effective fix, without changing the repository.

1. Read repository instructions. Record the current revision and any uncommitted changes without modifying them. Resolve the profile, scope, and budget, confirm the three preconditions, and create the output directory with its `skill/` copy and `run-metadata.json`.
2. Read the core skill files completely. Read every compatible prior run for this repository before planning coverage.
3. Run reconnaissance, write `architecture.md`, select the domain companions, and seed and validate `coverage-ledger.json`.
4. Run the hunting waves and coverage critics the profile and budget allow. Update and validate the ledger after every result.
5. Give every candidate to a fresh verifier, write and validate `findings.json`, and run the independent record verification.
6. Derive `REPORT.md`, `FINDINGS-DETAIL.md`, and `NEEDS-VALIDATION.md` from the final records. Run both validators a final time and set `run_status`.
7. Complete the documentation checkpoint. Verify that the target repository's files and Git state are unchanged by this phase.
8. Present the final response and stop. If I select findings for implementation, carry the exact selected findings, cited by fingerprint, into phase `01` as user-supplied context together with the paths to `findings.json` and `FINDINGS-DETAIL.md`. For an active human walkthrough, each follow-up still requires `AGREE` and the final go-ahead before phase `08`.

## Required output: the audit directory

Create these files only inside the output directory, with the names, formats, and contents `security-audit` defines:

```text
<output-dir>/
  skill/                  unchanged copies of the linked archive files
  run-metadata.json
  architecture.md
  coverage-ledger.json
  findings.json
  REPORT.md
  FINDINGS-DETAIL.md
  NEEDS-VALIDATION.md
  agents/<agent-id>/scratch/
  agents/<agent-id>/artifacts/
```

Record `Created by` and `Created at` for the run in `run-metadata.json`. `findings.json` must pass `validate-findings.cjs`, and `coverage-ledger.json` must pass `validate-coverage-ledger.cjs`. A run ends in one of two states: every file is written and both validators pass, or `run_status` is `incomplete` with its exact reason and `REPORT.md` opens with that gap. Never commit the output directory or copy it into the target repository.

## Required final response

Include:

- Run basis: revision, uncommitted changes present, profile, scope, budget and agents spent, prior runs used, and the output directory path.
- Run status: `complete` or `incomplete` with the exact reason, the result of both validators, and whether target code ran in a sandbox or the audit stayed source-only.
- Confirmed findings: for each, the fingerprint, severity, title, affected boundary, source location, one-line observed result, and smallest fix.
- Needs-validation leads: for each, the fingerprint, title, exact blocker, and the safe local or owner-observed check. Give no severity.
- Coverage: counts of covered, candidate, blocked, deferred, and out-of-scope ledger units, the final critic result, and limits on completeness. Do not claim the audit exhausts the target.
- Hardening notes and any incidentally discovered issue of another kind, kept separate from findings.
- Documentation checkpoint: affected durable files and validation needed for each confirmed finding, or evidence-based `Not applicable` decisions.
- Handoff: no change made to the target repository or its Git state; any selected finding still needs the applicable planning or human-approval path. If no finding is confirmed, say so without treating this audit as production approval.
