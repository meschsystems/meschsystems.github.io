---
layout: default
title: Multiplicative (*, /, %)
parent: Expressions
has_children: false
has_toc: false
permalink: /jyro/expressions/multiplicative/
---

# Multiplicative (*, /, %)

Multiplication, division, and modulo operators perform arithmetic operations with higher precedence than additive operators. Division by zero behavior is defined by the runtime implementation.

```
Multiplicative   = Unary { ("*" | "/" | "%") Unary } ;
```

**Examples:**
```jyro
quantity * price
total / count
value % 10
```

<a name="unary-operators"></a>