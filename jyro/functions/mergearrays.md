---
layout: default
title: MergeArrays
parent: Function Integration
has_children: false
has_toc: false
permalink: /jyro/functions/mergearrays/
---

# MergeArrays

Merges multiple arrays into a single array, concatenating all elements in order.

## Syntax

```jyro
MergeArrays(array1, array2, ...)
```

## Parameters

- **array1, array2, ...** (array): Multiple arrays to merge

## Returns

- **array**: A new array containing all elements from the input arrays

## Description

Supports merging variable numbers of arrays and handles mixed argument types by treating non-array values as individual elements. Null values are ignored during the merge process.

## Examples

```jyro
var arr1 = array [1, 2, 3]
var arr2 = array [4, 5]
var arr3 = array [6]
var merged = MergeArrays(arr1, arr2, arr3)
# Returns [1, 2, 3, 4, 5, 6]
```

```jyro
var colors = array ["red", "blue"]
var numbers = array [1, 2]
var combined = MergeArrays(colors, numbers)
# Returns ["red", "blue", 1, 2]
```