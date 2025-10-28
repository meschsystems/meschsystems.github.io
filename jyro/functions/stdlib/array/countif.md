---
layout: default
title: CountIf
parent: Standard Library Functions
has_children: false
has_toc: false
permalink: /jyro/functions/stdlib/array/countif/
---

# CountIf

Counts the number of elements in an array where a specified field matches a value using a comparison operator. Supports nested field paths and performs case-sensitive comparison.

## Syntax

```jyro
CountIf(array, fieldName, operator, value)
```

## Parameters

- **array** (array): The array of objects to count
- **fieldName** (string): The field name or nested path to compare (e.g., "status" or "address.city")
- **operator** (string): The comparison operator: `"=="`, `"!="`, `"<"`, `"<="`, `">"`, `">="`
- **value** (any): The value to compare against

## Returns

- **number**: The count of elements where the specified field satisfies the comparison with the value

## Description

The `CountIf` function searches through an array of objects and counts how many elements have a field that satisfies the comparison operator with the specified value. The function supports nested field paths using dot notation, allowing you to compare deeply nested properties.

Comparison operators enable powerful counting beyond simple equality: use `"=="` for equality, `"!="` for inequality, `"<"`, `"<="`, `">"`, `">="` for numeric comparisons. String comparisons are case-sensitive.

Non-object elements and objects with missing fields are skipped and not counted. Empty arrays return 0.

## Examples

### Equality comparison

```jyro
var users = [
    { "name": "Alice", "status": "active" },
    { "name": "Bob", "status": "inactive" },
    { "name": "Carol", "status": "active" },
    { "name": "Dan", "status": "active" }
]

var activeCount = CountIf(users, "status", "==", "active")
# activeCount is 3
```

### Inequality comparison

```jyro
var tickets = [
    { "id": 1, "status": "open" },
    { "id": 2, "status": "closed" },
    { "id": 3, "status": "open" },
    { "id": 4, "status": "pending" }
]

var notClosed = CountIf(tickets, "status", "!=", "closed")
# notClosed is 3
```

### Numeric comparison

```jyro
var orders = [
    { "id": 1, "quantity": 5, "priority": 1 },
    { "id": 2, "quantity": 10, "priority": 2 },
    { "id": 3, "quantity": 5, "priority": 1 },
    { "id": 4, "quantity": 15, "priority": 1 }
]

var highPriorityCount = CountIf(orders, "priority", "==", 1)
# highPriorityCount is 3

var largeOrders = CountIf(orders, "quantity", ">", 5)
# largeOrders is 2

var mediumPriority = CountIf(orders, "priority", "<=", 2)
# mediumPriority is 4
```

### Nested path comparison

```jyro
var employees = [
    { "name": "Alice", "address": { "city": "New York" } },
    { "name": "Bob", "address": { "city": "Los Angeles" } },
    { "name": "Carol", "address": { "city": "New York" } },
    { "name": "Dan", "address": { "city": "Chicago" } }
]

var nyCount = CountIf(employees, "address.city", "==", "New York")
# nyCount is 2
```

### Boolean field comparison

```jyro
var tasks = [
    { "title": "Task 1", "completed": true },
    { "title": "Task 2", "completed": false },
    { "title": "Task 3", "completed": true },
    { "title": "Task 4", "completed": true }
]

var completedCount = CountIf(tasks, "completed", "==", true)
# completedCount is 3

var incompleteCount = CountIf(tasks, "completed", "!=", true)
# incompleteCount is 1
```

### Counting null values

```jyro
var records = [
    { "id": 1, "email": "alice@example.com" },
    { "id": 2, "email": null },
    { "id": 3, "email": "bob@example.com" },
    { "id": 4, "email": null }
]

var missingEmailCount = CountIf(records, "email", "==", null)
# missingEmailCount is 2

var hasEmailCount = CountIf(records, "email", "!=", null)
# hasEmailCount is 2
```

### Building summary statistics

```jyro
var tickets = [
    { "id": 1, "severity": "high", "status": "open" },
    { "id": 2, "severity": "low", "status": "closed" },
    { "id": 3, "severity": "high", "status": "open" },
    { "id": 4, "severity": "medium", "status": "open" },
    { "id": 5, "severity": "high", "status": "closed" }
]

Data = {
    "totalTickets": Length(tickets),
    "highSeverity": CountIf(tickets, "severity", "==", "high"),
    "openTickets": CountIf(tickets, "status", "==", "open"),
    "closedTickets": CountIf(tickets, "status", "==", "closed")
}
# Result: { "totalTickets": 5, "highSeverity": 3, "openTickets": 3, "closedTickets": 2 }
```

### Combining with Filter

```jyro
var incidents = [
    { "id": 1, "team": "IT", "priority": 1, "status": "open" },
    { "id": 2, "team": "IT", "priority": 2, "status": "closed" },
    { "id": 3, "team": "HR", "priority": 1, "status": "open" },
    { "id": 4, "team": "IT", "priority": 1, "status": "open" }
]

var criticalOpen = CountIf(
    Filter(incidents, "priority", "==", 1),
    "status", "!=", "closed"
)
# criticalOpen is 3
```

### Dynamic counting across categories

```jyro
var products = [
    { "name": "Widget A", "category": "tools" },
    { "name": "Widget B", "category": "parts" },
    { "name": "Widget C", "category": "tools" },
    { "name": "Widget D", "category": "accessories" }
]

var categories = ["tools", "parts", "accessories"]
var categoryCounts = []

foreach category in categories do
    var count = CountIf(products, "category", "==", category)
    Append(categoryCounts, { "category": category, "count": count })
end

# categoryCounts = [
#   { "category": "tools", "count": 2 },
#   { "category": "parts", "count": 1 },
#   { "category": "accessories", "count": 1 }
# ]
```

## Notes

- Supported operators: `"=="`, `"!="`, `"<"`, `"<="`, `">"`, `">="`
- String comparisons are **case-sensitive**. "Active" and "active" are treated as different values
- For case-insensitive comparison, normalize values using the `Lower()` function before comparison
- Non-object elements in the array are skipped and not counted
- Objects missing the specified field are skipped and not counted
- Nested paths traverse objects using dot notation (e.g., "user.profile.age")
- Empty arrays always return 0
- Can be combined with Filter to count elements in a filtered subset
