# Include

Include loads a Markdown fragment and parses it into the current document. Use
it to compose a guide from reusable sections.

## Install and register

```bash
composer require alto/commonmark-include
```

The same class is included in `alto/commonmark`.

```php
use Alto\CommonMark\Extension\Include\IncludeExtension;
use League\CommonMark\Environment\Environment;
use League\CommonMark\Extension\CommonMark\CommonMarkCoreExtension;

$environment = new Environment();
$environment->addExtension(new CommonMarkCoreExtension());
$environment->addExtension(new IncludeExtension(
    basePath: __DIR__.'/content',
));
```

All requested paths are resolved beneath `basePath`.

## Include a fragment

Main document:

```markdown
# Guide

@include "sections/installation.md"
```

`sections/installation.md`:

```markdown
## Installation

Install the package with Composer.
```

The fragment is parsed with the current League CommonMark environment and
becomes part of the same output document.

Select a single line or an inclusive range before parsing:

```markdown
@include "sections/changelog.md" {lines: 1-5}
```

The directive can have up to three leading spaces. Four spaces make it a
normal indented code block.

## Constrain included files

```php
new IncludeExtension(
    basePath: __DIR__.'/content',
    maxDepth: 5,
    allowedExtensions: ['md'],
    maxFileSize: 262144,
);
```

- `maxDepth` limits nested parsing and defaults to `10`.
- `allowedExtensions` defaults to `['md', 'markdown']`.
- `maxFileSize` is measured in bytes and defaults to 1 MiB.

Invalid syntax, missing or rejected files, and oversized files render a
`div.include-error`. See [Security](../security.md) before processing untrusted
content.

Use [Import](import.md) for raw content and [Source](source.md) for source-code
presentation.
