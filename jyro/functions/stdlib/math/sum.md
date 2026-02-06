---
layout: default
title: Sum
parent: Standard Library Functions
has_children: false
has_toc: false
permalink: /jyro/functions/stdlib/math/sum/
---

# Sum

Calculates the sum of all numeric values in an array.

## Syntax

```jyro
Sum(array)
```

## Parameters

- **array** (array): An array of numeric values

## Returns

- **number**: The total sum of all numeric values in the array (returns 0 if the array is empty or contains no numeric values)

## Description

Sums all numeric values in the array, ignoring non-numeric items. Returns 0 if the array is empty or contains no numbers.

## Examples

```jyro
var result = Sum([1, 2, 3, 4, 5])  # Returns 15
```

```jyro
var result = Sum([10.5, 2.3, 1.2])  # Returns 14.0
```

```jyro
var result = Sum([-5, 10, -3])  # Returns 2
```

```jyro
var numbers = [1, 2, 3, 4, 5]
var result = Sum(numbers)  # Returns 15
```

## Notes

- Non-numeric items in the array are silently ignored
- Returns 0 for an empty array
- Related: `Average`, `Min`, `Max`
