---
layout: default
title: Sum
parent: Function Integration
has_children: false
has_toc: false
permalink: /jyro/functions/math/sum/
---

# Sum

Calculates the sum of all numeric arguments provided to the function.

## Syntax

```jyro
Sum(value1, value2, ...)
```

## Parameters

- **value1, value2, ...** (number): Multiple numeric values to sum

## Returns

- **number**: The total sum of all numeric arguments

## Description

Accepts a variable number of numeric values and computes their total, ignoring non-numeric arguments. Returns zero if no numeric arguments are provided.

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
var result4 = Sum()                     # Returns 0
```