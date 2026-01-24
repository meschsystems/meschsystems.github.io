---
layout: default
title: PositionOf
parent: Standard Library Functions
has_children: false
has_toc: false
permalink: /jyro/functions/stdlib/string/positionof/
---

# PositionOf

Finds the zero-based index position of a substring within a string.

## Syntax

```jyro
PositionOf(text, search)
```

## Parameters

- **text** (string): The source string to search within
- **search** (string): The substring to find

## Returns

- **number**: The zero-based index of the first occurrence of the substring, or -1 if not found

## Description

Searches for a substring within a string and returns its position. The search is case-sensitive. This function is the string equivalent of `IndexOf` for arrays.

## Examples

### Basic usage

```jyro
var pos = PositionOf("Hello World", "World")  # Returns 6
```

### Substring not found

```jyro
var pos = PositionOf("Hello World", "xyz")  # Returns -1
```

### Case-sensitive search

```jyro
var pos1 = PositionOf("Hello World", "world")  # Returns -1 (case mismatch)
var pos2 = PositionOf("Hello World", "World")  # Returns 6
```

### Finding a single character

```jyro
var pos = PositionOf("user@example.com", "@")  # Returns 4
```

### Checking if substring exists

```jyro
var email = "user@example.com"
if PositionOf(email, "@") != -1 then
    Data.isEmail = true
end
```

### Use with Substring

```jyro
var email = "user@example.com"
var atPos = PositionOf(email, "@")
if atPos != -1 then
    var username = Substring(email, 0, atPos)     # "user"
    var domain = Substring(email, atPos + 1)      # "example.com"
end
```

## Notes

- Returns the position of the first occurrence if the substring appears multiple times
- Returns -1 if the substring is not found (not an error)
- For checking existence without needing the position, you can also use `Contains`
- For finding elements in arrays, use `IndexOf`
