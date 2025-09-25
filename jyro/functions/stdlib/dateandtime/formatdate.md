---
layout: default
title: FormatDate
parent: Standard Library Functions
has_children: false
has_toc: false
permalink: /jyro/functions/stdlib/dateandtime/formatdate/
---

# FormatDate

Formats a date string according to a specified format pattern using .NET's standard date and time format strings.

## Syntax

```jyro
FormatDate(dateString, formatPattern)
```

## Parameters

- **dateString** (string): The date string to parse and format
- **formatPattern** (string): The format pattern to apply

## Returns

- **string**: The formatted date according to the specified pattern

## Description

Supports both standard and custom format patterns for flexible date presentation. Uses universal time parsing for consistent behavior.

## Examples

```jyro
var dateStr = "2024-06-15T14:30:45.000Z"
var formatted1 = FormatDate(dateStr, "yyyy-MM-dd")           # Returns "2024-06-15"
```

```jyro
var formatted2 = FormatDate(dateStr, "MMM dd, yyyy")         # Returns "Jun 15, 2024"
```

```jyro
var formatted3 = FormatDate(dateStr, "HH:mm:ss")             # Returns "14:30:45"
```

```jyro
var formatted4 = FormatDate(dateStr, "dddd, MMMM dd, yyyy")  # Returns day and full date
```