---
layout: default
title: Pop
parent: Standard Library Functions
has_children: false
has_toc: false
permalink: /jyro/functions/stdlib/array/pop/
---

# Pop

Removes and returns the last element from an array (stack pop operation).

## Syntax

```jyro
Pop(array)
```

## Parameters

- **array** (array): The array to modify

## Returns

- **any**: The removed last element, or null if the array is empty

## Description

Implements the classic stack pop operation: removes the last element from an array and returns that element. The array is modified in-place, with its length reduced by one.

This function is specifically designed for cases where you need the value of the removed element. If you only need to remove the last element without using its value, use RemoveLast instead, which returns the array to enable chaining.

Returns null if the array is empty, making it safe to call on any array.

## Examples

```jyro
var stack = [1, 2, 3, 4, 5]
var top = Pop(stack)
# top is 5
# stack is now [1, 2, 3, 4]
```

```jyro
var items = ["apple", "banana", "orange"]
var last = Pop(items)
# last is "orange"
# items is now ["apple", "banana"]
```

```jyro
var empty = []
var nothing = Pop(empty)
# nothing is null
# empty is still []
```

```jyro
# Classic stack pattern
var undoStack = []
Append(undoStack, "action1")
Append(undoStack, "action2")
Append(undoStack, "action3")

var lastAction = Pop(undoStack)
# lastAction is "action3"
# undoStack is now ["action1", "action2"]
```

```jyro
# Safe processing with check
var queue = GetWorkItems()
if Last(queue) != null then
    var item = Pop(queue)
    ProcessItem(item)
end
```

```jyro
# Processing all elements
var tasks = ["task1", "task2", "task3"]
while Length(tasks) > 0 do
    var task = Pop(tasks)
    ExecuteTask(task)
end
# tasks is now []
```

```jyro
# Comparing with RemoveLast
var numbers = [1, 2, 3, 4, 5]

# Use Pop when you need the element
var value = Pop(numbers)
# value is 5, numbers is [1, 2, 3, 4]

# Use RemoveLast for chaining
var length = Length(RemoveLast(numbers))
# length is 3, numbers is [1, 2, 3]
```

## Notes

- The array is modified in-place
- Returns the removed element (not the array)
- Returns null for empty arrays (does not throw an error)
- Use RemoveLast if you want to chain operations and don't need the element value
- Implements standard stack (LIFO - Last In, First Out) semantics
- Safe to call on empty arrays
