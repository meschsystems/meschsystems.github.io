---
layout: default
title: Values
parent: Standard Library Functions
has_children: false
has_toc: false
permalink: /jyro/functions/stdlib/utility/values/
---

# Values

Returns an array containing all property values of an object.

## Syntax

```jyro
Values(object)
```

## Parameters

- **object** (object): The object to extract values from

## Returns

- **array**: An array containing all property values of the object

## Description

The `Values` function extracts all property values from an object and returns them as an array. This is the complement to the `Keys` function which returns property names.

The order of values matches the order of properties in the object. If the object has no properties, an empty array is returned.

## Examples

### Basic usage

```jyro
var person = {"name": "Alice", "age": 30, "city": "New York"}
var vals = Values(person)
# vals is ["Alice", 30, "New York"]
```

### Empty object

```jyro
var empty = {}
var vals = Values(empty)
# vals is []
```

### Summing numeric values

```jyro
var scores = {"math": 95, "science": 88, "english": 92}
var allScores = Values(scores)

var total = 0
foreach score in allScores do
    total = total + score
end
# total is 275
```

### Working with Keys and Values together

```jyro
var config = {"timeout": 30, "retries": 3, "debug": true}

var keys = Keys(config)
var vals = Values(config)

# keys is ["timeout", "retries", "debug"]
# vals is [30, 3, true]
```

### Checking if any value matches

```jyro
var statuses = {"order1": "pending", "order2": "shipped", "order3": "pending"}

var hasShipped = false
foreach status in Values(statuses) do
    if status == "shipped" then
        hasShipped = true
    end
end
# hasShipped is true
```

### Finding unique values

```jyro
var assignments = {"task1": "Alice", "task2": "Bob", "task3": "Alice"}
var uniqueAssignees = Distinct(Values(assignments))
# Returns ["Alice", "Bob"]
```

### Converting object to array for processing

```jyro
var prices = {"apple": 1.50, "banana": 0.75, "cherry": 3.00}

var allPrices = Values(prices)
var avgPrice = Average(allPrices[0], allPrices[1], allPrices[2])
# avgPrice is 1.75
```

## Notes

- Returns an array of values, preserving the order they appear in the object
- The type of each value is preserved (numbers, strings, booleans, objects, arrays)
- Works seamlessly with `Keys` to iterate over objects
- Returns an empty array for empty objects or null values
## See Also

- [Keys](../keys/) - Extract property names from an object
