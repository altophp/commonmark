# Extensions

Install `alto/commonmark` for the complete collection, or install the split
package shown for one extension. Registration remains opt-in in both cases.

## Present titled code blocks

[Code block title](code-block-title.md) turns a title in the fenced-code info
string into a semantic caption.

Package: `alto/commonmark-code-block-title`

````markdown
```php title="src/App.php"
echo 'Hello';
```
````

The regular `pre` and `code` output is wrapped in a `figure` with a
`figcaption`. It can compose with a custom fenced-code renderer.

## Build semantic sections

[Content slicer](content-slicer.md) wraps heading ranges in nested `section`
elements without adding custom Markdown syntax.

Package: `alto/commonmark-content-slicer`

```markdown
# Guide

## Install
```

The `h2` and its following content become a section at the default threshold.
Apply heading-level changes before relying on a particular section hierarchy.

## Embed headings safely

[Heading level](heading-level.md) shifts or maps heading levels after parsing.

Package: `alto/commonmark-heading-level`

```text
# Included title    ->    ## Included title
```

Use it when a document fragment was authored for a different heading context.
It can be combined with Content Slicer or Table of Contents.

## Insert raw file content

[Import](import.md) reads a file and inserts its contents, optionally as a
language-tagged code block or a selected line range.

Package: `alto/commonmark-import`

```markdown
@import "src/Handler.php" {lines: 10-30, lang: php}
```

Use Import for raw text or source snippets. Use Include when the file must be
parsed as Markdown, or Source when the output needs a filename, line numbers,
or highlighted lines.

## Compose Markdown files

[Include](include.md) reads a Markdown fragment and parses it into the current
document.

Package: `alto/commonmark-include`

```markdown
@include "sections/installation.md"
```

Use it for reusable sections and multi-file documents. Included content runs
through the same configured environment, including other registered
extensions.

## Rewrite deployed URLs

[Link rewriter](link-rewriter.md) changes link and image destinations after
parsing.

Package: `alto/commonmark-link-rewriter`

```text
[Guide](/guide)    ->    [Guide](https://docs.example.com/guide)
```

Rules can add a base URI, map exact URLs, apply a regular expression, or call
application code. When combined, rules run in that order.

## Display source files

[Source](source.md) renders a file in a source-code container with optional
line selection, numbering, and highlighting.

Package: `alto/commonmark-source`

```markdown
@source "src/Service.php" {lines: 10-20, numbers: true, highlight: "14"}
```

Use Source for documentation that must stay synchronized with real source
files. It reads during conversion and does not execute the file.

## Generate navigation from headings

[Table of contents](table-of-contents.md) replaces an `@toc` marker with links
to selected document headings.

Package: `alto/commonmark-table-of-contents`

```markdown
@toc {min: 2, max: 3}
```

The extension also assigns IDs to headings. Apply Heading Level first if the
table of contents must use transformed levels.

## Present alternatives in tabs

[Tabs](tabs.md) turns `@tabs`, `@tab`, and `@endtabs` markers into tab buttons
and panels.

Package: `alto/commonmark-tabs`

```markdown
@tabs
@tab PHP
composer require alto/commonmark
@tab JSON
{"require":{"alto/commonmark":"*"}}
@endtabs
```

The output includes ARIA relationships and a click handler. Panel content is
escaped text with line breaks, not recursively parsed Markdown.
