---
layout: default
title: GetSchemaErrors
parent: Standard Library Functions
has_children: false
has_toc: false
permalink: /jyro/functions/stdlib/schema/getschemaerrors/
---

# GetSchemaErrors

Validates data against a JSON Schema and returns detailed error information for any validation failures.

## Syntax

```jyro
GetSchemaErrors(data, schema)
```

## Parameters

- **data** (any): The value to validate against the schema
- **schema** (object): A JSON Schema object defining the expected structure and constraints

## Returns

- **array**: An array of error objects, or an empty array if validation passes

Each error object contains:
- **path** (string): The JSON path to the failing value (e.g., `"/user/email"` or `"/items/0"`)
- **keyword** (string): The JSON Schema keyword that failed (e.g., `"type"`, `"required"`, `"minimum"`)
- **message** (string): A human-readable description of the validation error

## Description

GetSchemaErrors provides detailed feedback about why data fails JSON Schema validation. Unlike `ValidateSchema` which returns a simple boolean, this function returns comprehensive error information useful for debugging, user feedback, and error logging.

When the data is valid, an empty array is returned. When validation fails, each constraint violation is reported as a separate error object in the result array.

## Examples

### Basic Type Error

```jyro
var schema = { "type": "number" }
var errors = GetSchemaErrors("not a number", schema)
# Returns: [{ "path": "", "keyword": "type", "message": "Value is \"string\" but should be \"number\"" }]
```

### Missing Required Property

```jyro
var schema = {
    "type": "object",
    "properties": {
        "name": { "type": "string" },
        "email": { "type": "string" }
    },
    "required": array ["name", "email"]
}

var data = { "name": "Alice" }
var errors = GetSchemaErrors(data, schema)
# Returns error indicating "email" is required
```

### Multiple Validation Errors

```jyro
var schema = {
    "type": "object",
    "properties": {
        "age": { "type": "number", "minimum": 0 },
        "status": { "type": "string", "enum": array ["active", "inactive"] }
    }
}

var data = { "age": -5, "status": "unknown" }
var errors = GetSchemaErrors(data, schema)
# Returns multiple errors: age below minimum, status not in enum
```

### Nested Object Errors

```jyro
var schema = {
    "type": "object",
    "properties": {
        "user": {
            "type": "object",
            "properties": {
                "email": { "type": "string" }
            },
            "required": array ["email"]
        }
    }
}

var data = { "user": { "name": "Alice" } }
var errors = GetSchemaErrors(data, schema)
# Returns error with path "/user" indicating "email" is required
```

### Array Item Validation

```jyro
var schema = {
    "type": "array",
    "items": { "type": "number", "minimum": 0 }
}

var data = array [1, 2, -3, 4]
var errors = GetSchemaErrors(data, schema)
# Returns error with path "/2" indicating value -3 is below minimum
```

### Checking for Valid Data

```jyro
var schema = {
    "type": "object",
    "properties": {
        "id": { "type": "number" },
        "name": { "type": "string" }
    },
    "required": array ["id", "name"]
}

var data = { "id": 123, "name": "Test" }
var errors = GetSchemaErrors(data, schema)
# Returns: [] (empty array - data is valid)

if (Length(errors) == 0) {
    Data.message = "Data is valid"
}
```

### User Feedback Pattern

```jyro
var userSchema = {
    "type": "object",
    "properties": {
        "username": { "type": "string", "minLength": 3 },
        "age": { "type": "number", "minimum": 18 }
    },
    "required": array ["username", "age"]
}

var formData = Data.userInput
var errors = GetSchemaErrors(formData, userSchema)

if (Length(errors) > 0) {
    Data.validationErrors = errors
    Data.isValid = false
} else {
    Data.isValid = true
}
```

### Logging Validation Failures

```jyro
var apiResponseSchema = {
    "type": "object",
    "properties": {
        "success": { "type": "boolean" },
        "data": { "type": "object" }
    },
    "required": array ["success"]
}

var response = InvokeRestMethod("https://api.example.com/data", "GET")
var errors = GetSchemaErrors(response.content, apiResponseSchema)

if (Length(errors) > 0) {
    # Log each validation error
    foreach (var error in errors) {
        var logEntry = {
            "timestamp": Now(),
            "path": error.path,
            "keyword": error.keyword,
            "message": error.message
        }
        Data.errorLog = Append(Data.errorLog, logEntry)
    }
}
```

## Notes

- Returns an empty array when data is valid (use `Length(errors) == 0` to check)
- Error paths use JSON Pointer notation (e.g., `"/user/address/city"`)
- All validation errors are collected and returned, not just the first failure
- The same schema formats supported by `ValidateSchema` are supported here
- For simple pass/fail validation without error details, use `ValidateSchema` instead
