---
layout: default
title: Today
parent: Function Integration
has_children: false
has_toc: false
permalink: /jyro/functions/dateandtime/today/
---

# Today

Returns the current date in UTC timezone as an ISO 8601 formatted date string.

## Syntax

```jyro
Today()
```

## Parameters

None

## Returns

- **string**: The current UTC date in ISO 8601 format (yyyy-MM-dd)

## Description

Provides a consistent date representation without time components, suitable for date-only operations and comparisons across different time zones.

## Examples

```jyro
var currentDate = Today()
# Returns something like "2024-09-24"
```

```jyro
# Can be used for date-based logic
if Equal(Data.scheduledDate, Today()) then
    ProcessScheduledTask()
end
```