---
layout: default
title: All
parent: Standard Library Functions
has_children: false
has_toc: false
permalink: /jyro/functions/stdlib/array/all/
---

# All

Checks if all elements in an array satisfy a comparison condition on a specified field. Returns false on first non-match (short-circuits for efficiency).

## Syntax

```jyro
All(array, fieldName, operator, value)
```

## Parameters

- **array** (array): The array of objects to check
- **fieldName** (string): The field name or nested path to compare (e.g., "status" or "address.city")
- **operator** (string): The comparison operator: "==", "!=", "<", "<=", ">", ">="
- **value** (any): The value to compare against

## Returns

- **boolean**: `true` if all elements match the condition, `false` otherwise

## Description

The `All` function checks whether every element in an array satisfies the specified condition. It short-circuits on the first non-match, making it efficient for large arrays where a failure is likely to occur early.

The function supports nested field paths using dot notation. Non-object elements and objects with missing fields cause an immediate `false` return (they are considered non-matching).

For empty arrays, `All` returns `true` (vacuous truth - a universal statement is true if there are no counterexamples).

## Examples

### Basic all-match check

```jyro
var orders = [
    { "id": 1, "status": "active" },
    { "id": 2, "status": "active" },
    { "id": 3, "status": "active" }
]

var allActive = All(orders, "status", "==", "active")
# allActive is true
```

### Not all match

```jyro
var orders = [
    { "id": 1, "status": "active" },
    { "id": 2, "status": "pending" },
    { "id": 3, "status": "active" }
]

var allActive = All(orders, "status", "==", "active")
# allActive is false
```

### Checking numeric conditions

```jyro
var scores = [
    { "student": "Alice", "score": 85 },
    { "student": "Bob", "score": 92 },
    { "student": "Carol", "score": 78 }
]

var allPassing = All(scores, "score", ">=", 70)
# allPassing is true

var allExcellent = All(scores, "score", ">=", 90)
# allExcellent is false
```

### Nested field paths

```jyro
var users = [
    { "profile": { "verified": true } },
    { "profile": { "verified": true } },
    { "profile": { "verified": true } }
]

var allVerified = All(users, "profile.verified", "==", true)
# allVerified is true
```

### Empty array returns true

```jyro
var emptyArray = []

var result = All(emptyArray, "status", "==", "active")
# result is true (vacuous truth)
```

### Validation logic

```jyro
var formFields = [
    { "name": "email", "valid": true },
    { "name": "password", "valid": true },
    { "name": "username", "valid": false }
]

if All(formFields, "valid", "==", true) then
    Log("Form is valid, submitting...")
else
    Log("Please fix validation errors")
end
# Logs: "Please fix validation errors"
```

### Non-object elements cause false

```jyro
var items = [
    { "status": "active" },
    "string",
    { "status": "active" }
]

var allActive = All(items, "status", "==", "active")
# allActive is false (non-object element)
```

### Missing fields cause false

```jyro
var items = [
    { "status": "active" },
    { "other": "field" },
    { "status": "active" }
]

var allActive = All(items, "status", "==", "active")
# allActive is false (missing field)
```

## Notes

- Short-circuits on the first non-match for efficiency
- Returns `true` for empty arrays (vacuous truth)
- Non-object elements cause immediate `false` return
- Objects with missing fields cause immediate `false` return
- Supports all comparison operators: ==, !=, <, <=, >, >=
- Nested paths traverse objects using dot notation (e.g., "user.profile.verified")
- More efficient than `Length(Filter(...)) == Length(array)` due to short-circuit behavior
- For checking if ANY element matches, use the `Any` function instead
