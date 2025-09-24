---
layout: default
title: SortByField
parent: Function Integration
has_children: false
has_toc: false
permalink: /jyro/functions/sortbyfield/
---

# SortByField

Sorts an array of objects by a specified field in ascending or descending order.

## Syntax

```jyro
SortByField(array, fieldName, direction)
```

## Parameters

- **array** (array): The array of objects to sort
- **fieldName** (string): The field name to sort by
- **direction** (string): Sort direction - "asc" for ascending or "desc" for descending

## Returns

- **array**: A new array containing the sorted elements

## Description

Supports sorting by numeric and string properties with proper type-aware comparison. Non-object elements are treated as equal in the sort order, and missing properties are handled gracefully.

## Examples

```jyro
var users = array [
    object { "name": "John", "age": 30 },
    object { "name": "Alice", "age": 25 },
    object { "name": "Bob", "age": 35 }
]
var byAge = SortByField(users, "age", "asc")
# Sorted by age: Alice (25), John (30), Bob (35)
```

```jyro
var byName = SortByField(users, "name", "desc") 
# Sorted by name descending: John, Bob, Alice
```