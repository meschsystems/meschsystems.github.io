---
layout: default
title: Abs
parent: Standard Library Functions
has_children: false
has_toc: false
permalink: /jyro/functions/stdlib/math/abs/
---

# Abs

Calculates the absolute value of a numeric input, returning the non-negative magnitude of the number.

## Syntax

```jyro
Abs(value)
```

## Parameters

- **value** (number): The numeric value to process

## Returns

- **number**: The absolute value of the input (always non-negative)

## Description

The Abs function handles both integer and floating-point values according to standard mathematical absolute value semantics. Negative numbers become positive, while positive numbers remain unchanged.

## Examples

```jyro
var result1 = Abs(-5)      # Returns 5
```

```jyro
var result2 = Abs(3.14)    # Returns 3.14
```

```jyro
var result3 = Abs(-0.5)    # Returns 0.5
```

```jyro
var result4 = Abs(0)       # Returns 0
```