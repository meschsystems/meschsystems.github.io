---
layout: default
title: Jyro 0.8.0 - Standard Library Consistency Update
parent: Blog
permalink: /jyro/blog/jyro-0.8.0-release/
---

# Jyro 0.8.0: Standard Library Consistency Update

*January 2026*

Jyro 0.8.0 focuses on improving consistency across the standard library ahead of the 1.0 release. This update addresses several API inconsistencies that could cause confusion or bugs in production scripts. While this release includes breaking changes, the improvements establish a more predictable and intuitive API surface.

## Breaking Changes

### 1. `PositionOf` Removed - Use `IndexOf` Instead

The `PositionOf` function has been removed. The `IndexOf` function is now polymorphic and works with both strings and arrays:

```jyro
# Before (0.7.x)
var pos = PositionOf("Hello World", "World")  # String search
var idx = IndexOf(myArray, searchValue)        # Array search

# After (0.8.0)
var pos = IndexOf("Hello World", "World")     # String search
var idx = IndexOf(myArray, searchValue)        # Array search
```

This aligns with `Contains`, which already works polymorphically on both types.

### 2. `DateAdd` Parameter Order Changed

The `DateAdd` function now places the `unit` parameter last, matching `DateDiff`:

```jyro
# Before (0.7.x)
var nextWeek = DateAdd("2024-01-15", "days", 7)

# After (0.8.0)
var nextWeek = DateAdd("2024-01-15", 7, "days")
```

This reads more naturally ("add 7 days") and matches the parameter order in `DateDiff(endDate, startDate, unit)`.

### 3. Empty Aggregations Return `null` Instead of `0`

The `Sum`, `Average`, `Median`, and `Mode` functions now return `null` when called with no numeric arguments, matching the existing behavior of `Max` and `Min`:

```jyro
# Before (0.7.x)
var total = Sum()      # Returned 0
var avg = Average()    # Returned 0

# After (0.8.0)
var total = Sum()      # Returns `null`
var avg = Average()    # Returns `null`
```

This is mathematically correct—the sum or average of nothing is undefined, not zero. Update your scripts to handle null if you rely on this edge case.

### 4. `GroupBy` Boolean Keys Now Lowercase

When grouping by a boolean field, keys are now `"true"` and `"false"` (lowercase) instead of `"True"` and `"False"`:

```jyro
var byStatus = GroupBy(tasks, "done")

# Before (0.7.x)
var completed = byStatus["True"]

# After (0.8.0)
var completed = byStatus["true"]
```

This aligns with JSON conventions and the `TypeOf` function, which already returns lowercase type names.

## New Features

### Statistical Functions Accept Arrays

All statistical functions (`Sum`, `Average`, `Median`, `Mode`, `Max`, `Min`) now accept a single array argument, eliminating awkward element-by-element expansion:

```jyro
# Before (0.7.x)
var grades = [85, 92, 78, 95, 88]
var avg = Average(grades[0], grades[1], grades[2], grades[3], grades[4])

# After (0.8.0)
var grades = [85, 92, 78, 95, 88]
var avg = Average(grades)  # Much cleaner!
```

Both syntaxes work—variadic arguments are still supported for inline usage like `Sum(1, 2, 3)`.

### `RandomChoice` Returns `null` on Empty Arrays

Previously, `RandomChoice([])` threw an error. It now returns `null`, consistent with `First`, `Last`, and `Pop`:

```jyro
var items = []
var choice = RandomChoice(items)  # Returns `null` instead of throwing
```

## Internal Improvements

### Consistent Parameter Naming

String functions now use consistent parameter naming. The first parameter is named `text` across `Split`, `Contains`, `StartsWith`, and `EndsWith`. This improves error messages and IDE tooling but doesn't affect script behavior.

### Documentation Corrections

The `Length` function is now correctly categorized under Array Operations in the documentation index (it was incorrectly listed under Utility Functions).

## Migration Guide

1. **Search for `PositionOf`** - Replace all occurrences with `IndexOf`
2. **Search for `DateAdd`** - Swap the second and third arguments
3. **Search for `GroupBy` with boolean fields** - Update key access from `"True"`/`"False"` to `"true"`/`"false"`
4. **Review aggregation edge cases** - If you rely on `Sum()` or `Average()` returning `0` for empty inputs, add null checks

## Looking Ahead

These consistency improvements lay the groundwork for Jyro 1.0. The API surface is now more predictable:

- Polymorphic functions (`Contains`, `IndexOf`) work uniformly across types
- Parameter ordering follows consistent patterns
- Return values for edge cases are uniform across similar functions
- String representations align with JSON conventions

We recommend updating to 0.8.0 before the 1.0 release to address these breaking changes incrementally.

---

*Full changelog and documentation available at [jyro.meschsystems.com](https://meschsystems.github.io/jyro/)*
