# Semantic Versioning

## Purpose

We use Semantic Versioning (SemVer) to communicate the impact of a release clearly.

Version format:

`MAJOR.MINOR.PATCH`

Example:

`1.4.2`

---

## Rules

### MAJOR

Increase the **major** version when we make a breaking change.

A breaking change is any change that can force consumers of this module to modify their code.

Examples:

- rename a public class or method
- remove a public method
- change method parameters in a non-compatible way
- change return types in a breaking way
- change default behavior in a way that breaks existing usage

Example:

- `1.4.2` → `2.0.0`

---

### MINOR

Increase the **minor** version when we add functionality in a backward-compatible way.

Examples:

- add a new public method without breaking existing ones
- add support for a new markdown feature
- add new configuration options that do not change existing behavior

Example:

- `1.4.2` → `1.5.0`

---

### PATCH

Increase the **patch** version when we make backward-compatible fixes.

Examples:

- fix a table rendering bug
- fix an exception message
- improve logging
- fix CSS issues without changing public API behavior

Example:

- `1.4.2` → `1.4.3`

---

## Examples for this project

### Patch example

Current version: `1.0.2`

Change:

- fix bug where code blocks overflow the page

Next version:

- `1.0.3`

---

### Minor example

Current version: `1.0.2`

Change:

- add support for blockquotes and images in the PDF output

Next version:

- `1.1.0`

---

### Major example

Current version: `1.0.2`

Change:

- replace `generateFromFile(Path input, Path output)` with a new API that requires a config object and removes the old method

Next version:

- `2.0.0`

---

## Release guidance

### Use PATCH when

- behavior is corrected
- no integration changes are required by consumers

### Use MINOR when

- new features are added
- old integrations continue to work

### Use MAJOR when

- consumers need to change their code
- existing behavior changes in a breaking way

---

## Team convention

When preparing a release:

1. Review all merged changes since the last release
2. Determine if any are breaking
3. Choose the correct SemVer bump
4. Update `CHANGELOG.md`
5. Create the release tag

---

## Notes

- Do not bump MAJOR unless there is a real breaking change
- Do not hide breaking changes inside MINOR or PATCH releases
- When unsure, discuss in the PR before release
