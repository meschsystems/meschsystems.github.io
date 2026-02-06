---
layout: default
title: Clamp
parent: Standard Library Functions
has_children: false
has_toc: false
permalink: /jyro/functions/stdlib/math/clamp/
---

# Clamp

Constrains a numeric value to be within a specified range.

## Syntax

```jyro
Clamp(value, min, max)
```

## Parameters

- **value** (number): The value to constrain
- **min** (number): The minimum allowed value
- **max** (number): The maximum allowed value

## Returns

- **number**: The clamped value within the specified range

## Description

Returns a value that is constrained to be within the specified minimum and maximum bounds:
- If value is less than min, returns min
- If value is greater than max, returns max
- Otherwise, returns the original value unchanged

## Examples

### Value above maximum

```jyro
var result = Clamp(150, 0, 100)  # Returns 100
```

### Value below minimum

```jyro
var result = Clamp(-50, 0, 100)  # Returns 0
```

### Value within range

```jyro
var result = Clamp(50, 0, 100)  # Returns 50
```

### Limiting percentage values

```jyro
var rawPercentage = 125
var validPercentage = Clamp(rawPercentage, 0, 100)  # Returns 100
```

### Constraining user input

```jyro
var userAge = Data.inputAge
var validAge = Clamp(userAge, 0, 150)  # Ensure age is reasonable
```

### RGB color values

```jyro
var r = Clamp(Data.red, 0, 255)
var g = Clamp(Data.green, 0, 255)
var b = Clamp(Data.blue, 0, 255)
```

### Pagination bounds

```jyro
var requestedPage = Data.page
var totalPages = 10
var currentPage = Clamp(requestedPage, 1, totalPages)
```

## Notes

- If min is greater than max, an error is thrown
