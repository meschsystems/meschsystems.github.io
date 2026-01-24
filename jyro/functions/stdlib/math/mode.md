---
layout: default
title: Mode
parent: Standard Library Functions
has_children: false
has_toc: false
permalink: /jyro/functions/stdlib/math/mode/
---

# Mode

Finds the mode (most frequently occurring value) of all numeric arguments.

## Syntax

```jyro
Mode(value1, value2, ...)
```

## Parameters

- **values** (number...): One or more numeric values

## Returns

- **number**: The most frequently occurring value

## Description

Identifies the value that appears most frequently among all numeric arguments. If multiple values have the same highest frequency (a tie), returns the first one encountered in the argument list.

Non-numeric arguments are ignored. Returns zero if no numeric arguments are provided.

## Examples

### Basic mode

```jyro
var m = Mode(1, 2, 2, 3, 3, 3)  # Returns 3 (appears 3 times)
```

### Tie goes to first encountered

```jyro
var m = Mode(1, 1, 2, 2)  # Returns 1 (1 and 2 both appear twice, 1 came first)
```

### All unique values

```jyro
var m = Mode(1, 2, 3, 4, 5)  # Returns 1 (all appear once, first wins)
```

### Single value

```jyro
var m = Mode(42)  # Returns 42
```

### Finding most common category

```jyro
var ratings = [5, 4, 5, 3, 5, 4, 5, 3, 5]
var mostCommon = Mode(ratings[0], ratings[1], ratings[2], ratings[3],
                      ratings[4], ratings[5], ratings[6], ratings[7], ratings[8])
# Returns 5 (the most common rating)
```

### Statistical summary

```jyro
var data = [10, 20, 20, 30, 30, 30, 40]

var avg = Average(data[0], data[1], data[2], data[3], data[4], data[5], data[6])
# Average: ~25.7

var med = Median(data[0], data[1], data[2], data[3], data[4], data[5], data[6])
# Median: 30

var mod = Mode(data[0], data[1], data[2], data[3], data[4], data[5], data[6])
# Mode: 30
```

## Notes

- Returns 0 if no numeric arguments are provided
- Non-numeric arguments are silently ignored
- For continuous data, mode may be less meaningful than average or median
- For calculating average (arithmetic mean), use `Average`
- For calculating median (middle value), use `Median`
