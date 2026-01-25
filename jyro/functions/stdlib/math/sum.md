---
layout: default
title: Sum
parent: Standard Library Functions
has_children: false
has_toc: false
permalink: /jyro/functions/stdlib/math/sum/
---

# Sum

Calculates the sum of all numeric arguments provided to the function.

## Syntax

```jyro
Sum(value1, value2, ...)
Sum(array)
```

## Parameters

- **value1, value2, ...** (number): Multiple numeric values to sum, OR
- **array** (array): A single array of numeric values

## Returns

- **number**: The total sum of all numeric arguments, or `null` if no numeric arguments are provided

## Description

Accepts a variable number of numeric values or a single array and computes their total, ignoring non-numeric arguments. Returns `null` if no numeric arguments are provided.

## Examples

```jyro
var result1 = Sum(1, 2, 3, 4, 5)        # Returns 15
```

```jyro
var result2 = Sum(10.5, 2.3, 1.2)       # Returns 14.0
```

```jyro
var result3 = Sum(-5, 10, -3)           # Returns 2
```

```jyro
var result4 = Sum()                     # Returns `null`
```

```jyro
# Using with array
var numbers = [1, 2, 3, 4, 5]
var result5 = Sum(numbers)              # Returns 15
```