---
layout: default
title: fail Statement
parent: Control Flow
has_children: false
has_toc: false
permalink: /jyro/control-flow/fail-statement/
nav_order: 140
---

# `fail` Statement

The `fail` statement terminates the script immediately with a failure status. It accepts an optional string message that must appear on the **same line**.

```jyro
fail                                # Failure exit, default message
fail "Invalid input"                # Failure exit with message
```

## Behaviour

- The script stops executing at the `fail` statement
- The `Data` context is returned to the host with all modifications made up to that point
- The message is reported to the host as an error
- The host environment treats the script as having failed

## Message must be on the same line

The message is part of the `fail` statement syntax. If placed on a separate line, it becomes an independent string expression statement - not a fail message.

```jyro
# CORRECT
fail "Missing required field"

# INCORRECT - "Missing required field" is a separate statement
fail
"Missing required field"
```

## Intended use

Use `fail` for business logic validation errors and rule violations - situations where the script cannot produce a valid result.

```jyro
if Data.orders is null or Data.orders is not array then
    fail "Orders must be an array"
end

if AnyByField(Data.orders, "amount", "<", 0) then
    fail "Negative order amounts are not allowed"
end
```

## Comparison with `return`

| Keyword | Script Succeeds? | Message Severity |
|---------|-----------------|------------------|
| `return` | Yes | Info |
| `fail` | No | Error |

Both keywords return the `Data` context to the host with all mutations applied. See [return](/jyro/control-flow/return/) for the success counterpart.
