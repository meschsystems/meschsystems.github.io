---
layout: default
title: Any
parent: Standard Library Functions
has_children: false
has_toc: false
permalink: /jyro/functions/stdlib/array/any/
---

# Any

Checks if any element in an array satisfies a comparison condition on a specified field. Returns true on first match (short-circuits for efficiency).

## Syntax

```jyro
Any(array, fieldName, operator, value)
```

## Parameters

- **array** (array): The array of objects to check
- **fieldName** (string): The field name or nested path to compare (e.g., "status" or "address.city")
- **operator** (string): The comparison operator: "==", "!=", "<", "<=", ">", ">="
- **value** (any): The value to compare against

## Returns

- **boolean**: `true` if any element matches the condition, `false` otherwise

## Description

The `Any` function checks whether at least one element in an array satisfies the specified condition. It short-circuits on the first match, making it efficient for large arrays where a match is likely to occur early.

The function supports nested field paths using dot notation. Non-object elements and objects with missing fields are skipped (they don't cause a match).

## Examples

### Basic any-match check

```jyro
var orders = [
    { "id": 1, "status": "pending" },
    { "id": 2, "status": "shipped" },
    { "id": 3, "status": "pending" }
]

var hasShipped = Any(orders, "status", "==", "shipped")
# hasShipped is true

var hasCancelled = Any(orders, "status", "==", "cancelled")
# hasCancelled is false
```

### Checking for values above a threshold

```jyro
var products = [
    { "name": "Widget", "price": 25 },
    { "name": "Gadget", "price": 150 },
    { "name": "Gizmo", "price": 75 }
]

var hasExpensive = Any(products, "price", ">", 100)
# hasExpensive is true

var hasVeryExpensive = Any(products, "price", ">", 200)
# hasVeryExpensive is false
```

### Nested field paths

```jyro
var employees = [
    { "name": "Alice", "address": { "city": "Boston" } },
    { "name": "Bob", "address": { "city": "New York" } },
    { "name": "Carol", "address": { "city": "Chicago" } }
]

var hasNewYorker = Any(employees, "address.city", "==", "New York")
# hasNewYorker is true
```

### Conditional logic with Any

```jyro
var alerts = [
    { "level": "info", "message": "System started" },
    { "level": "warning", "message": "High memory usage" },
    { "level": "info", "message": "Request completed" }
]

if Any(alerts, "level", "==", "error") then
    Log("Critical: errors detected!")
elseif Any(alerts, "level", "==", "warning") then
    Log("Warning: issues detected")
else
    Log("All clear")
end
# Logs: "Warning: issues detected"
```

### Not-equals check

```jyro
var users = [
    { "name": "Alice", "role": "admin" },
    { "name": "Bob", "role": "admin" },
    { "name": "Carol", "role": "user" }
]

var hasNonAdmin = Any(users, "role", "!=", "admin")
# hasNonAdmin is true
```

### Handling non-object elements

```jyro
var mixed = [
    "string",
    null,
    { "status": "active" }
]

var hasActive = Any(mixed, "status", "==", "active")
# hasActive is true (non-objects are skipped)
```

## Notes

- Short-circuits on the first match for efficiency
- Returns `false` for empty arrays
- Non-object elements in the array are skipped
- Objects with missing fields are skipped (don't match)
- Supports all comparison operators: ==, !=, <, <=, >, >=
- Nested paths traverse objects using dot notation (e.g., "user.profile.verified")
- More efficient than `Length(Filter(...)) > 0` due to short-circuit behavior
- For checking if ALL elements match, use the `All` function instead
