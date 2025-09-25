---
layout: default
title: Unary (not, -)
parent: Expressions
has_children: false
has_toc: false
permalink: /jyro/expressions/unary/
---

# Unary (not, -)

Unary operators apply to single operands with the highest precedence among operators. The `not` operator performs logical negation, while the minus operator performs arithmetic negation.

```
Unary            = [ "not" | "-" ] Primary ;
```

**Examples:**
```jyro
not isValid
-balance
not user.isActive
```

**Notes**
- Operator precedence follows mathematical conventions
- The `is` operator performs type checking
- Logical operators (`and`, `or`, `not`) use words, not symbols
- Chaining comparisons (e.g., `a < b < c`) is not supported