---
layout: default
title: IndexOf
parent: Standard Library Functions
has_children: false
has_toc: false
permalink: /jyro/functions/stdlib/array/indexof/
---

# IndexOf

Returns the index of the first element in an array that matches a specified value using deep equality comparison.

## Syntax

```jyro
IndexOf(array, value)
```

## Parameters

- **array** (array): The array to search
- **value** (any): The value to find (compared using deep equality)

## Returns

- **number**: The zero-based index of the first matching element, or -1 if not found

## Description

The `IndexOf` function searches through an array and returns the zero-based index of the first element that is deeply equal to the specified search value. Deep equality means that complex objects and arrays are compared by their contents, not by reference.

If no matching element is found, the function returns -1.

## Examples

### Basic array search

```jyro
var numbers = [1, 2, 3, 4, 5]
var idx = IndexOf(numbers, 3)
# idx is 2
```

### Search with not found

```jyro
var colors = ["red", "green", "blue"]
var idx = IndexOf(colors, "yellow")
# idx is -1 (not found)
```

### Object array search with deep equality

```jyro
var orders = [
    { "id": "ORD-1001", "total": 100 },
    { "id": "ORD-1002", "total": 200 },
    { "id": "ORD-1003", "total": 150 }
]

var idx = IndexOf(orders, { "id": "ORD-1002", "total": 200 })
# idx is 1 (deep equality matches the object)
```

### Using IndexOf with RemoveAt

```jyro
var idx = IndexOf(Data.orders, { "id": "ORD-1005" })
if idx >= 0 then
    RemoveAt(Data.orders, idx)
end
```

### Nested array search

```jyro
var matrix = [[1, 2], [3, 4], [5, 6]]
var idx = IndexOf(matrix, [3, 4])
# idx is 1 (deep equality matches the nested array)
```
