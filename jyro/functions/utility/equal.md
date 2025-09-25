---
layout: default
title: Equal
parent: Function Integration
has_children: false
has_toc: false
permalink: /jyro/functions/equal/
---

# Equal

Tests whether two values are equal using Jyro's standard equality semantics.

## Syntax

```jyro
Equal(value1, value2)
```

## Parameters

- **value1** (any): The first value to compare
- **value2** (any): The second value to compare

## Returns

- **boolean**: True if the values are considered equal

## Description

Performs deep comparison for complex types including objects and arrays, and handles type coercion according to Jyro language rules.

## Examples

```jyro
var result1 = Equal(5, 5)                    # Returns true
```

```jyro
var result2 = Equal("hello", "hello")        # Returns true
```

```jyro
var result3 = Equal(5, "5")                  # Returns false (different types)
```

```jyro
var result4 = Equal(null, null)              # Returns true
```