---
layout: default
title: Function Calls
parent: Jyro
has_children: true
has_toc: false
permalink: /jyro/functions/
nav_order: 130
---

# Function Calls

Function calls invoke host-provided functions with optional arguments passed as expressions. Functions extend the language capabilities by providing access to external data sources, computational operations, and system services that are not built into the core language. Jyro comes with a comprehensive [**standard library**](stdlib/) of functions that provide data manipulation capabilities.

```
FunctionCall     = Identifier "(" [ Expression { "," Expression } ] ")" ;
```

Arguments are evaluated from left to right before being passed to the function. The function identifier must match a function provided by the host environment, as the language does not support user-defined functions within scripts.

Jyro comes with a standard library that provides common functionality. Hosts can extend the function set available to Jyro by registering host-side functions with the Jyro runtime. These functions are then available to call within Jyro scripts, providing unlimited host interop. The casing convention for host-side function registration (and the casing convention used by the standard library) is PascalCase.

> ⚠ Hosts must ensure that the functions provided to Jyro scripts cannot result in privilege escalation or other security issues, especially when running untrusted scripts.

**Valid Syntax:**
```jyro
GetData()
CalculateSum(a, b)
ProcessUser(user.id, user.name, user.isActive)
FormatMessage("Hello", name, GetCurrentTime())
```

**Notes**
- Function calls always require parentheses, even with no arguments
- Arguments are evaluated left to right
- Trailing commas in argument lists are not permitted
- Functions must be provided by the host environment