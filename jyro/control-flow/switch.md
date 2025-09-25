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
SwitchStmt       = "switch" Expression
                     { "case" Expression "then" { Statement } }
                     [ "default" { Statement } ]
                   "end" ;
```

Cases are evaluated in the order they appear until a matching value is found. The optional `default` case executes if no explicit cases match. Each case is independent with no fall-through behavior, eliminating the need for explicit `break` statements.

**Valid Syntax:**
```jyro
switch status
case "pending" then
    ProcessPending()
case "approved" then
    ProcessApproved()
default
    HandleError()
end
```

**Notes**
- `switch` statements must be terminated with `end`
- Each `case` requires the `then` keyword
- `default` case does not use `then`
- No fall-through behavior; each case is independent
- Cases do not require `break` statements