---
layout: default
title: NotEqual
parent: Standard Library Functions
has_children: false
has_toc: false
permalink: /jyro/functions/stdlib/utility/notequal/
---

# NotEqual

Tests whether two values are not equal using Jyro's standard equality semantics.

## Syntax

```jyro
NotEqual(value1, value2)
```

## Parameters

- **value1** (any): The first value to compare
- **value2** (any): The second value to compare

## Returns

- **boolean**: True if the values are not equal, false if they are equal

## Description

Returns the logical negation of the equality comparison, performing deep comparison for complex types with appropriate type coercion.

## Examples

```jyro
var result1 = NotEqual(5, 3)              # Returns `true`
```

```jyro
var result2 = NotEqual("hello", "world")  # Returns `true`
```

```jyro
var result3 = NotEqual(5, 5)              # Returns `false`
```

```jyro
var result4 = NotEqual("test", "test")    # Returns `false`
```