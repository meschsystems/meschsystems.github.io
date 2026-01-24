---
layout: default
title: Distinct
parent: Standard Library Functions
has_children: false
has_toc: false
permalink: /jyro/functions/stdlib/array/distinct/
---

# Distinct

Removes duplicate values from an array, returning only unique elements.

## Syntax

```jyro
Distinct(array)
```

## Parameters

- **array** (array): The array to remove duplicates from

## Returns

- **array**: A new array containing only unique elements

## Description

Creates a new array containing only the unique elements from the input array. Uses deep equality comparison for determining duplicates, meaning objects and arrays are compared by their contents, not by reference.

The order of first occurrence is preserved - elements appear in the result in the same order they first appeared in the input.

## Examples

### Basic deduplication

```jyro
var unique = Distinct([1, 2, 2, 3, 1])  # Returns [1, 2, 3]
```

### String deduplication

```jyro
var unique = Distinct(["apple", "banana", "apple", "cherry", "banana"])
# Returns ["apple", "banana", "cherry"]
```

### Preserves first occurrence order

```jyro
var unique = Distinct([3, 1, 2, 1, 3, 2])  # Returns [3, 1, 2]
```

### Empty array

```jyro
var unique = Distinct([])  # Returns []
```

### Single element

```jyro
var unique = Distinct([42])  # Returns [42]
```

### Deduplicating IDs

```jyro
var allIds = [101, 102, 101, 103, 102, 104]
var uniqueIds = Distinct(allIds)
# Returns [101, 102, 103, 104]
```

### Removing duplicate tags

```jyro
var tags = ["urgent", "review", "urgent", "approved", "review"]
var uniqueTags = Distinct(tags)
# Returns ["urgent", "review", "approved"]
```

### Objects with deep equality

```jyro
var items = [
    {"id": 1, "name": "A"},
    {"id": 2, "name": "B"},
    {"id": 1, "name": "A"}
]
var unique = Distinct(items)
# Returns [{"id": 1, "name": "A"}, {"id": 2, "name": "B"}]
```

## Notes

- Returns a new array; the original array is not modified
- Uses deep equality comparison (objects and arrays are compared by value)
- Null values are treated as equal to each other
- Performance: O(n²) comparison, suitable for typical array sizes
- For counting occurrences of each value, consider using `GroupBy` with `Length`
