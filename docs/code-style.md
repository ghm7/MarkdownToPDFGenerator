# Prettier Convention

## Purpose

We use Prettier to reduce formatting discussions and keep files consistent across the team.

Prettier is the source of truth for formatting in supported file types.

---

## Why we use it

Benefits:

- fewer formatting arguments in code reviews
- smaller and cleaner diffs
- more focus on logic and architecture
- easier onboarding for junior developers

---

## Scope

We use Prettier for files such as:

- Markdown (`.md`)
- JSON (`.json`)
- YAML (`.yml`, `.yaml`)
- HTML (`.html`)
- CSS (`.css`)
- JavaScript / TypeScript if present in tooling or examples

---

## Team rules

1. Run Prettier before opening a PR
2. Do not manually fight Prettier formatting
3. If formatting changes are large, separate them from logic changes when possible
4. Prefer automatic formatting in the editor

---

## Installation

## [See the documentation in this repo](https://github.com/jhipster/prettier-java)

## Example `.prettierrc`

Create this file in the repository root:

```json
{
  "printWidth": 80,
  "tabWidth": 2,
  "useTabs": false,
  "semi": true,
  "singleQuote": false,
  "trailingComma": "es5",
  "proseWrap": "preserve"
}
```

## Example `package.json` scripts

```json
{
  "scripts": {
    "format": "prettier . --write",
    "format:check": "prettier . --check"
  },
  ...
}
```

## Recommended usage

```bash
npm run format
```

```bash
npm run format:check
```

## Example workflow

Before committing:

```bash
npm install
npm run format
git add .
git commit -m "docs(conventions): add prettier convention"
```
