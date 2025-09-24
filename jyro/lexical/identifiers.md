---
layout: default
title: Identifiers
parent: Lexical Conventions
has_children: false
has_toc: false
permalink: /jyro/lexical/identifiers/
---

# Identifiers

Identifiers name variables, functions, and properties within the language. They must begin with a letter and can contain letters, digits, and underscores in any combination.

```
Identifier       = Letter { Letter | Digit | "_" } ;
Letter           = "A"…"Z" | "a"…"z" ;
Digit            = "0"…"9" ;
```

**Important Considerations:**
- Must start with a letter (A-Z, a-z)
- Can contain letters, digits, and underscores
- Case-sensitive