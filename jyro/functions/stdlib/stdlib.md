---
layout: default
title: Standard Library Functions
parent: Function Calls
has_children: true
has_toc: false
permalink: /jyro/functions/stdlib
---

# Standard Library Functions

The Jyro standard library provides a comprehensive set of functions organized into logical categories for efficient data transformation and processing tasks.

## Mathematical Functions

Functions for numeric calculations and mathematical operations.

- [**Abs**](stdlib/math/abs/) - Calculate absolute value of a number
- [**Max**](stdlib/math/max/) - Find maximum value from multiple arguments
- [**Min**](stdlib/math/min/) - Find minimum value from multiple arguments
- [**Round**](stdlib/math/round/) - Round number to specified decimal places
- [**Sum**](stdlib/math/sum/) - Calculate sum of multiple numeric arguments

## String Manipulation

Functions for processing and transforming text data.

- [**Contains**](stdlib/string/contains/) - Test if string contains substring or array contains value
- [**EndsWith**](stdlib/string/endswith/) - Test if string ends with specified suffix
- [**Join**](stdlib/string/join/) - Join array elements into single string with delimiter
- [**Lower**](stdlib/string/lower/) - Convert string to lowercase
- [**Replace**](stdlib/string/replace/) - Replace all occurrences of substring with replacement
- [**Split**](stdlib/string/split/) - Split string into array using delimiter
- [**StartsWith**](stdlib/string/startswith/) - Test if string begins with specified prefix
- [**Trim**](stdlib/string/trim/) - Remove leading and trailing whitespace
- [**Upper**](stdlib/string/upper/) - Convert string to uppercase
- [**ToNumber**](stdlib/string/tonumber/) - Convert a string to a number

## Array Operations

Functions for manipulating and processing array data structures.

- [**Append**](stdlib/array/append/) - Add value to end of array
- [**Clear**](stdlib/array/clear/) - Remove all elements from array
- [**CountIf**](stdlib/array/countif/) - Count elements where field equals specified value
- [**IndexOf**](stdlib/array/indexof/) - Find index of element in array using deep equality
- [**Insert**](stdlib/array/insert/) - Insert value at specific array index
- [**MergeArrays**](stdlib/array/mergearrays/) - Combine multiple arrays into single array
- [**RemoveAt**](stdlib/array/removeat/) - Remove element at specific index
- [**RemoveLast**](stdlib/array/removelast/) - Remove and return last array element
- [**Reverse**](stdlib/array/reverse/) - Reverse order of array elements
- [**Sort**](stdlib/array/sort/) - Sort array elements using type-aware comparison
- [**SortByField**](stdlib/array/sortbyfield/) - Sort array of objects by specified field

## Date and Time Functions

Functions for handling date parsing, formatting, and calculations.

- [**DateAdd**](stdlib/dateandtime/dateadd/) - Add time interval to date
- [**DateDiff**](stdlib/dateandtime/datediff/) - Calculate difference between two dates
- [**DatePart**](stdlib/dateandtime/datepart/) - Extract specific component from date
- [**FormatDate**](stdlib/dateandtime/formatdate/) - Format date using specified pattern
- [**Now**](stdlib/dateandtime/now/) - Get current date and time in UTC
- [**ParseDate**](stdlib/dateandtime/parsedate/) - Parse date string into normalized format
- [**Today**](stdlib/dateandtime/today/) - Get current date without time components

## Utility Functions

Miscellaneous functions for inspecting and testing data types, value generation, and calling scripts.

- [**CallScript**](stdlib/utility/callscript/) - Execute Jyro script with isolated data context
- [**Equal**](stdlib/utility/equal/) - Test equality between two values
- [**Exists**](stdlib/utility/exists/) - Test if value is not null
- [**InvokeRestMethod**](stdlib/utility/invokerestmethod/) - Execute HTTP REST API requests (experimental)
- [**IsNull**](stdlib/utility/isnull/) - Test if value is null
- [**Length**](stdlib/utility/length/) - Get length/count of strings, arrays, or objects
- [**NewGuid**](stdlib/utility/newguid) - Generate a new globally unique identifier (GUID)
- [**Base64Encode**](stdlib/utility/base64encode) - Encodes a string to Base64 format
- [**NotEqual**](stdlib/utility/notequal/) - Test inequality between two values
- [**TypeOf**](stdlib/utility/typeof/) - Get type name of value as string

## Usage Patterns

Most functions follow consistent patterns for parameter handling and return values:

- **Mutation vs Immutation**: Array functions like `Sort` and `Reverse` modify arrays in-place, while functions like `MergeArrays` return new arrays
- **Type Coercion**: Functions automatically handle reasonable type conversions (e.g., converting values to strings in `Join`)
- **Error Handling**: Functions return null or default values for invalid inputs rather than throwing exceptions
- **Chaining Support**: Many functions return values that enable method chaining patterns