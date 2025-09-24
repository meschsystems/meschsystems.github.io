---
layout: default
title: RemoveAt
parent: Function Integration
has_children: false
has_toc: false
permalink: /jyro/functions/removeat/
---

# RemoveAt

Removes an element at a specific index from an array and returns the removed element.

## Syntax

```jyro
RemoveAt(array, index)
```

## Parameters

- **array** (array): The array to modify
- **index** (number): The zero-based index of the element to remove (must be integer)

## Returns

- **any**: The removed element, or null if index is out of bounds

## Description

The array is modified in-place with all subsequent elements shifted down by one position. Returns null if the specified index is out of bounds rather than throwing an exception.

## Examples

```jyro
var items = array ["apple", "banana", "orange"]
var removed = RemoveAt(items, 1)
# removed is "banana", items is now ["apple", "orange"]
```

```jyro
var numbers = array [10, 20, 30, 40]
var first = RemoveAt(numbers, 0)
# first is 10, numbers is now [20, 30, 40]
```