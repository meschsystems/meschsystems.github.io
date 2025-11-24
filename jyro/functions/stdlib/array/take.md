---
layout: default
title: Take
parent: Standard Library Functions
has_children: false
has_toc: false
permalink: /jyro/functions/stdlib/array/take/
---

# Take

Returns a new array containing the first n elements from a source array without modifying the original.

## Syntax

```jyro
Take(array, count)
```

## Parameters

- **array** (array): The source array to take elements from
- **count** (number): The number of elements to take from the beginning (must be integer)

## Returns

- **array**: A new array containing the first n elements, or an empty array if count is zero or negative

## Description

Creates a new array containing the first `count` elements from the source array. The original array is never modified. If `count` is greater than the array length, all elements are returned. If `count` is zero or negative, an empty array is returned.

Unlike `First` which returns a single element, `Take` always returns an array, making it ideal for pagination, limiting results, or processing batches of data.

## Examples

```jyro
var numbers = [1, 2, 3, 4, 5]
var first_three = Take(numbers, 3)
# first_three is [1, 2, 3]
# numbers is still [1, 2, 3, 4, 5]
```

```jyro
var items = ["apple", "banana", "orange", "grape"]
var top_two = Take(items, 2)
# top_two is ["apple", "banana"]
```

```jyro
# Count greater than array length returns all elements
var numbers = [1, 2, 3]
var result = Take(numbers, 10)
# result is [1, 2, 3]
```

```jyro
# Zero or negative count returns empty array
var numbers = [1, 2, 3, 4, 5]
var empty = Take(numbers, 0)
# empty is []
```

```jyro
# Pagination example
var all_items = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
var page_size = 3
var page_one = Take(all_items, page_size)
# page_one is [1, 2, 3]
```

```jyro
# Top scorers example
var scores = [
    { "name": "Alice", "score": 95 },
    { "name": "Bob", "score": 87 },
    { "name": "Charlie", "score": 92 },
    { "name": "Diana", "score": 88 }
]

var sorted = SortByField(scores, "score", false)
var top_three = Take(sorted, 3)
# top_three contains the three highest scorers
```

```jyro
# Processing batches
var work_queue = GetAllTasks()
var batch = Take(work_queue, 5)

foreach task in batch do
    ProcessTask(task)
end
# Processes first 5 tasks without modifying work_queue
```

```jyro
# Preview pattern
var search_results = PerformSearch(query)
var preview = Take(search_results, 10)
Data.preview = preview
Data.total_count = Length(search_results)
# Shows first 10 results with total count
```

```jyro
# Safe take with Filter
var active_users = Filter(users, "status", "==", "active")
var recent_active = Take(active_users, 5)
# Gets up to 5 active users, handles cases where there are fewer
```

## Notes

- The original array is never modified
- Always returns a new array (even when taking 1 element)
- Count must be an integer; non-integer values throw an error
- Count greater than array length returns all elements
- Count of zero or negative returns an empty array
- Works with arrays containing any type of elements (numbers, strings, objects, nested arrays)
- Ideal for pagination, limiting results, or batch processing
- Use with `First` when you need a single element instead of an array
- Combine with `Sort` or `SortByField` to get top N elements
