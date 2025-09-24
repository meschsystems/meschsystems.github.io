---
layout: default
title: Logical AND (and)
parent: Expressions
has_children: false
has_toc: false
permalink: /jyro/expressions/logical-and/
---

# Logical AND (and)

The logical AND operator performs short-circuit evaluation, returning true only if all operands evaluate to true. Evaluation stops at the first false operand, preventing unnecessary computation.

```
LogicalAnd       = Equality { "and" Equality } ;
```

**Examples:**
```jyro
isActive and hasAccess
x > 0 and x < 100
```

<a name="equality-operators"></a>