---
layout: default
title: Loop Control (break, continue)
parent: Iteration and Looping
has_children: false
has_toc: false
permalink: /jyro/iteration/control/
---

# Loop Control (break, continue)

Loop control statements modify the normal flow of iteration within loops. The `break` statement immediately exits the innermost containing loop, while `continue` skips the remaining statements in the current iteration and proceeds to the next iteration. All loop blocks must be terminated by an `end` statement.

```
BreakStmt        = "break" ;
ContinueStmt     = "continue" ;
```

These statements provide fine-grained control over loop execution, allowing early termination or selective processing of loop iterations based on runtime conditions.

**Valid Syntax:**
```jyro
while true do
    if shouldExit then
        break
    end
    if shouldSkip then
        continue
    end
    ProcessItem()
end

foreach item in items do
    if item.isInvalid then
        continue
    end
    ProcessValidItem(item)
end
```

**Notes**
- `break` and `continue` can only be used within loop constructs
- `break` exits the innermost containing loop
- `continue` skips to the next iteration of the innermost containing loop