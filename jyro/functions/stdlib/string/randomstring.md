---
layout: default
title: RandomString
parent: Standard Library Functions
has_children: false
has_toc: false
permalink: /jyro/functions/stdlib/string/randomstring/
---

# RandomString

Generates a cryptographically secure random string of specified length from a character set using System.Security.Cryptography.RandomNumberGenerator.

## Syntax

```jyro
RandomString(length)
RandomString(length, characterSet)
```

## Parameters

- **length** (number): The length of the string to generate. Must be a non-negative integer.
- **characterSet** (string, optional): The set of characters to select from. When omitted, defaults to alphanumeric characters (a-z, A-Z, 0-9).

## Returns

- **string**: A cryptographically secure random string of the specified length

## Description

Generates a random string using cryptographically secure randomization, making it suitable for passwords, tokens, authentication codes, and other security-sensitive scenarios.

The default character set includes all alphanumeric characters: `ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789`

You can provide a custom character set for specialized use cases like numeric PINs, hex strings, or restricted character sets.

Uses `System.Security.Cryptography.RandomNumberGenerator` for cryptographic security rather than pseudo-random generation, ensuring unpredictability suitable for security contexts.

## Examples

```jyro
# Generate an 8-character alphanumeric password
var password = RandomString(8)
# password could be "aB3xK9mP" or similar
```

```jyro
# Generate a 16-character secure token
var token = RandomString(16)
# token could be "7hF3kL9mN2pQ5tV8" or similar
```

```jyro
# Generate a 6-digit numeric PIN
var pin = RandomString(6, "0123456789")
# pin could be "483921" or similar
```

```jyro
# Generate a hexadecimal string (lowercase)
var hex = RandomString(32, "0123456789abcdef")
# hex could be "3a7f2e1d9c4b8f6a2e5d7c9b4f8a6e3d" or similar
```

```jyro
# Generate uppercase-only code
var code = RandomString(12, "ABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789")
# code could be "H3K9M2P5Q7T8" or similar
```

```jyro
# Generate password with special characters
var secure_password = RandomString(16, "ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789!@#$%^&*")
# secure_password includes letters, numbers, and special characters
```

```jyro
# Generate a session ID
var session_id = RandomString(32)
Data.session_id = session_id
# Creates unpredictable session identifier
```

```jyro
# Generate short URL suffix
var url_suffix = RandomString(6, "abcdefghijklmnopqrstuvwxyz0123456789")
var short_url = "https://example.com/" + url_suffix
# short_url could be "https://example.com/k3m9p2" or similar
```

```jyro
# Generate API key
var api_key = RandomString(40)
# api_key is a 40-character cryptographically secure string
```

```jyro
# Generate temporary filename
var temp_file = "temp_" + RandomString(10) + ".dat"
# temp_file could be "temp_aB3xK9mP4q.dat" or similar
```

## Notes

- Uses cryptographically secure random string generation (not pseudo-random)
- Default character set is alphanumeric: a-z, A-Z, 0-9 (62 characters)
- Custom character sets enable specialized use cases (PINs, hex, etc.)
- Length must be a non-negative integer; non-integer or negative values throw an error
- Empty or null character sets throw an error
- Suitable for security-sensitive scenarios: passwords, tokens, session IDs, API keys
- For random integer generation, see [RandomInt](../math/randomint/)
- For random array element selection, see [RandomChoice](../array/randomchoice/)
- Each call produces an independent random string (no seeding required)
- Longer strings and larger character sets provide more entropy and security
