# AGENTS.md

## Project Goal

Build a small but polished MVP with clear product value, clean structure, and a reliable core flow.

## Must Read Before Coding

Before coding, read the relevant project docs:

- `docs/PRD.md`
- `docs/DESIGN.md`
- `docs/ARCHITECTURE.md`
- `docs/TODO.md`

## Development Rules

- Work on one clear task at a time.
- Do not rewrite unrelated files.
- Do not introduce large dependencies without a clear reason.
- Do not change product scope without updating `docs/PRD.md`.
- Do not change architecture without updating `docs/ARCHITECTURE.md`.
- Keep implementation simple and readable; avoid over-engineering.
- Treat implementation and verification as part of the same task.

## Git Rules

- If the project is not yet a Git repository, initialize Git during project bootstrap.
- Maintain an appropriate `.gitignore`.
- Never commit secrets, API keys, tokens, credentials, or local environment files.
- Create a local commit after each independent task is completed and relevant verification passes.
- Keep commits small, coherent, and easy to roll back.
- Use concise commit messages that describe the core change, for example:
  - `feat: add portfolio import flow`
  - `fix: handle invalid stock symbols`
  - `test: add regression coverage`
  - `docs: update product scope`
- Local commits do not require user confirmation.
- Never push, force-push, merge, publish, or otherwise modify the remote repository without explicit user confirmation.
- Never run destructive Git commands such as `git reset --hard` or `git push --force` unless explicitly authorized.

## Verification Rules

- Every completed task must be verified before it is considered done.
- Decide whether tests need to be added or updated based on the nature and risk of the change.
- Choose verification methods based on the project and the change; do not use tests for their own sake.
- Appropriate verification may include:
  - lint / typecheck / build
  - unit / integration / regression tests
  - runtime checks
  - exercising the actual user flow
  - Browser / Computer Use / Simulator or other available tools when useful
- UI or workflow changes should be exercised through the actual user flow when practical.
- An independent QA Sub Agent may be used for complex or high-risk tasks, but is not required for every task.
- When using a QA Agent, prefer read-only review and verification; let the main implementation Agent make the fixes.
- Do not claim completion while relevant verification is failing.

## Commands

Update these commands to match the actual project.

```bash
npm install
npm run dev
npm run lint
npm run build
npm test
```

## Definition of Done

A task is done only when:

- The implementation matches the intended requirement.
- Necessary tests have been added or updated when appropriate.
- Relevant verification passes.
- There are no known blocking issues or obvious runtime errors.
- The diff has been reviewed for unrelated or risky changes.
- A clear, rollback-friendly local Git commit has been created.

Human acceptance remains the final check for product quality, UX, and whether the result is actually desirable.
