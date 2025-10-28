---
layout: default
title: RemoveAt
parent: Standard Library Functions
has_children: false
has_toc: false
permalink: /jyro/functions/stdlib/array/removeat/
---

# RemoveAt

Removes an element at a specific index from an array and returns the modified array.

## Syntax

```jyro
RemoveAt(array, index)
```

## Parameters

- **array** (array): The array to modify
- **index** (number): The zero-based index of the element to remove (must be integer)

## Returns

- **array**: The modified array after removing the element, or the original array if index is out of bounds

## Description

The array is modified in-place with all subsequent elements shifted down by one position. Returns the modified array to enable chaining operations. If the specified index is out of bounds, the array is returned unchanged.

If you need the removed element value, access it with `array[index]` before calling RemoveAt.

## Examples

```jyro
var items = ["apple", "banana", "orange"]
var result = RemoveAt(items, 1)
# result is ["apple", "orange"]
# items is also ["apple", "orange"] (modified in-place)
```

```jyro
var numbers = [10, 20, 30, 40]
var result = RemoveAt(numbers, 0)
# result is [20, 30, 40]
# numbers is also [20, 30, 40]
```

```jyro
# Access element before removing if you need it
var items = ["apple", "banana", "orange"]
var removed = items[1]
RemoveAt(items, 1)
# removed is "banana", items is ["apple", "orange"]
```

```jyro
# Chaining operations
var numbers = [1, 2, 3, 4, 5]
var length = Length(RemoveAt(RemoveAt(numbers, 0), 0))
# length is 3, numbers is [3, 4, 5]
```

## Notes

- The array is modified in-place and also returned
- Returns the modified array (not the removed element) to enable chaining
- Use `array[index]` before calling RemoveAt if you need the element value
- Out-of-bounds indices return the array unchanged (no error thrown)
- For removing and retrieving the last element, use the Pop function