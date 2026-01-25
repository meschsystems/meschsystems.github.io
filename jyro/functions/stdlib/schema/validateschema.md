---
layout: default
title: ValidateSchema
parent: Standard Library Functions
has_children: false
has_toc: false
permalink: /jyro/functions/stdlib/schema/validateschema/
---

# ValidateSchema

Validates data against a JSON Schema definition and returns whether the data conforms to the schema.

## Syntax

```jyro
ValidateSchema(data, schema)
```

## Parameters

- **data** (any): The value to validate against the schema
- **schema** (object): A JSON Schema object defining the expected structure and constraints

## Returns

- **boolean**: True if the data conforms to the schema, false otherwise

## Description

ValidateSchema performs JSON Schema validation on any Jyro value. It supports the JSON Schema specification including type validation, required properties, nested objects, arrays, enums, numeric constraints, and string patterns.

This function is useful for validating API responses, user input, or any structured data before processing. For detailed error information when validation fails, use `GetSchemaErrors` instead.

## Examples

### Basic Type Validation

```jyro
var schema = { "type": "string" }
var isValid = ValidateSchema("hello", schema)    # Returns true
```

```jyro
var schema = { "type": "number" }
var isValid = ValidateSchema(42, schema)         # Returns true
```

```jyro
var schema = { "type": "number" }
var isValid = ValidateSchema("not a number", schema)  # Returns false
```

### Object Validation with Required Properties

```jyro
var schema = {
    "type": "object",
    "properties": {
        "name": { "type": "string" },
        "age": { "type": "number" }
    },
    "required": ["name"]
}

var validData = { "name": "Alice", "age": 30 }
var isValid = ValidateSchema(validData, schema)  # Returns true
```

```jyro
var schema = {
    "type": "object",
    "required": ["name"]
}

var missingRequired = { "age": 30 }
var isValid = ValidateSchema(missingRequired, schema)  # Returns false
```

### Numeric Constraints

```jyro
var schema = {
    "type": "number",
    "minimum": 0,
    "maximum": 100
}

var isValid1 = ValidateSchema(50, schema)   # Returns true
var isValid2 = ValidateSchema(150, schema)  # Returns false
var isValid3 = ValidateSchema(-5, schema)   # Returns false
```

### Array Validation

```jyro
var schema = {
    "type": "array",
    "items": { "type": "number" }
}

var numbers = [1, 2, 3, 4, 5]
var isValid = ValidateSchema(numbers, schema)  # Returns true
```

```jyro
var schema = {
    "type": "array",
    "items": { "type": "number" }
}

var mixed = [1, "two", 3]
var isValid = ValidateSchema(mixed, schema)  # Returns false
```

### Enum Validation

```jyro
var schema = {
    "type": "string",
    "enum": ["draft", "published", "archived"]
}

var isValid1 = ValidateSchema("published", schema)  # Returns true
var isValid2 = ValidateSchema("deleted", schema)    # Returns false
```

### Nested Object Validation

```jyro
var schema = {
    "type": "object",
    "properties": {
        "user": {
            "type": "object",
            "properties": {
                "email": { "type": "string" },
                "role": { "type": "string" }
            },
            "required": ["email"]
        }
    }
}

var data = {
    "user": {
        "email": "alice@example.com",
        "role": "admin"
    }
}
var isValid = ValidateSchema(data, schema)  # Returns true
```

### Conditional Validation Pattern

```jyro
var responseSchema = {
    "type": "object",
    "properties": {
        "status": { "type": "number" },
        "data": { "type": "object" }
    },
    "required": ["status", "data"]
}

var apiResponse = InvokeRestMethod("https://api.example.com/users", "GET", null, null)
if ValidateSchema(apiResponse.content, responseSchema) then
    # Process the validated response
    Data.users = apiResponse.content.data
else
    # Handle invalid response
    Data.error = "Invalid API response format"
end
```

## Notes

- The schema parameter must be a valid JSON Schema object
- Supports JSON Schema Draft 2020-12, Draft 2019-09, Draft 7, and Draft 6
- For detailed validation error messages, use `GetSchemaErrors` instead
- Null values are validated according to JSON Schema rules (use `"type": "null"` to explicitly allow null)
