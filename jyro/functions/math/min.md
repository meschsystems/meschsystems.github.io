---
layout: default
title: Min
parent: Function Integration
has_children: false
has_toc: false
permalink: /jyro/functions/math/min/
---

# Min

Returns the minimum numeric value from a variable number of arguments.

## Syntax

```jyro
Min(value1, value2, ...)
```

## Parameters

- **value1, value2, ...** (number): Multiple numeric values to compare

## Returns

- **number**: The minimum value found, or null if no numeric arguments provided

## Description

Accepts multiple numeric values and determines the smallest value among them. Non-numeric arguments are ignored during the comparison process.

## Examples

```jyro
var result1 = Min(5, 10, 3, 8)         # Returns 3
```

```jyro
var result2 = Min(-5, -2, -10)         # Returns -10
```

```jyro
var result3 = Min(3.14, 2.71, 1.41)    # Returns 1.41
```

```jyro
var result4 = Min(42)                  # Returns 42
```