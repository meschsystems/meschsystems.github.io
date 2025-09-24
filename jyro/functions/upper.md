---
layout: default
title: Upper
parent: Function Integration
has_children: false
has_toc: false
permalink: /jyro/functions/upper/
---

# Upper

Converts a string to uppercase using culture-invariant conversion rules.

## Syntax

```jyro
Upper(text)
```

## Parameters

- **text** (string): The string to convert to uppercase

## Returns

- **string**: The input string converted to uppercase

## Description

Ensures consistent uppercase conversion behavior across different system locales and cultural settings for reliable text processing.

## Examples

```jyro
var result1 = Upper("hello world")     # Returns "HELLO WORLD"
```

```jyro
var result2 = Upper("MiXeD CaSe")      # Returns "MIXED CASE"
```

```jyro
var result3 = Upper("ALREADY UPPER")  # Returns "ALREADY UPPER"
```

```jyro
var result4 = Upper("abc123")          # Returns "ABC123"
```