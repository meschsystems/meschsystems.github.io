---
layout: default
title: Number Literals
parent: Lexical Conventions
has_children: false
has_toc: false
permalink: /jyro/lexical/numbers/
---

# Number Literals

Number literals represent numeric values in both integer and decimal formats. Scientific notation is not supported.

```
NumberLiteral    = Digit { Digit } [ "." Digit { Digit } ] ;
```

**Important Considerations:**
- Integer and decimal numbers supported
- No scientific notation
- No leading zeros (except for `0` itself)