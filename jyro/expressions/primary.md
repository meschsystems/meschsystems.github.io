---
layout: default
title: Primary Expressions
parent: Expressions
has_children: false
has_toc: false
permalink: /jyro/expressions/primary/
---

# Primary Expressions

Primary expressions form the fundamental building blocks of more complex expressions, including literals, identifiers with property access, function calls, and parenthesized expressions.

```
Primary          = Literal
                 | Identifier { ( "." Identifier | "[" Expression "]" ) }
                 | FunctionCall
                 | "(" Expression ")"
                 | ObjectLiteral
                 | ArrayLiteral ;
```

Property access using dot notation and indexing using bracket notation can be chained to access deeply nested data structures. Function calls invoke host-provided functions with optional arguments. Parenthesized expressions override operator precedence by explicitly grouping sub-expressions.

**Examples:**
```jyro
user.profile.name
items[index]
config["database"]["host"]
data.users[userId].permissions
(a + b) * c
not (isValid and hasPermission)
```