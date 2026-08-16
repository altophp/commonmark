# Tabs

Tabs converts `@tabs`, `@tab`, and `@endtabs` markers into tab buttons and
panels. The generated output includes ARIA relationships and a click handler.

## Install and register

```bash
composer require alto/commonmark-tabs
```

The same class is included in `alto/commonmark`.

```php
use Alto\CommonMark\Extension\Tabs\TabsExtension;
use League\CommonMark\Environment\Environment;
use League\CommonMark\Extension\CommonMark\CommonMarkCoreExtension;

$environment = new Environment();
$environment->addExtension(new CommonMarkCoreExtension());
$environment->addExtension(new TabsExtension());
```

## Create tabs

```markdown
@tabs
@tab PHP
composer require alto/commonmark
@tab JavaScript
npm install example
@endtabs
```

The first tab and panel receive the active class. Other panels receive the
`hidden` attribute. The embedded script switches panels on click and updates
`aria-selected`.

Tab titles can be quoted or unquoted. The complete group can have up to three
leading spaces; four spaces make it a normal indented code block.

Panel content is escaped and line breaks become `br` elements. It is not parsed
as Markdown, so fenced code blocks and inline emphasis remain literal text.

## Configure classes

```php
new TabsExtension([
    'container_class' => 'tabs-container',
    'tabs_class' => 'tabs-list',
    'tab_class' => 'tab',
    'panel_class' => 'tab-panel',
    'active_class' => 'active',
]);
```

The outer container receives a generated `data-tabs-id`. Buttons and panels
receive matching generated IDs for `aria-controls` and `aria-labelledby`.

The built-in script handles pointer activation only. Add application behavior
if arrow-key navigation or another interaction model is required.
