---
layout: default
title: ToNumber
parent: Standard Library Functions
has_children: false
has_toc: false
permalink: /jyro/functions/stdlib/string/tonumber/
---

# ToNumber

Converts a string representation of a number to a numeric value.

## Syntax

```jyro
ToNumber(text)
```

## Parameters

- **text** (string): The string to convert to a number

## Returns

- **number**: The numeric value parsed from the input string, or 0 if the string cannot be parsed

## Description

Parses numeric strings using culture-invariant formatting rules to ensure consistent number parsing behavior across different system locales and cultural settings. If the string cannot be parsed as a valid number, the function returns zero.

This function is particularly useful for converting form input, query parameters, or user-provided text into numeric values for mathematical operations or database storage.

## Examples

```jyro
var result1 = ToNumber("123")          # Returns 123
```

```jyro
var result2 = ToNumber("45.67")        # Returns 45.67
```

```jyro
var result3 = ToNumber("-89.2")        # Returns -89.2
```

```jyro
var result4 = ToNumber("invalid")      # Returns 0
```

```jyro
var result5 = ToNumber("")             # Returns 0
```

```jyro
# Common use case: Converting form data
var userId = ToNumber(Data.request.body.id)
var user = GetUser(userId)
```

```jyro
# Common use case: Converting query parameters
var pageNumber = ToNumber(Data.request.query.page)
var items = GetItemsForPage(pageNumber)
```
