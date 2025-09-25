---
layout: default
title: Object Literals
parent: Literals and Data Structures
has_children: false
has_toc: false
permalink: /jyro/literals/objects/
---

# Object Literals

Object literals create key-value data structures. Keys can be string literals or computed expressions enclosed in brackets for dynamic key generation.

```
ObjectLiteral    = "{" [ ObjectEntry { "," ObjectEntry } ] "}" ;
ObjectEntry      = (StringLiteral | InterpolatedKey) ":" Expression ;
InterpolatedKey  = "[" Expression "]" ;
```

Interpolated keys are created where they don't exist.

**Valid Syntax:**
```jyro
{}
{ "name": "John", "age": 30 }
{ "key1": value1, "key2": value2 }
{ [dynamicKey]: "value" }
{ "nested": { "inner": true } }
```

**Notes**
- Keys must be string literals or computed using interpolated syntax `[expression]`
- Trailing commas are not permitted in object literals