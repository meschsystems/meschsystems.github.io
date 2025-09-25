---
layout: default
title: IsNull
parent: Standard Library Functions
has_children: false
has_toc: false
permalink: /jyro/functions/stdlib/isnull/
---

# IsNull

Tests whether a value is null within the Jyro type system.

## Syntax

```jyro
IsNull(value)
```

## Parameters

- **value** (any): The value to test for null

## Returns

- **boolean**: True if the value is null, false for all non-null values

## Description

Provides the logical inverse of the Exists function and is useful for conditional logic and validation.

## Examples

```jyro
var result1 = IsNull(null)         # Returns true
```

```jyro
var result2 = IsNull("hello")      # Returns false
```

```jyro
var result3 = IsNull(0)            # Returns false
```

```jyro
var result4 = IsNull(array [])     # Returns false
```