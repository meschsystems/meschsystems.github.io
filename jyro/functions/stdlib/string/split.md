---
layout: default
title: Split
parent: Standard Library Functions
has_children: false
has_toc: false
permalink: /jyro/functions/stdlib/string/split/
---

# Split

Splits a string into an array of substrings based on a specified delimiter.

## Syntax

```jyro
Split(text, delimiter)
```

## Parameters

- **text** (string): The string to split
- **delimiter** (string): The delimiter string used for splitting

## Returns

- **array**: Array of string elements representing the split parts

## Description

Returns all parts including empty strings that result from consecutive delimiters or delimiters at the beginning or end of the string.

## Examples

```jyro
var result1 = Split("apple,banana,orange", ",")
# Returns ["apple", "banana", "orange"]
```

```jyro
var result2 = Split("one::two::three", "::")
# Returns ["one", "two", "three"]
```

```jyro
var result3 = Split("a,,b", ",")
# Returns ["a", "", "b"] (preserves empty string)
```