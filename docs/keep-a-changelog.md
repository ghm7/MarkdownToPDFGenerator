# Keep a Changelog

## Purpose

We maintain a human-readable changelog so engineers and stakeholders can quickly understand what changed in each release.

The changelog is not a dump of all commits.
It is a curated summary of notable changes.

Main file:

- `CHANGELOG.md`

---

## Standard sections

We use these sections when relevant:

- `Added`
- `Changed`
- `Fixed`
- `Removed`
- `Deprecated`
- `Security`

---

## Format

Each release should look like this:

```md
## [1.2.0] - 2026-03-29

### Added

- Support for rendering markdown tables into PDF
- New public API for generating PDFs from raw markdown strings

### Changed

- Improved default CSS for headings and code blocks

### Fixed

- Fixed page overflow issue in fenced code blocks
```

---

# Unreleased section

Always keep an `Unreleased` section at the top.

Example:

```md
# Changelog

## [Unreleased]

### Added

- Support for ordered lists in PDF output

### Fixed

- Fixed image alignment issue in generated PDFs
```

When releasing:

- move items from `Unreleased` to the new version section
- add the release date
- create a new empty `Unreleased` section

## Example for this project

```md
# Changelog

## [Unreleased]

### Added

- Added support for PDF generation from markdown strings

### Fixed

- Fixed XHTML conversion issue for nested lists

## [1.0.0] - 2026-03-29

### Added

- Initial release of the Markdown to PDF generator
- Support for headings, paragraphs, lists, blockquotes, code blocks, links, and tables
- Default PDF stylesheet
- Integration tests for sample markdown fixtures
```

# Writing guidelines

Good changelog entries are:

- short
- specific
- focused on user impact

Good:

- Added support for markdown tables in generated PDFs

Bad:

- Refactored code
- Updated stuff
- Fixed issue

# Team convention

- Update `CHANGELOG.md` in the sme PR when the change is notable
- Small internal refactors do not always need an entry
- User-visible changes should almost always be added
- Breaking changes must always be documented clearly

# Checklist before release

- `Unreleased` entries reviewed
- Version chosen correctly
- Date added
- Notable breaking changes called out clearly
