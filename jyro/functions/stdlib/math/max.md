---
layout: default
title: Max
parent: Standard Library Functions
has_children: false
has_toc: false
permalink: /jyro/functions/stdlib/math/max
---

# Max

Returns the maximum numeric value from a variable number of arguments.

## Syntax

```jyro
Max(value1, value2, ...)
Max(array)
```

## Parameters

- **value1, value2, ...** (number): Multiple numeric values to compare, OR
- **array** (array): A single array of numeric values

## Returns

- **number**: The maximum value found, or `null` if no numeric arguments provided

## Description

Accepts multiple numeric values or a single array and determines the largest value among them. Non-numeric arguments are ignored during the comparison process.

## Examples

```jyro
var result1 = Max(5, 10, 3, 8)         # Returns 10
```

```jyro
var result2 = Max(-5, -2, -10)         # Returns -2
```

```jyro
var result3 = Max(3.14, 2.71, 1.41)    # Returns 3.14
```

```jyro
var result4 = Max(42)                  # Returns 42
```

```jyro
# Using with array
var numbers = [5, 10, 3, 8]
var result5 = Max(numbers)             # Returns 10
```