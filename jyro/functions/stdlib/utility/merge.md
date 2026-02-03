---
layout: default
title: Merge
parent: Standard Library Functions
has_children: false
has_toc: false
permalink: /jyro/functions/stdlib/utility/merge/
---

# Merge

Merges multiple objects into a single new object. Properties from later arguments override properties from earlier arguments (shallow merge).

## Syntax

```jyro
Merge(object1, object2, ...)
```

## Parameters

- **object1, object2, ...** (objects): Two or more objects to merge. Non-object arguments are silently skipped.

## Returns

- **object**: A new object containing all properties from the input objects

## Description

The `Merge` function combines multiple objects into a single new object. Properties from later arguments override properties from earlier arguments when there are key conflicts. This is a shallow merge - nested objects are not recursively merged but replaced entirely.

The function is variadic and accepts any number of arguments. Non-object arguments (strings, numbers, arrays, null) are silently skipped.

## Examples

### Basic merge

```jyro
var obj1 = { "a": 1, "b": 2 }
var obj2 = { "c": 3, "d": 4 }

var merged = Merge(obj1, obj2)
# merged is { "a": 1, "b": 2, "c": 3, "d": 4 }
```

### Override semantics

```jyro
var defaults = { "theme": "light", "language": "en", "notifications": true }
var userPrefs = { "theme": "dark", "language": "es" }

var settings = Merge(defaults, userPrefs)
# settings is { "theme": "dark", "language": "es", "notifications": true }
```

### Multiple objects (variadic)

```jyro
var base = { "a": 1 }
var overrides1 = { "b": 2 }
var overrides2 = { "c": 3 }

var result = Merge(base, overrides1, overrides2)
# result is { "a": 1, "b": 2, "c": 3 }
```

### Order matters for conflicts

```jyro
var obj1 = { "x": 1 }
var obj2 = { "x": 2 }
var obj3 = { "x": 3 }

var result = Merge(obj1, obj2, obj3)
# result is { "x": 3 } (last value wins)
```

### Creating object copies

```jyro
var original = { "name": "Alice", "age": 30 }
var copy = Merge(original)

copy.name = "Bob"
# original.name is still "Alice"
# copy.name is "Bob"
```

### Non-object arguments are skipped

```jyro
var obj1 = { "a": 1 }
var obj2 = { "b": 2 }

var result = Merge(obj1, "string", null, 42, obj2)
# result is { "a": 1, "b": 2 } (non-objects ignored)
```

### Shallow merge behavior

```jyro
var obj1 = { "nested": { "a": 1, "b": 2 } }
var obj2 = { "nested": { "c": 3 } }

var result = Merge(obj1, obj2)
# result is { "nested": { "c": 3 } }
# Note: obj1's nested object is replaced, not merged
```

### Building configuration objects

```jyro
var systemDefaults = {
    "timeout": 30000,
    "retries": 3,
    "debug": false
}

var environmentConfig = {
    "debug": true,
    "apiUrl": "https://api.example.com"
}

var userOverrides = {
    "timeout": 60000
}

var config = Merge(systemDefaults, environmentConfig, userOverrides)
# config is {
#     "timeout": 60000,
#     "retries": 3,
#     "debug": true,
#     "apiUrl": "https://api.example.com"
# }
```

### Adding properties to an object

```jyro
var user = { "id": 1, "name": "Alice" }
var timestamp = { "createdAt": Now() }
var metadata = { "version": "1.0" }

var enriched = Merge(user, timestamp, metadata)
# enriched has all properties from user, timestamp, and metadata
```

### Empty merge

```jyro
var result = Merge()
# result is {} (empty object)
```

## Notes

- Creates a new object (does not mutate input objects)
- Later arguments override earlier arguments for conflicting keys
- Shallow merge only - nested objects are replaced, not recursively merged
- Non-object arguments are silently skipped
- With zero arguments, returns an empty object
- With one argument, returns a shallow copy of that object
- Order of arguments determines override priority (last wins)
- Useful for applying configuration defaults, creating copies, and combining partial objects
