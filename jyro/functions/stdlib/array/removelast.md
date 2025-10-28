---
layout: default
title: RemoveLast
parent: Standard Library Functions
has_children: false
has_toc: false
permalink: /jyro/functions/stdlib/array/removelast/
---

# RemoveLast

Removes the last element from an array and returns the modified array.

## Syntax

```jyro
RemoveLast(array)
```

## Parameters

- **array** (array): The array to modify

## Returns

- **array**: The modified array after removing the last element

## Description

The array is modified in-place by removing the final element, reducing the array length by one. Returns the modified array to enable chaining operations. If the array is empty, it is returned unchanged.

If you need the removed element value, use the Pop function instead, which removes and returns the last element.

## Examples

```jyro
var items = ["apple", "banana", "orange"]
var result = RemoveLast(items)
# result is ["apple", "banana"]
# items is also ["apple", "banana"] (modified in-place)
```

```jyro
var numbers = [1]
var result = RemoveLast(numbers)
# result is []
# numbers is also []
```

```jyro
var empty = []
var result = RemoveLast(empty)
# result is []
# empty is still []
```

```jyro
# Chaining operations
var numbers = [1, 2, 3, 4, 5]
var length = Length(RemoveLast(RemoveLast(numbers)))
# length is 3, numbers is [1, 2, 3]
```

```jyro
# Use Pop if you need the element value
var items = ["apple", "banana", "orange"]
var last = Pop(items)
# last is "orange", items is ["apple", "banana"]
```

## Notes

- The array is modified in-place and also returned
- Returns the modified array (not the removed element) to enable chaining
- Use the Pop function if you need the removed element value
- Empty arrays are returned unchanged (no error thrown)
- The array length is reduced by one after this operation