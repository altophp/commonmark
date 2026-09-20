# Alto CommonMark

Alto CommonMark bundles focused extensions for League CommonMark. Install the
meta-package when an application needs several extensions or when you want one
version to keep the complete set aligned.

```php
use Alto\CommonMark\Extension\CodeBlockTitle\CodeBlockTitleExtension;
use League\CommonMark\Environment\Environment;
use League\CommonMark\Extension\CommonMark\CommonMarkCoreExtension;
use League\CommonMark\MarkdownConverter;

$environment = new Environment();
$environment->addExtension(new CommonMarkCoreExtension());
$environment->addExtension(new CodeBlockTitleExtension());

$converter = new MarkdownConverter($environment);
$html = $converter->convert("```php title=\"example.php\"\necho 'Hello';\n```");
```

## Documentation

- [Installation](installation.md): install the complete collection or one extension.
- [Getting started](getting-started.md): register extensions and render Markdown.

## Extensions

- [All extensions](extensions/index.md): choose an extension by the problem it solves.

## Security

- [Security](security.md): constrain extensions that read files.

The package extends League CommonMark; it does not replace its parser or core
syntax. Each extension is opt-in.
