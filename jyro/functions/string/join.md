---
layout: default
title: Join
parent: Function Integration
has_children: false
has_toc: false
permalink: /jyro/functions/string/join/
---

# Join

Joins elements of an array into a single string using a specified delimiter.

## Syntax

```jyro
Join(array, delimiter)
```

## Parameters

- **array** (array): The array of elements to join
- **delimiter** (string): The delimiter string to place between elements

## Returns

- **string**: All array elements joined with the delimiter

## Description

Converts all array elements to their string representation and concatenates them with the delimiter between each element. String elements are used directly, null values become "null", and other types are converted using their ToString() representation.

## Examples

```jyro
var fruits = array ["apple", "banana", "orange"]
var result1 = Join(fruits, ", ")        # Returns "apple, banana, orange"
```

```jyro
var result2 = Join(fruits, " | ")       # Returns "apple | banana | orange"
```

```jyro
var mixed = array ["hello", 42, true, null]
var result3 = Join(mixed, "-")          # Returns "hello-42-true-null"
```