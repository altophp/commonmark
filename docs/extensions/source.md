# Source

Source reads a file and renders it in a source-code container. It can select a
line range, display original line numbers, and mark selected lines.

## Install and register

```bash
composer require alto/commonmark-source
```

The same class is included in `alto/commonmark`.

```php
use Alto\CommonMark\Extension\Source\SourceExtension;
use League\CommonMark\Environment\Environment;
use League\CommonMark\Extension\CommonMark\CommonMarkCoreExtension;

$environment = new Environment();
$environment->addExtension(new CommonMarkCoreExtension());
$environment->addExtension(new SourceExtension(
    basePath: __DIR__,
    allowedExtensions: ['php', 'js'],
));
```

All requested paths are resolved beneath `basePath`.

## Display source

```markdown
@source "src/Calculator.php"
```

The result contains `.source-block`, `.source-path`, and a language-tagged
`code` element. The language is inferred from common file extensions.

Select and annotate lines:

```markdown
@source "src/Calculator.php" {title: "Add method", lines: 9-11, numbers: true, highlight: "10"}
```

Available options are:

- `lines: 9-11` or `lines: 9` selects original lines.
- `lang: php` overrides language detection.
- `title: "Add method"` adds a `.source-title` element.
- `numbers: true` adds the original line number to each line.
- `highlight: "9,11-13"` adds `highlighted` to selected lines.

The directive can have up to three leading spaces. Four spaces make it a
normal indented code block.

## Constrain source access

```php
new SourceExtension(
    basePath: __DIR__.'/examples',
    allowedExtensions: ['php'],
    escapeHtml: true,
    maxFileSize: 262144,
);
```

The extension escapes source content by default. The extension allowlist is
empty by default, which permits every extension beneath the base directory.
The default maximum file size is 1 MiB.

Failures render a `div.source-error`. Review [Security](../security.md) before
changing these defaults. Use [Import](import.md) when only raw inserted content
is needed.
