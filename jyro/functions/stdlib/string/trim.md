---
layout: default
title: Trim
parent: Standard Library Functions
has_children: false
has_toc: false
permalink: /jyro/functions/stdlib/string/trim/
---

# Trim

Removes leading and trailing whitespace characters from a string.

## Syntax

```jyro
Trim(text)
```

## Parameters

- **text** (string): The string to trim

## Returns

- **string**: The input string with leading and trailing whitespace removed

## Description

Removes spaces, tabs, carriage returns, line feeds, and other Unicode whitespace characters as defined by the .NET framework. Preserves internal whitespace.

## Examples

```jyro
var result1 = Trim("  hello world  ")    # Returns "hello world"
```

```jyro
var result2 = Trim("\t\ntest\r\n")       # Returns "test"
```

```jyro
var result3 = Trim("no spaces")          # Returns "no spaces"
```

```jyro
var result4 = Trim("  space inside  ")   # Returns "space inside"
```