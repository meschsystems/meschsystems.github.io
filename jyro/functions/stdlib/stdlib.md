---
layout: default
title: Standard Library Functions
parent: Function Calls
has_children: false
has_toc: false
permalink: /jyro/functions/stdlib
---

# Standard Library Functions

The Jyro standard library provides a comprehensive set of functions organized into logical categories for efficient data transformation and processing tasks.

## Mathematical Functions

Functions for numeric calculations and mathematical operations.

- [**Abs**](abs/) - Calculate absolute value of a number
- [**Max**](max/) - Find maximum value from multiple arguments
- [**Min**](min/) - Find minimum value from multiple arguments
- [**Round**](round/) - Round number to specified decimal places
- [**Sum**](sum/) - Calculate sum of multiple numeric arguments

## String Manipulation

Functions for processing and transforming text data.

- [**Contains**](contains/) - Test if string contains substring or array contains value
- [**EndsWith**](endswith/) - Test if string ends with specified suffix
- [**Join**](join/) - Join array elements into single string with delimiter
- [**Lower**](lower/) - Convert string to lowercase
- [**Replace**](replace/) - Replace all occurrences of substring with replacement
- [**Split**](split/) - Split string into array using delimiter
- [**StartsWith**](startswith/) - Test if string begins with specified prefix
- [**Trim**](trim/) - Remove leading and trailing whitespace
- [**Upper**](upper/) - Convert string to uppercase

## Array Operations

Functions for manipulating and processing array data structures.

- [**Append**](append/) - Add value to end of array
- [**Clear**](clear/) - Remove all elements from array
- [**Insert**](insert/) - Insert value at specific array index
- [**MergeArrays**](mergearrays/) - Combine multiple arrays into single array
- [**RemoveAt**](removeat/) - Remove element at specific index
- [**RemoveLast**](removelast/) - Remove and return last array element
- [**Reverse**](reverse/) - Reverse order of array elements
- [**Sort**](sort/) - Sort array elements using type-aware comparison
- [**SortByField**](sortbyfield/) - Sort array of objects by specified field

## Date and Time Functions

Functions for handling date parsing, formatting, and calculations.

- [**DateAdd**](dateadd/) - Add time interval to date
- [**DateDiff**](datediff/) - Calculate difference between two dates
- [**DatePart**](datepart/) - Extract specific component from date
- [**FormatDate**](formatdate/) - Format date using specified pattern
- [**Now**](now/) - Get current date and time in UTC
- [**ParseDate**](parsedate/) - Parse date string into normalized format
- [**Today**](today/) - Get current date without time components

## Type Operations

Functions for inspecting and testing data types.

- [**Equal**](equal/) - Test equality between two values
- [**Exists**](exists/) - Test if value is not null
- [**IsNull**](isnull/) - Test if value is null
- [**Length**](length/) - Get length/count of strings, arrays, or objects
- [**NotEqual**](notequal/) - Test inequality between two values
- [**TypeOf**](typeof/) - Get type name of value as string

## Script Execution

Functions for advanced script execution and control flow.

- [**CallScript**](callscript/) - Execute Jyro script with isolated data context

## Usage Patterns

Most functions follow consistent patterns for parameter handling and return values:

- **Mutation vs Immutation**: Array functions like `Sort` and `Reverse` modify arrays in-place, while functions like `MergeArrays` return new arrays
- **Type Coercion**: Functions automatically handle reasonable type conversions (e.g., converting values to strings in `Join`)
- **Error Handling**: Functions return null or default values for invalid inputs rather than throwing exceptions
- **Chaining Support**: Many functions return values that enable method chaining patterns