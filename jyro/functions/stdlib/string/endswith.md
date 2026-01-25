---
layout: default
title: EndsWith
parent: Standard Library Functions
has_children: false
has_toc: false
permalink: /jyro/functions/stdlib/string/endswith/
---

# EndsWith

Tests whether a string ends with a specified suffix using case-sensitive comparison.

## Syntax

```jyro
EndsWith(source, suffix)
```

## Parameters

- **source** (string): The source string to test
- **suffix** (string): The suffix to search for

## Returns

- **boolean**: True if the source string ends with the suffix

## Description

Performs case-sensitive string suffix comparison using ordinal string comparison semantics.

## Examples

```jyro
var result1 = EndsWith("Hello World", "World")    # Returns `true`
```

```jyro
var result2 = EndsWith("filename.txt", ".txt")    # Returns `true`
```

```jyro
var result3 = EndsWith("Hello", "world")          # Returns `false` (case-sensitive)
```

```jyro
var result4 = EndsWith("test", "testing")         # Returns `false`
```