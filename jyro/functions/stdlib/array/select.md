---
layout: default
title: Select
parent: Standard Library Functions
has_children: false
has_toc: false
permalink: /jyro/functions/stdlib/array/select/
---

# Select

Extracts a single field value from each object in an array, returning an array of those values.

## Syntax

```jyro
Select(array, fieldName)
```

## Parameters

- **array** (array): The array of objects to extract from
- **fieldName** (string): The field name or nested path to extract (e.g., "status" or "address.city")

## Returns

- **array**: A new array containing the extracted field values from each object

## Description

The `Select` function creates a new array by extracting the specified field from each object in the source array. This enables powerful composition with aggregate functions like `Sum`, `Max`, `Min`, and `Avg`.

The function supports nested field paths using dot notation, allowing you to extract deeply nested properties. Non-object elements result in null values at those positions. Objects missing the specified field also return null for that position.

## Examples

### Basic field extraction

```jyro
var orders = [
    { "id": 1, "amount": 100, "customer": "Alice" },
    { "id": 2, "amount": 200, "customer": "Bob" },
    { "id": 3, "amount": 150, "customer": "Charlie" }
]

var amounts = Select(orders, "amount")
# amounts is [100, 200, 150]

var customers = Select(orders, "customer")
# customers is ["Alice", "Bob", "Charlie"]
```

### Composing with aggregate functions

```jyro
var orders = [
    { "amount": 100 },
    { "amount": 200 },
    { "amount": 150 }
]

var total = Sum(Select(orders, "amount"))
# total is 450

var highest = Max(Select(orders, "amount"))
# highest is 200

var average = Avg(Select(orders, "amount"))
# average is 150
```

### Nested field extraction

```jyro
var employees = [
    { "name": "Alice", "address": { "city": "New York", "zip": "10001" } },
    { "name": "Bob", "address": { "city": "Los Angeles", "zip": "90001" } },
    { "name": "Carol", "address": { "city": "Chicago", "zip": "60601" } }
]

var cities = Select(employees, "address.city")
# cities is ["New York", "Los Angeles", "Chicago"]
```

### Getting unique values with Distinct

```jyro
var products = [
    { "name": "Widget A", "category": "Electronics" },
    { "name": "Widget B", "category": "Clothing" },
    { "name": "Widget C", "category": "Electronics" },
    { "name": "Widget D", "category": "Home" },
    { "name": "Widget E", "category": "Clothing" }
]

var categories = Distinct(Select(products, "category"))
# categories is ["Electronics", "Clothing", "Home"]
```

### Handling missing fields

```jyro
var items = [
    { "a": 1, "b": 2 },
    { "a": 3 },
    { "b": 4 }
]

var aValues = Select(items, "a")
# aValues is [1, 3, null]
```

### Handling non-object elements

```jyro
var mixed = [
    { "x": 10 },
    "not an object",
    42,
    { "x": 20 },
    null
]

var xValues = Select(mixed, "x")
# xValues is [10, null, null, 20, null]
```

## Notes

- The original array is never modified; a new array is always returned
- Non-object elements in the array result in null values at those positions
- Objects missing the specified field result in null values
- Nested paths traverse objects using dot notation (e.g., "user.profile.email")
- Empty arrays return an empty array
- Can be chained with aggregate functions like `Sum`, `Max`, `Min`, `Avg`
- Can be chained with array functions like `Distinct`, `Sort`, `Filter`
