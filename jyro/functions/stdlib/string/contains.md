---
layout: default
title: Contains
parent: Standard Library Functions
has_children: false
has_toc: false
permalink: /jyro/functions/stdlib/string/contains/
---

# Contains

Tests whether a source value contains a specified search value. Supports substring searching within strings and value searching within arrays.

## Syntax

```jyro
Contains(source, searchValue)
```

## Parameters

- **source** (string or array): The source value to search within
- **searchValue** (any): The value to search for

## Returns

- **boolean**: True if the source contains the search value, false otherwise

## Description

For strings, performs case-sensitive substring searching. For arrays, searches for exact value matches using Jyro equality semantics. Returns `false` if either argument is null.

## Examples

### String searching

```jyro
var hasSubstring = Contains("Hello World", "World")  # Returns `true`
```

```jyro
var notFound = Contains("Hello", "Goodbye")          # Returns `false`
```

### Array searching

```jyro
var fruits = array ["apple", "banana", "orange"]
var hasApple = Contains(fruits, "apple")             # Returns `true`
```

```jyro
var hasGrape = Contains(fruits, "grape")             # Returns `false`
```