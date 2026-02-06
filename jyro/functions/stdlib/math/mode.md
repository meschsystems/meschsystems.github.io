---
layout: default
title: Mode
parent: Standard Library Functions
has_children: false
has_toc: false
permalink: /jyro/functions/stdlib/math/mode/
---

# Mode

Finds the mode (most frequently occurring value) of all numeric values in an array.

## Syntax

```jyro
Mode(array)
```

## Parameters

- **array** (array): An array of numeric values

## Returns

- **number**: The most frequently occurring numeric value, or `null` if the array is empty or contains no numeric values

## Description

Identifies the numeric value that appears most frequently in the array. If multiple values share the same highest frequency (a tie), returns the first one encountered during iteration.

Non-numeric items in the array are ignored. Returns `null` if no numeric values are found.

## Examples

### Basic mode

```jyro
var m = Mode([1, 2, 2, 3, 3, 3])  # Returns 3 (appears 3 times)
```

### Tie goes to first encountered

```jyro
var m = Mode([1, 1, 2, 2])  # Returns 1 (1 and 2 both appear twice, 1 came first)
```

### All unique values

```jyro
var m = Mode([1, 2, 3, 4, 5])  # Returns 1 (all appear once, first wins)
```

### Single value

```jyro
var m = Mode([42])  # Returns 42
```

### Finding most common rating

```jyro
var ratings = [5, 4, 5, 3, 5, 4, 5, 3, 5]
var mostCommon = Mode(ratings)
# Returns 5 (the most common rating)
```

### Statistical summary

```jyro
var data = [10, 20, 20, 30, 30, 30, 40]

var avg = Average(data)   # ~25.7
var med = Median(data)    # 30
var mod = Mode(data)      # 30
```

## Notes

- Returns `null` if the array is empty or contains no numeric values
- Non-numeric items in the array are silently ignored
- For continuous data, mode may be less meaningful than average or median
- For calculating average (arithmetic mean), use `Average`
- For calculating median (middle value), use `Median`
