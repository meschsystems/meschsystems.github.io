---
layout: default
title: Type Checking (is)
parent: Expressions
has_children: false
has_toc: false
permalink: /jyro/expressions/typechecking/
---

# Type Checking (is)

The `is` operator performs runtime type checking, returning true if the left operand matches the specified type. This enables scripts to make decisions based on the actual types of values encountered during execution.

```
Relational       = Additive { ("<" | "<=" | ">" | ">=" | "is") Additive } ;
```

Type checking occurs at runtime and can be used in conditional statements to handle different data types appropriately within the same script execution path.

**Valid Syntax:**
```jyro
if value is number then
    PerformNumericOperation(value)
end

if data is object then
    ProcessObjectData(data)
end
```

**Supported Type Checks:**
- `value is number`
- `value is string`
- `value is boolean`
- `value is object`
- `value is array`

**Type Checking Cascade Rules:**

The `is` operator checks the runtime type of the evaluated expression, not the literal syntax. The cascade follows this hierarchy:

1. **`null`** - Null values return `false` for all type checks
2. **`number`** - Numeric values (integers and decimals), regardless of how they were created
3. **`string`** - Text values enclosed in quotes or returned from string operations
4. **`boolean`** - The literals `true` and `false`, or results of boolean operations
5. **`array`** - Collections created with `array []` syntax or returned from functions
6. **`object`** - Key-value structures created with `object {}` syntax or returned from functions

**Examples:**
```jyro
42 is number          # true (number literal)
"42" is string        # true (string literal)
"42" is number        # false (string containing digits)
ToNumber("42") is number  # true (converted to number)
array [1,2,3] is array    # true
object {} is object       # true
null is number            # false
null is string            # false
```

Scripts can change variable types at runtime by invoking standard library conversion functions (e.g., `ToNumber("42")` to convert string "42" to number 42).

**Notes**
- Type checking is performed at runtime
- The `is` operator returns a boolean value
- Null values will not match any specific type