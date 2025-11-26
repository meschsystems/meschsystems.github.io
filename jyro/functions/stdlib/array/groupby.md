---
layout: default
title: GroupBy
parent: Standard Library Functions
has_children: false
has_toc: false
permalink: /jyro/functions/stdlib/array/groupby/
---

# GroupBy

Groups an array of objects by a specified field, returning an object where keys are the distinct field values and values are arrays of matching items.

## Syntax

```jyro
GroupBy(array, fieldName)
```

## Parameters

- **array** (array): The array of objects to group
- **fieldName** (string): The field name or nested path to group by (e.g., "status" or "address.city")

## Returns

- **object**: An object where each key is a distinct field value (as a string) and each value is an array of items with that field value

## Description

The `GroupBy` function organizes an array of objects into groups based on the values of a specified field. It returns a new object where:

- Each key represents a unique value found in the specified field
- Each value is an array containing all items that have that field value

The function supports nested field paths using dot notation, allowing you to group by deeply nested properties. All field values are converted to strings to serve as object keys.

Non-object elements in the input array are silently skipped. Items with null or missing field values are grouped together under the key `"null"`. The original array is not modified.

## Examples

### Basic grouping

```jyro
var orders = [
    { "id": 1, "status": "pending", "amount": 100 },
    { "id": 2, "status": "completed", "amount": 200 },
    { "id": 3, "status": "pending", "amount": 150 },
    { "id": 4, "status": "completed", "amount": 50 }
]

var byStatus = GroupBy(orders, "status")
# byStatus is:
# {
#   "pending": [{ "id": 1, ... }, { "id": 3, ... }],
#   "completed": [{ "id": 2, ... }, { "id": 4, ... }]
# }

# Access a specific group:
var pendingOrders = byStatus["pending"]
# pendingOrders is [{ "id": 1, ... }, { "id": 3, ... }]
```

### Grouping with nested field paths

```jyro
var employees = [
    { "name": "Alice", "address": { "city": "New York" } },
    { "name": "Bob", "address": { "city": "Los Angeles" } },
    { "name": "Carol", "address": { "city": "New York" } },
    { "name": "Dave", "address": { "city": "Chicago" } }
]

var byCity = GroupBy(employees, "address.city")
# byCity is:
# {
#   "New York": [{ "name": "Alice", ... }, { "name": "Carol", ... }],
#   "Los Angeles": [{ "name": "Bob", ... }],
#   "Chicago": [{ "name": "Dave", ... }]
# }
```

### Handling null and missing values

```jyro
var items = [
    { "id": 1, "category": "A" },
    { "id": 2, "category": null },
    { "id": 3 },
    { "id": 4, "category": "A" }
]

var byCategory = GroupBy(items, "category")
# byCategory is:
# {
#   "A": [{ "id": 1, ... }, { "id": 4, ... }],
#   "null": [{ "id": 2, ... }, { "id": 3, ... }]
# }
```

### Grouping by numeric field

```jyro
var tasks = [
    { "name": "Task A", "priority": 1 },
    { "name": "Task B", "priority": 2 },
    { "name": "Task C", "priority": 1 },
    { "name": "Task D", "priority": 3 }
]

var byPriority = GroupBy(tasks, "priority")
# byPriority is:
# {
#   "1": [{ "name": "Task A", ... }, { "name": "Task C", ... }],
#   "2": [{ "name": "Task B", ... }],
#   "3": [{ "name": "Task D", ... }]
# }

# Access priority 1 tasks:
var highPriority = byPriority["1"]
```

### Grouping by boolean field

```jyro
var todos = [
    { "task": "Write docs", "done": true },
    { "task": "Fix bug", "done": false },
    { "task": "Review PR", "done": true }
]

var byDone = GroupBy(todos, "done")
# byDone is:
# {
#   "True": [{ "task": "Write docs", ... }, { "task": "Review PR", ... }],
#   "False": [{ "task": "Fix bug", ... }]
# }
```

### Combining with other functions

```jyro
var transactions = [
    { "id": 1, "type": "credit", "amount": 100, "date": "2024-01-15" },
    { "id": 2, "type": "debit", "amount": 50, "date": "2024-01-10" },
    { "id": 3, "type": "credit", "amount": 200, "date": "2024-01-20" },
    { "id": 4, "type": "debit", "amount": 75, "date": "2024-01-05" }
]

# Group by type, then sort each group by date
var byType = GroupBy(transactions, "type")
var sortedCredits = SortByField(byType["credit"], "date", "asc")
var sortedDebits = SortByField(byType["debit"], "date", "asc")

# Count items in each group
var creditCount = Length(byType["credit"])  # 2
var debitCount = Length(byType["debit"])    # 2
```

### Iterating over groups

```jyro
var products = [
    { "name": "Widget", "category": "Electronics" },
    { "name": "Gadget", "category": "Electronics" },
    { "name": "Chair", "category": "Furniture" }
]

var byCategory = GroupBy(products, "category")

# Iterate over all groups
foreach categoryName in byCategory do
    var items = byCategory[categoryName]
    Data.summary = Data.summary + categoryName + ": " + Length(items) + " items\n"
end
```

## Notes

- The original array is never modified; a new object is returned
- Non-object elements in the input array are silently skipped
- Items with null or missing field values are grouped under the key `"null"`
- All field values are converted to strings to serve as object keys:
  - Numbers: `1` becomes `"1"`
  - Booleans: `true` becomes `"True"`, `false` becomes `"False"`
  - Strings: used as-is
- Nested paths traverse objects using dot notation (e.g., "user.profile.role")
- Empty arrays return an empty object
- The order of items within each group matches their order in the original array
- Can be combined with other array functions like Filter, SortByField, and Length
