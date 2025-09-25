---
layout: default
title: Round
parent: Function Integration
has_children: false
has_toc: false
permalink: /jyro/functions/math/round/
---

# Round

Rounds a numeric value to a specified number of decimal places using standard mathematical rounding rules.

## Syntax

```jyro
Round(value, digits)
```

## Parameters

- **value** (number): The numeric value to round
- **digits** (number, optional): Number of decimal places (defaults to 0, must be integer)

## Returns

- **number**: The rounded value using banker's rounding (round half to even)

## Description

Uses .NET's Math.Round implementation with banker's rounding rules for consistent mathematical behavior. The digits parameter specifies the number of decimal places to preserve.

## Examples

```jyro
var result1 = Round(3.14159, 2)       # Returns 3.14
```

```jyro
var result2 = Round(2.5)              # Returns 2 (banker's rounding)
```

```jyro
var result3 = Round(3.5)              # Returns 4 (banker's rounding)
```

```jyro
var result4 = Round(123.456, 0)       # Returns 123
```