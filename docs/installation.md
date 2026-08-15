# Installation

Alto CommonMark requires PHP 8.3 or later and League CommonMark 2.7.

Install the meta-package to use several extensions with one aligned version:

```bash
composer require alto/commonmark
```

The meta-package contains every extension documented here. Each extension is
still opt-in and must be registered on a League CommonMark environment.

## Install one extension

Applications that need only one capability can install its split package:

```bash
composer require alto/commonmark-code-block-title
```

The split packages use the same namespaces and classes as the meta-package.
Choose the package name from [All extensions](extensions/index.md).

Do not require the meta-package and one of its split packages together. The
meta-package already replaces every split package at the same version.

## Verify the installation

```bash
composer show alto/commonmark
```

For a split installation, replace the package name with the extension package
you installed.

Continue with [Getting started](getting-started.md).
