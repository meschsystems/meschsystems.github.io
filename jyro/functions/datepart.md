---
layout: default
title: DatePart
parent: Function Integration
has_children: false
has_toc: false
permalink: /jyro/functions/datepart/
---

# DatePart

Extracts a specific component from a date string, returning the component as a numeric value.

## Syntax

```jyro
DatePart(dateString, partName)
```

## Parameters

- **dateString** (string): The date string to parse
- **partName** (string): The part name to extract

## Returns

- **number**: The requested date component value

## Description

Extracts date components including year, month, day, hour, minute, second, dayofweek, and dayofyear. Day of week returns 0-6 (Sunday=0).

## Examples

```jyro
var dateStr = "2024-06-15T14:30:45.000Z"
var year = DatePart(dateStr, "year")      # Returns 2024
```

```jyro
var month = DatePart(dateStr, "month")    # Returns 6
```

```jyro
var hour = DatePart(dateStr, "hour")      # Returns 14
```

```jyro
var dayOfWeek = DatePart(dateStr, "dayofweek")  # Returns day of week (0-6)
```