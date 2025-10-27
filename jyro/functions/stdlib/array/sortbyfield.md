---
layout: default
title: SortByField
parent: Standard Library Functions
has_children: false
has_toc: false
permalink: /jyro/functions/stdlib/array/sortbyfield/
---

# SortByField

Sorts an array of objects by a specified field in ascending or descending order. Supports nested field paths using dot notation.

## Syntax

```jyro
SortByField(array, fieldName, direction)
```

## Parameters

- **array** (array): The array of objects to sort
- **fieldName** (string): The field name or nested path to sort by (e.g., "age" or "address.city")
- **direction** (string): Sort direction - "asc" for ascending or "desc" for descending

## Returns

- **array**: A new array containing the sorted elements

## Description

The `SortByField` function sorts an array of objects by comparing values from a specified field. It supports both simple field names and nested paths using dot notation, allowing you to sort by deeply nested properties.

The function performs type-aware comparison, handling numeric and string values appropriately. String comparisons are case-sensitive and use ordinal comparison. Non-object elements are treated as equal in the sort order, and missing properties are handled gracefully by treating them as null values.

## Examples

### Basic sorting by numeric field

```jyro
var users = [
    { "name": "John", "age": 30 },
    { "name": "Alice", "age": 25 },
    { "name": "Bob", "age": 35 }
]

var byAge = SortByField(users, "age", "asc")
# Sorted by age: Alice (25), John (30), Bob (35)
```

### Sorting by string field descending

```jyro
var byName = SortByField(users, "name", "desc")
# Sorted by name descending: John, Bob, Alice
```

### Sorting by nested field path

```jyro
var employees = [
    { "name": "Alice", "address": { "city": "New York", "zip": "10001" } },
    { "name": "Bob", "address": { "city": "Los Angeles", "zip": "90001" } },
    { "name": "Carol", "address": { "city": "Chicago", "zip": "60601" } }
]

var byCity = SortByField(employees, "address.city", "asc")
# Sorted by city: Chicago, Los Angeles, New York
```

### Sorting with multiple levels of nesting

```jyro
var orders = [
    { "id": 1, "customer": { "profile": { "tier": "gold" } } },
    { "id": 2, "customer": { "profile": { "tier": "silver" } } },
    { "id": 3, "customer": { "profile": { "tier": "platinum" } } }
]

var byTier = SortByField(orders, "customer.profile.tier", "desc")
# Sorted by tier descending: silver, platinum, gold
```

## Notes

- String comparisons are **case-sensitive**
- The direction parameter is case-insensitive ("asc", "ASC", "Asc" all work)
- Non-object elements maintain their relative positions in the sort
- Objects with missing fields are sorted as if the field contains null
- Nested paths traverse objects using dot notation (e.g., "address.city.name")
- Only numeric and string fields are compared; other types are treated as equal