---
layout: default
title: Last
parent: Standard Library Functions
has_children: false
has_toc: false
permalink: /jyro/functions/stdlib/array/last/
---

# Last

Returns the last element of an array without modifying it, or null if the array is empty.

## Syntax

```jyro
Last(array)
```

## Parameters

- **array** (array): The array to access

## Returns

- **any**: The last element of the array, or null if the array is empty

## Description

Provides safe, non-destructive access to the last element of an array. Unlike direct index access (`array[Length(array) - 1]`), this function Returns `null` for empty arrays instead of throwing an error, making it ideal for defensive programming patterns.

The array is never modified by this operation.

## Examples

```jyro
var numbers = [5, 2, 8, 1, 9]
var last = Last(numbers)
# last is 9
# numbers is still [5, 2, 8, 1, 9]
```

```jyro
var items = ["apple", "banana", "orange"]
var last = Last(items)
# last is "orange"
```

```jyro
var empty = []
var last = Last(empty)
# last is null
```

```jyro
# Safe access pattern
var stack = GetRecentActions()
if Last(stack) != null then
    var latest = Last(stack)
    # Process latest action
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
# Combining with Filter and Sort
var orders = [
    { "id": 1, "amount": 50.00, "date": "2024-01-01" },
    { "id": 2, "amount": 75.00, "date": "2024-01-02" },
    { "id": 3, "amount": 100.00, "date": "2024-01-03" }
]

var highestOrder = Last(Sort(orders))
# Returns the order with highest natural sort order
```

```jyro
# Safe peek before Pop
var stack = [1, 2, 3, 4, 5]
var top = Last(stack)
if top != null then
    var removed = Pop(stack)
    # removed is 5, stack is [1, 2, 3, 4]
end
```

## Notes

- The array is never modified
- Returns `null` for empty arrays (does not throw an error)
- Safer than direct index access for potentially empty arrays
- More readable than `array[Length(array) - 1]`
- Can be elegantly composed with Sort, Filter, and other array functions
- Use with Pop to safely check before removing elements
