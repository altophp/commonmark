# Import

Import inserts raw file content at an `@import` directive. It can select lines,
indent them, or wrap them in a language-tagged code block.

## Install and register

```bash
composer require alto/commonmark-import
```

The same class is included in `alto/commonmark`.

```php
use Alto\CommonMark\Extension\Import\ImportExtension;
use League\CommonMark\Environment\Environment;
use League\CommonMark\Extension\CommonMark\CommonMarkCoreExtension;

$environment = new Environment();
$environment->addExtension(new CommonMarkCoreExtension());
$environment->addExtension(new ImportExtension(
    basePath: __DIR__.'/content',
));
```

All requested paths are resolved beneath `basePath`.

## Import content

```markdown
@import "fragments/introduction.txt"
```

Without a language, file contents are inserted directly into the rendered
output. They are not parsed as Markdown.

Use `lang` to produce a code block:

```markdown
@import "src/Calculator.php" {lines: 9-11, lang: php, indent: 2}
```

```html
<pre><code class="language-php">  public function add(int $a, int $b): int
  {
      return $a + $b;</code></pre>
```

## Options

- `lines: 5` selects one 1-indexed line.
- `lines: 5-12` selects an inclusive range.
- `lang: php` adds the `language-php` class and escapes the content.
- `indent: 2` adds two spaces to every selected line.

The directive can have up to three leading spaces. Four spaces make it a
normal indented code block.

The constructor also accepts `maxDepth`, which defaults to `10`. Invalid
syntax, missing files, rejected paths, repeated imports, and depth failures
render a `div.import-error` instead of stopping the complete conversion.

Import does not restrict file extensions or file sizes. Review
[Security](../security.md), and use [Include](include.md) for parsed Markdown or
[Source](source.md) for a structured source-code presentation.
