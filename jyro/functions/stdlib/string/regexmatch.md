---
layout: default
title: RegexMatch
parent: Standard Library Functions
has_children: false
has_toc: false
permalink: /jyro/functions/stdlib/string/regexmatch/
---

# RegexMatch

Extracts the first regex match from text as a string.

## Syntax

```jyro
RegexMatch(text, pattern)
```

## Parameters

- **text** (string): The source text to search
- **pattern** (string): The regex pattern to match

## Returns

- **string**: The first matching substring, or **null** if no match is found

## Description

Searches the input text for the first occurrence of the specified regex pattern and returns the matched string. Returns null if no match is found.

This function is designed for composability with other string functions. The simple string return type allows direct chaining with functions like `Upper()`, `Lower()`, `Length()`, `Replace()`, etc.

For access to capture groups or match position, use `RegexMatchDetail()` instead.

## Examples

### Basic match extraction

```jyro
var email = RegexMatch("Contact: john@example.com", "[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+[.][a-zA-Z]{2,}")
# Returns "john@example.com"
```

### Chaining with string functions

```jyro
var upperEmail = Upper(RegexMatch(text, "[a-z]+@[a-z]+[.][a-z]+"))
# Extract and uppercase in one expression
```

```jyro
var digitCount = Length(RegexMatch(data, "[0-9]+"))
# Get length of first number found
```

### Extract specific patterns

```jyro
var url = RegexMatch(content, "https?://[^ ]+")
# Extract first URL
```

### No match returns null

```jyro
var result = RegexMatch("Hello World", "[0-9]+")
# Returns null (no digits in text)
```

## Notes

- Uses .NET regular expression syntax
- Throws a runtime exception if the regex pattern is invalid
- For multiple matches, use `RegexMatchAll()`
- For capture groups and match metadata, use `RegexMatchDetail()`

## Pattern Escaping in Jyro Strings

Jyro strings support a subset of escape sequences (`\n`, `\t`, `\r`, `\"`, `\\`). Common regex shortcuts like `\d` or `\w` require character class alternatives.

Use character classes instead:

| Instead of | Use |
|------------|-----|
| `\d` | `[0-9]` |
| `\w` | `[a-zA-Z0-9_]` |
| `\s` | `[ \t\n\r]` |
| `\.` | `[.]` |

```jyro
# This will not work:
var num = RegexMatch(text, "\d+")

# Use this instead:
var num = RegexMatch(text, "[0-9]+")
```
