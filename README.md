# PDF - Markdown to PDF Generator for Java 17

## Document Information

**Product Name:** Markdown PDF Generator
**Project Type:** Backend library / service feature
**Target Platform:** Java 17 application
**Document Owner:** Gabriel Pozzi
**Version:** 1.0

# 1. Overview

## 1.1 Purpose

Build an app that generates PDF documents from Markdown files in a Java 17 project, most common use case will be for UTU's notes so this way the propagation of the notes can be achieved to everybody.

The solution should:

- Accept Markdown content from a file or string
- Convert Markdown into styled HTML
- Render the HTML into PDF
- Support common Markdown elements such as headings, paragraphs, lists, blockquotes, code blocks, tables, and images
- Produce stable, readable, print-friendly PDFs

## 1.2 Background

The team needs a maintainable PDF generation feature based on Markdown so document content can be authored in a simple text format while preserving strong layout control in the generated PDF.

The recommended architecture is:

**Markdown → HTML → PDF**

This is preferred over building PDFs manually because:

- Markdown is easy to author and version
- HTML/CSS allows styling and layout control
- The implementation is modular and testable
- The system is easier to extend later with templates, headers, footers, fonts, branding, and localization

## 1.3 Goal

Deliver a production-ready Markdown-to-PDF generator module for Java 17 that can be integrated into the project and reused by other features.

# 2. Problem Statement

Today, there is no standardized way in the [project](https://github.com/ghm7/2mn-isbo-docs) to convert Markdown content into PDFs.

This causes:

- The team members have to alternate between GitHub MD Viewer and VSCode MD Viewer
- The inability to print the class notes
- Being forced to have a computer with VSCode installed in order to read the notes
- Difficulties sharing notes with other classmates

We need a single reusable component that provides predictable, testable PDF generation.

# 3. Objectives

## 3.1 Primary Objectives

- Create a reusable Java 17 PDF generation component from Markdown
- Support the most common Markdown syntax used in product documents
- Provide configurable HTML/CSS styling
- Ensure generated PDFs are consistent across environments
- Make the feature easy for other engineering teams to consume

## 3.2 Secondary Objectives

- Support future customization such as branded themes
- Enable API integration later
- Enable template-based document generation later
- Enable LaTex compatibility later
- Make testing and regression detection straightforward

# 4. Non-goals

This version will not include:

- A full WYSIWYG editor
- Live Markdown preview UI
- Advanced PDF Editing after generation
- Digital signatures
- OCR
- Collaborative document editing in real time
- JavaScript-executed HTML rendering
- Full browser-level CSS feature parity
- DOCX export
- PDF merging/splitting (maybe we'll add this one)

# 5. Users / Stakeholders

## 5.1 Primary Users

- Future backend engineers integrating document generation into the product
- Agents generating reports, invoices, summaries, or exports

## 5.2 Stakeholders

- 2<sup>nd</sup> MN Team
- Tech lead / architect
- QA team
- Product owner

# 6. User Stories

## 6.1 Core User Stories

1. **As a developer,** I want to pass a Markdown file and receive a PDF file so that I can generate printable documents from content files.
2. **As a developer,** I want to pass Markdown as a string so that I can generate PDFs from dynamic content.
3. **As a developer,** I want Markdown elements like headings, lists, tables, and code blocks to render correctly so that document remains readable and structured.
4. **As a developer,** I want to configure CSS styling so that the PDF output matches product branding or formatting rules.
5. **As a QA engineer,** I want deterministic output rules and test coverage so that regressions can be caught early.
6. **As a platform engineer,** I want the module to fail with clear error messages so that integration issues are easy to diagnose.

# 7. Functional Requirements

## 7.1 Input Handling

The system must:

- Accept Markdown as a `String`
- Accept Markdown from a file path
- Support UTF-8 input
- Validate that input is not null
- Return meaningful errors for unreadable or invalida file paths

## 7.2 Markdown Parsing

The system must:

- Parse standard Markdown syntax
- Support headings
- Support paragraphs
- Support unordered and ordered lists
- Support blockquotes
- Support inline code
- Support fenced code blocks
- Support tables
- Support links
- Support images

The system should:

- Support extension-based enhancements when needed
- Allow parses options to be configured centrally

## 7.3 HTML Generation

The system must:

- Convert Markdown into HTML
- Wrap generated HTML in a full HTML document
- Apply a consistent CSS stylesheet
- Support an external HTML template and/or CSS file in a future-friendly way

## 7.4 PDF Rendering

The system must:

- Render HTML into a PDF
- Support A4 by default
- Support configurable margins
- Generate readable output for multi-page documents
- Write output to a specified file path or output stream

# 7.5 Styling

The system must:

- Provide a default stylesheet
- Support print-friendly typography
- Style headings, paragraphs, lists, code blocks, tables, and blockquotes

The system should:

- Support theme overrides later
- Support external CSS loading later

## 7.6 Error Handling

The system must:

- Fail gracefully with a domain-specific exceptions
- Provide meaningful messages for:
  - Invalid input
  - Template loading failures
  - HTML conversion issues
  - PDF rendering failures
  - Output write failures

## 7.7 Logging

The system should:

- Log start/end of generation
- Log failures with enough context for debugging
- Avoid logging sensitive document content by default

# 8. Non-Functional Requirements

## 8.1 Performance

- Should generate a small-to-medium document in an acceptable time for backend processing
- Must not block indefinitely
- Should handle common document sizes safely

## 8.2 Reliability

- Must generate the same visual output given the same input and configuration
- Must fail predictably

## 8.3 Maintainability

- Code should be modular
- HTML template and CSS concerns should be separated from orchestration logic
- The implementation should be covered by unit and integration tests

## 8.4 Security

- Must not execute arbitrary JavaScript from HTML
- Must sanitize or normalize HTML output appropriately if needed
- Must validate file paths where relevant
- Must avoid unsafe resources loading rules by default

## 8.5 Compatibility

- Must run on Java 17
- Must work in local development and CI environments

# 9 Proposed Technical Solution

## 9.1 Recommended Libraries

- flexmark-java for Markdown parsing
- OpenHTMLtoPDF for HTML to PDF rendering
- jsoup optionally for HTML normalization/cleanup

## 9.2 High-Level Architecture

### Components

1. **MarkdownInputService**
   - Reads Markdown from file or receives raw text

2. **MarkdownRendererService**
   - Converts Markdown into HTML using flexmark

3. **HTMlTemplateService**
   - Injects rendered HTML into a full HTML template
   - Applies default CSS

4. **HTMLSanitizationService** (optional first version, or lightweight normalization)
   - Normalizes HTML/XHTML before PDF rendering

5. **PDFRenderService**
   - Converts HTML/XHTML into PDF using OpenHTMLtoPDF

6. **Facade / Public API**
   - Exposes simple methods like:
     - `generateFromFile(Path input, Path output)`
     - `generateFromMarkdown(String markdown, Path output)`

## 9.3 Suggested Package Structure

```
com.example.pdf
├── api
│   └── MarkdownPDFGenerator.java
├── markdown
│   └── MarkdownRendererService.java
├── template
│   └── HTMLTemplateService.java
├── pdf
│   └── PDFRenderService.java
├── io
│   └── MarkdownInputService.java
├── exception
│   ├── MarkdownPDFException.java
│   ├── MarkdownParsingException.java
│   ├── PDFRenderingException.java
│   └── TemplateProcessingException.java
└── config
    └── PDFGeneratorConfig.java
```

# 10. Scope

## 10.1 In Scope for MVP

- Markdown string input
- Markdown file input
- HTML generation
- PDF generation to file
- Default CSS theme
- Support for basic Markdown features
- Basic error handling
- Unit tests
- Integration tests with sample Markdown files

## 10.2 Out of Scope for MVP

- REST API endpoint
- Theme management UI
- Multiple branded templates
- Table of contents generation
- Header/footer page numbers
- Embedded custom fonts beyond default baseline
- Remote images fetching rules beyond basic local-safe usage policy
- Async job queue support

# 11. Acceptance Criteria

## 11.1 Feature Acceptance Criteria

1. Given a valida Markdown file, the system generates a PDF file successfully.
2. Given valida Markdown string content, the system generates a PDF file successfully.
3. The generated PDF correctly renders:
   - headings
   - paragraphs
   - unordered and ordered lists
   - blockquotes
   - inline code
   - fenced code blocks
   - tables
   - links
4. The generated PDF uses the default stylesheet consistently.
5. Invalid file paths result in a meaningful exception.
6. Rendering failures return meaningful exceptions and logs.
7. The module is compatible with Java 17.
8. Automated tests cover the main success and failure paths.

# 11.2 QA Acceptance Criteria

- QA has simple Markdown fixtures covering core syntax
- Output PDF files are generated in test runs
- No unhandled exceptions occur in expected edge cases
- Visual review of baseline fixtures is approved

# 12. Risks and Constraints

## 12.1 Risks

### Risk 1: HTML/CSS to PDF rendering limitations

Some CSS features may not behave like a browser.

#### Mitigation:

Define supported styling rules and test them with fixture documents.

### Risk 2: Markdown edge cases

Different Markdown flavors may behave differently.

#### Mitigation:

Standardize on a selected flexmark configuration and define supported syntax.

### Risk 3: Image/resource loading issues

Images may fail if paths or resources loading policies are unclear.

#### Mitigation:

Define supported image loading rules early.

### Risk 4: Regression in document appearance

Minor code or CSS changes could affect layout.

#### Mitigation:

Use fixture-based integration tests and visual sample review.

# 13. Dependencies

- Java 17
- flexmark-java
- OpenHTMLtoPDF
- jsoup
- test framework already used by the project (TBD)

# 14. Implementation Plan

## Phase 1 - Foundation

Build the core architecture and dependency setup.

## Phase 2 - Markdown to HTML

Implement parser and renderer services.

## Phase 3 - HTML to PDF

Implement PDF rendering service and output handling.

## Phase 4 - Styling and Templates

Add base HTML template and default CSS.

## Phase 5 - Testing

Add unit tests, integration tests, and sample fixtures.

## Phase 6 - Hardening

Improve exceptions, logging, and documentation.
