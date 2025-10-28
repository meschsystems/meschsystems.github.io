---
layout: default
title: Base64Decode
parent: Standard Library Functions
has_children: false
has_toc: false
permalink: /jyro/functions/stdlib/utility/base64decode/
---

# Base64Decode

Decodes a Base64-encoded string back to its original format using UTF-8 encoding.

## Syntax

```jyro
Base64Decode(input)
```

## Parameters

- **input** (string): The Base64-encoded string to decode

## Returns

- **string**: The decoded string in its original format

## Description

Converts a Base64-encoded string back to its original representation. The function decodes the Base64 format to bytes and then interprets those bytes as a UTF-8 encoded string.

This is the inverse operation of Base64Encode. It is commonly used to decode data received from APIs or to reverse Base64 encoding applied for transmission over text-based protocols.

Throws a `JyroRuntimeException` if the input string is not valid Base64 format.

## Examples

```jyro
var result1 = Base64Decode("SGVsbG8sIFdvcmxkIQ==")
# Returns "Hello, World!"
```

```jyro
var result2 = Base64Decode("Snlybw==")
# Returns "Jyro"
```

```jyro
var result3 = Base64Decode("")
# Returns ""
```

```jyro
# Decode a basic authentication header
var decoded = Base64Decode("dXNlcm5hbWU6cGFzc3dvcmQ=")
# Returns "username:password"
```

```jyro
# Round-trip encoding and decoding
var original = "Sensitive Data"
var encoded = Base64Encode(original)
var decoded = Base64Decode(encoded)
# decoded equals "Sensitive Data"
```

```jyro
# Decode API response data
var apiResponse = {
    "data": "eyJuYW1lIjogIkpvaG4ifQ=="
}
var decodedData = Base64Decode(apiResponse["data"])
# decodedData contains the original JSON string
```

## Notes

- Assumes the encoded data uses UTF-8 encoding
- Throws `JyroRuntimeException` if the input is not valid Base64
- Empty strings return empty strings
- This is the inverse operation of Base64Encode
- Use for decoding data received from APIs or text-based protocols
- See [**Base64Encode()**](../base64encode) and [**InvokeRestMethod()**](../invokerestmethod)
