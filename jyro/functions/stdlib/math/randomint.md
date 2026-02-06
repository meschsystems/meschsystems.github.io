---
layout: default
title: RandomInt
parent: Standard Library Functions
has_children: false
has_toc: false
permalink: /jyro/functions/stdlib/math/randomint/
---

# RandomInt

Generates a cryptographically secure random integer within a specified inclusive range.

## Syntax

```jyro
RandomInt(min, max)
```

## Parameters

- **min** (number): The inclusive lower bound. Must be an integer.
- **max** (number): The inclusive upper bound. Must be an integer.

## Returns

- **number**: A random integer in the range [min, max] (both bounds inclusive)

## Description

Generates a cryptographically secure random integer between `min` and `max`, inclusive on both ends. Uses `System.Security.Cryptography.RandomNumberGenerator` for unpredictable, security-grade randomness. Both parameters are required.

## Examples

```jyro
# Simulate dice roll (1-6)
var dice = RandomInt(1, 6)
# dice could be 1, 2, 3, 4, 5, or 6
```

```jyro
# Generate random number from 0 to 9
var digit = RandomInt(0, 9)
```

```jyro
# Generate random year in range
var year = RandomInt(2000, 2025)
# year could be 2000, 2001, ..., 2025
```

```jyro
# Random selection from array by index
var items = ["apple", "banana", "cherry"]
var randomIndex = RandomInt(0, Length(items) - 1)
var selected = items[randomIndex]
```

```jyro
# Generate multiple random values
var lottery_numbers = []
var i = 0
while i < 6 do
    var num = RandomInt(1, 49)
    lottery_numbers = Append(lottery_numbers, num)
    i = i + 1
end
# lottery_numbers contains 6 random values from 1-49
```

## Notes

- Uses cryptographically secure random number generation (not pseudo-random)
- Both bounds are **inclusive** - `RandomInt(1, 6)` can return 1, 2, 3, 4, 5, or 6
- Both parameters are required
- Each call produces an independent random value
