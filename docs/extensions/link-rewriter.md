# Link rewriter

Link Rewriter changes destinations on Markdown links and images after parsing.
It is useful when authored paths differ from deployed URLs.

## Install and register

```bash
composer require alto/commonmark-link-rewriter
```

The same class is included in `alto/commonmark`.

```php
use Alto\CommonMark\Extension\LinkRewriter\LinkRewriterExtension;
use League\CommonMark\Environment\Environment;
use League\CommonMark\Extension\CommonMark\CommonMarkCoreExtension;

$environment = new Environment();
$environment->addExtension(new CommonMarkCoreExtension());
$environment->addExtension(new LinkRewriterExtension([
    'base_uri' => 'https://docs.example.com',
]));
```

`[Guide](/guide)` then links to `https://docs.example.com/guide`. URLs with a
scheme, such as `https:` or `mailto:`, remain unchanged by `base_uri`.

## Configure rewrite rules

Map exact destinations:

```php
new LinkRewriterExtension([
    'map' => ['/old-api' => '/api/v2'],
]);
```

Apply a regular expression:

```php
new LinkRewriterExtension([
    'pattern' => [
        'pattern' => '#^/docs/(v\d+)/(.+)$#',
        'replacement' => 'https://docs.example.com/$1/$2',
    ],
]);
```

Use application code when the node type matters:

```php
use League\CommonMark\Node\Node;

new LinkRewriterExtension([
    'callback' => static function (string $url, Node $node): string {
        return rtrim($url, '/');
    },
]);
```

You can configure `base_uri`, `map`, `pattern`, and `callback` together. They
run in that order, with each rule receiving the previous result. Both link
destinations and image sources are processed.

Invalid configuration types throw `TypeError` during construction.
