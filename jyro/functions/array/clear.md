---
layout: default
title: Clear
parent: Function Integration
has_children: false
has_toc: false
permalink: /jyro/functions/array/clear/
---

# Clear

Removes all elements from an array, resulting in an empty array with zero length.

## Syntax

```jyro
Clear(array)
```

## Parameters

- **array** (array): The array to clear

## Returns

- **array**: The same array instance after all elements have been removed

## Description

The Clear function modifies the original array in-place and returns the same array instance to support method chaining patterns. After clearing, the array will have a length of zero but retains its identity for reference equality.

## Examples

```jyro
var items = array ["one", "two", "three"]
Clear(items)
# items is now [] with length 0
```

```jyro
var data = array [1, 2, 3, 4, 5]
var result = Clear(data)
# Both data and result refer to the same empty array
```