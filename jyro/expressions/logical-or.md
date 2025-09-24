---
layout: default
title: Logical OR (or)
parent: Expressions
has_children: false
has_toc: false
permalink: /jyro/expressions/logical-or/
---

# Logical OR (or)

The logical OR operator performs short-circuit evaluation, returning true if any operand evaluates to true. Evaluation stops at the first true operand, making it efficient for conditional chains.

```
LogicalOr        = LogicalAnd { "or" LogicalAnd } ;
```

**Examples:**
```jyro
isValid or hasPermission
condition1 or condition2 or condition3
```