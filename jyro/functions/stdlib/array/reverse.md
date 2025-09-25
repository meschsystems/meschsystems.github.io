---
layout: default
title: Reverse
parent: Standard Library Functions
has_children: false
has_toc: false
permalink: /jyro/functions/stdlib/array/reverse/
---

# Reverse

Reverses the order of elements in an array in-place.

## Syntax

```jyro
Reverse(array)
```

## Parameters

- **array** (array): The array to reverse

## Returns

- **array**: The same array instance with elements in reversed order

## Description

The first element becomes the last and the last element becomes the first. The array is modified directly and returned to support method chaining patterns.

## Examples

```jyro
var items = array ["first", "second", "third"]
Reverse(items)
# items is now ["third", "second", "first"]
```

```jyro
var numbers = array [1, 2, 3, 4, 5]
var reversed = Reverse(numbers)
# Both numbers and reversed refer to [5, 4, 3, 2, 1]
```