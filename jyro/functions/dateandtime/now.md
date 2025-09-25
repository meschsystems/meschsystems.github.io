---
layout: default
title: Now
parent: Function Integration
has_children: false
has_toc: false
permalink: /jyro/functions/dateandtime/now/
---

# Now

Returns the current date and time as an ISO 8601 formatted string in UTC.

## Syntax

```jyro
Now()
```

## Parameters

None

## Returns

- **string**: The current UTC date and time in ISO 8601 format

## Description

Provides a consistent timestamp format suitable for logging, data processing, and cross-system communication requirements.

## Examples

```jyro
var currentTime = Now()
# Returns something like "2024-09-24T14:30:15.123Z"
```

```jyro
# Can be used for timestamping
Data.processedAt = Now()
Data.created = Now()
```