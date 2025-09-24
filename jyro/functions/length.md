---
layout: default
title: Length
parent: Function Integration
has_children: false
has_toc: false
permalink: /jyro/functions/length/
---

# Length

Calculates the length or count of elements for various Jyro value types.

## Syntax

```jyro
Length(value)
```

## Parameters

- **value** (any): The value to measure

## Returns

- **number**: The length or count based on the value type

## Description

Returns character count for strings, element count for arrays, property count for objects, zero for null values, and one for primitive values.

## Examples

```jyro
var result1 = Length("hello")                    # Returns 5
```

```jyro
var result2 = Length(array [1, 2, 3])           # Returns 3
```

```jyro
var result3 = Length(object {"a": 1, "b": 2})   # Returns 2
```

```jyro
var result4 = Length(null)                      # Returns 0
```

```jyro
var result5 = Length(42)                        # Returns 1
```