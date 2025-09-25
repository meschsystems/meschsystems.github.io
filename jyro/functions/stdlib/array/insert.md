---
layout: default
title: Insert
parent: Standard Library Functions
has_children: false
has_toc: false
permalink: /jyro/functions/stdlib/array/insert/
---

# Insert

Inserts a value at a specific index position within an array, shifting existing elements to accommodate the new value.

## Syntax

```jyro
Insert(array, index, value)
```

## Parameters

- **array** (array): The target array to modify
- **index** (number): The zero-based index position for insertion (must be integer)
- **value** (any): The value to insert

## Returns

- **array**: The modified array with the value inserted

## Description

Elements at and after the insertion point are shifted to higher indices. The index must be between 0 and array.Length inclusive (allowing insertion at the end).

## Examples

```jyro
var items = array ["apple", "banana", "orange"]
Insert(items, 1, "grape")
# items is now ["apple", "grape", "banana", "orange"]
```

```jyro
var numbers = array [1, 3, 4]
Insert(numbers, 0, 0)
# numbers is now [0, 1, 3, 4]
```