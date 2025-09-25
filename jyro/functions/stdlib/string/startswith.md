---
layout: default
title: StartsWith
parent: Standard Library Functions
has_children: false
has_toc: false
permalink: /jyro/functions/stdlib/string/startswith/
---

# StartsWith

Tests whether a string begins with a specified prefix using case-sensitive comparison.

## Syntax

```jyro
StartsWith(source, prefix)
```

## Parameters

- **source** (string): The source string to test
- **prefix** (string): The prefix to search for

## Returns

- **boolean**: True if the source string begins with the prefix

## Description

Performs case-sensitive comparison using ordinal string comparison semantics for consistent behavior.

## Examples

```jyro
var result1 = StartsWith("Hello World", "Hello")    # Returns true
```

```jyro
var result2 = StartsWith("filename.txt", "file")    # Returns true
```

```jyro
var result3 = StartsWith("Hello", "hello")          # Returns false (case-sensitive)
```

```jyro
var result4 = StartsWith("test", "testing")         # Returns false
```