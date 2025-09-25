---
layout: default
title: ParseDate
parent: Function Integration
has_children: false
has_toc: false
permalink: /jyro/functions/dateandtime/parsedate/
---

# ParseDate

Parses a date string using multiple format patterns and returns a normalized ISO 8601 formatted date string.

## Syntax

```jyro
ParseDate(dateString)
```

## Parameters

- **dateString** (string): The date string to parse

## Returns

- **string**: The parsed date in ISO 8601 format in UTC timezone

## Description

Attempts parsing with common date formats before falling back to general date parsing for maximum compatibility. Supported formats include ISO dates, slash-separated formats, and general date parsing.

## Examples

```jyro
var result1 = ParseDate("2024-06-15")              # ISO format
```

```jyro
var result2 = ParseDate("06/15/2024")              # US format
```

```jyro
var result3 = ParseDate("15/06/2024")              # European format
```

```jyro
var result4 = ParseDate("June 15, 2024")           # Text format
# All return normalized ISO format like "2024-06-15T00:00:00.000Z"
```