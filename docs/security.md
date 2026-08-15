# Security

Import, Include, and Source read local files while Markdown is converted. Use a
narrow, trusted base directory and never derive it directly from user input.

```php
$contentDirectory = __DIR__.'/content';

$environment->addExtension(new IncludeExtension(
    basePath: $contentDirectory,
    allowedExtensions: ['md'],
    maxFileSize: 262144,
));
```

## File boundaries

All three extensions resolve requested paths beneath their configured base
directory and reject traversal outside it. This boundary limits reach, but it
does not decide which files inside the directory are safe to publish.

Include accepts an extension allowlist and a maximum file size. Source accepts
the same controls, but its allowlist is empty by default. Import has neither a
file type filter nor a file size limit, so reserve it for trusted content and a
carefully scoped directory.

Include also limits nested parsing depth. Imported content is not parsed as a
nested Markdown document.

## Output handling

Source escapes file content by default. Keep `escapeHtml: true` for untrusted
or mixed-trust files. Disabling it allows file content to reach the generated
HTML without escaping.

Include parses the loaded fragment with the current League CommonMark
environment. Its raw HTML and URL behavior therefore follow that environment's
configuration.

Read failures are rendered as `include-error`, `import-error`, or
`source-error` elements. Import errors may contain resolved filesystem paths.
Do not expose conversion errors directly when local paths are sensitive.

None of these extensions fetches remote URLs or executes included code.
