---
layout: default
title: RegexMatchAll
parent: Standard Library Functions
has_children: false
has_toc: false
permalink: /jyro/functions/stdlib/string/regexmatchall/
---

# RegexMatchAll

Extracts all regex matches from text as an array of strings.

## Syntax

```jyro
RegexMatchAll(text, pattern)
```

## Parameters

- **text** (string): The source text to search
- **pattern** (string): The regex pattern to match

## Returns

- **array**: An array of all matching substrings, or an empty array if no matches are found

## Description

Searches the input text for all occurrences of the specified regex pattern and returns them as an array of strings. Returns an empty array if no matches are found.

This function is designed for composability with array functions. The array return type allows direct chaining with functions like `First()`, `Last()`, `Length()`, `Filter()`, `Join()`, etc.

## Examples

### Extract all matches

```jyro
var emails = RegexMatchAll("Contact john@example.com or jane@test.org", "[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+")
# Returns ["john@example.com", "jane@test.org"]
```

### Chaining with array functions

```jyro
var emailCount = Length(RegexMatchAll(text, "[a-z]+@[a-z]+[.][a-z]+"))
# Count all email addresses
```

```jyro
var firstEmail = First(RegexMatchAll(document, "[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+"))
# Get the first email found
```

```jyro
var allNumbers = Join(RegexMatchAll(data, "[0-9]+"), ", ")
# Join all numbers with commas
```

### Extract all URLs

```jyro
var urls = RegexMatchAll(htmlContent, "https?://[^ \"'<>]+")
# Returns array of all URLs found
```

### Extract all words

```jyro
var words = RegexMatchAll("Hello, World! How are you?", "[a-zA-Z]+")
# Returns ["Hello", "World", "How", "are", "you"]
```

### No matches returns empty array

```jyro
var result = RegexMatchAll("Hello World", "[0-9]+")
# Returns [] (empty array - no digits in text)
```

## Notes

- Uses .NET regular expression syntax
- Throws a runtime exception if the regex pattern is invalid
- For a single match, use `RegexMatch()`
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
