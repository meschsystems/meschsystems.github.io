---
layout: default
title: CallScript
parent: Function Integration
has_children: false
has_toc: false
permalink: /jyro/functions/callscript/
---

# CallScript

Executes a Jyro script in an isolated execution context with the provided data as its Data context.

## Syntax

```jyro
CallScript(scriptSource, data)
```

## Parameters

- **scriptSource** (string): The Jyro script source code to execute
- **data** (any): The data object to provide as the Data context for the child script

## Returns

- **any**: The modified data object returned by the child script execution

## Description

The CallScript function compiles and executes a Jyro script within the current execution context. The child script receives the provided data as its Data variable and shares all resource limits with the parent script. Includes cycle detection to prevent infinite recursion and enforces call depth limits. If compilation or execution fails, returns the original data unchanged.

## Examples

```jyro
var processScript = `
    Data.processed = true
    Data.timestamp = Now()
`
var inputData = object { "id": 123 }
var result = CallScript(processScript, inputData)
# result contains the processed data with added fields
```

```jyro
var mathScript = "Data.total = Data.a + Data.b"
var calculation = object { "a": 10, "b": 5 }
var sum = CallScript(mathScript, calculation)
# sum.total is now 15
```