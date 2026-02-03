---
layout: default
title: RegexMatchDetail
parent: Standard Library Functions
has_children: false
has_toc: false
permalink: /jyro/functions/stdlib/string/regexmatchdetail/
---

# RegexMatchDetail

Extracts the first regex match from text with full metadata including the matched string, index position, and capture groups.

## Syntax

```jyro
RegexMatchDetail(text, pattern)
```

## Parameters

- **text** (string): The source text to search
- **pattern** (string): The regex pattern to match (may include capture groups)

## Returns

- **object**: An object containing match details, or **null** if no match is found

The returned object has the following properties:
- **match** (string): The full matched string
- **index** (number): The zero-based position where the match starts in the source text
- **groups** (array): An array of captured group values (excluding the full match)

## Description

Searches the input text for the first occurrence of the specified regex pattern and returns detailed information about the match, including any captured groups.

Use this function when you need access to capture groups or the match position. For simpler use cases where you only need the matched string, prefer `RegexMatch()` for better composability.

## Examples

### Extract with capture groups

```jyro
var result = RegexMatchDetail("Contact: john@example.com", "([a-zA-Z]+)@([a-zA-Z]+)[.]([a-zA-Z]+)")
# result.match = "john@example.com"
# result.index = 9
# result.groups[0] = "john"
# result.groups[1] = "example"
# result.groups[2] = "com"
```

### Parse structured data

```jyro
var dateResult = RegexMatchDetail("Date: 2024-03-15", "([0-9]{4})-([0-9]{2})-([0-9]{2})")
var year = dateResult.groups[0]   # "2024"
var month = dateResult.groups[1]  # "03"
var day = dateResult.groups[2]    # "15"
```

### Extract URL components

```jyro
var urlResult = RegexMatchDetail(text, "(https?)://([^/]+)(/.+)?")
var protocol = urlResult.groups[0]  # "https"
var domain = urlResult.groups[1]    # "example.com"
var path = urlResult.groups[2]      # "/page/123"
```

### Get match position

```jyro
var result = RegexMatchDetail("Find the number 42 here", "[0-9]+")
var position = result.index  # 16 (position of "42")
```

### No match returns null

```jyro
var result = RegexMatchDetail("Hello World", "[0-9]+")
# Returns null (no digits in text)
```

### Check before accessing properties

```jyro
var result = RegexMatchDetail(input, "([a-zA-Z]+)@([a-zA-Z]+)")
if result != null
    var username = result.groups[0]
    var domain = result.groups[1]
end
```

## Notes

- Uses .NET regular expression syntax
- Throws a runtime exception if the regex pattern is invalid
- Capture groups are numbered starting from 0 in the groups array
- Groups that don't participate in a match return empty strings
- For simpler use cases, prefer `RegexMatch()` which returns just the matched string

## Pattern Escaping in Jyro Strings

Jyro strings support a subset of escape sequences (`\n`, `\t`, `\r`, `\"`, `\\`). Common regex shortcuts like `\d` or `\w` require character class alternatives.

Use character classes instead:

| Instead of | Use |
|------------|-----|
| `\d` | `[0-9]` |
| `\w` | `[a-zA-Z0-9_]` |
| `\s` | `[ \t\n\r]` |
| `\.` | `[.]` |
