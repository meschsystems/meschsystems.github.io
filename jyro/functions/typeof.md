---
layout: default
title: TypeOf
parent: Function Integration
has_children: false
has_toc: false
permalink: /jyro/functions/typeof/
---

# TypeOf

Returns the type name of a Jyro value as a lowercase string representation.

## Syntax

```jyro
TypeOf(value)
```

## Parameters

- **value** (any): The value to inspect for type information

## Returns

- **string**: The lowercase type name of the input value

## Description

Provides runtime type inspection capabilities for dynamic type checking and conditional logic based on value types within Jyro scripts.

## Examples

```jyro
var result1 = TypeOf(42)                    # Returns "number"
```

```jyro
var result2 = TypeOf("hello")               # Returns "string"
```

```jyro
var result3 = TypeOf(true)                  # Returns "boolean"
```

```jyro
var result4 = TypeOf(array [1, 2, 3])       # Returns "array"
```

```jyro
var result5 = TypeOf(object {"a": 1})       # Returns "object"
```

```jyro
var result6 = TypeOf(null)                  # Returns "null"
```