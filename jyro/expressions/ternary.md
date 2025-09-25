---
layout: default
title: Ternary Conditional Operator (?:)
parent: Expressions
has_children: false
has_toc: false
permalink: /jyro/expressions/ternary/
---

# Ternary Conditional Operator (?:)

The ternary conditional operator provides a concise way to select between two expressions based on a boolean condition. It follows the syntax `condition ? trueExpression : falseExpression` and evaluates to either the true expression or false expression depending on the truthiness of the condition.

```
Ternary          = LogicalOr [ "?" Ternary ":" Ternary ] ;
```

The ternary operator uses short-circuit evaluation, meaning only the condition and the selected expression are evaluated. If the condition is truthy, only the true expression executes; if falsy, only the false expression executes. This provides performance benefits and prevents side effects in the non-selected branch.

The ternary operator is right-associative, meaning nested ternary operators are grouped from right to left. Multiple ternary operators can be chained together, though readability may suffer with excessive nesting.

**Valid Syntax:**
```jyro
status = isActive ? "active" : "inactive"
result = score >= 60 ? "pass" : "fail"
message = user.hasPermission ? GetWelcomeMessage() : "Access denied"
value = condition1 ? expr1 : condition2 ? expr2 : defaultExpr
```

**Notes**
- The ternary operator has lower precedence than logical OR but higher precedence than assignment
- Right-associative: `a ? b : c ? d : e` is parsed as `a ? b : (c ? d : e)`
- Only the condition and selected expression are evaluated (short-circuit behavior)
- Both true and false expressions must be present