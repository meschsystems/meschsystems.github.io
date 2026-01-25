---
layout: default
title: PadLeft
parent: Standard Library Functions
has_children: false
has_toc: false
permalink: /jyro/functions/stdlib/string/padleft/
---

# PadLeft

Pads a string on the left side to a specified total length.

## Syntax

```jyro
PadLeft(text, length)
PadLeft(text, length, padChar)
```

## Parameters

- **text** (string): The string to pad
- **length** (number): The target total length (must be integer)
- **padChar** (string, optional): The character to use for padding (first character used). Defaults to space

## Returns

- **string**: The padded string

## Description

Pads a string on the left (beginning) with a specified character until it reaches the target length. If the string is already equal to or longer than the target length, it is returned unchanged.

## Examples

### Zero-padding numbers

```jyro
var orderId = PadLeft("42", 5, "0")  # Returns "00042"
```

### Default space padding

```jyro
var aligned = PadLeft("Hi", 10)  # Returns "        Hi"
```

### Fixed-width formatting

```jyro
var items = [
    {"name": "Apple", "price": 1.50},
    {"name": "Banana", "price": 0.75},
    {"name": "Cherry", "price": 3.00}
]

foreach item in items do
    var priceStr = PadLeft(item.price, 6)
    Append(Data.lines, item.name + ": $" + priceStr)
end
```

### String already at target length

```jyro
var result = PadLeft("Hello", 5, "x")  # Returns "Hello" (unchanged)
```

### String longer than target

```jyro
var result = PadLeft("Hello World", 5, "x")  # Returns "Hello World" (unchanged)
```

## Notes

- Only the first character of the padding string is used
- If padding character is empty string, defaults to space
- Commonly used for zero-padding numbers or right-aligning text
## See Also

- [PadRight](../padright/) - Pad a string on the right side to a specified total length
