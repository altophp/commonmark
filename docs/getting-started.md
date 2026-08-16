# Getting started

Register only the extensions needed by the current converter. This example
adds titled code blocks and a table of contents.

````php
use Alto\CommonMark\Extension\CodeBlockTitle\CodeBlockTitleExtension;
use Alto\CommonMark\Extension\TableOfContents\TableOfContentsExtension;
use League\CommonMark\Environment\Environment;
use League\CommonMark\Extension\CommonMark\CommonMarkCoreExtension;
use League\CommonMark\MarkdownConverter;

$environment = new Environment();
$environment->addExtension(new CommonMarkCoreExtension());
$environment->addExtension(new CodeBlockTitleExtension());
$environment->addExtension(new TableOfContentsExtension([
    'min_level' => 2,
]));

$converter = new MarkdownConverter($environment);

$markdown = <<<'MARKDOWN'
# Guide

@toc

## Install

```bash title="Terminal"
composer require alto/commonmark
```
MARKDOWN;

echo $converter->convert($markdown);
````

The converter adds an `id` to the `Install` heading, replaces `@toc` with a
linked list, and wraps the code block in a `figure` with a caption.

## Choose extensions

Use [All extensions](extensions/index.md) to select extensions by task. Each
detail page documents registration, input syntax, configuration, and output.

Extensions that read files need an explicit trusted base directory. Review
[Security](security.md) before enabling Import, Include, or Source for content
you do not fully control.
