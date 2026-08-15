# Heading level

Heading Level changes heading depth after parsing. Use it when content authored
as a complete document must fit inside another heading hierarchy.

## Install and register

```bash
composer require alto/commonmark-heading-level
```

The same class is included in `alto/commonmark`.

```php
use Alto\CommonMark\Extension\HeadingLevel\HeadingLevelExtension;
use League\CommonMark\Environment\Environment;
use League\CommonMark\Extension\CommonMark\CommonMarkCoreExtension;

$environment = new Environment();
$environment->addExtension(new CommonMarkCoreExtension());
$environment->addExtension(new HeadingLevelExtension([
    'down' => 1,
]));
```

With this configuration, `# Title` becomes `h2`, and `## Section` becomes
`h3`.

## Choose one strategy

Shift every heading by the same amount:

```php
new HeadingLevelExtension(['down' => 1]);
new HeadingLevelExtension(['down' => -1]);
```

Map selected levels and leave all other levels unchanged:

```php
new HeadingLevelExtension([
    'map' => [1 => 2, 2 => 3],
]);
```

Compute each level and return `null` to leave one unchanged:

```php
new HeadingLevelExtension([
    'callback' => static fn (int $level): ?int => 6 === $level
        ? null
        : min(6, $level + 1),
]);
```

If several strategies are configured, only the first available strategy is
used, in this order: `map`, `down`, then `callback`.

The extension does not clamp results to levels 1 through 6. Clamp callback
results or choose a safe shift when input headings can sit at either boundary.

See [Content slicer](content-slicer.md) for semantic sections and
[Table of contents](table-of-contents.md) for heading navigation.
