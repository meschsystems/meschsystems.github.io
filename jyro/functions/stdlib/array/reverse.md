---
layout: default
title: Reverse
parent: Standard Library Functions
has_children: false
has_toc: false
permalink: /jyro/functions/stdlib/array/reverse/
---

# Reverse

Returns a new array with elements in reversed order without modifying the original array.

## Syntax

```jyro
Reverse(array)
```

## Parameters

- **array** (array): The array to reverse

## Returns

- **array**: A new array with elements in reversed order. The original array remains unchanged.

## Description

Creates and returns a new array with elements in reversed order, leaving the original array unmodified. The first element of the original becomes the last in the result, and the last element becomes the first. This immutable behavior enables predictable data flow and safe function composition.

## Examples

```jyro
var items = ["first", "second", "third"]
var reversed = Reverse(items)
# reversed is ["third", "second", "first"]
# items is still ["first", "second", "third"]
```

```jyro
var numbers = [1, 2, 3, 4, 5]
var reversed = Reverse(numbers)
# reversed is [5, 4, 3, 2, 1]
# numbers is still [1, 2, 3, 4, 5]
```

```jyro
# Chaining with other array functions
var numbers = [3, 1, 4, 1, 5]
var sortedReversed = Reverse(Sort(numbers))
# sortedReversed is [5, 4, 3, 1, 1]
# numbers is still [3, 1, 4, 1, 5]
```

## Notes

- The original array is never modified
- Returns a new array with reversed elements
- Can be safely composed with other array functions like Sort and Filter