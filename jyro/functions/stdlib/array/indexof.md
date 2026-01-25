---
layout: default
title: IndexOf
parent: Standard Library Functions
has_children: false
has_toc: false
permalink: /jyro/functions/stdlib/array/indexof/
---

# IndexOf

Returns the index of the first occurrence of a value in a string or array.

## Syntax

```jyro
IndexOf(text, search)
IndexOf(array, value)
```

## Parameters

- **text** (string or array): The string or array to search
- **search** (any): The value to find (substring for strings, value with deep equality for arrays)

## Returns

- **number**: The zero-based index of the first match, or -1 if not found

## Description

The `IndexOf` function is polymorphic and works with both strings and arrays:

- **For strings**: Returns the zero-based index of the first occurrence of a substring. The comparison is case-sensitive using ordinal comparison semantics.
- **For arrays**: Returns the zero-based index of the first element that is deeply equal to the specified search value. Deep equality means that complex objects and arrays are compared by their contents, not by reference.

If no match is found, the function returns -1.

## Examples

### String search

```jyro
var text = "Hello World"
var pos = IndexOf(text, "World")
# pos is 6
```

### String search - not found

```jyro
var text = "Hello World"
var pos = IndexOf(text, "xyz")
# pos is -1 (not found)
```

### String search - case sensitive

```jyro
var text = "Hello World"
var pos = IndexOf(text, "world")
# pos is -1 (case-sensitive, "world" != "World")
```

### Basic array search

```jyro
var numbers = [1, 2, 3, 4, 5]
var idx = IndexOf(numbers, 3)
# idx is 2
```

### Array search - not found

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

### Using IndexOf with Substring

```jyro
var filename = "document.pdf"
var dotPos = IndexOf(filename, ".")
if dotPos >= 0 then
    var extension = Substring(filename, dotPos + 1)
    # extension is "pdf"
end
```

### Using IndexOf with RemoveAt

```jyro
var idx = IndexOf(Data.orders, { "id": "ORD-1005" })
if idx >= 0 then
    RemoveAt(Data.orders, idx)
end
```

## See Also

- [Contains](../../string/contains/) - Test if string contains substring or array contains value
- [Substring](../../string/substring/) - Extract a portion of a string
