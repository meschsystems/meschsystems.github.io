---
layout: default
title: Additive (+, -)
parent: Expressions
has_children: false
has_toc: false
permalink: /jyro/expressions/additive/
---

# Additive (+, -)

Addition and subtraction operators perform arithmetic operations on numeric values. The behavior with non-numeric types depends on the runtime's type conversion and operation semantics.

```
Additive         = Multiplicative { ("+" | "-") Multiplicative } ;
```

**Examples:**
```jyro
total + tax
endDate - startDate
```

<a name="multiplicative-operators"></a>