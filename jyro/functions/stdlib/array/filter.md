---
layout: default
title: Filter
parent: Standard Library Functions
has_children: false
has_toc: false
permalink: /jyro/functions/stdlib/array/filter/
---

# Filter

Returns a new array containing only elements where a specified field matches a value using a comparison operator.

## Syntax

```jyro
Filter(array, fieldName, operator, value)
```

## Parameters

- **array** (array): The array of objects to filter
- **fieldName** (string): The field name or nested path to compare (e.g., "status" or "address.city")
- **operator** (string): The comparison operator: `"=="`, `"!="`, `"<"`, `"<="`, `">"`, `">="`
- **value** (any): The value to compare against

## Returns

- **array**: A new array containing only the elements that match the filter criteria

## Description

The `Filter` function creates a new array containing only the elements from the original array where the specified field satisfies the comparison operator with the given value. The original array is not modified.

The function supports nested field paths using dot notation, allowing you to filter on deeply nested properties. Comparison operators enable powerful filtering beyond simple equality checks.

Non-object elements and objects missing the specified field are excluded from the result. Empty arrays return an empty array.

## Examples

### Equality filtering

```jyro
var users = [
    { "name": "Alice", "status": "active" },
    { "name": "Bob", "status": "inactive" },
    { "name": "Carol", "status": "active" }
]

var activeUsers = Filter(users, "status", "==", "active")
# activeUsers is [{ "name": "Alice", "status": "active" }, { "name": "Carol", "status": "active" }]
# users is unchanged
```

### Inequality filtering

```jyro
var tickets = [
    { "id": 1, "status": "open" },
    { "id": 2, "status": "closed" },
    { "id": 3, "status": "open" }
]

var notClosed = Filter(tickets, "status", "!=", "closed")
# notClosed is [{ "id": 1, "status": "open" }, { "id": 3, "status": "open" }]
```

### Numeric comparison filtering

```jyro
var orders = [
    { "id": 1, "quantity": 5, "priority": 1 },
    { "id": 2, "quantity": 10, "priority": 2 },
    { "id": 3, "quantity": 15, "priority": 1 }
]

var highQuantity = Filter(orders, "quantity", ">", 5)
# highQuantity is [{ "id": 2, "quantity": 10, "priority": 2 }, { "id": 3, "quantity": 15, "priority": 1 }]

var lowPriority = Filter(orders, "priority", "<=", 1)
# lowPriority is [{ "id": 1, "quantity": 5, "priority": 1 }, { "id": 3, "quantity": 15, "priority": 1 }]
```

### Nested path filtering

```jyro
var employees = [
    { "name": "Alice", "address": { "city": "New York" } },
    { "name": "Bob", "address": { "city": "Los Angeles" } },
    { "name": "Carol", "address": { "city": "New York" } }
]

var nyEmployees = Filter(employees, "address.city", "==", "New York")
# nyEmployees is [{ "name": "Alice", ... }, { "name": "Carol", ... }]
```

### Chaining filters

```jyro
var incidents = [
    { "id": 1, "team": "IT", "priority": 1, "status": "open" },
    { "id": 2, "team": "IT", "priority": 2, "status": "closed" },
    { "id": 3, "team": "HR", "priority": 1, "status": "open" },
    { "id": 4, "team": "IT", "priority": 1, "status": "open" }
]

var result = Filter(
    Filter(
        Filter(incidents, "team", "==", "IT"),
        "priority", "<=", 1
    ),
    "status", "!=", "closed"
)
# result is [{ "id": 1, ... }, { "id": 4, ... }]
```

### Filtering null values

```jyro
var records = [
    { "id": 1, "email": "alice@example.com" },
    { "id": 2, "email": null },
    { "id": 3, "email": "bob@example.com" }
]

var withEmail = Filter(records, "email", "!=", null)
# withEmail is [{ "id": 1, "email": "alice@example.com" }, { "id": 3, "email": "bob@example.com" }]
```

### Complex filtering patterns

```jyro
var products = [
    { "name": "Widget A", "price": 10.99, "stock": 50 },
    { "name": "Widget B", "price": 5.99, "stock": 0 },
    { "name": "Widget C", "price": 15.99, "stock": 25 },
    { "name": "Widget D", "price": 8.99, "stock": 5 }
]

# Find affordable in-stock products
var affordable = Filter(products, "price", "<=", 10.00)
var inStock = Filter(affordable, "stock", ">", 0)
# inStock is [{ "name": "Widget A", ... }, { "name": "Widget D", ... }]
```

## Notes

- The original array is never modified; a new array is returned
- String comparisons are **case-sensitive**. "Active" and "active" are treated as different values
- Supported operators: `"=="`, `"!="`, `"<"`, `"<="`, `">"`, `">="`
- Non-object elements in the array are excluded from results
- Objects missing the specified field are excluded from results
- Nested paths traverse objects using dot notation (e.g., "user.profile.age")
- Empty arrays return an empty array
- Can be chained with other array functions like Sort, Reverse, and CountIf
