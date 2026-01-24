---
layout: default
title: Substring
parent: Standard Library Functions
has_children: false
has_toc: false
permalink: /jyro/functions/stdlib/string/substring/
---

# Substring

Extracts a portion of a string starting at a specified position.

## Syntax

```jyro
Substring(text, start)
Substring(text, start, length)
```

## Parameters

- **text** (string): The source string to extract from
- **start** (number): The zero-based starting position (must be integer)
- **length** (number, optional): The number of characters to extract. If omitted, extracts to the end of the string

## Returns

- **string**: The extracted substring

## Description

Extracts a portion of a string starting at the specified position. If a length is provided, extracts that many characters; otherwise extracts from the start position to the end of the string.

Handles edge cases gracefully:
- Negative start indices are treated as 0
- Start positions beyond the string length return an empty string
- Length values that would exceed the string are automatically clamped
- Zero or negative length values return an empty string

## Examples

### Basic extraction

```jyro
var result = Substring("Hello World", 0, 5)  # Returns "Hello"
```

### Extract to end of string

```jyro
var result = Substring("Hello World", 6)  # Returns "World"
```

### Extract middle portion

```jyro
var email = "user@example.com"
var domain = Substring(email, 5)  # Returns "example.com"
```

### With calculated positions

```jyro
var filename = "document.pdf"
var extension = Substring(filename, 9, 3)  # Returns "pdf"
```

### Edge case handling

```jyro
var result1 = Substring("Hello", 10)     # Returns "" (start beyond length)
var result2 = Substring("Hello", 0, 100) # Returns "Hello" (length clamped)
var result3 = Substring("Hello", -5, 3)  # Returns "Hel" (negative start treated as 0)
```

## Notes

- Uses zero-based indexing (first character is at position 0)
- The function never throws for out-of-bounds values; it returns empty string or clamped results
- For finding the position of a substring, use `PositionOf`
