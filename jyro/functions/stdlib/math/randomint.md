---
layout: default
title: RandomInt
parent: Standard Library Functions
has_children: false
has_toc: false
permalink: /jyro/functions/stdlib/math/randomint/
---

# RandomInt

Generates a cryptographically secure random integer within a specified range using System.Security.Cryptography.RandomNumberGenerator.

## Syntax

```jyro
RandomInt(max)
RandomInt(min, max)
```

## Parameters

- **max** (number): When used alone, the exclusive upper bound for range [0, max). When used with min, the exclusive upper bound for range [min, max). Must be an integer.
- **min** (number, optional): The inclusive lower bound. Must be an integer. When omitted, defaults to 0.

## Returns

- **number**: A cryptographically secure random integer within the specified range (upper bound is exclusive)

## Description

Generates a random integer using cryptographically secure randomization, making it suitable for security-sensitive scenarios including password generation, token creation, and unpredictable selection.

Supports two calling patterns:
- **Single argument**: `RandomInt(max)` returns a random integer in the range [0, max)
- **Two arguments**: `RandomInt(min, max)` returns a random integer in the range [min, max)

Note that the upper bound (max) is **exclusive** - it will not be included in the possible values.

Uses `System.Security.Cryptography.RandomNumberGenerator` for cryptographic security rather than pseudo-random generation, ensuring unpredictability suitable for security contexts.

## Examples

```jyro
# Generate random number from 0 to 9 (inclusive)
var digit = RandomInt(10)
# digit could be 0, 1, 2, ..., 9 (but never 10)
```

```jyro
# Simulate dice roll (1-6)
var dice = RandomInt(1, 7)
# dice could be 1, 2, 3, 4, 5, or 6
```

```jyro
# Generate random year in range
var year = RandomInt(2000, 2025)
# year could be 2000, 2001, ..., 2024 (but not 2025)
```

```jyro
# Random selection from 100 items
var items = GetAllItems()
var random_index = RandomInt(Length(items))
var selected = items[random_index]
# Selects a random item from the array
```

```jyro
# Generate random port number (1024-65535)
var port = RandomInt(1024, 65536)
# port is in range 1024-65535 (unprivileged port range)
```

```jyro
# Secure token generation (4-digit PIN)
var pin = ToString(RandomInt(1000, 10000))
# pin is a 4-digit number like "3847" or "0123"
```

```jyro
# Random sample size
var total_records = 1000
var sample_size = RandomInt(50, 101)
# sample_size is between 50 and 100 records
```

```jyro
# Generate multiple random values
var lottery_numbers = []
var i = 0
while i < 6 do
    var num = RandomInt(1, 50)
    lottery_numbers = Append(lottery_numbers, num)
    i = i + 1
end
# lottery_numbers contains 6 random values from 1-49
```

## Notes

- Uses cryptographically secure random number generation (not pseudo-random)
- Upper bound (max) is **exclusive** - the range does not include the max value
- Both parameters must be integers; non-integer values throw an error
- max must be greater than min; otherwise throws an error
- Suitable for security-sensitive scenarios: passwords, tokens, authentication codes
- For random string generation, see [RandomString](../string/randomstring/)
- For random array element selection, see [RandomChoice](../array/randomchoice/)
- Each call produces an independent random value (no seeding required)
