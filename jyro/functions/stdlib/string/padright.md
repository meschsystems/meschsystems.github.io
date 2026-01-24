---
layout: default
title: PadRight
parent: Standard Library Functions
has_children: false
has_toc: false
permalink: /jyro/functions/stdlib/string/padright/
---

# PadRight

Pads a string on the right side to a specified total length.

## Syntax

```jyro
PadRight(text, length)
PadRight(text, length, padChar)
```

## Parameters

- **text** (string): The string to pad
- **length** (number): The target total length (must be integer)
- **padChar** (string, optional): The character to use for padding (first character used). Defaults to space

## Returns

- **string**: The padded string

## Description

Pads a string on the right (end) with a specified character until it reaches the target length. If the string is already equal to or longer than the target length, it is returned unchanged.

## Examples

### Space padding for alignment

```jyro
var aligned = PadRight("Hi", 10)  # Returns "Hi        "
```

### Custom padding character

```jyro
var result = PadRight("Test", 8, "-")  # Returns "Test----"
```

### Fixed-width column formatting

```jyro
var items = [
    {"name": "Apple", "qty": 5},
    {"name": "Banana", "qty": 12},
    {"name": "Cherry", "qty": 3}
]

foreach item in items do
    var nameCol = PadRight(item.name, 15)
    Append(Data.lines, nameCol + item.qty)
end
# Results in:
# "Apple          5"
# "Banana         12"
# "Cherry         3"
```

### String already at target length

```jyro
var result = PadRight("Hello", 5, "x")  # Returns "Hello" (unchanged)
```

### String longer than target

```jyro
var result = PadRight("Hello World", 5, "x")  # Returns "Hello World" (unchanged)
```

## Notes

- Only the first character of the padding string is used
- If padding character is empty string, defaults to space
- Commonly used for left-aligning text in fixed-width columns
- See also `PadLeft` for padding on the left side
