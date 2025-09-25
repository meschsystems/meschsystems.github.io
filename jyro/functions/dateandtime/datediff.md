---
layout: default
title: DateDiff
parent: Function Integration
has_children: false
has_toc: false
permalink: /jyro/functions/dateandtime/datediff/
---

# DateDiff

Calculates the difference between two dates in the specified time unit.

## Syntax

```jyro
DateDiff(endDate, startDate, unit)
```

## Parameters

- **endDate** (string): The end date string
- **startDate** (string): The start date string  
- **unit** (string): The time unit for the result

## Returns

- **number**: The calculated time difference (positive if end date is later)

## Description

Calculates the difference as (end date - start date). Valid units are: days, weeks, months, years, hours, minutes, seconds. Month and year calculations use approximate values (30.44 days per month, 365.25 days per year).

## Examples

```jyro
var start = "2024-01-01T00:00:00.000Z"
var end = "2024-01-08T00:00:00.000Z"
var daysDiff = DateDiff(end, start, "days")  # Returns 7.0
```

```jyro
var timeDiff = DateDiff("2024-01-01T14:00:00.000Z", "2024-01-01T12:00:00.000Z", "hours")
# Returns 2.0
```