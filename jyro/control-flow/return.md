---
layout: default
title: Script Termination (return)
parent: Control Flow
has_children: false
has_toc: false
permalink: /jyro/control-flow/return/
---

# Script Termination (return)

The `return` statement immediately halts script execution and makes the current `Data` context available to the caller. As the host and script share a single mutable `Data` context, Jyro's `return` statement does not carry an expression value.

```
ReturnStmt       = "return" ;
```

When `return` is encountered, all remaining statements in the script are skipped and control returns to the host environment or calling context (i.e. the calling script). The data object reflects all modifications made up to the point where `return` was executed. Scripts should therefore ensure that `Data` is in a valid state before invoking `return` (e.g. recovery from an error condition).

**Valid Syntax:**
```jyro
return
```

**Important Considerations:**
- `return` is always written without an expression
- Execution stops immediately when `return` is encountered
- The current `Data` context is returned to the caller