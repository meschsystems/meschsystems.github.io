---
layout: default
title: RegexTest
parent: Standard Library Functions
has_children: false
has_toc: false
permalink: /jyro/functions/stdlib/string/regextest/
---

# RegexTest

Tests whether text contains a match for the specified regex pattern.

## Syntax

```jyro
RegexTest(text, pattern)
```

## Parameters

- **text** (string): The source text to search
- **pattern** (string): The regex pattern to test for

## Returns

- **boolean**: `true` if the pattern matches anywhere in the text, `false` otherwise

## Description

Checks whether the input text contains at least one match for the specified regex pattern. Returns a boolean indicating whether a match exists.

Use this function when you only need to know if a pattern exists, without extracting the actual matched text.

## Examples

### Check for email presence

```jyro
var hasEmail = RegexTest(userInput, "[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+[.][a-zA-Z]{2,}")
# Returns true if text contains an email address
```

### Check for digits

```jyro
var hasNumbers = RegexTest(text, "[0-9]")
# Returns true if text contains any digit
```

### Check for URL

```jyro
var hasUrl = RegexTest(content, "https?://")
# Returns true if text contains http:// or https://
```

### Use in conditionals

```jyro
if RegexTest(input, "^[a-zA-Z]+$")
    # Input contains only letters
    result = "Valid alphabetic input"
else
    result = "Input contains non-letter characters"
end
```

### No match returns false

```jyro
var result = RegexTest("Hello World", "[0-9]+")
# Returns false (no digits in text)
```

## Notes

- Uses .NET regular expression syntax
- Throws a runtime exception if the regex pattern is invalid
- For extracting the matched text, use `RegexMatch()` or `RegexMatchAll()`
- More efficient than `RegexMatch()` when you only need a boolean check

## Pattern Escaping in Jyro Strings

Jyro strings support a subset of escape sequences (`\n`, `\t`, `\r`, `\"`, `\\`). Common regex shortcuts like `\d` or `\w` require character class alternatives.

Use character classes instead:

| Instead of | Use |
|------------|-----|
| `\d` | `[0-9]` |
| `\w` | `[a-zA-Z0-9_]` |
| `\s` | `[ \t\n\r]` |
| `\.` | `[.]` |
