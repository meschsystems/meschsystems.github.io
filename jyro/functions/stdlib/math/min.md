---
layout: default
title: Min
parent: Standard Library Functions
has_children: false
has_toc: false
permalink: /jyro/functions/stdlib/math/min/
---

# Min

Returns the minimum numeric value from an array.

## Syntax

```jyro
Min(array)
```

## Parameters

- **array** (array): An array of numeric values

## Returns

- **number**: The minimum numeric value found, or `null` if the array is empty or contains no numeric values

## Description

Finds the smallest numeric value in the array. Non-numeric items are ignored. Returns `null` if no numeric values are found.

## Examples

```jyro
var result = Min([5, 10, 3, 8])  # Returns 3
```

```jyro
var result = Min([-5, -2, -10])  # Returns -10
```

```jyro
var result = Min([3.14, 2.71, 1.41])  # Returns 1.41
```

```jyro
var numbers = [5, 10, 3, 8]
var result = Min(numbers)  # Returns 3
```

```jyro
# Min of two values
var result = Min([a, b])
```

## Notes

- Returns `null` if the array is empty or contains no numeric values
- Non-numeric items in the array are silently ignored
- Related: `Max`, `Clamp`
