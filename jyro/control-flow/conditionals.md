---
layout: default
title: Conditional Execution (if, then, else, end)
parent: Control Flow
has_children: false
has_toc: false
permalink: /jyro/control-flow/conditionals/
---

# Conditional Execution (if, then, else, end)

Conditional statements execute different code paths based on boolean expression evaluation. The `if` statement supports multiple `elseif` branches for complex decision trees and an optional final `else` branch for default behavior.

```
IfStmt           = "if" Expression "then" { Statement }
                   { "elseif" Expression "then" { Statement } }
                   [ "else" { Statement } ] "end" ;
```

Each condition is evaluated in sequence until one evaluates to true, at which point the corresponding statement block executes and control transfers to the statement following the `end` keyword. If no conditions evaluate to true, the optional `else` block executes.

**Valid Syntax:**
```jyro
if condition then
    DoSomething()
end

if score >= 90 then
    grade = "A"
elseif score >= 80 then
    grade = "B"
else
    grade = "F"
end

if condition then DoSomething() end  # Statements can be on the same line
```

**Notes**
- `if` statements must be terminated with `end`
- The `then` keyword is required after each condition
- `elseif` is a single keyword (not `else if`)