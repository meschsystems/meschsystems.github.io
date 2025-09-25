---
layout: default
title: Lower
parent: Standard Library Functions
has_children: false
has_toc: false
permalink: /jyro/functions/stdlib/string/lower/
---

# Lower

Converts a string to lowercase using culture-invariant conversion rules.

## Syntax

```jyro
Lower(text)
```

## Parameters

- **text** (string): The string to convert to lowercase

## Returns

- **string**: The input string converted to lowercase

## Description

Ensures consistent lowercase conversion behavior across different system locales and cultural settings.

## Examples

```jyro
var result1 = Lower("HELLO WORLD")     # Returns "hello world"
```

```jyro
var result2 = Lower("MiXeD CaSe")      # Returns "mixed case"
```

```jyro
var result3 = Lower("already lower")  # Returns "already lower"
```

```jyro
var result4 = Lower("ABC123")          # Returns "abc123"
```