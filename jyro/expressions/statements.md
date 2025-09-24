---
layout: default
title: Expression Statement
parent: Expressions
has_children: false
has_toc: false
permalink: /jyro/expressions/statements/
---

# Expression Statement

Expression statements evaluate standalone expressions primarily for their side effects, such as function calls that modify the data context or produce output. The result of the expression is computed but not stored unless the expression itself performs storage operations.

```
ExpressionStmt   = Expression ;
```

**Valid Syntax:**
```jyro
CalculateTotal()
user.name
42
```