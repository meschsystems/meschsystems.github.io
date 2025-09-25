---
layout: default
title: Array Literals
parent: Literals and Data Structures
has_children: false
has_toc: false
permalink: /jyro/literals/arrays/
---

# Array Literals

Array literals create ordered collections. Elements are specified as a comma-separated list of expressions within brackets.

```
ArrayLiteral     = "[" [ Expression { "," Expression } ] "]" ;
```

**Valid Syntax:**
```jyro
[]
[1, 2, 3]
["a", "b", "c"]
[{ "id": 1 }, { "id": 2 }]
```

**Invalid Syntax:**
```jyro
[1, 2, 3,]          # Trailing comma not supported
```

**Important Considerations:**
- Trailing commas are not permitted in array literals
- Elements can be any valid expression including nested objects and arrays