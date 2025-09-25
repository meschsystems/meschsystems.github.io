---
layout: default
title: Variable Declaration (var)
parent: Variables and Assignment
has_children: false
has_toc: false
permalink: /jyro/variables/declaration/
---

# Variable Declaration (var)

Variable declarations introduce new identifiers into the current scope with optional type annotations and initialization values. The `var` keyword explicitly marks the creation of a new variable, distinguishing declaration from assignment operations.

```
VariableDecl     = "var" Identifier [ ":" Type ] [ "=" Expression ] ;
Type             = "number" | "string" | "boolean" | "object" | "array" ;
```

Type annotations provide documentation of expected value types and may be used by development tools for analysis, though the runtime does not enforce these constraints. Variables declared without initial values are set to `null` by default.

**Valid Syntax:**
```jyro
var counter
var name: string
var total: number = 100
var isActive: boolean = true
var data = GetSomeData()
```

parent: Jyro**Variable Scope and Blocks**

Variables are scoped to the block in which they are declared, following lexical scoping rules where inner blocks have access to variables declared in outer blocks. Each control flow construct including `if`, `while`, `foreach`, and `switch` statements creates a new scope boundary, and variables declared within these constructs are only accessible within that specific block and any nested blocks contained within it.

Variable lifetime is tied directly to scope, meaning that variables cease to exist when execution leaves the block in which they were declared. This automatic cleanup ensures predictable memory management and prevents accidental access to variables outside their intended scope.

**Variable Shadowing**

Variable shadowing (where variables declared in inner scopes can share the same identifier as variables in outer scopes) is permitted. When shadowing occurs, the inner variable takes precedence and the outer variable becomes temporarily inaccessible until execution exits the inner scope. This behavior is particularly relevant with `foreach` loops, where the iterator variable automatically shadows any existing variable that shares the same identifier, without generating warnings or errors.

Shadowing provides flexibility in variable naming while maintaining scope isolation, though developers should be aware that shadowed variables remain in memory and will become accessible again when the shadowing scope ends.

**Data Context Restrictions**

The identifier `Data` is reserved, and refers to the primary data object being processed by the script. Jyro prohibits certain operations on the `Data` identifier itself.

Attempting to declare `Data` as a variable using `var Data` syntax results in a runtime error. Similarly, direct assignment to `Data` such as `Data = newValue` is prohibited to prevent accidental replacement of the entire data context.

However, Jyro fully supports modification of the data context's child contents through property assignment and indexing operations. Scripts can freely modify data using syntax like `Data.property = value` or `Data[key] = value`, allowing comprehensive data transformation while maintaining the root context structure throughout script execution.

**Important Considerations:**
- Type annotations are optional but recommended for clarity
- Variables without initial values are implicitly null
- Variable names must follow identifier rules (letter followed by letters, digits, or underscores)