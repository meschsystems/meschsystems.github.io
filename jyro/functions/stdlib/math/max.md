---
layout: default
title: Max
parent: Standard Library Functions
has_children: false
has_toc: false
permalink: /jyro/functions/stdlib/math/max
---

# Max

Returns the maximum numeric value from an array.

## Syntax

```jyro
Max(array)
```

## Parameters

- **array** (array): An array of numeric values

## Returns

- **number**: The maximum numeric value found, or `null` if the array is empty or contains no numeric values

## Description

Finds the largest numeric value in the array. Non-numeric items are ignored. Returns `null` if no numeric values are found.

## Examples

```jyro
var result = Max([5, 10, 3, 8])  # Returns 10
```

```jyro
var result = Max([-5, -2, -10])  # Returns -2
```

```jyro
var result = Max([3.14, 2.71, 1.41])  # Returns 3.14
```

```jyro
var numbers = [5, 10, 3, 8]
var result = Max(numbers)  # Returns 10
```

```jyro
# Max of two values
var result = Max([a, b])
```

## Notes

- Returns `null` if the array is empty or contains no numeric values
- Non-numeric items in the array are silently ignored
- Related: `Min`, `Clamp`
