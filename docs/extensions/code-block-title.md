# Code block title

Code Block Title reads `title="..."` or `filename="..."` from a fenced-code
info string. It preserves the normal code rendering and adds a semantic
caption around it.

## Install and register

```bash
composer require alto/commonmark-code-block-title
```

The same class is included in `alto/commonmark`.

```php
use Alto\CommonMark\Extension\CodeBlockTitle\CodeBlockTitleExtension;
use League\CommonMark\Environment\Environment;
use League\CommonMark\Extension\CommonMark\CommonMarkCoreExtension;

$environment = new Environment();
$environment->addExtension(new CommonMarkCoreExtension());
$environment->addExtension(new CodeBlockTitleExtension());
```

## Add a title

Place the attribute after the language name:

````markdown
```php title="example.php"
echo "Hello, World!";
```
````

The result keeps the standard `pre` and `code` elements:

```html
<figure class="code-block has-title" data-title="example.php">
  <figcaption class="code-title">example.php</figcaption>
  <pre><code class="language-php">echo &quot;Hello, World!&quot;;
</code></pre>
</figure>
```

`filename="example.php"` is an alias. When both attributes are present,
`title` wins. A fenced block without either attribute renders normally.

## Compose with another renderer

The constructor accepts a `NodeRendererInterface` used for the inner code
block:

```php
$environment->addExtension(new CodeBlockTitleExtension($codeRenderer));
```

Use this when another extension or application renderer controls the code
markup. The title value and caption are HTML-escaped.

See [Source](source.md) when the code must be read from a real file.
