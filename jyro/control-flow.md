---
layout: default
title: Control Flow
parent: Jyro
has_children: true
has_toc: true
permalink: /jyro/control-flow/
nav_order: 110
---

# Control Flow

Jyro supports control flow through two primary constructs that enable dynamic program execution based on runtime conditions. Conditional execution provides standard if-then-else logic for binary decision making, while multi-way branching offers switch-case statements for efficient handling of multiple discrete conditions. These constructs allow scripts to alter their execution path based on variable values, function results, or other runtime state, enabling the creation of responsive and adaptive automation workflows.

## Statements vs Clauses

Jyro distinguishes between **statements** and **clauses** in control flow constructs:

| Type | Description | Termination | Examples |
|------|-------------|-------------|----------|
| **Statement** | A complete syntactic unit that can appear anywhere a statement is valid | Terminated by `end` | `if`, `switch`, `while`, `foreach` |
| **Clause** | A syntactic component that only exists within a specific parent statement | Terminated by the next clause or parent's `end` | `elseif`, `else`, `case`, `default` |

This design means that clauses like `case` and `elseif` don't have their own `end` keywords - they are delimited by the next clause or the enclosing statement's `end`.

```jyro
# 'if' is a statement (has end), 'elseif' and 'else' are clauses (no end)
if x > 10 then
    Data.result = "high"
elseif x > 5 then
    Data.result = "medium"
else
    Data.result = "low"
end

# 'switch' is a statement (has end), 'case' and 'default' are clauses (no end)
switch status do
case "active" then
    Data.message = "Running"
case "paused" then
    Data.message = "On hold"
default then
    Data.message = "Unknown"
end
```

