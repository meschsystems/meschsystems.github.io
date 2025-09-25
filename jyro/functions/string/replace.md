---
layout: default
title: Replace
parent: Function Integration
has_children: false
has_toc: false
permalink: /jyro/functions/string/replace/
---

# Replace

Replaces all occurrences of a specified substring with a replacement string within a source string.

## Syntax

```jyro
Replace(source, oldValue, newValue)
```

## Parameters

- **source** (string): The source string to process
- **oldValue** (string): The substring to search for and replace
- **newValue** (string): The replacement string to substitute

## Returns

- **string**: The modified string with all occurrences replaced

## Description

Performs case-sensitive string replacement using ordinal comparison for consistent behavior across different cultural contexts.

## Examples

```jyro
var result1 = Replace("Hello World", "World", "Universe")
# Returns "Hello Universe"
```

```jyro
var result2 = Replace("test test test", "test", "demo")
# Returns "demo demo demo"
```

```jyro
var result3 = Replace("no matches here", "xyz", "abc")
# Returns "no matches here" (unchanged)
```