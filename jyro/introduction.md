---
layout: default
title: Introduction to the Language
parent: Jyro
has_children: false
has_toc: false
permalink: /jyro/introduction/
---

# Introduction to the Language

The language emphasizes explicit syntax with structured block delimiters and provides runtime type checking capabilities while maintaining simplicity and readability.

The language operates on a single data object context, allowing scripts to query, modify, and transform data through a controlled execution environment. Jyro follows a procedural programming paradigm where statements execute sequentially, with support for conditional branching, iterative constructs, and host-provided function integration.

Type annotations in Jyro are optional but supported, serving primarily as documentation and potential optimization hints rather than compile-time constraints. The runtime performs type checking through the `is` operator, enabling scripts to make decisions based on the actual types of values encountered during execution. This approach provides flexibility while maintaining type awareness when needed.

Block structures in Jyro require explicit termination using the `end` keyword, creating clear visual boundaries for control flow constructs. This design choice eliminates ambiguity in nested structures and provides consistent syntax patterns across all block-based statements including conditionals, loops, and switch statements.

Object and array construction requires explicit type keywords (`object` and `array` respectively) rather than relying on bracket notation alone. This explicit syntax improves readability and removes potential parsing ambiguities, making the code's intent clear at the lexical level.

Logical operations use word-based operators (`and`, `or`, `not`) rather than symbolic representations, aligning with the language's emphasis on readability and explicit intent. The operator precedence follows standard mathematical conventions while maintaining clear distinctions between logical and arithmetic operations.

Function capabilities are limited to calling host-provided functions rather than defining custom functions within the script. This constraint keeps the language focused on data transformation tasks while allowing extensibility through the host environment. The runtime does not support implicit type conversions, requiring explicit handling of type differences in expressions and operations.

Whitespace is insignificant for all language constructs except for comments, which use a newline to terminate. Statement blocks are deliminated explicitly, and whitespace is therefore ignored. The Jyro convention is to indent each block level using either 4 spaces or a tab. The examples shown in this document reflect that convention.

The standard file extension for Jyro scripts is `.jyro`. The content type can be specified as `Content-Type: application/vnd.mesch.jyro`

Jyro is a case sensitive language. The case conventions are:

* **keywords**: lowercase (e.g. `foreach`)
* **local variables**: lowerCamelCase (e.g. `var myFoo = 42`)
* **iterator variables**: Follow the array key (e.g. `foreach item in Data.items` or `foreach Item in Data.Items`)
* **host function calls**: PascalCase (e.g. `Today()`)
* **script names**: PascalCase (e.g. `CallScript("ProcessVipOrders.jyro", vipOrders)`)
* **the `Data` object**: PascalCase (i.e. upper-case `D`, lower-case everthing else: `Data`)
* **object property names**: These are typically string literals in Jyro (e.g. `object { "propertyName": value }`), so the convention depends on the data domain.
* **added properties**: Again, follow the data domain.
* **interpolated keys**: Depends on the expression that generated the key.

A Jyro program consists of a sequence of statements that execute in order from top to bottom. Each statement represents a complete instruction such as variable declaration, assignment, expression evaluation, or control flow operation.

```
Program          = { Statement } ;
Comment          = "#" { Character } EndOfLine ;
```

At the heart of every Jyro script execution is the `Data` context, a special built-in identifier that represents the primary data object being processed. The `Data` context is provided by the host environment when a script begins execution and serves as both the input to the transformation process and the output that will be returned to the host upon completion.

`Data` is automatically available in every script without declaration and maintains its identity throughout the entire execution lifecycle. The host environment populates `Data` with the initial data structure before script execution begins, and any modifications made to `Data` during script execution are reflected in the final result returned to the host. This design creates a clear contract between the host and script: the host provides data for transformation, and the script modifies that data in place. Hosts may pass complex objects of any practical size to Jyro, or may simply pass a null object `{}` if the target script is intended to construct a data structure from scratch.

Scripts may not declare a new variable named `Data` using `var Data =` syntax, as this would shadow the built-in context and break the host-script communication contract. Similarly, direct assignment to the `Data` root itself is prohibited - scripts cannot execute statements like `Data = newObject` as this would replace the entire context rather than transforming it.

However, the language provides full access to modify the contents and structure of the `Data` context through property assignment, indexing, and method calls. Scripts can freely execute operations such as `Data.newProperty = "value"`, `Data["dynamicKey"] = calculation`, or `Data.existingArray[index] = updatedValue`. This approach ensures that while the `Data` context remains stable and accessible throughout execution, its contents can be completely transformed to meet the script's processing requirements.

> ⚠ The script has complete control over the `Data` object that was passed to it, therefore it is the host's responsibility to ensure that `Data` only contains objects that are safe for reading and writing. This is especially important in untrusted scenarios, where the host does not trust the script that is being run (e.g. multi-tenanted applications with scripting support).

> ⚠ Never directly evaluate an expression passed back on the `Data` object. Doing so could lead to privilege escalation and host compromise. Hosts should treat all data returned from scripts as potentially malicious content that should be sanitized or validated before any further processing.

When script execution completes, either by reaching the end of the statement list or encountering a `return` statement, the current state of the `Data` context is returned to the host environment. This return mechanism ensures that all modifications made during script execution are captured and made available to the calling code, completing the data transformation workflow.