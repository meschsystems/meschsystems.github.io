---
layout: default
title: SelectMany
parent: Standard Library Functions
has_children: false
has_toc: false
permalink: /jyro/functions/stdlib/array/selectmany/
---

# SelectMany

Extracts an array field from each object in the source array and flattens all results into a single array.

## Syntax

```jyro
SelectMany(array, fieldName)
```

## Parameters

- **array** (array): The array of objects to extract from
- **fieldName** (string): The field name or nested path containing arrays to flatten (e.g., "items" or "metadata.tags")

## Returns

- **array**: A new array containing all elements from the extracted array fields, flattened into a single array

## Description

The `SelectMany` function extracts an array-valued field from each object in the source array and concatenates all the extracted arrays into a single flat array. This is useful for flattening nested array structures.

The function supports nested field paths using dot notation. Non-object elements, missing fields, and non-array field values are skipped (they don't contribute to the result).

## Examples

### Flattening nested arrays

```jyro
var orders = [
    { "id": 1, "items": ["apple", "banana"] },
    { "id": 2, "items": ["orange"] },
    { "id": 3, "items": ["grape", "melon", "kiwi"] }
]

var allItems = SelectMany(orders, "items")
# allItems is ["apple", "banana", "orange", "grape", "melon", "kiwi"]
```

### Collecting all tags from documents

```jyro
var documents = [
    { "title": "Doc A", "tags": ["urgent", "review"] },
    { "title": "Doc B", "tags": ["archived"] },
    { "title": "Doc C", "tags": ["urgent", "important", "follow-up"] }
]

var allTags = SelectMany(documents, "tags")
# allTags is ["urgent", "review", "archived", "urgent", "important", "follow-up"]

# Get unique tags
var uniqueTags = Distinct(SelectMany(documents, "tags"))
# uniqueTags is ["urgent", "review", "archived", "important", "follow-up"]
```

### Nested field paths

```jyro
var users = [
    { "profile": { "skills": ["JavaScript", "Python"] } },
    { "profile": { "skills": ["Go", "Rust", "C++"] } }
]

var allSkills = SelectMany(users, "profile.skills")
# allSkills is ["JavaScript", "Python", "Go", "Rust", "C++"]
```

### Counting total items

```jyro
var orders = [
    { "lineItems": [{ "qty": 2 }, { "qty": 1 }] },
    { "lineItems": [{ "qty": 3 }] },
    { "lineItems": [{ "qty": 1 }, { "qty": 2 }, { "qty": 1 }] }
]

var allLineItems = SelectMany(orders, "lineItems")
var totalItems = Sum(Select(allLineItems, "qty"))
# totalItems is 10
```

### Handling missing and non-array fields

```jyro
var items = [
    { "values": [1, 2, 3] },
    { "values": "not an array" },  # Skipped - not an array
    { "other": "field" },          # Skipped - missing "values" field
    { "values": [4, 5] }
]

var result = SelectMany(items, "values")
# result is [1, 2, 3, 4, 5]
```

### Handling non-object elements

```jyro
var mixed = [
    { "arr": ["a", "b"] },
    "string",              # Skipped - not an object
    null,                  # Skipped - not an object
    { "arr": ["c"] }
]

var result = SelectMany(mixed, "arr")
# result is ["a", "b", "c"]
```

## Notes

- The original array is never modified; a new array is always returned
- Non-object elements in the source array are skipped
- Objects missing the specified field are skipped
- Non-array field values are skipped (only arrays are flattened)
- Nested paths traverse objects using dot notation (e.g., "data.items")
- Empty arrays return an empty array
- Can be chained with functions like `Distinct`, `Length`, `Sort`
- Useful for aggregating nested collections (e.g., all items across all orders)
