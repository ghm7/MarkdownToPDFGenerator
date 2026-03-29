# Branching Convention

## Purpose

We use a simple branch naming convention so the repository stays easy to understand and navigate.

This project follows a lightweight branching model:

- `main` is always the primary branch
- work is done in short-lived feature branches
- changes are merged through pull requests

---

## Main rules

1. Do not commit directly to `main`
2. Create a branch for each piece of work
3. Keep branches focused on a single goal
4. Prefer small branches and small PRs
5. Delete branches after merge when possible

---

## Branch naming format

Use:

`<type>/<short-description>`

Examples:

- `feature/pdf-render-service`
- `feature/support-markdown-tables`
- `fix/code-block-overflow`
- `fix/null-input-validation`
- `docs/add-prd`
- `docs/update-conventions`
- `chore/update-dependencies`
- `test/add-integration-fixtures`
- `refactor/simplify-template-service`

---

## Allowed branch types

### feature

Use for new functionality.

Examples:

- `feature/markdown-renderer`
- `feature/add-image-support`

### fix

Use for bug fixes.

Examples:

- `fix/xhtml-normalization`
- `fix/pdf-output-path-validation`

### docs

Use for documentation changes.

Examples:

- `docs/add-adr-template`
- `docs/update-readme`

### test

Use for test-only changes.

Examples:

- `test/add-fixture-coverage`
- `test/improve-integration-tests`

### chore

Use for maintenance work.

Examples:

- `chore/update-libraries`
- `chore/configure-ci`

### refactor

Use for internal structure changes with no intended functional change.

Examples:

- `refactor/split-render-services`
- `refactor/rename-config-classes`

---

## Naming rules

- use lowercase letters
- use hyphens instead of spaces
- keep names short but descriptive
- do not use vague names like:
  - `feature/stuff`
  - `fix/bug`
  - `test/changes`

Good:

- `fix/table-border-rendering`

Bad:

- `fix/pdf`
- `feature/new`
- `branch1`

---

## Example workflow

```bash
git checkout main
git pull origin main
git checkout -b feature/pdf-render-service
```
