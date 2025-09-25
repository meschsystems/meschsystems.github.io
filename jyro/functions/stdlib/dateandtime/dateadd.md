---
layout: default
title: DateAdd
parent: Standard Library Functions
has_children: false
has_toc: false
permalink: /jyro/functions/stdlib/dateandtime/dateadd/
---

# DateAdd

Adds a specified amount of time to a date, supporting various time units.

## Syntax

```jyro
DateAdd(date, unit, amount)
```

## Parameters

- **date** (string): The base date string to modify
- **unit** (string): The time unit for the addition
- **amount** (number): The amount to add (must be integer)

## Returns

- **string**: The modified date in ISO 8601 format

## Description

Adds the specified time amount to the date using the given unit. Valid units are: days, weeks, months, years, hours, minutes, seconds (singular and plural forms accepted). Returns the result as an ISO 8601 formatted string.

## Examples

```jyro
var baseDate = "2024-01-15T10:30:00.000Z"
var nextWeek = DateAdd(baseDate, "days", 7)
# Returns "2024-01-22T10:30:00.000Z"
```

```jyro
var futureDate = DateAdd("2024-06-01", "months", 3)
# Returns "2024-09-01T00:00:00.000Z"
```

```jyro
var laterTime = DateAdd("2024-01-01T12:00:00.000Z", "hours", 2)
# Returns "2024-01-01T14:00:00.000Z"
```