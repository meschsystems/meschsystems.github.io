---
layout: default
title: CallScriptByName
parent: Standard Library Functions
has_children: false
has_toc: false
permalink: /jyro/functions/stdlib/utility/callscriptbyname/
---

# CallScriptByName

Executes a Jyro script by name using the configured script resolver, with the provided data as its Data context.

## Syntax

```jyro
CallScriptByName(scriptName, data)
```

## Parameters

- **scriptName** (string): The name of the script to resolve and execute
- **data** (any): The data object to provide as the Data context for the child script

## Returns

- **any**: The modified data object returned by the child script execution

## Description

The CallScriptByName function resolves a script by name using the host-configured script resolver, then compiles and executes it within the current execution context. This allows scripts to call other scripts by name without needing to know the script source code.

The host application must configure a script resolver using `.WithResolver()` on the JyroBuilder. The resolver is a delegate that receives a script name and returns the script source code. If the resolver is not configured or the script cannot be found, a runtime error is thrown.

The child script receives the provided data as its Data variable and shares all resource limits with the parent script. Includes cycle detection to prevent infinite recursion and enforces call depth limits. If compilation or execution fails, returns the original data unchanged.

## Host Configuration

To use CallScriptByName, the host application must configure a script resolver:

```csharp
var jyro = JyroBuilder.Create()
    .WithStdlib()
    .WithResolver(name =>
    {
        // Return script source for the given name, or null if not found
        return name switch
        {
            "validate-customer" => "Data.valid = Data.age >= 18",
            "calculate-total" => "Data.total = Data.price * Data.quantity",
            _ => null
        };
    });
```

## Examples

```jyro
# Call a script by name to validate customer data
var customer = object { "name": "Alice", "age": 25 }
var validated = CallScriptByName("validate-customer", customer)
# validated.valid is now true
```

```jyro
# Call a script by name to calculate order total
var order = object { "price": 10.50, "quantity": 3 }
var result = CallScriptByName("calculate-total", order)
# result.total is now 31.50
```

```jyro
# Pass the entire Data object to a subscript
var processed = CallScriptByName("transform-data", Data)
```

## Errors

- Throws a runtime error if the script resolver is not configured
- Throws a runtime error if the script name cannot be resolved (resolver Returns `null`)
- Throws a runtime error if a script execution cycle is detected

## See Also

- [CallScript](../callscript/) - Execute a script with inline source code
