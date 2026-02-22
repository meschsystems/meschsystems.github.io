---
layout: default
title: return Statement
parent: Control Flow
has_children: false
has_toc: false
permalink: /jyro/control-flow/return-statement/
nav_order: 130
---

# `return` Statement

The `return` statement terminates the script immediately with a success status. It accepts an optional string message that must appear on the **same line**.

```jyro
return                              # Clean exit, no message
return "Processing complete"        # Clean exit with message
```

## Behaviour

- The script stops executing at the `return` statement
- The `Data` context is returned to the host with all modifications made up to that point
- If a message is provided, it is reported to the host as an informational message

## Message must be on the same line

The message is part of the `return` statement syntax. If placed on a separate line, it becomes an independent string expression statement - not a return message.

```jyro
# CORRECT
return "Done"

# INCORRECT - "Done" is a separate statement that never executes
return
"Done"
```

## Comparison with `fail`

| Keyword | Script Succeeds? | Message Severity |
|---------|-----------------|------------------|
| `return` | Yes | Info |
| `fail` | No | Error |

Both keywords return the `Data` context to the host, regardless of success or failure. See [fail](/jyro/control-flow/fail/) for the failure counterpart.
