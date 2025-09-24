---
layout: default
title: String Literals
parent: Lexical Conventions
has_children: false
has_toc: false
permalink: /jyro/lexical/strings/
---

# String Literals

String literals represent text values enclosed in double quotation marks.

```
StringLiteral    = '"' { Character } '"' ;
Character        = ? any character except " or newline ? ;
```

**Important Considerations:**
- Enclosed in double quotes
- Cannot contain newlines