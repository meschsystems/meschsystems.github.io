---
layout: default
title: Keys
parent: Standard Library Functions
has_children: false
has_toc: false
permalink: /jyro/functions/stdlib/utility/keys/
---

# Keys

Returns an array containing all property names (keys) of an object.

## Syntax

```jyro
Keys(object)
```

## Parameters

- **object** (object): The object to extract keys from

## Returns

- **array**: An array of strings containing the property names of the object

## Description

The `Keys` function extracts all property names from an object and returns them as an array of strings. This is particularly useful for iterating over an object's properties, inspecting object structure, or working with the results of `GroupBy`.

If the object has no properties, an empty array is returned. If the argument is null, it is coerced to an empty object and an empty array is returned.

## Examples

### Basic usage

```jyro
var person = {
    "name": "Alice",
    "age": 30,
    "city": "New York"
}

var propertyNames = Keys(person)
# propertyNames is ["name", "age", "city"]
```

### Iterating over object properties

```jyro
var scores = {"math": 95, "science": 88, "english": 92}

var total = 0
foreach subject in Keys(scores) do
    total = total + scores[subject]
end

Data.average = total / Length(Keys(scores))
# Data.average is 91.666...
```

### Working with GroupBy results

```jyro
var orders = [
    {"id": 1, "status": "pending", "amount": 100},
    {"id": 2, "status": "completed", "amount": 200},
    {"id": 3, "status": "pending", "amount": 150},
    {"id": 4, "status": "cancelled", "amount": 50}
]

var grouped = GroupBy(orders, "status")
var statuses = Keys(grouped)
# statuses is ["pending", "completed", "cancelled"]

# Process each group
foreach status in statuses do
    var count = Length(grouped[status])
    Append(Data.summary, {"status": status, "count": count})
end
```

### Checking object structure

```jyro
var config = {"apiUrl": "https://api.example.com", "timeout": 30}

var requiredKeys = ["apiUrl", "timeout", "retries"]
foreach key in requiredKeys do
    if IndexOf(Keys(config), key) == -1 then
        Append(Data.missingKeys, key)
    end
end
# Data.missingKeys is ["retries"]
```

### Empty object

```jyro
var empty = {}
var keys = Keys(empty)
# keys is []

Data.hasKeys = Length(keys) > 0
# Data.hasKeys is false
```

### Dynamic property access

```jyro
var translations = {
    "hello": "Hola",
    "goodbye": "Adiós",
    "thank you": "Gracias"
}

Data.entries = []
foreach english in Keys(translations) do
    Append(Data.entries, {
        "english": english,
        "spanish": translations[english]
    })
end
```

## Notes

- Returns an array of strings, even if the object was created with non-string keys (all keys are strings in Jyro)
- The order of keys in the returned array matches the order they were added to the object
- Works seamlessly with `GroupBy` to iterate over grouped data
- Can be combined with `Length` to count the number of properties
- Can be used with `IndexOf` to check if a property exists (alternative to `Exists`)
- Returns an empty array for empty objects or null values
