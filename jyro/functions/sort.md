---
layout: default
title: Sort
parent: Function Integration
has_children: false
has_toc: false
permalink: /jyro/functions/sort/
---

# Sort

Sorts an array in-place using type-aware comparison logic.

## Syntax

```jyro
Sort(array)
```

## Parameters

- **array** (array): The array to sort

## Returns

- **array**: The same array instance after sorting

## Description

Handles mixed-type arrays by grouping like types together. Sort order: null values first, then numbers (ascending), strings (lexicographic), booleans (false before true). Uses natural ordering for each type.

## Examples

```jyro
var numbers = array [3, 1, 4, 1, 5]
Sort(numbers)
# numbers is now [1, 1, 3, 4, 5]
```

```jyro
var mixed = array [null, "zebra", 5, "apple", 1, true, false]
Sort(mixed)
# Result: [null, 1, 5, "apple", "zebra", false, true]
```