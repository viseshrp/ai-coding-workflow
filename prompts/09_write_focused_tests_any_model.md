# 09 - Write Minimal Focused Tests - Any Model

This final test-writing prompt is intentionally model-agnostic. Apply the same evidence, scope, test-design, verification, Git, and human-handoff contract whether the model is GPT, Claude, Gemini, or another capable repository-aware coding model. Do not rely on vendor-specific tools, hidden reasoning formats, or model-specific behavior.

## Skills

Load these skills from the sibling `../ai-skills-archive` repository:

- `python-testing`: `archives/affaan-m__ECC/snapshot/skills/python-testing/SKILL.md`
- `code-review-and-quality`: `archives/addyosmani__agent-skills/snapshot/skills/code-review-and-quality/SKILL.md`
- `source-driven-development`: `archives/addyosmani__agent-skills/snapshot/skills/source-driven-development/SKILL.md`
- `verification-before-completion`: `archives/obra__Superpowers/snapshot/skills/verification-before-completion/SKILL.md`
- `no-ai-slop`: `archives/petergyang__no-ai-slop/snapshot/SKILL.md`

## Skill Handling Rule

Before inspecting the target change or using a skill:

1. Record the target repository root so you can return to it.
2. Run `cd ../ai-skills-archive` from the target repository root.
3. Run `git pull --ff-only origin main`.
4. Read every `SKILL.md` listed above completely. Also read `archives/petergyang__no-ai-slop/snapshot/eval.md` before using `no-ai-slop`.
5. Return to the target repository root before inspecting or changing its files.

If the sibling repository is missing, the pull fails, a listed skill cannot be read completely, or the required `eval.md` cannot be read, stop and report the blocker. Do not substitute remembered or remote skill content.

Use only the local skills listed in this prompt:

- use `python-testing` for pytest structures, fixtures, parametrization, mocking, and coverage mechanics,
- use `code-review-and-quality` to review the final test diff for correctness, readability, architecture, and unnecessary complexity,
- use `source-driven-development` only when a pytest or plugin API is version-sensitive or uncertain, and verify it against authoritative documentation,
- use `verification-before-completion` to require fresh command output before any passing or completion claim,
- use `no-ai-slop` as writing guidance for every chat response and for prose in test names, comments, docstrings, and the final human handoff. Apply its editing principles and run its `eval.md` self-check internally. Ignore its draft-request, detection-mode, and mandatory `What changed` workflow unless this prompt explicitly asks for them. Preserve code meaning, technical detail, and the required handoff.

The prompt is the contract. Locked task artifacts are the contract for expected behavior. Skills are supporting procedures only.

If a skill conflicts with this prompt, this prompt wins. In particular:

- use this prompt's minimum of 85% coverage for new or changed lines instead of another skill's generic coverage target,
- do not apply a skill's production-code TDD cycle because this phase may change tests only and the implementation already exists,
- prefer existing pytest fixtures and plugin APIs over `unittest`, `unittest.mock`, `tempfile`, or other Python/standard-library substitutes when the repository already provides the pytest-native option,
- interpret the verification skill's "full command" as the complete focused command needed to prove the stated claim, not authorization to run the entire repository suite,
- use authoritative documentation to verify uncertain APIs, but do not add source-citation comments to tests unless that is already a repository convention,
- do not add more tests, edge cases, dependencies, plugins, or infrastructure merely because a skill recommends them.

If a conflict is material, stop and ask instead of silently choosing.

Do not use a skill to expand scope, change production architecture, add unrelated refactors, or add more tests than this prompt justifies.

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

### Minimum test set

- Write the fewest tests that provide meaningful confidence.
- Zero new tests is valid only when existing tests already cover every changed behavior and material regression risk and fresh evidence shows at least 85% coverage for new or changed lines.
- Before editing, identify the smallest set of distinct behaviors that need coverage and explain why each proposed test is necessary.
- Extend an existing test when that remains clear and preserves one behavior per test. Do not create a parallel test for behavior already covered.
- Use parametrization only for meaningful variants of the same behavior. Do not combine unrelated behaviors to reduce the test count.
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

### Pytest-native APIs

- Inspect the repository's pytest configuration, existing fixtures, plugins, and test conventions before writing tests.
- Reuse existing project fixtures and helpers when they fit.
- Prefer pytest-native APIs and already-installed plugin fixtures over hand-rolled Python or standard-library mechanisms.
- Prefer:
  - fixtures over manual setup/teardown or `unittest.TestCase` lifecycle methods,
  - `monkeypatch` over directly mutating environment variables, module globals, attributes, dictionaries, or the working directory,
  - `tmp_path` over `tempfile` or manually managed temporary paths,
  - `capsys` or `capfd` over manual stdout/stderr redirection,
  - `caplog` over custom logging handlers,
  - `pytest.raises` and `pytest.warns` over manual `try`/`except` or warning-capture code,
  - `pytest.mark.parametrize` over duplicated tests for variants of one behavior,
  - the repository's existing mock fixture, such as `mocker`, when already installed and appropriate.
- Never monkeypatch, patch, or mock the function, method, or callable under test. Replacing the behavior the test is supposed to exercise defeats the purpose of the test. Patch only collaborators outside the subject under test, at the lookup boundary used by that subject.
- If no existing pytest or plugin API covers the need, prefer a small test-local fake over elaborate standard-library machinery.
- Do not install `pytest-mock` or another plugin. If a new dependency or unavoidable standard-library workaround would be required, stop and ask.
- Use mocks only at external, slow, nondeterministic, or otherwise impractical boundaries. Do not mock the unit's own implementation details or assert incidental call choreography.

### Brittleness and isolation

- Do not leave process-global state mutated.
- Do not depend on private constants or private helper methods.
- Do not assert exact error wording unless that wording is an intentional user-facing contract.
- Do not encode packaging or filesystem-layout assumptions that are not part of the public contract.
- Do not mirror production logic inside the expected-value calculation.
- Do not use real time, sleeps, network access, uncontrolled randomness, or machine-specific state.
- When an existing relevant test has one of these problems, do not refactor unrelated test code. Report it as a flake risk, acceptable contract test, or maintainability concern and suggest a behavior-level alternative.

### Coverage and verification

- Use the repository's existing pytest and coverage commands and configuration.
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
- Stage only intended test files and test-local support code.
- Do not stage or commit workflow-generated Markdown artifacts, including `DRAFT_PLAN.md`, `INITIAL_OPUS_PLANNING_PROMPT.md`, `FEATURE_SPEC_AND_PLAN.md`, `GPT_EXECUTION_PROMPT.md`, `PLAN_CRITIQUE.md`, `OPUS_PLAN_REVISION_REQUEST.md`, `PLAN_REVISION_SUMMARY.md`, `PLAN_REVISION_VERIFICATION.md`, `REVIEW.md`, `WALKTHROUGH.md`, `GPT_REVIEW_FIX_PROMPT.md`, `REVIEW_FIX_VERIFICATION.md`, and `FOLLOWUP.md`, unless I explicitly ask.
- When test changes are needed, create one focused test commit unless separate logical test groups clearly justify more.
- If fresh evidence proves that zero test changes are needed, do not create an empty commit.
- Use a detailed commit message and description.
- Push the current branch after committing.
- Check whether a pull request already exists for the current branch.
- Create a pull request if and only if one does not already exist. Use GitHub CLI (`gh`) as the fallback for checking.
- Never create a duplicate pull request.
- After the tests are verified and Git handling is complete, stop and hand the test diff to the human reviewer. Do not generate a downstream artifact or prompt.

## Prompt

Role:

- You are a capable repository-aware coding model performing the final focused test-writing phase for an existing implementation.
- Reason from repository evidence before editing.
- Optimize for confidence per test, not test count or raw coverage.

Goal:

- add the smallest meaningful pytest test set for the behavior changed on the current branch,
- demonstrate at least 85% coverage for new or changed lines,
- leave the branch with focused passing verification and no unrelated changes,
- hand only the resulting test-file changes to the human for final review.

Context to read before acting:

- repository instructions such as `AGENTS.md`,
- the current branch diff against the head of `main`,
- changed production code and its callers,
- existing relevant tests, fixtures, helpers, pytest configuration, coverage configuration, and installed test plugins,
- `FEATURE_SPEC_AND_PLAN.md`, if present,
- `FOLLOWUP.md`, if present,
- relevant public documentation or source for pytest/plugin APIs when their use is uncertain.

Success criteria:

- every new or changed test protects a distinct changed behavior or material regression risk,
- no existing coverage is duplicated,
- tests stay behavior-focused, small, readable, deterministic, and isolated,
- pytest-native or existing plugin APIs replace hand-rolled Python/standard-library mechanisms where available,
- fresh evidence shows the focused tests pass,
- fresh evidence shows at least 85% coverage for new or changed lines,
- no production or configuration files are changed,
- no prompt, plan, review, walkthrough, summary, or workflow artifact is created or updated, and no generated coverage output remains in the repository,
- any intended test changes are committed and pushed, and a pull request is created only if missing,
- the verified test diff is ready for direct human review with no later AI phase.

Working method:

1. Inspect the branch diff, repository instructions, test layout, relevant source, existing tests, fixtures, pytest configuration, coverage configuration, and installed plugins.
2. Trace each changed observable behavior through its public entry point and important failure or boundary paths.
3. Build a compact behavior-to-test matrix containing:
   - changed behavior or regression risk,
   - existing test coverage,
   - proposed test, if still needed,
   - why that test is necessary.
4. Reduce the proposal to the minimum set. Prefer zero or one high-value test over several overlapping tests when the same confidence is preserved.
5. Implement the tests using existing conventions and pytest-native APIs.
6. Run the smallest relevant tests and focused coverage measurement.
7. Add or adjust a test only for a demonstrated behavior or coverage gap; do not chase line execution blindly.
8. Review the finished tests for duplication, brittleness, excessive mocking, hidden global-state changes, oversized functions, and implementation coupling.
9. Run focused test-file lint/static checks when available.
10. If tests changed, review the diff, stage only intended test files, commit, push, and create a pull request only if the branch has none. If no test change is justified, do not create an empty commit.
11. Remove only the temporary coverage output generated by this phase; do not delete pre-existing repository files. Then stop after a concise chat handoff to the human reviewer. Do not create another prompt, review artifact, walkthrough, plan, summary file, or workflow phase.

Stop rules:

- Stop and ask if expected behavior is ambiguous or conflicts with code, plans, or follow-up decisions.
- Stop and ask if meaningful testing requires a production-code, dependency, plugin, build, or configuration change.
- Stop and ask if the repository does not use pytest.
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
- any blocker or existing-test concern that was deliberately left unchanged.

End with: `Tests are ready for human review.`

Do not generate another prompt or suggest an automated follow-up phase. Do not claim changed-line coverage when only broader file/package coverage was measured.
