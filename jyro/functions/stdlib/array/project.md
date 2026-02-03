---
layout: default
title: Project
parent: Standard Library Functions
has_children: false
has_toc: false
permalink: /jyro/functions/stdlib/array/project/
---

# Project

Creates new objects containing only the specified fields from each object in the source array.

## Syntax

```jyro
Project(array, fieldNames)
```

## Parameters

- **array** (array): The array of objects to project from
- **fieldNames** (array): An array of field names or nested paths to include in the projected objects

## Returns

- **array**: A new array of objects containing only the specified fields

## Description

The `Project` function creates a new array where each object contains only the fields specified in the `fieldNames` array. This is similar to a SQL SELECT statement that picks specific columns.

The function supports nested field paths using dot notation. For nested paths like "address.city", the leaf field name ("city") is used as the key in the projected object.

Non-object elements in the source array are skipped. Missing fields result in null values in the projected objects.

## Examples

### Basic projection

```jyro
var employees = [
    { "id": 1, "name": "Alice", "salary": 50000, "ssn": "123-45-6789" },
    { "id": 2, "name": "Bob", "salary": 60000, "ssn": "987-65-4321" }
]

# Project only public-safe fields
var publicInfo = Project(employees, ["id", "name"])
# publicInfo is [
#   { "id": 1, "name": "Alice" },
#   { "id": 2, "name": "Bob" }
# ]
```

### Projection with nested fields

```jyro
var customers = [
    { "id": 1, "name": "Alice", "address": { "city": "NYC", "zip": "10001" } },
    { "id": 2, "name": "Bob", "address": { "city": "LA", "zip": "90001" } }
]

var summary = Project(customers, ["name", "address.city"])
# summary is [
#   { "name": "Alice", "city": "NYC" },
#   { "name": "Bob", "city": "LA" }
# ]
```

### Data sanitization

```jyro
var userData = [
    { "username": "alice", "email": "alice@example.com", "password": "secret123", "apiKey": "key123" },
    { "username": "bob", "email": "bob@example.com", "password": "secret456", "apiKey": "key456" }
]

# Remove sensitive fields before sending to client
var safeData = Project(userData, ["username", "email"])
# safeData is [
#   { "username": "alice", "email": "alice@example.com" },
#   { "username": "bob", "email": "bob@example.com" }
# ]
```

### Creating summary views

```jyro
var orders = [
    { "orderId": "A001", "customer": "Alice", "total": 150, "items": [...], "shippingAddress": {...} },
    { "orderId": "A002", "customer": "Bob", "total": 200, "items": [...], "shippingAddress": {...} }
]

var orderSummary = Project(orders, ["orderId", "customer", "total"])
# orderSummary is [
#   { "orderId": "A001", "customer": "Alice", "total": 150 },
#   { "orderId": "A002", "customer": "Bob", "total": 200 }
# ]
```

### Handling missing fields

```jyro
var items = [
    { "a": 1, "b": 2 },
    { "a": 3 },
    { "b": 4 }
]

var projected = Project(items, ["a", "b"])
# projected is [
#   { "a": 1, "b": 2 },
#   { "a": 3, "b": null },
#   { "a": null, "b": 4 }
# ]
```

### Handling non-object elements

```jyro
var mixed = [
    { "x": 1, "y": 2 },
    "string",
    null,
    { "x": 3, "y": 4 }
]

var projected = Project(mixed, ["x"])
# projected is [
#   { "x": 1 },
#   { "x": 3 }
# ]
# Non-object elements are skipped
```

### Empty field list

```jyro
var items = [{ "a": 1 }, { "b": 2 }]

var empty = Project(items, [])
# empty is [{}, {}]
# Objects with no fields
```

## Notes

- The original array is never modified; a new array is always returned
- Non-object elements in the source array are skipped entirely
- Missing fields result in null values in the projected objects
- For nested paths (e.g., "address.city"), the leaf name ("city") is used as the property key
- Nested paths traverse objects using dot notation
- Empty arrays return an empty array
- An empty field list results in empty objects for each source object
- Non-string values in the fieldNames array are ignored
