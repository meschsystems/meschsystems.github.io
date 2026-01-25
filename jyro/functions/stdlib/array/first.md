---
layout: default
title: First
parent: Standard Library Functions
has_children: false
has_toc: false
permalink: /jyro/functions/stdlib/array/first/
---

# First

Returns the first element of an array without modifying it, or null if the array is empty.

## Syntax

```jyro
First(array)
```

## Parameters

- **array** (array): The array to access

## Returns

- **any**: The first element of the array, or null if the array is empty

## Description

Provides safe, non-destructive access to the first element of an array. Unlike direct index access (`array[0]`), this function Returns `null` for empty arrays instead of throwing an error, making it ideal for defensive programming patterns.

The array is never modified by this operation.

## Examples

```jyro
var numbers = [5, 2, 8, 1, 9]
var first = First(numbers)
# first is 5
# numbers is still [5, 2, 8, 1, 9]
```

```jyro
var items = ["apple", "banana", "orange"]
var first = First(items)
# first is "apple"
```

```jyro
var empty = []
var first = First(empty)
# first is null
```

```jyro
# Safe access pattern
var queue = GetWorkItems()
if First(queue) != null then
    var item = First(queue)
    # Process item
end
```

```jyro
# Elegant minimum/maximum patterns
var numbers = [5, 2, 8, 1, 9]
var min = First(Sort(numbers))
var max = Last(Sort(numbers))
# min is 1, max is 9
```

```jyro
# Combining with Filter
var users = [
    { "name": "Alice", "status": "active" },
    { "name": "Bob", "status": "inactive" },
    { "name": "Carol", "status": "active" }
]

var firstActive = First(Filter(users, "status", "==", "active"))
# firstActive is { "name": "Alice", "status": "active" }
```

## Notes

- The array is never modified
- Returns `null` for empty arrays (does not throw an error)
- Safer than direct index access for potentially empty arrays
- Can be elegantly composed with Sort, Filter, and other array functions
- Use with Pop to safely check before removing elements
