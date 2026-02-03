---
layout: default
title: Find
parent: Standard Library Functions
has_children: false
has_toc: false
permalink: /jyro/functions/stdlib/array/find/
---

# Find

Finds the first element in an array that satisfies a comparison condition on a specified field. Returns null if no match is found.

## Syntax

```jyro
Find(array, fieldName, operator, value)
```

## Parameters

- **array** (array): The array of objects to search
- **fieldName** (string): The field name or nested path to compare (e.g., "status" or "address.city")
- **operator** (string): The comparison operator: "==", "!=", "<", "<=", ">", ">="
- **value** (any): The value to compare against

## Returns

- **any**: The first matching element, or `null` if no match is found

## Description

The `Find` function searches through an array and returns the first element that satisfies the specified condition. It short-circuits on the first match, making it more efficient than using `Filter` followed by `First` when you only need one result.

The function supports nested field paths using dot notation. Non-object elements and objects with missing fields are skipped (they don't match).

## Examples

### Basic find

```jyro
var users = [
    { "id": 1, "name": "Alice", "role": "user" },
    { "id": 2, "name": "Bob", "role": "admin" },
    { "id": 3, "name": "Carol", "role": "admin" }
]

var firstAdmin = Find(users, "role", "==", "admin")
# firstAdmin is { "id": 2, "name": "Bob", "role": "admin" }
```

### No match returns null

```jyro
var users = [
    { "id": 1, "role": "user" },
    { "id": 2, "role": "user" }
]

var admin = Find(users, "role", "==", "admin")
# admin is null
```

### Finding with numeric comparison

```jyro
var products = [
    { "id": 1, "name": "Widget", "price": 25 },
    { "id": 2, "name": "Gadget", "price": 150 },
    { "id": 3, "name": "Gizmo", "price": 200 }
]

var firstExpensive = Find(products, "price", ">", 100)
# firstExpensive is { "id": 2, "name": "Gadget", "price": 150 }
```

### Nested field paths

```jyro
var employees = [
    { "id": 1, "name": "Alice", "address": { "city": "Boston" } },
    { "id": 2, "name": "Bob", "address": { "city": "New York" } },
    { "id": 3, "name": "Carol", "address": { "city": "Chicago" } }
]

var newYorker = Find(employees, "address.city", "==", "New York")
# newYorker is { "id": 2, "name": "Bob", "address": { "city": "New York" } }
```

### Safe access pattern

```jyro
var orders = [
    { "id": 1, "status": "pending" },
    { "id": 2, "status": "shipped" },
    { "id": 3, "status": "pending" }
]

var pendingOrder = Find(orders, "status", "==", "pending")

if not IsNull(pendingOrder) then
    Log("Found pending order: " + pendingOrder.id)
else
    Log("No pending orders")
end
# Logs: "Found pending order: 1"
```

### Finding first unprocessed item

```jyro
var tasks = [
    { "id": 1, "processed": true },
    { "id": 2, "processed": false },
    { "id": 3, "processed": false }
]

var nextTask = Find(tasks, "processed", "==", false)
# nextTask is { "id": 2, "processed": false }
```

### Not-equals operator

```jyro
var items = [
    { "status": "active" },
    { "status": "inactive" },
    { "status": "active" }
]

var firstNonActive = Find(items, "status", "!=", "active")
# firstNonActive is { "status": "inactive" }
```

### Handling non-object elements

```jyro
var mixed = [
    "string",
    null,
    { "id": 1, "status": "active" }
]

var found = Find(mixed, "status", "==", "active")
# found is { "id": 1, "status": "active" } (non-objects are skipped)
```

### Empty array returns null

```jyro
var emptyArray = []

var result = Find(emptyArray, "status", "==", "active")
# result is null
```

## Notes

- Short-circuits on the first match for efficiency
- Returns `null` if no matching element is found
- Returns `null` for empty arrays
- Non-object elements in the array are skipped
- Objects with missing fields are skipped (don't match)
- Supports all comparison operators: ==, !=, <, <=, >, >=
- Nested paths traverse objects using dot notation (e.g., "user.profile.email")
- More efficient than `First(Filter(...))` due to short-circuit behavior
- Use `IsNull()` to check if a match was found
