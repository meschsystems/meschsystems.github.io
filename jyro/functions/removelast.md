---
layout: default
title: RemoveLast
parent: Function Integration
has_children: false
has_toc: false
permalink: /jyro/functions/removelast/
---

# RemoveLast

Removes and returns the last element from an array.

## Syntax

```jyro
RemoveLast(array)
```

## Parameters

- **array** (array): The array to modify

## Returns

- **any**: The removed last element, or null if array is empty

## Description

The array is modified in-place by removing the final element, reducing the array length by one. Returns null if the array is empty rather than throwing an exception.

## Examples

```jyro
var items = array ["apple", "banana", "orange"]
var last = RemoveLast(items)
# last is "orange", items is now ["apple", "banana"]
```

```jyro
var numbers = array [1]
var only = RemoveLast(numbers)
# only is 1, numbers is now []
```

```jyro
var empty = array []
var nothing = RemoveLast(empty)
# nothing is null, empty is still []
```