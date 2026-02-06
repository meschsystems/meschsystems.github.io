---
layout: default
title: Average
parent: Standard Library Functions
has_children: false
has_toc: false
permalink: /jyro/functions/stdlib/math/average/
---

# Average

Calculates the arithmetic mean of all numeric values in an array.

## Syntax

```jyro
Average(array)
```

## Parameters

- **array** (array): An array of numeric values

## Returns

- **number**: The arithmetic mean of all numeric values in the array, or `null` if the array is empty or contains no numeric values

## Description

Calculates the arithmetic mean (average) by summing all numeric values in the array and dividing by their count. Non-numeric items in the array are ignored. Returns `null` if no numeric values are found.

`Avg` is an alias for `Average` with identical behaviour.

## Examples

### Basic average

```jyro
var avg = Average([10, 20, 30])  # Returns 20
```

### Average with decimals

```jyro
var avg = Average([1.5, 2.5, 3.0])  # Returns 2.333...
```

### Single value

```jyro
var avg = Average([42])  # Returns 42
```

### Calculate grade average

```jyro
var grades = [85, 92, 78, 95, 88]
var avg = Average(grades)
# Returns 87.6
```

### With Sum for comparison

```jyro
var numbers = [10, 20, 30, 40, 50]
var total = Sum(numbers)
var count = Length(numbers)
var manualAvg = total / count  # 30

var funcAvg = Average(numbers)
# Both equal 30
```

## Notes

- Returns `null` if the array is empty or contains no numeric values
- Non-numeric items in the array are silently ignored
- `Avg` is an alias with identical behaviour
- For calculating median (middle value), use `Median`
- For calculating mode (most frequent), use `Mode`
- Related: `Sum`, `Min`, `Max`
