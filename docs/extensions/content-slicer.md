# Content slicer

Content Slicer converts a heading hierarchy into nested `section` elements.
It uses standard headings and adds no Markdown syntax.

## Install and register

```bash
composer require alto/commonmark-content-slicer
```

The same class is included in `alto/commonmark`.

```php
use Alto\CommonMark\Extension\ContentSlicer\ContentSlicerExtension;
use League\CommonMark\Environment\Environment;
use League\CommonMark\Extension\CommonMark\CommonMarkCoreExtension;

$environment = new Environment();
$environment->addExtension(new CommonMarkCoreExtension());
$environment->addExtension(new ContentSlicerExtension());
```

## Build sections

```markdown
# Main

Introduction.

## Install

Installation details.

### Requirements

PHP 8.3 or later.
```

At the default threshold, the `h1` stays at the document root. The `h2` opens
a section and the `h3` opens a nested section:

```html
<h1>Main</h1>
<p>Introduction.</p>
<section>
  <h2>Install</h2>
  <p>Installation details.</p>
  <section>
    <h3>Requirements</h3>
    <p>PHP 8.3 or later.</p>
  </section>
</section>
```

Content before the first wrapped heading stays at the document root.

## Choose the threshold

```php
new ContentSlicerExtension(minSectionLevel: 0); // Wrap h1 and deeper.
new ContentSlicerExtension(minSectionLevel: 1); // Wrap h2 and deeper.
new ContentSlicerExtension(minSectionLevel: 2); // Wrap h3 and deeper.
```

The threshold means that headings deeper than the given level open sections.
When combining this extension with [Heading level](heading-level.md), register
the desired transformations and verify the resulting hierarchy together.
