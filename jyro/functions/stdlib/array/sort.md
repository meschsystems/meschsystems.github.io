---
layout: default
title: Sort
parent: Standard Library Functions
has_children: false
has_toc: false
permalink: /jyro/functions/stdlib/array/sort/
---

# Sort

Returns a new sorted array using type-aware comparison logic without modifying the original array.

## Syntax

```jyro
Sort(array)
```

## Parameters

- **array** (array): The array to sort

## Returns

- **array**: A new sorted array. The original array remains unchanged.

## Description

Creates and returns a new sorted array, leaving the original array unmodified. This immutable behavior enables predictable data flow and safe function composition.

Handles mixed-type arrays by grouping like types together. Sort order: null values first, then numbers (ascending), strings (lexicographic), booleans (false before true). Uses natural ordering for each type.

## Examples

```jyro
var numbers = [3, 1, 4, 1, 5]
var sorted = Sort(numbers)
# sorted is [1, 1, 3, 4, 5]
# numbers is still [3, 1, 4, 1, 5]
```

```jyro
var mixed = [null, "zebra", 5, "apple", 1, true, false]
var sorted = Sort(mixed)
# sorted is [null, 1, 5, "apple", "zebra", false, true]
# mixed is unchanged
```

```jyro
# Chaining with other array functions
var numbers = [5, 2, 8, 1, 9]
var min = First(Sort(numbers))
var max = Last(Sort(numbers))
# min is 1, max is 9, numbers is still [5, 2, 8, 1, 9]
```

## Notes

- The original array is never modified
- Returns a new array with the sorted elements
- Can be safely composed with other array functions like Filter and Reverse