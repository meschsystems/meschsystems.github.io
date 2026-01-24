---
layout: default
title: Round
parent: Standard Library Functions
has_children: false
has_toc: false
permalink: /jyro/functions/stdlib/math/round/
---

# Round

Rounds a numeric value to a specified number of decimal places using configurable rounding rules.

## Syntax

```jyro
Round(value)
Round(value, digits)
Round(value, digits, mode)
```

## Parameters

- **value** (number): The numeric value to round
- **digits** (number, optional): Number of decimal places (defaults to 0, must be integer)
- **mode** (string, optional): The rounding mode to use. Options:
  - `"floor"` - Round toward negative infinity
  - `"ceiling"` - Round toward positive infinity
  - `"away"` - Round away from zero (standard mathematical rounding)
  - Default (omitted) - Banker's rounding (round half to even)

## Returns

- **number**: The rounded value using the specified rounding mode

## Description

Rounds a numeric value to the specified number of decimal places using the chosen rounding mode. The default behavior uses banker's rounding (round half to even) for consistent mathematical behavior, but you can specify floor, ceiling, or away-from-zero modes.

## Examples

### Basic rounding (banker's rounding)

```jyro
var result = Round(3.14159, 2)  # Returns 3.14
```

### Banker's rounding behavior

```jyro
var result1 = Round(2.5)  # Returns 2 (rounds to even)
var result2 = Round(3.5)  # Returns 4 (rounds to even)
var result3 = Round(4.5)  # Returns 4 (rounds to even)
```

### Floor mode (round down)

```jyro
var result1 = Round(3.7, 0, "floor")   # Returns 3
var result2 = Round(3.2, 0, "floor")   # Returns 3
var result3 = Round(-3.2, 0, "floor")  # Returns -4 (toward negative infinity)
```

### Ceiling mode (round up)

```jyro
var result1 = Round(3.2, 0, "ceiling")  # Returns 4
var result2 = Round(3.7, 0, "ceiling")  # Returns 4
var result3 = Round(-3.7, 0, "ceiling") # Returns -3 (toward positive infinity)
```

### Away from zero mode

```jyro
var result1 = Round(2.5, 0, "away")   # Returns 3 (standard math rounding)
var result2 = Round(-2.5, 0, "away")  # Returns -3 (away from zero)
```

### Rounding to decimal places

```jyro
var price = Round(19.995, 2)              # Returns 20.00 (banker's)
var priceUp = Round(19.994, 2, "ceiling") # Returns 20.00
var priceDown = Round(19.999, 2, "floor") # Returns 19.99
```

### No decimal places

```jyro
var result = Round(123.456)  # Returns 123
```

## Notes

- **Banker's rounding** (default): Rounds 0.5 to the nearest even number. This reduces cumulative rounding bias over many operations.
- **Floor**: Always rounds toward negative infinity (not toward zero).
- **Ceiling**: Always rounds toward positive infinity (not away from zero).
- **Away**: Traditional mathematical rounding where 0.5 rounds away from zero.
- Related: `Abs`, `Clamp`, `Min`, `Max`
