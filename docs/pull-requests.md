# Pull Request Convention

## Purpose

We use pull requests to review code, share knowledge, and maintain quality.

A pull request should explain:

- what changed
- why it changed
- how it was tested
- any risks or follow-up work

---

## Main rules

1. Every change goes through a PR
2. PRs should be small and focused
3. PR titles should be clear
4. PR descriptions should be complete
5. At least one reviewer should understand the change before merge

---

## PR title convention

Prefer a concise title based on the main change.

Examples:

- `Add PDF rendering service`
- `Fix fenced code block overflow in generated PDFs`
- `Add integration tests for markdown fixtures`

---

## PR description template

Recommended template:

```md
## Summary

Describe what changed.

## Why

Explain the reason for the change.

## Scope

Describe what is included and what is intentionally not included.

## Testing

- [ ] Unit tests added or updated
- [ ] Integration tests added or updated
- [ ] Manual verification completed

## Risks

List known limitations, risks, or follow-up work.

## Notes

Any extra context for reviewers.
```

## Example PR description

```md
## Summary

Add the first version of the PDF rendering service using OpenHTMLtoPDF.

## Why

We need a reusable service that converts rendered HTML into a PDF output file.

## Scope

Included:

- PDF rendering service
- output file handling
- exception wrapping

Not included:

- custom header/footer support
- font customization

## Testing

- [x] Unit tests added
- [x] Integration test added for sample HTML input
- [x] Manual verification completed

## Risks

- CSS support remains limited to the renderer capabilities
- image loading behavior will be refined in a later PR
```
