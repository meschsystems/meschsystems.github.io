---
layout: default
title: Multi-way Branching (switch, case, default, end)
parent: Control Flow
has_children: false
has_toc: false
permalink: /jyro/control-flow/switch/
---

# Multi-way Branching (switch, case, default, end)

Switch statements provide multi-way branching based on expression value matching. Each `case` compares its expression against the switch expression for equality, executing the corresponding statement block when a match is found.

```
SwitchStmt       = "switch" Expression "do"
                     { "case" Expression "then" { Statement } }
                     [ "default" "then" { Statement } ]
                   "end" ;
```

Cases are evaluated in the order they appear until a matching value is found. The optional `default` case executes if no explicit cases match. Each case is independent with no fall-through behavior, eliminating the need for explicit `break` statements.

**Valid Syntax:**
```jyro
switch status do
case "pending" then
    ProcessPending()
case "approved" then
    ProcessApproved()
default then
    HandleError()
end
```

**Notes**
- `switch` statements require the `do` keyword after the expression
- `switch` statements must be terminated with `end`
- Each `case` requires the `then` keyword
- `default` also requires the `then` keyword
- No fall-through behavior; each case is independent
- Cases do not require `break` statements

## Statements vs Clauses

In Jyro, control flow constructs follow a consistent pattern:

- **Statements** are complete syntactic units that can appear anywhere a statement is valid. They are terminated by `end`. Examples: `if`, `switch`, `while`, `foreach`.

- **Clauses** are syntactic components that only exist within a specific parent statement. They are terminated by the next clause or the parent's `end`, not by their own `end`. Examples: `elseif`, `else`, `case`, `default`.

This is why `case` and `default` don't have their own `end` keywords - they are clauses within the `switch` statement, delimited by the next clause or the final `end`.