---
layout: default
title: Append
parent: Function Integration
has_children: false
has_toc: false
permalink: /jyro/functions/array/append/
---

# Append

Appends a value to the end of an array and returns the modified array. This function mutates the original array.

## Syntax

```jyro
Append(array, value)
```

## Parameters

- **array** (array): The target array to append to
- **value** (any): The value to append

## Returns

- **array**: The modified array with the new value appended

## Description

The Append function adds the specified value as a new element at the end of the array. The append operation supports all Jyro value types including primitive values and complex values. The function modifies the original array in-place and returns it to enable method chaining.

## Examples

```jyro
var items = array ["apple", "banana"]
Append(items, "orange")
# items is now ["apple", "banana", "orange"]
```

```jyro
var numbers = array []
Append(numbers, 42)
Append(numbers, 3.14)
# numbers is now [42, 3.14]
```