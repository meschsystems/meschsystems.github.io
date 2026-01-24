---
layout: default
title: Average
parent: Standard Library Functions
has_children: false
has_toc: false
permalink: /jyro/functions/stdlib/math/average/
---

# Average

Calculates the arithmetic mean of all numeric arguments.

## Syntax

```jyro
Average(value1, value2, ...)
```

## Parameters

- **values** (number...): One or more numeric values to average

## Returns

- **number**: The arithmetic mean of all provided numeric values

## Description

Calculates the arithmetic mean (average) by summing all numeric arguments and dividing by the count. Non-numeric arguments are ignored. Returns zero if no numeric arguments are provided.

## Examples

### Basic average

```jyro
var avg = Average(10, 20, 30)  # Returns 20
```

### Average with decimals

```jyro
var avg = Average(1.5, 2.5, 3.0)  # Returns 2.333...
```

### Single value

```jyro
var avg = Average(42)  # Returns 42
```

### Calculate grade average

```jyro
var grades = [85, 92, 78, 95, 88]
var avg = Average(grades[0], grades[1], grades[2], grades[3], grades[4])
# Returns 87.6
```

### With Sum for comparison

```jyro
var numbers = [10, 20, 30, 40, 50]
var total = Sum(numbers[0], numbers[1], numbers[2], numbers[3], numbers[4])
var count = Length(numbers)
var manualAvg = total / count  # 30

var funcAvg = Average(numbers[0], numbers[1], numbers[2], numbers[3], numbers[4])
# Both equal 30
```

## Notes

- Returns 0 if no numeric arguments are provided
- Non-numeric arguments are silently ignored
- For calculating median (middle value), use `Median`
- For calculating mode (most frequent), use `Mode`
- Related: `Sum`, `Min`, `Max`
