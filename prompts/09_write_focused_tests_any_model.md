# 09 - Write Minimal Focused Tests - Any Model

Use any capable repository-aware coding model and the target repository's language/framework. Do not rely on vendor-specific tools, hidden reasoning formats, or model-specific behavior. Apply language-specific guidance only where labeled.

## Skills

The GitHub links identify every skill; load their matching paths from the sibling `../ai-skills-archive` repository using the procedure below.

### Shared

- [code-review-and-quality](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/code-review-and-quality/SKILL.md)
- [source-driven-development](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/addyosmani__agent-skills/snapshot/skills/source-driven-development/SKILL.md)
- [verification-before-completion](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/obra__Superpowers/snapshot/skills/verification-before-completion/SKILL.md)
- [no-ai-slop](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/petergyang__no-ai-slop/snapshot/skills/no-ai-slop/SKILL.md)
- Required [no-ai-slop evaluator](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/petergyang__no-ai-slop/snapshot/skills/no-ai-slop/eval.md)

### Python / pytest

- [python-testing](https://github.com/viseshrp/ai-skills-archive/blob/main/archives/affaan-m__ECC/snapshot/skills/python-testing/SKILL.md)

### Other languages

- No language-specific archive skill is prescribed. Use the shared skills and the repository's established test tooling; do not substitute Python or pytest guidance.

## Skill Handling Rule

Before inspecting the target change in detail or using a skill:

1. Record the target repository root so you can return to it, and use only repository metadata or changed file paths to identify applicable language categories.
2. Run `cd ../ai-skills-archive` from the target repository root.
3. Run `git pull --ff-only origin main`.
4. Read every Shared and applicable language-specific `SKILL.md` completely, plus the required `no-ai-slop/eval.md` and companion resources. For each GitHub link, its path after `/blob/main/` is the path inside the sibling checkout; resolve relative resources from the skill directory.
5. Return to the target repository root before inspecting or changing its files.

If the sibling repository is missing, the pull fails, a required skill cannot be read completely, or the required `eval.md` cannot be read, stop and report the blocker. Do not substitute remembered or remote skill content.

Use only the listed local skills and required companions. Reuse them after reading; do not infer their content from names. This prompt controls scope, technical meaning, constraints, and outputs; locked artifacts define expected behavior. Stop and ask about unresolved material conflicts. Skills cannot expand scope, alter production architecture, add unrelated refactors, or justify extra tests/dependencies/infrastructure.

Use `code-review-and-quality` to assess the final test diff; `source-driven-development` for uncertain or version-sensitive test/coverage APIs; and `verification-before-completion` for fresh evidence. Use `python-testing` only for Python with pytest. Read authoritative version-matched docs for uncertain APIs, but add source-citation comments only if repository conventions require them.

Apply `no-ai-slop` while drafting as the hard requirement and ultimate prose/presentation guide for chat, test names/comments/docstrings, and the final handoff. It wins over conflicting writing-style guidance. Run `eval.md` before sending the handoff. Preserve technical meaning, required structure, scope, and evidence; ignore its draft-request, detection-mode, and mandatory `What changed` workflows. No Markdown artifact may be created or revised in this phase.

This prompt overrides a skill's generic coverage target with at least 85% coverage for new or changed lines, forbids its production-code TDD cycle, and prefers repository fixtures/native APIs/installed extensions over hand-rolled infrastructure. The verification skill's "full command" means the complete focused command proving the claim, not the entire suite.

## Engineering Contract

### Scope

- This phase is explicit authorization to create or update tests for the behavior changed on the current branch.
- Test files, test-local fixtures, and test-local helpers are the only repository files this phase may create or modify.
- Compare the current branch with the head of `main` and test only changed behavior and material regression risks.
- Treat actual code and observable contracts as authoritative. Use planning and follow-up artifacts as context, not as substitutes for inspecting code.
- Do not change production code, public APIs, documentation, dependency files, build files, test configuration, or coverage configuration.
- Do not create or update a test plan, review, walkthrough, summary file, generated prompt, or any other workflow artifact. Coverage tools may create temporary output while running, but do not retain, stage, or commit that output.
- Do not produce a prompt for another model, restart an AI review loop, or define another workflow phase.
- Do not add or upgrade a dependency, plugin, or test framework.
- Preserve backwards compatibility.
- Stop and ask when expected behavior, scope, or repository reality conflicts with the task artifacts or user instructions.
- Do not make assumptions to force a test to pass.
- The resulting test diff will be reviewed directly by a human. That human review ends the workflow.

### Documentation checkpoint

- Before test work, verify that every material changed behavior already has a documentation-checkpoint result from an earlier phase: exact durable documentation updated and validated, or an evidence-based `Not applicable` decision.
- Inspect the changed behavior and the relevant durable documentation closely enough to validate that result; do not treat code comments, commit messages, or workflow artifacts as substitutes.
- This phase may not edit documentation. If a required durable documentation update is missing, inaccurate, unvalidated, or lacks an evidence-based `Not applicable` decision, stop and ask for it to be resolved in an authorized implementation or follow-up stage before continuing.
- State the documentation-checkpoint status in the final human-review handoff.

### Minimum test set

- Write the fewest tests that provide meaningful confidence.
- Zero new tests is valid only when existing tests already cover every changed behavior and material regression risk and fresh evidence shows at least 85% coverage for new or changed lines.
- Before editing, identify the smallest set of distinct behaviors that need coverage and explain why each proposed test is necessary.
- Extend an existing test when that remains clear and preserves one behavior per test. Do not create a parallel test for behavior already covered.
- Use the repository's native parameterization mechanism only for meaningful variants of the same behavior. Do not combine unrelated behaviors to reduce the test count.
- Do not add tests solely to execute lines or inflate coverage.

### Test design

- Keep test code in test files or test directories, separate from production code.
- Test observable architecture and behavior, not implementation details.
- Each test must cover one behavior and have one clear reason to fail.
- Keep test functions, fixtures, and helpers small, linear, and easy to read and reason about.
- Prefer a simple Arrange-Act-Assert flow and descriptive behavior-based names.
- Extract repeated setup into a fixture or small helper only when doing so makes the tests easier to understand.
- Tests must be meaningful, non-duplicative, deterministic, non-flaky, and independent of execution order.
- Cover the important success path, failure behavior, boundary condition, or regression risk only when each is materially distinct.
- Assert the smallest stable public result that proves the behavior.

### Test-framework conventions

- Inspect the languages relevant to the changed behavior, the repository's existing test-runner and framework configuration, fixtures or helpers, extensions, and test conventions before writing tests.
- Reuse existing project fixtures and helpers when they fit.
- Prefer the repository's native test-framework APIs and already-installed extensions over hand-rolled test infrastructure.
- Never patch or mock the function, method, or callable under test. Replacing the behavior the test is supposed to exercise defeats the purpose of the test. Patch only collaborators outside the subject, at the lookup boundary used by that subject.
- If no existing test-framework API covers the need, prefer a small test-local fake over elaborate custom harnesses.
- Do not install a test dependency or extension. If a new dependency or unavoidable framework workaround would be required, stop and ask.
- Use mocks only at external, slow, nondeterministic, or otherwise impractical boundaries. Do not mock the unit's own implementation details or assert incidental call choreography.

### Language-specific testing guidance

#### Python / pytest

- When the changed code and relevant tests use Python with pytest, inspect the repository's pytest configuration, existing fixtures, plugins, and test conventions before writing tests.
- Treat the following as hard requirements for added or changed Python test code:
  - Every parameter, including `*args` and `**kwargs`, and return value of a function or method must have an explicit, accurate type hint. Treat `self` and `cls` as implicit; do not annotate them solely for this requirement.
  - Every class variable, class attribute, instance attribute, and module-level mutable or optional state must have an explicit, accurate type hint. A trivial immutable module constant may remain inferred unless the configured type checker needs an annotation.
  - Declare instance-attribute types at class scope where feasible. Do not type annotate local variables or add `self.attribute: Type` annotations inside function or method bodies unless a real configured type-checker error requires one.
  - Keep required annotations simple and accurate. Do not add advanced type constructs or type-only refactors unless the configured type checker requires them.
- Prefer:
  - fixtures over manual setup/teardown or `unittest.TestCase` lifecycle methods,
  - `monkeypatch` over directly mutating environment variables, module globals, attributes, dictionaries, or the working directory,
  - `tmp_path` over `tempfile` or manually managed temporary paths,
  - `capsys` or `capfd` over manual stdout/stderr redirection,
  - `caplog` over custom logging handlers,
  - `pytest.raises` and `pytest.warns` over manual `try`/`except` or warning-capture code,
  - `pytest.mark.parametrize` over duplicated tests for variants of one behavior,
  - the repository's existing mock fixture, such as `mocker`, when already installed and appropriate.
- If no existing pytest or plugin API covers the need, prefer a small test-local fake over elaborate Python standard-library machinery.
- Do not install `pytest-mock` or another plugin. If a new dependency or unavoidable standard-library workaround would be required, stop and ask.

#### Other languages and non-pytest Python projects

- Follow the repository's established test runner, framework conventions, and installed extensions. Do not introduce or migrate a test framework during this phase.

### Brittleness and isolation

- Do not leave process-global state mutated.
- Do not depend on private constants or private helper methods.
- Do not assert exact error wording unless that wording is an intentional user-facing contract.
- Do not encode packaging or filesystem-layout assumptions that are not part of the public contract.
- Do not mirror production logic inside the expected-value calculation.
- Do not use real time, sleeps, network access, uncontrolled randomness, or machine-specific state.
- When an existing relevant test has one of these problems, do not refactor unrelated test code. Report it as a flake risk, acceptable contract test, or maintainability concern and suggest a behavior-level alternative.

### Coverage and verification

- Use the repository's existing test and coverage commands and configuration.
- Reach at least 85% coverage for new or changed lines.
- Measure changed-line coverage directly when existing tooling supports it. Otherwise report the closest focused coverage measurement available and its limitation; do not present it as changed-line coverage.
- Do not weaken exclusions, omit relevant files, or alter coverage configuration to reach the threshold.
- Run the smallest relevant test selection first.
- Do not manually run the entire test suite unless explicitly asked.
- Run any focused lint or static checks that apply to changed test files.
- If a command fails, include the exact command and exact error output. Do not paraphrase logs.
- Do not claim completion without fresh passing test and coverage evidence.

### Git

- Review the final diff before staging.
- Stage only intended test files and test-local support code with `git add`.
- Do not stage or commit workflow-generated Markdown artifacts, including `DRAFT_PLAN.md`, `INITIAL_OPUS_PLANNING_PROMPT.md`, `FEATURE_SPEC_AND_PLAN.md`, `EXECUTION_PROMPT.md`, `PLAN_CRITIQUE.md`, `OPUS_PLAN_REVISION_REQUEST.md`, `PLAN_REVISION_SUMMARY.md`, `PLAN_REVISION_VERIFICATION.md`, `REVIEW.md`, `WALKTHROUGH.md`, `REVIEW_FIX_PROMPT.md`, `REVIEW_FIX_VERIFICATION.md`, and `FOLLOWUP.md`, unless I explicitly ask.
- When test changes are needed, create one focused test commit unless separate logical test groups clearly justify more.
- If fresh evidence proves that zero test changes are needed, do not create an empty commit.
- Use a detailed commit message and description.
- Push the current branch after committing and verify the remote status.
- Check whether a pull request already exists for the current branch.
- Create a pull request if and only if one does not already exist. Use GitHub CLI (`gh`) as the fallback for checking.
- Never create a duplicate pull request.
- After the tests are verified and Git handling is complete, stop and hand the test diff to the human reviewer. Do not generate a downstream artifact or prompt.

## Prompt

Write the smallest meaningful test set for the final branch's changed behavior and material regression risks. Require fresh passing focused tests and at least 85% changed-line coverage, then hand the test diff directly to a human. Follow all Engineering Contract gates above.

1. After skill loading, read repository instructions, the branch diff against `main`, changed code/callers, relevant tests/fixtures/helpers, test and coverage configuration, installed extensions, affected durable documentation and its validation, and available `FEATURE_SPEC_AND_PLAN.md` / `FOLLOWUP.md`. Verify the prior documentation checkpoint before editing. Batch independent reads when useful.
2. Trace changed observable behavior through public entry points and important failure/boundary paths. In chat, make a compact behavior-to-test matrix: behavior/risk, existing coverage, proposed test if needed, and why. Reduce it to the minimum distinct set, including zero tests when fresh evidence justifies that.
3. Implement using existing conventions and native test-framework APIs. Run the smallest relevant tests, focused coverage, and applicable test-file lint/static checks. Adjust tests only for demonstrated behavior or coverage gaps; repeat/broaden verification only for changes, failures, or unresolved risks.
4. Review the final diff for duplication, brittleness, subject-under-test mocking, global-state mutation, large helpers, and implementation coupling. Remove only temporary coverage output created by this phase, preserving pre-existing files. Stage only intended tests, commit, push, and create a PR only if missing; no empty commit when no edits are needed.
5. Give the concise chat handoff below. Create no prompt, plan, review, walkthrough, summary file, or other workflow artifact. Human review of the tests ends the workflow.

Stop rules:

- Stop and ask if expected behavior is ambiguous or conflicts with code, plans, or follow-up decisions.
- Stop and ask if any material changed behavior lacks a complete documentation checkpoint; do not edit documentation in this test-only phase or silently waive the requirement.
- Stop and ask if meaningful testing requires a production-code, dependency, plugin, build, or configuration change.
- Stop and ask if the repository has no established test runner or framework that can exercise the changed behavior without adding dependencies.
- Stop and ask if unrelated baseline failures prevent reliable focused verification.
- Stop and ask if the 85% changed-line requirement cannot be measured or met without weakening the test or coverage configuration.
- Otherwise, continue through implementation, focused verification, commit, push, and pull-request handling without waiting for step-by-step approval.

## Final human-review handoff

The repository output of this phase is the test diff only.

Do not write the handoff to a file. In the final chat response, state concisely:

- which test files changed,
- why this is the minimum test set,
- the exact focused test and coverage commands with their results,
- the commit, push, and pull-request status,
- the documentation-checkpoint status for the changed behavior, including any reason work was escalated rather than edited here,
- any blocker or existing-test concern that was deliberately left unchanged.

After all required verification and Git handling succeed, end with: `Tests are ready for human review.` If blocked, state the blocker and do not claim readiness.

Do not generate another prompt or suggest an automated follow-up phase. Do not claim changed-line coverage when only broader file/package coverage was measured.
