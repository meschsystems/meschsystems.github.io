---
layout: default
title: Median
parent: Standard Library Functions
has_children: false
has_toc: false
permalink: /jyro/functions/stdlib/math/median/
---

# Median

Finds the median (middle value) of all numeric values in an array.

## Syntax

```jyro
Median(array)
```

## Parameters

- **array** (array): An array of numeric values

## Returns

- **number**: The median of all numeric values in the array, or `null` if the array is empty or contains no numeric values

## Description

Calculates the median by extracting all numeric values from the array, sorting them, and returning the middle value. For an odd count of numbers, returns the middle value. For an even count, returns the average of the two middle values.

Non-numeric items in the array are ignored. Returns `null` if no numeric values are found.

## Examples

### Odd count of values

```jyro
var med = Median([1, 3, 5])  # Returns 3
```

### Even count of values

```jyro
var med = Median([1, 3, 5, 7])  # Returns 4 (average of 3 and 5)
```

### Unsorted input

```jyro
var med = Median([5, 1, 9, 3, 7])  # Returns 5 (middle of sorted: 1,3,5,7,9)
```

### Single value

```jyro
var med = Median([42])  # Returns 42
```

### Statistical analysis

```jyro
var salaries = [45000, 52000, 48000, 150000, 51000]

var avg = Average(salaries)
# Returns 69200 (skewed by outlier)

var med = Median(salaries)
# Returns 51000 (better represents typical salary)
```

## Notes

- Returns `null` if the array is empty or contains no numeric values
- Non-numeric items in the array are silently ignored
- Median is less sensitive to outliers than average
- For calculating average (arithmetic mean), use `Average`
- For calculating mode (most frequent), use `Mode`
