---
layout: default
title: Exists
parent: Standard Library Functions
has_children: false
has_toc: false
permalink: /jyro/functions/stdlib/utility/exists/
---

# Exists

Tests whether a value exists (is not null) within the Jyro type system.

## Syntax

```jyro
Exists(value)
```

## Parameters

- **value** (any): The value to test for existence

## Returns

- **boolean**: True if the value is not null, false if null

## Description

Provides a convenient way to check for the presence of meaningful data before performing operations that require non-null values.

## Examples

```jyro
var result1 = Exists("hello")      # Returns true
```

```jyro
var result2 = Exists(42)           # Returns true
```

```jyro
var result3 = Exists(null)         # Returns false
```

```jyro
var result4 = Exists(array [])     # Returns true (empty array exists)
```