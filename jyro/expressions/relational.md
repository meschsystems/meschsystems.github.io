---
layout: default
title: Relational (<, <=, >, >=, is)
parent: Expressions
has_children: false
has_toc: false
permalink: /jyro/expressions/relational/
---

# Relational (<, <=, >, >=, is)

Relational operators perform magnitude comparisons for numeric values and the `is` operator performs runtime type checking. Type checking returns true if the operand matches the specified type.

```
Relational       = Additive { ("<" | "<=" | ">" | ">=" | "is") Additive } ;
```

**Examples:**
```jyro
age >= 18
score < 100
value is number
```

<a name="additive-operators"></a>