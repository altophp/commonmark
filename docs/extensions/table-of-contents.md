# Table of contents

Table of Contents replaces an `@toc` marker with a linked list built from the
document headings. It also assigns generated IDs to those headings.

## Install and register

```bash
composer require alto/commonmark-table-of-contents
```

The same class is included in `alto/commonmark`.

```php
use Alto\CommonMark\Extension\TableOfContents\TableOfContentsExtension;
use League\CommonMark\Environment\Environment;
use League\CommonMark\Extension\CommonMark\CommonMarkCoreExtension;

$environment = new Environment();
$environment->addExtension(new CommonMarkCoreExtension());
$environment->addExtension(new TableOfContentsExtension());
```

## Add a table of contents

```markdown
# Guide

@toc {min: 2, max: 3}

## Install

### Requirements

## Usage
```

`min` and `max` filter heading levels for that marker. Use
`ordered: true` to render an ordered list. The directive can have up to three
leading spaces.

Multiple markers in one document each receive their own filtered heading
list.

## Configure defaults

```php
new TableOfContentsExtension([
    'min_level' => 2,
    'max_level' => 4,
    'style' => 'ordered',
    'class' => 'toc-nav',
    'id' => 'main-toc',
    'title' => 'Contents',
    'marker' => '@contents',
]);
```

- `style` accepts `bullet` or `ordered`.
- `class` and `id` configure the wrapper.
- `title` adds an `h2` before the list.
- `marker` replaces the default `@toc` marker.

Heading IDs are lowercase slugs containing ASCII letters, digits, and hyphens.
The current implementation does not disambiguate duplicate headings.

See [Heading level](heading-level.md) when levels must be transformed and
[Content slicer](content-slicer.md) when headings must also create sections.
