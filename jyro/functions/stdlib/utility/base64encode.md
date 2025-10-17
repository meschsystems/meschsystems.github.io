---
layout: default
title: Base64Encode
parent: Standard Library Functions
has_children: false
has_toc: false
permalink: /jyro/functions/stdlib/utility/base64encode/
---

# Base64Encode

Encodes a string to Base64 format using UTF-8 encoding.

## Syntax

```jyro
Base64Encode(input)
```

## Parameters

- **input** (string): The string to encode

## Returns

- **string**: The Base64-encoded representation of the input string

## Description

Converts the input string to bytes using UTF-8 encoding, then encodes those bytes as a Base64 string. The Base64 format can be safely transmitted over text-based protocols.

## Examples

```jyro
var result1 = Base64Encode("Hello, World!")  # Returns "SGVsbG8sIFdvcmxkIQ=="
```

```jyro
var result2 = Base64Encode("Jyro")           # Returns "Snlybw=="
```

```jyro
var result3 = Base64Encode("")               # Returns ""
```

```jyro
# Encode a basic authentication header
var encoded = Base64Encode("username:password")
# Returns "dXNlcm5hbWU6cGFzc3dvcmQ="
```
